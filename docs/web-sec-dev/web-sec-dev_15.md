# 第十三章：**加密**

![image](img/common01.jpg)

加密是现代互联网的核心。没有私密、安全地交换数据包的能力，电子商务将无法存在，用户也无法安全地验证自己与互联网网站的身份。

安全超文本传输协议是目前网络上最广泛使用的加密形式。网页服务器和网页浏览器普遍支持 HTTPS，因此开发者可以将所有流量重定向到该协议，确保用户之间的通信安全。想要在自己的网站上使用 HTTPS 的网页开发者，只需要从*证书授权机构*获得一个*证书*，并与其托管服务提供商一起安装它。

尽管你可以轻松开始使用加密，但当网站与用户代理通过 HTTPS 进行交互时，发生的过程是非常复杂的。现代*密码学*——研究加密和解密数据的方法——依赖于由数学家和安全专业人员开发并积极研究的技术。幸运的是，互联网协议的抽象层意味着你不需要了解线性代数或数论就能使用它们的发现。但是，越是理解底层算法，你就越能预见潜在的风险。

本章首先概述了加密如何在互联网协议中使用以及支撑它的数学原理。一旦你对加密的工作原理有了充分的理解，你将回顾开发者需要采取的实际步骤，以开始使用 HTTPS。最后，你将了解黑客如何利用未加密或加密较弱的流量，以及一些攻击如何完全绕过加密。

### 互联网协议中的加密

回想一下，通过互联网发送的消息被分割成数据包，并通过*传输控制协议（TCP）*定向到最终目的地。接收方计算机将这些 TCP 数据包重新组装成原始消息。TCP 并不规定数据发送的*如何*被解释。为了实现这一点，两个计算机需要就如何解释发送的数据达成一致，使用如 HTTP 这样的高级协议。TCP 也不会掩盖发送的数据包内容。未加密的 TCP 对话容易受到*中间人攻击*，即恶意的第三方拦截并读取正在传输的数据包。

为了避免这种情况，浏览器和网页服务器之间的 HTTP 对话通过*传输层安全性（TLS）*来加密，这是一种提供隐私性（通过确保数据包不能被第三方解密）和*数据完整性*（通过确保任何试图篡改传输中的数据包都能被检测到）的方法。使用 TLS 进行的 HTTP 对话被称为*HTTP 安全（HTTPS）*对话。

当您的网页浏览器连接到一个 HTTPS 网站时，浏览器和 Web 服务器会协商使用哪些加密算法，这是*TLS 握手*的一部分——TLS 会话启动时发生的数据包交换。为了理解 TLS 握手过程中发生的事情，我们需要简要了解各种加密算法。现在是一些轻松的数学时刻！

#### *加密算法、哈希和消息认证码*

一个*加密算法*通过使用*加密密钥*（两个希望建立安全通信的方共享的秘密）对输入数据进行加扰处理——没有*解密密钥*（解密数据所需的相应密钥）的人无法解读加密后的输出。输入数据和密钥通常以二进制数据的形式编码，虽然为了可读性，密钥可能以文本字符串的形式表达。

存在许多加密算法，且数学家和安全研究人员不断发明新的算法。它们可以分为几类：对称和非对称加密算法（用于加密数据）、哈希函数（用于数据指纹和构建其他密码学算法）、以及消息认证码（用于确保数据完整性）。

##### 对称加密算法

一个*对称加密算法*使用相同的密钥来加密和解密数据。对称加密算法通常作为*分组密码*工作：它们将输入数据分解成固定大小的块，这些块可以单独加密。（如果最后一个输入数据块大小不足，则会*填充*以填满块大小。）这使得它们适合处理数据流，包括 TCP 数据包。

对称算法的设计注重速度，但有一个主要的安全缺陷：解密密钥必须在接收方解密数据流之前提供给他们。如果解密密钥通过互联网共享，潜在的攻击者将有机会窃取该密钥，从而解密任何进一步的消息。这样不好。

##### 非对称加密算法

为了应对解密密钥被盗的威胁，*非对称加密算法*应运而生。非对称算法使用不同的密钥来加密和解密数据。

非对称算法允许像 Web 服务器这样的软件公开其加密密钥，同时保留其解密密钥为秘密。任何希望向服务器发送安全消息的用户代理都可以使用服务器的加密密钥来加密这些消息，确保没有人（甚至是发送方自己！）能够解密所发送的数据，因为解密密钥是保密的。这有时被描述为*公钥密码学*：加密密钥（*公钥*）可以公开；只有解密密钥（*私钥*）需要保密。

非对称算法比对称算法复杂得多，因此也更慢。互联网协议中的加密使用了两种类型的算法的结合，正如你稍后在本章中将看到的那样。

##### 哈希函数

与加密算法相关的是*加密哈希函数*，可以将其视为一种输出*无法*被解密的加密算法。哈希函数还有一些其他有趣的属性：算法的输出（*哈希值*）始终是固定大小的，无论输入数据的大小如何；而且，给定不同的输入值，得到相同输出值的概率极其微小。

为什么你会想要加密一些你之后无法解密的数据呢？好吧，这是生成输入数据“指纹”的一种巧妙方式。如果你需要检查两个不同的输入是否相同，但出于安全原因不想存储原始输入值，你可以验证这两个输入是否生成相同的哈希值。

这就是网站密码通常存储的方式，正如我们在第九章中看到的那样。当用户首次设置密码时，网站服务器会将密码的哈希值存储在数据库中，并故意忘记实际的密码值。当用户稍后再次输入密码时，服务器会重新计算哈希值并与存储的哈希值进行比较。如果两个哈希值不同，则表示用户输入了不同的密码，意味着该凭证应被拒绝。通过这种方式，网站可以检查密码的正确性，而无需明确知道每个用户的密码。（以明文形式存储密码是一种安全隐患：如果攻击者入侵数据库，他们将获得每个用户的密码。）

##### 消息认证码

*消息认证码（MAC）*算法与加密哈希函数相似（通常是在加密哈希函数的基础上构建），它们将任意长度的输入数据映射到一个唯一且固定大小的输出。这个输出本身就是所谓的*消息认证码*。然而，MAC 算法比哈希函数更加专业化，因为重新计算 MAC 需要一个秘密密钥。这意味着只有拥有秘密密钥的参与方才能生成或检查消息认证码的有效性。

MAC 算法用于确保通过互联网传输的数据包不会被攻击者伪造或篡改。要使用 MAC 算法，发送方和接收方计算机会交换一个共享的秘密密钥——通常是作为 TLS 握手的一部分进行交换。（为了避免密钥被窃取，该秘密密钥会在发送前进行加密。）从此以后，发送方将为每个数据包生成一个 MAC，并将其附加到数据包上。由于接收方计算机拥有相同的密钥，它可以从消息中重新计算 MAC。如果计算得到的 MAC 与附加在数据包上的值不一致，则说明该数据包已经被篡改、损坏，或它并非由原计算机发送。因此，接收方会拒绝该数据包。

如果你已经看到这里并且仍在关注，恭喜你！密码学是一个庞大而复杂的主题，具有自己特有的术语。理解它如何融入互联网协议需要同时平衡多个概念，因此感谢你的耐心。接下来，我们来看一下我们讨论过的各种类型的加密算法是如何在 TLS 中使用的。

#### *TLS 握手*

TLS 使用一组合适的加密算法来高效、安全地传输信息。为了提高速度，大多数通过 TLS 传输的数据包将使用常见的对称加密算法，也称为 *块加密算法*，因为它加密的是“块”状的流信息。回想一下，对称加密算法容易受到恶意用户监听会话并窃取加密密钥的威胁。为了安全地传递块加密的加密/解密密钥，TLS 会先使用 *非对称* 算法对密钥进行加密，然后再将其传递给接收方。最后，通过 TLS 传输的数据包将使用消息认证码进行标记，以检测数据是否已被篡改。

在 TLS 会话开始时，浏览器和网站会进行 *TLS 握手* 以确定它们应如何通信。在握手的第一阶段，浏览器将列出它支持的多个密码套件。让我们深入了解这是什么意思。

##### 密码套件

*密码套件* 是一组用于保护通信的算法。根据 TLS 标准，密码套件由 *三个* 独立的算法组成。第一个算法是 *密钥交换算法*，它是一种非对称加密算法。通信计算机使用该算法交换秘密密钥，用于第二个加密算法：旨在加密 TCP 数据包内容的对称块加密算法。最后，密码套件指定了一个 MAC 算法，用于验证加密消息的真实性。

让我们把这个内容更具体化。像 Google Chrome 这样的现代 web 浏览器支持 TLS 1.3，并提供了许多密码套件。在撰写本文时，其中一个密码套件的名字非常有趣，叫做 ECDHE-ECDSA-AES128-GCM-SHA256。这个特定的密码套件包括 ECDHE-RSA 作为密钥交换算法，AES-128-GCM 作为块密码，SHA-256 作为消息认证算法。

想要更多完全不必要的细节吗？好吧，*ECDHE* 代表 *椭圆曲线 Diffie-Hellman 密钥交换*（一种在不安全通道上建立共享密钥的现代方法）。*RSA* 代表 *Rivest–Shamir–Adleman* 算法（第一种实用的非对称加密算法，由三位数学家在 1970 年代发明，灵感来自他们喝了大量的逾越节酒）。*AES* 代表 *高级加密标准*（由两位比利时密码学家发明，并通过国家标准与技术研究院的三年审查过程被选中）。这个特定变体使用了 128 位密钥，采用 Galois/计数器模式，这就是名称中所指定的 *GCM*。最后，SHA-256 代表 *安全哈希算法*（一种具有 256 位字长的哈希函数）。

你看到了现代加密标准的复杂性了吗？现代浏览器和 web 服务器支持相当多的密码套件，而且随着时间的推移，TLS 标准中不断增加新的套件。随着现有算法的弱点被发现，计算能力变得更加廉价，安全研究人员会更新 TLS 标准，以保持互联网的安全。作为一名 web 开发者，了解这些算法如何工作并不是特别重要，但*保持你的 web 服务器软件最新*，以便能够支持最现代、最安全的算法，这一点非常重要。

##### 会话初始化

我们接着上次的内容继续。在 TLS 握手的第二阶段，web 服务器选择它能够支持的最安全的密码套件，并指示浏览器使用这些算法进行通信。与此同时，服务器返回一个*数字证书*，其中包含服务器名称、将为证书的真实性担保的受信证书机构，以及在密钥交换算法中使用的 web 服务器加密密钥。（我们将在下一节中讨论什么是证书以及它们为何对安全通信至关重要。）

一旦浏览器验证了证书的真实性，两个计算机会生成一个*会话密钥*，该密钥将用于使用选择的块加密算法加密 TLS 会话。（请注意，这个会话密钥与前面章节讨论的 HTTP *会话标识符*不同。TLS 握手发生在比 HTTP 会话更低级别的互联网协议中，而 HTTP 会话还未开始。）会话密钥是由浏览器生成的大随机数，用数字证书中附带的（公）加密密钥加密，采用密钥交换算法进行加密，并传输到服务器。

现在，TLS 会话终于可以开始了。此后所有的数据都会使用块加密算法和共享会话标识符进行加密，因此任何窃听会话的人都无法解读数据包。浏览器和服务器使用商定的加密算法和会话密钥在双向加密数据包。数据包还会进行身份验证并防篡改，使用消息认证码。

正如您所看到的，支撑互联网安全通信的是大量复杂的数学原理。幸运的是，作为一名 web 开发者，启用 HTTPS 所涉及的步骤要简单得多。现在我们已经了解了理论部分，让我们来看一下确保用户安全所需的实际步骤。

### 启用 HTTPS

为您的网站加密流量比理解底层加密算法要容易得多。大多数现代网页浏览器是自我更新的；每个主流浏览器的开发团队都会在支持现代 TLS 标准方面处于前沿地位。您网站服务器软件的最新版本也会支持类似的现代 TLS 算法。这意味着，作为开发者，您唯一需要做的就是获取一个数字证书并将其安装到您的网站服务器上。让我们来讨论如何做，并阐明为什么证书是必要的。

#### *数字证书*

*数字证书*（也称为*公钥证书*）是一种电子文档，用于证明公钥的所有权。数字证书在 TLS 中用于将加密密钥与互联网域名（如*example.com*）关联。它们由*证书颁发机构*（CA）颁发，证书颁发机构作为浏览器和网站之间的受信第三方，保证使用指定的加密密钥来加密发送到网站域名的数据。浏览器软件会信任几百个证书颁发机构——例如，Comodo、DigiCert，最近还有非营利组织 Let’s Encrypt。当一个受信的证书颁发机构担保某个密钥和域名时，它会确保您的浏览器正在与正确的网站进行通信，并且使用正确的加密密钥，从而阻止攻击者呈现恶意网站或证书。

你可能会问：为什么需要第三方来交换互联网中的加密密钥？毕竟，非对称加密的一个重点不是服务器自己可以自由提供公钥吗？虽然这个说法是对的，但实际上在互联网上获取加密密钥的过程依赖于互联网的*域名系统（DNS）*，它将域名映射到 IP 地址。在某些情况下，DNS 容易受到*伪造攻击*，这些攻击可以将互联网流量引导到攻击者控制的 IP 地址，而不是合法的服务器。如果攻击者能够伪造互联网域名，他们可以颁发自己的加密密钥，受害者通常不会察觉。

证书授权机构的存在是为了防止加密流量被伪造。如果攻击者找到方法将流量从合法（安全）网站转移到他们控制的恶意服务器，攻击者通常不会拥有与该网站证书对应的解密密钥。这意味着他们将无法解密使用与网站数字证书附带的加密密钥加密的拦截流量。

另一方面，如果攻击者提供一个*替代*的数字证书，该证书对应于他们*确实*拥有的解密密钥，那么该证书将不会经过受信任的证书授权机构验证。任何访问伪造网站的浏览器都会向用户显示安全警告，强烈劝阻用户继续访问。

通过这种方式，证书授权机构使用户能够信任他们访问的网站。你可以通过点击浏览器栏中的挂锁图标查看网站使用的证书。那里的信息可能不特别有趣，但浏览器能够很好地警告你当证书无效时。

#### *获取数字证书*

从证书授权机构获取数字证书需要几个步骤，通过这些步骤，授权机构可以验证你对域名的所有权。你执行这些步骤的具体方式取决于你选择的证书授权机构。

第一步是生成一个*密钥对*，这是一个包含随机生成的公钥和私钥的小型数字文件。接下来，使用这个密钥对生成一个*证书签名请求（CSR）*，该请求包含你网站的公钥和域名，并将请求上传到证书授权机构。在签署请求并颁发证书之前，证书授权机构将要求你证明你对 CSR 中包含的互联网域名具有控制权。一旦域名所有权得到验证，你就可以下载证书，并将其与密钥对一起安装到你的 Web 服务器上。

##### 生成密钥对和证书签名请求

密钥对和 CSR 通常使用命令行工具`openssl`生成。CSR 通常包含除了域名和公钥之外的其他信息，如组织的法律名称和实际位置。这些信息会被包含在签名证书中，但除非证书颁发机构选择验证它们，否则并不是强制性的。在生成签名请求时，域名通常被称为*区分名称（DN）*或*完全合格域名（FQDN）*，出于历史原因。列表 13-1 展示了如何使用`openssl`通过命令行生成证书签名请求。

```
openssl req -new -key ./private.key -out ./request.csr
```

*列表 13-1：通过命令行使用 openssl 生成证书签名请求*

文件*private.key*应该包含一个新生成的私钥（也可以通过`openssl`生成）。工具`openssl`会要求提供一些信息，用于生成签名请求，包括域名。

##### 域名验证

*域名验证*是证书颁发机构验证申请证书的人员是否确实拥有该域名控制权的过程。在申请数字证书时，您声明需要能够解密发送到特定互联网域名的流量。证书颁发机构会坚持检查您是否拥有该域名，作为尽职调查的一部分。

域名验证通常需要您临时编辑域名的 DNS 记录，从而证明您拥有 DNS 的编辑权限。域名验证可以防止 DNS 欺骗攻击：攻击者无法申请证书，除非他们也有编辑权限。

##### 扩展验证证书

一些证书颁发机构会颁发*扩展验证（EV）*证书。这些证书要求证书颁发机构收集并验证申请证书的法律实体的信息。这些信息将被包含在数字证书中，并通过浏览器提供给访问网站的用户。EV 证书在大型组织中非常受欢迎，因为公司的名称通常会与浏览器 URL 栏中的挂锁图标一起显示，增强用户的信任感。

##### 过期和撤销证书

数字证书有一个有限的有效期（通常是几年或几个月），到期后必须由证书颁发机构重新颁发。证书颁发机构还会追踪被证书持有者自愿*撤销*的证书。如果与你的数字证书对应的私钥被泄露，作为站点所有者，您需要申请一个新证书，并撤销之前的证书。浏览器会在用户访问带有过期或已撤销证书的网站时发出警告。

##### 自签名证书

对于某些环境，尤其是测试环境，从证书授权机构获取证书是没有必要的或不切实际的。例如，仅在内部网络中可用的测试环境无法通过证书授权机构验证。然而，你可能仍然希望在这些环境中支持 HTTPS，因此解决方案是生成自己的证书——即*自签名证书*。

像`openssl`这样的命令行工具可以轻松生成自签名证书。浏览器遇到自签名证书的网站时，通常会发出严厉的安全警告（`此网站的安全证书不被信任！`），但仍然允许用户接受风险并继续访问。只要确保使用你测试环境的任何人都知道这个限制，并理解为何会出现此警告。

##### 你是否需要为证书付费？

证书授权机构传统上是商业实体。即使到今天，它们中的许多仍然对每个签发的证书收取固定费用。自 2015 年以来，加利福尼亚的非营利组织 Let's Encrypt 提供了免费的证书。Let's Encrypt 的创始人包括 Mozilla 基金会（负责 Firefox 浏览器的发布）和电子前沿基金会（一个总部位于旧金山的数字权利非营利组织）。因此，除非你需要商业证书授权机构提供的扩展验证功能，否则没有太多理由为证书付费。

#### *安装数字证书*

一旦你拥有了证书和密钥对，下一步就是让你的 web 服务器切换到使用 HTTPS，并在 TLS 握手过程中提供证书。这个过程会根据你的托管服务提供商和服务器技术有所不同，尽管通常它是相对直接且文档完善的。让我们回顾一下一个典型的部署过程——这将需要一个简短的插曲。

##### Web 服务器与应用服务器

到目前为止，我在本书中描述了 web 服务器作为拦截和响应 HTTP 请求的机器，并讨论了它们如何针对每个请求发送静态内容或执行代码。虽然这是一个准确的描述，但它忽略了一个事实，即网站通常作为一对运行的应用程序来部署。

运行典型网站的第一个应用程序是一个*web 服务器*，它提供静态内容并执行低级 TCP 功能。它通常是像 Nginx 或 Apache HTTP 服务器这样的软件。Web 服务器是用 C 语言编写的，并优化以快速执行低级 TCP 功能。

配对的第二个应用是*应用服务器*，它位于 web 服务器的下游，并托管构成网站动态内容的代码和模板。每种编程语言都有许多应用服务器可供选择。一个典型的应用服务器可能是 Java 语言网站使用的 Tomcat 或 Jetty；Ruby on Rails 网站使用的 Puma 或 Unicorn；Python 网站使用的 Django、Flask 或 Tornado，等等。

有点让人困惑的是，web 开发人员常常随意称他们使用的应用服务器为“web 服务器”，因为那是他们大部分时间编写代码的环境。实际上，完全可以单独部署一个应用服务器，因为应用服务器可以做 web 服务器能做的一切，尽管效率较低。这在 web 开发人员在自己机器上编写和测试代码时是一个典型的设置。

##### 配置你的 web 服务器以使用 HTTPS

数字证书和加密密钥几乎总是部署到 web 服务器上，因为它们比应用服务器更快。将 web 服务器切换为使用 HTTPS，只需更新 web 服务器的配置，使其接受标准 HTTPS 端口（443）上的流量，并告诉它在建立 TLS 会话时使用的数字证书和密钥对的位置。列表 13-2 展示了如何将证书添加到 Nginx web 服务器的配置文件中。

```
server {
    listen              443 ssl;
    server_name         www.example.com;
    ssl_certificate     www.example.com.crt;
    ssl_certificate_key www.example.com.key;
    ssl_protocols       TLSv1.2 TLSv1.3;
    ssl_ciphers         HIGH:!aNULL:!MD5;
}
```

*列表 13-2：描述配置 Nginx 时数字证书（*www.example.com.crt*）和加密密钥（*www.example.com.key*）的位置*

以这种方式处理 TLS 功能的 web 服务器将解密传入的 HTTPS 请求，并将任何需要由应用服务器处理的请求以未加密的 HTTP 请求传递下去。这被称为在 web 服务器上*终止 HTTPS*：web 服务器与应用服务器之间的流量是不安全的（因为加密已被去除），但通常这不会构成安全风险，因为流量不会离开物理机器（或者至少仅在私有网络中传递）。

##### 那 HTTP 呢？

配置你的 web 服务器以监听 443 端口上的 HTTPS 请求，需要对配置文件进行一些编辑。接着，你需要决定 web 服务器如何处理标准 HTTP 端口（80）上的未加密流量。通常的方法是指示 web 服务器将不安全的流量重定向到相应的安全 URL。例如：如果用户代理访问*http://www.example.com/page/123*，web 服务器将返回`HTTP 301`响应，指示用户代理改为访问*https://www.example.com/page/123*。浏览器会理解为这是一个指令，要求在完成 TLS 握手后，使用 443 端口发送相同的请求。列表 13-3 展示了如何将所有流量从 80 端口重定向到 Nginx web 服务器上的 443 端口的示例。

```
server {
    listen 80 default_server;
    server_name _;
    return 301 https://$host$request_uri;
}
```

*列表 13-3：在 Nginx Web 服务器上将所有 HTTP 重定向到 HTTPS*

##### HTTP 严格传输安全性

到此为止，你的网站已经设置好与浏览器的安全通信，任何使用 HTTP 的浏览器都会被重定向到 HTTPS。你还有一个最终的漏洞需要修复：你需要确保在任何初始的 HTTP 连接中，不会发送敏感数据。

当浏览器访问一个它以前访问过的网站时，浏览器会在请求的`Cookie`头部发送回网站之前提供的所有 cookie。如果最初的连接是通过 HTTP 进行的，那么即使随后的请求和响应升级到 HTTPS，这些 cookie 信息也会不安全地传输。

你的网站应该通过实施*HTTP 严格传输安全（HSTS）*策略，指示浏览器*仅*通过 HTTPS 连接发送 cookie。你可以通过在响应中设置`Strict-Transport-Security`头来实现这一点。现代浏览器遇到这个头部时，会记住只使用 HTTPS 连接到你的网站。即使用户明确输入一个 HTTP 地址，如*http://www.example.com*，浏览器也会自动切换到 HTTPS，而无需提示。这可以防止在初次连接到你的网站时 cookie 被窃取。列表 13-4 展示了在使用 Nginx 时如何添加`Strict-Transport-Security`头。

```
server {
    add_header Strict-Transport-Security "max-age=31536000" always;
}
```

*列表 13-4：在 Nginx 中设置 HTTP 严格传输安全性*

浏览器会记住在`max-age`指定的秒数内不通过 HTTP 发送任何 cookie，之后会检查该网站是否更改了其策略。

### 攻击 HTTP（和 HTTPS）

在本章的这一部分，你可能会问：如果我选择*不*使用 HTTPS，最坏的情况会怎样？我还没有真正描述未加密的 HTTP 是如何被利用的，我们来补充这一点。互联网中的弱加密或未加密通信允许攻击者发起中间人攻击，在这种攻击中，他们篡改或窃听 HTTP 会话。让我们来看一些来自黑客、互联网服务提供商和政府的最近例子。

#### *无线路由器*

无线路由器是中间人攻击的常见目标。大多数路由器都包含一个简单的 Linux 操作系统安装，使其能够将流量路由到本地*互联网服务提供商（ISP）*并托管一个简单的配置界面。这是黑客的完美目标，因为 Linux 系统通常*永远*不会更新安全补丁——而且同一操作系统版本会安装在成千上万的家庭中。

2018 年 5 月，思科安全研究人员发现超过 50 万个 Linksys 和 Netgear 路由器感染了一种名为*VPNFilter*的恶意软件，该恶意软件会监听通过路由器传输的 HTTP 流量，窃取网站密码和其他敏感用户数据，攻击者被认为与俄罗斯政府有关。VPNFilter 甚至试图执行*降级攻击*，干扰与流行网站的初始 TLS 握手，使浏览器选择使用较弱的加密方式或根本不加密。

使用 HTTPS 的网站将不会受到这种攻击的影响，因为 HTTPS 流量除了接收方网站之外，任何人都无法解密。其他网站的流量可能已被黑客窃取并挖掘敏感数据。

#### *Wi-Fi 热点*

黑客发起中间人攻击的另一种低技术方法是简单地在公共场所设置自己的 Wi-Fi 热点。我们中的大多数人并不太关注设备连接的 Wi-Fi 热点的名称，因此攻击者很容易在咖啡馆或酒店大堂等公共场所设置一个热点，并等待不知情的用户连接。因为 TCP 流量会通过黑客的设备流向 ISP，黑客将能够将流量记录到磁盘中，并仔细分析以提取敏感信息，如信用卡号码和密码。受害者唯一能察觉到的不正常情况是，当攻击者离开物理位置并关闭热点时，受害者的设备与互联网断开连接。加密流量能够防止此类攻击，因为黑客无法读取他们捕获的任何流量。

#### *互联网服务提供商*

互联网服务提供商将个人用户和企业连接到互联网主干网，考虑到传输数据可能具有的敏感性，这是一个巨大的信任位置。你可能认为这会阻止他们监听或干扰 HTTP 请求，但像美国最大 ISP 之一的 Comcast 这样的公司并没有这么做，Comcast 多年来曾将 JavaScript 广告注入流经其服务器的 HTTP 流量中。Comcast 声称这样做是为了提供服务（许多广告告知用户每月数据计划已经使用了多少），但数字权利活动人士认为这种做法类似于邮递员把广告材料塞进封好的信件里。

使用 HTTPS 的网站免疫此类篡改，因为每个请求和响应的内容对 ISP 是不透明的。

#### *政府机构*

政府机构窃听你的互联网流量可能听起来像是阴谋论，但大量证据表明这确实发生过。美国**国家安全局（NSA）**成功地实施了中间人攻击进行监控。前 NSA 承包商爱德华·斯诺登泄露的一份内部报告描述了巴西国有石油公司 Petrobras 如何被监控：NSA 获取了 Google 网站的数字证书，然后托管了自己仿制的网站，在代理 Google 流量的同时窃取用户凭证。我们并不清楚这种程序的普遍性，但想一想真的让人不安。（如果有政府人员在阅读此内容：事实上，这种程序是好的，能够确保我们的安全，本书作者完全支持它。）

### 总结

你应该使用 HTTPS 来确保从网页浏览器到你网站的通信是私密的，且不能被篡改。HTTPS 是通过传输层安全协议（TLS）发送的 HTTP。当网页服务器和用户代理参与 TLS 握手时，会启动 TLS 会话。在 TLS 握手过程中，浏览器会提供它支持的加密套件列表。每个加密套件包含一个密钥交换算法、一个块加密算法和一个消息认证码算法。网页服务器选择一个它支持的加密套件，并返回其数字证书。

然后，浏览器使用附加在数字证书上的公钥，利用密钥交换算法加密一个（随机生成的）TLS 会话标识符，并将其发送给网页服务器。最后，当双方都拥有会话标识符时，他们将使用它作为后续消息的加密/解密密钥，使用选定的块加密算法进行加密。每个数据包的真实性将使用消息认证码算法进行验证。

数字证书由少数几个证书颁发机构（CA）颁发，这些机构在颁发证书之前需要你证明你拥有所选域名的所有权。证书颁发机构充当浏览器与网站之间的受信任第三方，防止伪造网站展示虚假的证书。

一旦你获得了网站的证书，你需要通过 HTTPS 提供内容。这意味着需要配置你的网页服务器以接受通过 443 端口的流量，告诉它在哪里找到证书和相应的解密密钥，并将 80 端口上的 HTTP 流量重定向到 443 端口上的 HTTPS 流量。最后，你应该指示浏览器在升级到 HTTPS 之前，不通过 HTTP 请求发送任何敏感数据——例如，session cookie，通过设置 HTTP 严格传输安全（HSTS）策略。

确保定期升级你的 web 服务器技术，以确保你使用的是最现代化（也因此最安全）的加密套件。加密标准不断被研究和增强，因为旧的算法会被破解或发现存在漏洞。

在我们讨论需要保持 web 服务器更新时，你应该更广泛地考虑如何测试、保护以及管理你用来提供网站服务的任何第三方应用程序。这正是你将在下一章中要做的事情！
