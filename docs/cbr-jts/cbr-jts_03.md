# 第三章：排外安全

如果你没有多加思考就接纳陌生人，敌方忍者可能会伪装成陌生人进入，并从内部获取情报。

> 如果乞丐或弃民接近警卫室，要粗暴对待并赶走他们。
> 
> —吉守百首 #91

在本章中，我们将探讨*排外安全*的概念——即基于对外部人员的不信任的安全性——以及如何将其应用为一种反特权保护域。为了说明这个概念，我们将考虑忍者必须面对的敌对环境。

想要渗透村庄并在明面上收集情报的忍者面临着一个普遍的挑战：中世纪日本的普遍排外情绪。国家的村庄与世隔绝，形成了独特的方言、发型、服饰和其他习俗，使每个社区都有自己的社会生态系统。^(1) 这些偏远地区的小规模人口意味着每个人通常都认识彼此，而外来者显然无法融入。^(2)

作为外来者，忍者常常被怀疑并受到监视。他们不能在镇上自由行动，通常也无法租房和购买食物。当然，村民们也不会与他们共享信息。社区的排外情绪将忍者降为反特权身份。

## 理解反特权

为了理解反特权的意义，我们首先需要了解*特权*的概念，在网络安全中，它指的是用户执行某些操作的权限，例如读取或删除文件。现代计算机系统采用分层架构，具有不同级别的特权：

1.  **ring4** 默认（无特权）

1.  **ring3** 普通用户（最低特权）

1.  **ring2** 超级用户（管理员）

1.  **ring1** 根用户（提升特权）

1.  **ring0** 内核（系统）

例如，一名普通村民（最低特权）或一只猫（无特权）可以随时离开村庄。而一位拥有更高特权的村长则具有随意锁闭村门的额外权限。然而，一个被怀疑有不轨行为的外来者（反特权）可能拥有比流浪猫（无特权）更少的权限，因此不能离开村庄。

这种反特权和非特权身份的区别非常重要。在某些计算机系统中，诸如注销这样的操作被视为非特权操作，通常默认所有环中的行为者都有权限进行。不可被信任的进程/用户可以利用这些默认的非特权权限，执行更具恶意的操作，或自由操作以实现更复杂的目标。另一方面，通过拒绝反特权进程注销，你可以防止其清除会话历史或消除其存在的证据。试想一下，计算机系统是否可以采用一个 ring5（反特权）安全控制。以我们的村庄为例，可以设想强制怀疑是忍者的人在离开村庄前接受搜查和审问。这样，村庄可以抓住小偷和间谍。此外，通过让潜入者的任务变得更加危险和昂贵，村庄无疑会阻止敌对活动。

为了渗透这样一个排外的村庄，忍者首先必须记住并练习一系列文化上具有特色的伪装，熟练掌握该地区的穿着风格、方言、梳理技巧、货币习俗和社会规范。

当文化伪装掌握后，忍者仍然需要有一个令人信服的理由进入村庄；通常这是与工作相关的。*《忍秘传》*描述了忍者如何适用一个通用的掩护故事，或许声称自己是一个进行精神旅行的僧侣，一个商人，一个乞丐，甚至是一个奉命出行的武士。（尽管武士也被村民认作是外来者，但他们不像潜在的逃犯或盗贼那样遭遇同等的怀疑。）

在伪装成与自己相同职业、阶层或种姓的人群中，忍者被建议表现出足够的专业知识，使自己在职业上看起来可信，但也要装作愚笨，需要帮助才能完成常见任务。装作无知的行为旨在让目标误解忍者的真实智慧，同时抬高目标自己的自尊心，从而让他们放松警惕，自愿提供信息。*《忍秘传》*列出了忍者应尝试用这些策略争取的特定目标，例如地方官员、法官、医生、僧侣以及可能在当地领主或权威面前工作的人。这些目标通常拥有对任务有价值的信息。^(3)

请注意，中世纪日本村庄的社会等级结构类似于现代计算机系统中的特权环结构，甚至类似于计算机网络的分层隔离，其中外层像是 DMZ，最不受信任。同样，普通村民（最低特权者）无法与位于中心的领主互动，或者说是 ring0\。

我们可以将忍者识别潜在目标的方式应用于网络安全领域。正如忍者将目标瞄准那些比喻上接近 ring0 或拥有 ring0 访问权限的人一样，现代的威胁行为者也会针对特权系统/用户。因此，防御者应考虑在其系统中，类似僧侣和地方官员等高地位人物的计算机等价物是什么。此外，您还应该考虑现代威胁行为者可能使用什么伪装来接近更有特权的系统/用户。

## 互操作性和通用标准的问题

无论他们是否有意识地思考，*互操作性*对于技术消费者来说都是重中之重：人们期望他们的设备、应用程序、系统和软件能够无缝地与新旧版本兼容，并且可以在不同平台之间以及与其他品牌和型号互换使用。国际标准化组织（ISO）、国际电工委员会（IEC）、互联网工程任务组（IETF）、互联网协会（ISOC）和其他管理机构已经制定了广泛认可的技术设计、操作和集成标准。

这些努力催生了许多 ISO 标准、请求评论（RFC）以及其他使计算机更加易于访问的互操作性协议，更不用说它们也让计算机的构建、管理、诊断、修复、编程、网络和运行变得更加容易了。一个典型的例子是 1995 年引入的即插即用（PnP）标准，它指示主机系统通过 USB、PCI、PCMCIA、PCIe、FireWire、Thunderbolt 或其他方式检测并接受任何插入的外部设备，然后自动配置、加载、安装并自动连接。

不幸的是，当目标是建立功能并保持其可操作性时，安全性几乎从未是优先考虑的问题。事实上，PnP 标准——它促进了对陌生实体的信任和接受——的构建恰恰与中世纪日本的排外安全标准相反。例如，一个陌生的系统可以作为外部者连接到网络，并从动态主机配置协议（DHCP）请求 IP 地址，向本地路由器请求指令，查询权威 DNS 服务器以获取其他设备的名称，并从地址解析协议（ARP）、服务器消息块（SMB）、Web 代理自动发现（WPAD）和其他旨在简化兼容性负担的协议中获取本地信息。您将系统插入网络，它就能工作，展现出用户期望和希望的行为。然而，网络安全行业如果能在其网络协议中更加“排外”，将会受益匪浅。

为了减轻由于 PnP（即插即用）类似的可访问性带来的弱点，已经引入了如网络访问控制（NAC）和组策略对象（GPO）等安全控制。在主机系统上，这些技术可以防范可能存在恶意的外部设备，这些设备物理连接到内部网络或系统。

NAC 通常会锁定 DHCP，将未识别的计算机分配到访客 IP 子网或未授权的 VLAN。这允许外部系统连接到互联网以进行一般访问，但将它们与其他受信网络隔离开来。这种行为在会议室和大厅中特别受到青睐，以便外部合作伙伴和供应商能够在不暴露网络威胁的情况下操作。

本地主机上的 GPO（组策略对象）强制执行哪些类型的设备——外部硬盘、USB、媒体读取器等——可以在系统上配置和安装。GPO 甚至可以在组织内白名单已知应用程序，同时阻止所有不熟悉的软件从下载或安装到主机系统中。

然而，这些安全控制是显著的例外。从使用 EIA/TIA-561 和 Yost 标准的 RJ45 以太网插座，到使用 IEEE 802 标准的基于数据包的网络——以及其中的一切——大多数技术都是基于透明、广泛知晓的默认标准构建的，这些标准确保了跨外部系统和网络的快速、简便的使用，但也使它们容易受到未经授权的流氓系统的攻击，这些系统可能进行网络发现、侦察、嗅探和通信。

## 为您的环境开发独特的特征

在您的 IT 资产清单中拥有独特的属性和特征将有助于区分您的资产与可能进入环境的流氓资产，甚至可以保护您的网络免受侵害。这些特征可以通过检查或分析观察到，但它们的使用不应公开披露，因为公开披露会削弱反制措施。现代 IT 系统和软件中的大多数元素都是可配置的，这种配置的变化有效地在您的系统中创建了排外的 IT 模型。

最近推出的采用零信任模型的商业产品，通过技术协议和不信任的结合，能够帮助使您的网络或系统对不熟悉的系统、软件和设备“排外”。严格的白名单和身份验证/授权程序可以达到类似的效果，但一个适当的解决方案将引入计算机版本的“方言”——设置、习惯和其他与通用计算标准不同的独特特征。连接到您内部网络的系统或设备需要“灌输”组织的独特文化，而未经灌输的服务器、组件、网络设备和协议将不信任或拒绝这些不熟悉的外部代理，并向安全团队报告其存在。

通过一些创造性和工程手段，这些文化计算机标识符可以在开放系统互联（OSI）模型的任何层（应用层、表示层、会话层、传输层、网络层、数据链路层、物理层）中实现，用于识别网络外部人员，并为对抗敌人提供额外的防御层。无论是在 RJ45 插口的隐藏适配器中交换某些线路，期望在 TCP/IP 级别进行秘密握手（SYN、SYN ACK、ACK-PUSH），还是在以太网头部使用保留位，排外解决方案都应该是模块化的、可定制的，并且每个实例都应是独一无二的。

## 推荐的安全控制和缓解措施

在相关情况下，以下推荐措施与 NIST 800-53 标准中的适用安全控制一起呈现。每一项都应根据排外安全的概念进行评估。

1.  检查系统以确定其规格或要求是否偏离先前达成的基准配置。[CM-2: 基准配置]

1.  保持贵组织所有信息系统的文档，以便更容易识别环境中的外部系统。[CM-8: 信息系统清单]

1.  在通信中使用加密信息、嵌入数据、特殊数据类型或元数据（例如，将所有数据包填充到特定大小）作为特殊标识符，以便过滤器能够识别并限制不熟悉的流量。[AC-4: 信息流控制；SA-4: 获取过程]

1.  限制将排外标识符应用于新获得的系统和设备的实施和知识。[SA-4: 获取过程]

1.  将排外检查嵌入为安全控制，用于识别和验证贵组织中的系统和设备。[IA-3: 设备识别与验证]

## 汇报

本章描述了历史上忍者所处的排外环境，需要投入时间和精力，以及先进的技术，才能使用公开伪装战术进行预备侦察，然后才能开始实际目标侦察。你学习了反特权的概念，以及如何创建独特的内部特征来识别环境中的流氓资产或用户。现在，你可能已经能够识别出环境中可能成为目标的关键资源或人物，这些是你可能未曾考虑过的攻击面，你可以进一步考虑与这些潜在目标紧密合作的系统或账户。

然而，通过使用正确的徽章、服装、发型、口音和其他特征，忍者可以避开本章详细描述的排外检查。因此，在下一章中，我们将探讨日本领主历史上用于检测忍者的匹配对安全技术，以防忍者通过伪装渗透其防御工事。
