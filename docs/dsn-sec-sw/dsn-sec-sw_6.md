# 第三章：B

术语表

![](img/chapterart.png)

专门针对软件安全的术语可能看起来很直观，但细微差别很重要，我根据在多个公司和众多项目中的经验，发展出了以下关于术语的安全特定含义，尽管这些定义普遍被接受，但如果你在实际使用中发现术语有所不同，也不要感到意外。如果你留心观察，你会发现安全专家在定义和使用相同的术语时，往往会带有稍微不同的含义，并从各自独特的角度来阐述这一领域的基础原则。你会听到很多变体，因为没有公认的标准词汇表；然而，这些变体通常可以根据上下文轻松推断出来。

受影响的用户

评估可能受到特定漏洞利用影响的用户比例。（*DREAD*的组成部分）

允许列表

允许的安全值的枚举。（参见 *Blocklist*）

评估报告

安全设计评审（SDR）的书面结果，包括按排名排列的发现和建议的总结，涉及特定设计变更和提高安全性的策略。

资产

有价值的数据或资源，特别是攻击的可能目标，需要被保护。

非对称加密

数据加密使用独立的密钥进行加密（公钥）和解密（私钥）。（参见 *对称加密*）

攻击

采取的行动，试图破坏安全性。

攻击者

一个恶意代理，试图破坏系统的安全性。（也称为 *威胁行为者*）

攻击面

系统中所有潜在入侵点的总和，用于攻击。

攻击向量

一系列步骤构成了一个完整的攻击过程，从攻击面开始，最终导致对资产的访问。

审计

保持可靠的记录，以便定期检查，检测可能表明不当活动的可疑行为。（*金标准*的组成部分）

身份验证（authN）

高度保证的主体身份确认。（*金标准*的组成部分）

真实性

确保数据真实性的保证，比数据完整性更强的声明。

授权（authZ）

确保特权访问仅限于某些已认证主体的安全策略控制。（*金标准*的组成部分）

可用性

确保数据访问始终对授权主体可用；换句话说，系统避免了妨碍合法访问的重大延迟或停机。（*C-I-A*的组成部分）

回溯

算法行为，如正则表达式匹配，其中进展可能会前进或回退，呈指数级重复。当回溯导致过多的计算时，可能会出现潜在的安全问题，从而降低可用性。

分组密码

一种对固定长度数据块进行加密处理的对称加密算法，与比特流相对。

阻止列表

一种列举应当禁止的危险值的方式。通常不推荐使用，因为除非完全列举，否则存在漏洞的风险。（参见*允许列表*）

瓶颈

代码执行路径中的单一节点，保护对特定资产的所有访问。瓶颈对于安全性至关重要，因为它们确保所有访问都进行统一的授权检查。

缓冲区溢出

一类涉及无效访问超出分配内存范围的漏洞。

证书授权机构（CA）

数字证书的颁发者。

瓶颈点

见*瓶颈*。

选择明文攻击

对加密的分析，攻击者能够学习明文对应的密文，从而削弱加密强度。

C-I-A

信息安全的基本模型。（见*机密性*、*完整性*和*可用性*）

密文

消息的加密形式，如果没有密钥则无法解读。

代码访问安全（CAS）

一种根据所有调用者的权限动态调整授权的安全模型，以减轻混淆代理漏洞。

碰撞

当两个不同的输入生成相同的消息摘要值时。

碰撞攻击

一种利用已知碰撞来颠覆依赖于加密消息摘要值唯一性的真实性的攻击。

命令注入

一种漏洞，允许恶意输入导致执行攻击者控制的任意命令。

机密性

强制只允许授权访问数据的信息安全基本属性。（*C-I-A* 组件）

混淆代理

一种脆弱模式，其中未经授权的代理可以欺骗授权的代理或代码，代表其执行有害的操作。

凭证

作为身份验证依据的身份、属性或权限的证据。

跨站请求伪造（CSRF 或 XSRF）

一种修改网站服务器状态的攻击，通常通过使用带有受害者客户端的 Cookie 上下文的 POST 请求。

跨站脚本攻击（XSS）

一种针对网站的特定注入攻击，其中恶意输入改变了网站的行为，通常会导致执行未经授权的脚本。

加密技术

将数据可逆地转换以隐藏其内容的数学方法。

加密安全伪随机数生成器（CSPRNG）

一种随机数源，认为其不可预测到足以无法猜测，因此适用于加密。（参见*伪随机数生成器*）

损害潜力

通过利用特定漏洞所造成的潜在危害程度的评估。（*DREAD* 组件）

去匿名化

对假定匿名的数据进行分析，推断出身份特征，从而破坏匿名性的程度。

解密

将密文转换回原始明文消息的过程。

拒绝服务（DoS）

一种消耗计算资源以降低可用性的攻击。（也是*STRIDE*组件）

依赖关系

软件库或系统中的其他组件，软件操作时所需的资源。

对话疲劳

人类对重复或无信息的软件下载对话框的反应，通常导致用户反射性地回应对话框以完成目标。当用户未能理解或考虑其行为的安全后果时，便会产生安全影响。

摘要

从任意大数据输入中计算出的唯一固定大小的数值。不同的摘要值保证输入不同，但可能会发生碰撞。（也叫做 *哈希*）

数字证书

一种经过数字签名的声明，宣称签名者的特定主张。常见的数字证书标准包括 TLS/SSL 安全通信（无论是服务器端还是客户端）、代码签名、电子邮件签名和证书颁发机构（根、中间、叶）。

数字签名

证明掌握私钥的一种计算方法，验证签名者的真实性。

可发现性

评估潜在攻击者如何容易地得知特定漏洞存在的过程。（*DREAD* 的组成部分）

分布式拒绝服务攻击（DDoS）

协调的拒绝服务攻击，通常使用大量机器人群体进行协调。

DREAD

用于评估漏洞严重性的五个组成部分的首字母缩略词。（见 *损害潜力*、*可复现性*、*可利用性*、*受影响的用户* 和 *可发现性*）

电子密码本（ECB）模式

一种块加密模式，其中每个块独立加密。由于相同的块会生成相同的输出，ECB 模式较弱，通常不推荐使用。

权限提升

任何通过攻击者利用漏洞获取更高权限的手段。（*STRIDE* 的组成部分）

加密

一种将明文转换为密文以秘密传达消息的算法。

熵源

一种生成不可预测比特流的随机输入源。

利用

违反安全规则并造成伤害的有效攻击方法。

可利用性

评估特定漏洞是否容易被利用的程度。通常这是一个主观的猜测，因为存在许多未知因素。（*DREAD* 的组成部分）

通信事实

知道两个通信者是否交换了信息，例如通过窃听者观察无法解密的加密消息。

缺陷

可能是漏洞也可能不是漏洞的缺陷，可能出现在设计或实现中。

脚枪

一种使得引入漏洞，尤其是安全漏洞，变得容易的软件特性。

模糊测试

通过自动化暴力测试和任意输入来发现软件缺陷。

金标准

三个基本安全执行机制的昵称。（见 *审计*、*认证* 和 *授权*）

守护

软件中的一种授权执行机制，用于控制对资源的访问。

硬件随机数生成器（HRNG）

一种硬件设备，旨在高效产生高度随机的数据。（见*加密安全伪随机数生成器*）

哈希

见*摘要*。

哈希消息认证码（HMAC）

一类消息摘要函数，其中每个密钥值决定唯一的消息摘要函数。

事件

安全攻击的特定实例。

信息泄露

未授权的信息泄露。（*STRIDE*组件之一）

注入攻击

一种安全攻击，利用恶意输入来利用漏洞，其中部分输入被以意外的方式解释。常见形式包括 SQL 注入、跨站脚本、命令注入和路径遍历。

输入验证

防御性检查输入数据，确保其格式有效，能够正确处理。

集成测试

多个组件协同操作的软件测试。（参见*单元测试*）

完整性

维护数据准确性的基本信息安全属性，或仅允许授权的修改和删除。（*C-I-A*组件之一）

密钥

决定数据如何转化的密码算法参数。（见*私钥*，*公钥*）

带密钥哈希函数

见*哈希消息认证码（HMAC）*。

密钥交换

一种协议，供两个通信方建立一个秘密密钥，即使所有交换的消息内容被攻击者揭露，密钥仍然安全。

消息认证码（MAC）

附带消息的数据，作为证据证明消息的真实性且未被篡改。（参见*哈希消息认证码*）

消息摘要

见*摘要*。

缓解措施

一种预防性对策，用于防止潜在攻击或减少其危害，如通过最小化损害、使攻击可恢复或便于检测来降低影响。

随机数

一次性使用的任意数字，例如在通信协议中防止重放攻击。

一次性密码本

用于消息加密的共享秘密密钥，由于重用会削弱其安全性，因此只能使用一次。

溢出

算术指令的错误结果，当值超出变量的容量时。未被检测到的溢出通常会通过引入意外的结果导致漏洞。

路径遍历

一种常见的漏洞，恶意输入将意外的内容注入文件系统路径，允许其指定超出预定访问范围的文件。

明文

加密前的原始消息，或由预定接收方解密后的消息。

预映像攻击

一种对消息摘要函数的攻击，试图找到一个输入值，该值生成特定的消息摘要值。

主要参与者

经过认证的代理：一个人、企业、组织、应用、服务或设备。

私钥

解密所需的参数，由授权接收方保密。

追溯

提供可靠的历史记录，追溯数据的来源和链条，增强数据有效性的信心。

伪随机数生成器（PRNG）

一种“相当好”的随机数生成器，易受到复杂分析的预测。这些随机数适用于许多用途，例如模拟，但由于它们不够随机，因此不适用于加密。（参见 *加密安全伪随机数生成器*）

公钥

为特定接收者加密消息所需的广泛已知参数。

随机数

一个任意选择的无法可靠预测的数字。

限速

一种减缓过程的方法，通常用于缓解依赖暴力重复才能成功的攻击。

重放攻击

通过重新发送先前的真实消息来攻击安全通信协议。如果攻击者重新发送之前的真实通信副本，并被误认为是原始发送者发送的后续相同消息，则重放攻击成功。

可重现性

评估在多次重复尝试中，特定漏洞被利用的可靠性。（*DREAD*的组成部分）

否认

行为的可信否认，特别是允许攻击者逃避责任。（*STRIDE*的组成部分）

根证书

自签名数字证书，授权信任证书颁发机构。

同源策略（SOP）

一组由网页客户端强制执行的限制，用于限制不同网站的不同窗口之间的访问。

沙箱

一种限制执行环境，旨在限制代码执行时可用的最大权限。

安全设计评审（SDR）

对软件设计安全性的结构化评审。

安全帽

一种表达方式，故意以安全思维为重点，思考事情可能出错的方式。

安全回归

已修复的已知安全漏洞的复发。

安全测试用例

检查安全控制是否正确实施的软件测试用例。

安全测试

确保安全控制正常工作的软件测试。

辅助通道攻击

一种间接推导机密信息的攻击方式，而不是直接破解保护机制。例如，通过计算结果的时间延迟可靠地推断计算结果的知识。

投机执行

现代处理器中使用的优化方法，通过提前执行未来指令来节省时间，如果不需要，则通过回溯逻辑丢弃结果。投机执行对缓存状态的影响可能泄露原本无法访问的信息，构成安全威胁。

欺骗

身份验证的颠覆，攻击者冒充授权主体。（*STRIDE*的组成部分）

SQL 注入

一种漏洞，允许攻击者构造恶意输入以运行任意 SQL 命令。

STRIDE

六种基本软件安全威胁的缩写，有助于指导威胁建模。（参见 *欺骗*、*篡改*、*拒绝*、*信息披露*、*拒绝服务*、*权限提升*）

对称加密

一种加密方法，使用相同的密钥进行加密或解密。其对称性在于任何可以加密的人也可以解密。（参见 *非对称加密*）

污染

追踪数据来源的过程，使用软件来缓解不可信输入，或由这些输入影响的数据，防止它们用于特权操作，如注入攻击。

篡改

数据的未经授权修改。（*STRIDE* 的组成部分）

威胁

潜在或假设的安全问题。

威胁行为者

参见 *攻击者*。

威胁建模

对系统模型的分析，用于识别需要缓解的威胁。

定时攻击

一种侧信道攻击，通过测量操作的时间来推测信息。

信任

选择依赖于一个主体或组件，而在发生失败时无法通过求助保护。

下溢

浮点计算结果的精度丧失。

单元测试

独立于其他组件对单个模块进行的软件测试。

不可信输入

来源于不可信来源的输入数据，特别是来自潜在攻击面。

漏洞

使安全攻击成为可能的软件缺陷。

漏洞链

一系列漏洞，当这些漏洞结合在一起时，构成了一个安全攻击。

弱点

导致脆弱性的错误，因此可能成为漏洞。
