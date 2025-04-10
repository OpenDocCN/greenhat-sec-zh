

## 第八章：8 吸引业务方参与



![](img/opener.jpg)

有时候，很难向非技术人员解释，他们在网络安全事件中也有责任。 在本章的最后，我们重点介绍了旨在吸引业务部门特定群体参与的演练——即物理安全、沟通和人力资源部门。

虽然这些情景可能也涉及信息技术和信息安全人员，但我们设计这些情景的目的是要展示一个组织的事件响应不仅仅依赖于技术应急响应人员。当一个网络安全事件影响到业务时，组织才会真正感受到其带来的影响。

### 物理安全漏洞

很容易忽视信息安全事件可能源于物理世界中的安全漏洞。事实上，突破建筑物物理安全的威胁行为者，可能造成的破坏不亚于，甚至超过那些从远程攻破信息技术网络的攻击者。

探讨这样一个情景的好处之一是它涉及一个通常不会出现在信息安全桌面演练中的团队：物理安全。有些组织可能甚至没有这样的角色，而是将确保财产安全的责任交给风险管理或其他不相关的职能部门。

物理安全漏洞当然可能显得牵强，像是*碟中谍*电影中的场景（想象威胁行为者爬过加热和冷却的空气管道）。但即便是一个简单的攻击也能引发麻烦，正如我们在这里列举的例子。

#### 情景描述

威胁行为者通过绕过安全控制措施进入了物理建筑物。在建筑内，他们相对不受阻碍，可以自由地探索设施。经过一段时间后，他们带着一些有价值的物品离开，包括笔记本电脑、外部存储设备（如硬盘）和文件。

在演练的介绍中，威胁行为者穿着商务休闲服，进入 MedCo 总部大堂，MedCo 是一家医疗保险公司。为了继续前进，威胁行为者必须将通行卡放在射频识别（RFID）阅读器上，以获得访问权限并解锁门。

在早上 8:30，当员工们开始到 MedCo 上班时，脚步声最为密集，威胁行为者在背包里摸索，直到一位 MedCo 员工使用卡片进入，导致 RFID 阅读器发出哔哔声并解锁门。威胁行为者微笑并做出手势，表示他们找到了自己的卡片，从背包里拿出一张颜色相似的通行卡。他们把卡片靠近 RFID 阅读器（此时没有发出哔哔声），并抓住门，趁着门关上时进入。

威胁行为者现在已经进入了 MedCo 的安全设施。

+   MedCo 员工是否接受过关于物理安全访问威胁（例如尾随进入，这里发生过的事件）方面的培训？如果有的话，员工们会被培训做些什么？

+   是否有保安、监控摄像头或其他监视设备观察到这种不当的访问行为？

+   谁负责设施的物理安全？

##### 注入 1

威胁行为者伪装成 MedCo 员工，坐在为远程员工准备的桌子前。他们拿出一台笔记本电脑，并将可用的网络电缆插入自己的笔记本电脑，然后尝试连接到网络。

+   连接到组织网络的笔记本电脑是否需要进行身份验证？威胁行为者可能合理访问哪些 MedCo 资源？

+   信息安全团队是否会被提醒发现一个未知的信息系统连接到网络？是否会触发任何其他警报？

##### 注入 2

威胁行为者走到一名行政助理的桌前，说：“我是菲尔与儿子 HVAC 系统公司的员工。我们约定对服务器房间的 HVAC 系统进行维护检查。你能让我进去吗？Dave 应该知道我会来。”威胁行为者带着一小袋工具，乍一看像是 HVAC 技术员。Dave 是 MedCo 的 IT 经理，他的信息在 LinkedIn 上很容易找到。

+   承包商需要遵循什么流程来请求访问某个系统或房间？

+   是否有一个独特的流程用于请求访问敏感房间，例如包含服务器的房间？

+   MedCo 员工是否被鼓励或不鼓励在社交媒体上分享他们的工作信息？

##### 注入 3

行政助理要求威胁行为者坐下，同时明智地向信息技术部门核实。威胁行为者借口去洗手间。担心自己被发现，他们悄悄走向出口。

在离开之前，威胁行为者从无人看管的工作区收集三台笔记本电脑，将其放入背包中，然后走出大门。

+   假设员工在返回自己的工作区时发现他们的笔记本电脑丢失，是否有专门的流程供他们报告盗窃事件？

+   过去，员工是否使用过这个指定流程？

+   大厅、停车场、工作区域或其他地点是否有安全摄像头？如果有，它们的录像会保存多久？

+   为了追踪被盗或丢失的 MedCo 资产，采用了哪些方法？

##### 注入 4

威胁行为者离开设施并开车离开。丢失笔记本电脑的员工提醒信息安全部门，信息安全部门迅速通知了物理安全部门。

+   如果威胁行为者在离开之前关闭笔记本电脑或将其关机，他们是否可以稍后访问其内容？如果可以，他们怎么做？

+   确定被盗笔记本电脑的识别信息（如序列号）需要多长时间？组织是否能够确定（a）设备是否被加密，（b）设备上有哪些敏感信息？

+   是否可以远程禁用或清除设备？

+   是否有通知执法机关的流程？

+   如果笔记本电脑中包含敏感数据，是否应该通知其他 MedCo 部门，如法务团队，关于数据丢失的情况？

+   如果有安装摄像头，录像会保留多长时间？安防摄像头能否重建攻击者在设施内的活动轨迹？

#### 可能的修改

为了调整场景，可以考虑做出以下修改：

+   攻击者是一个前员工，熟悉如何在设施内进行导航。

+   攻击者窃取了存储在笔记本电脑或外部硬盘中的极其敏感的数据，需要采取重大响应措施。

+   攻击者成功进入组织网络，占领了更为重要的立足点。

+   攻击者伪装成帮助台团队成员，假装工作站存在问题，并请求访问员工的系统。

+   攻击者在下班后进入设施，伪装成清洁人员。

+   攻击者在环境中制造干扰，可能是通过虚拟手段，或通过物理篡改网络设备。

+   攻击者在环境中安装了物理设备，如模仿合法信号的恶意 Wi-Fi 接入点。

### 社交媒体泄露

组织使用社交媒体账户的程度各不相同。对于一些组织，这些账户是与客户（甚至员工）沟通的主要方式。社交媒体还使组织能够塑造其品牌形象，而这可能需要多年的努力。以下场景最适用于这些社交媒体导向型公司。

由于社交媒体泄露自一开始就是公开的，因此应对这一事件的响应需要更加紧急。更重要的是，这需要通常不紧密合作的团队之间的协作，如信息安全团队和负责社交媒体的团队（通常是市场营销团队）。而且，正如你可能会发现的那样，市场营销团队在运营社交媒体账户时，往往没有像多因素身份验证和密码管理等信息安全控制措施。

#### 场景

在这个场景中，攻击者向组织的社交媒体账户发布内容。虽然操作简单，但这一事件可以迅速引发关于各种紧迫问题的讨论，并且事件可能会扩展到公众领域。由于组织已经失去了对账户的控制，无法登录，员工必须迅速确定如何（a）重新获得账户的控制权，以及（b）如何与公众沟通，解答他们对帖子内容的关注。

从周六凌晨 3 点开始，Happy Bear 儿童护理中心，一家在加拿大拥有超过 150 个地点和近 4000 名全职及兼职员工的区域性儿童看护机构，发现其社交媒体动态被黎凡特解放军的宣传内容填充。

宣传内容包括对各方的贬损信息，并有若干其他冒犯性言论。这些信息与 Happy Bear 儿童护理中心以往在社交媒体上推广业务的内容形成鲜明对比。

+   在周末凌晨 3 点，Happy Bear 是否有员工在监控社交媒体平台？

+   Happy Bear 是否聘请了一个社交媒体品牌声誉公司，可能已经看到来自黎凡特解放军的信息？如果是的话，告知员工的流程是什么？

+   员工大概多久才能发现这些信息？

##### 注入 1

在警觉的员工通知下，Happy Bear 的营销团队尝试登录账户、删除内容并更改密码。在此过程中，员工发现密码已经被更改，无法登录。

+   该事件是否符合 Happy Bear 的事件响应计划（如果有的话）所定义的网络安全事件？

+   应该联系组织内的谁以获得帮助？还需要通知谁？

+   是否有从社交媒体账户恢复密码的流程？

##### 注入 2

Happy Bear 的营销团队尝试通过提供商的账户恢复选项重新获得社交媒体账户的控制权。社交媒体提供商告知员工，账户恢复需要 24 至 48 小时。

> 注意事项

*在现实情况下，恢复账户不太可能需要这么长时间。然而，加入时间延迟会增加事件的压力。*

+   知道贬损性信息将在接下来的 1 至 2 天内仍广泛可见，Happy Bear 应如何应对？

+   如果遇到类似此类问题（如登录凭据无法使用）或其他支持相关问题，获取社交媒体平台支持的流程是什么？该流程是否有文档记录？

+   是否存在其他渠道，无论是基于社交媒体还是其他方式，使 Happy Bear 员工能够与家长及其他关心的方进行沟通？

+   是否有任何创建和批准与客户、员工及公众沟通的流程，无论是文档化的还是其他方式的？

+   Happy Bear 是否聘请了危机管理公司，以便能迅速协助处理沟通事务？

##### 注入 3

威胁者继续发布更多贬损信息。此外，他们发布了一则帖子，要求组织支付 50,000 美元比特币，以换取释放账户；否则，他们威胁将公布他们声称窃取的学生信息。部分信息包含有特殊需求学生的敏感医疗信息。

+   Happy Bear 会考虑支付赎金吗？

+   Happy Bear 是否拥有能够覆盖声誉损害和赎金支付费用的网络保险？

+   Happy Bear 员工应如何与攻击者互动？

+   Happy Bear 员工应如何与关心的家长互动？

+   如果学生信息确实被窃取，应通知哪些监管机构，并且通知的时间应为何时？

+   是否应该联系执法部门？如果是，他们可能提供哪些帮助？

##### 注入 4

快乐熊的首席执行官，越来越担心公共舆论的反响和敏感数据的泄露，已经要求事件响应团队调查是否发生了数据泄露。

+   快乐熊是否与某个事件响应公司已有合作关系？

+   谁将领导和指挥此次调查？调查的目标是什么？

##### 注入 5

这些帖子在互联网上引起了广泛关注，媒体已联系快乐熊寻求评论。一家全国新闻频道计划播出一段关于网络安全的节目，并将重点讨论此次事件对无辜儿童和担忧父母的影响。

+   是否有人事先被指定为与媒体沟通？选择此类代表的过程是怎样的？

+   是否有一份网络保险政策，能够帮助快乐熊恢复其品牌形象？

+   是否有一个公关公司可以为快乐熊提供外部媒体沟通的帮助？

##### 注入 6

快乐熊重新获得社交媒体账户的访问权限，并立即删除了相关内容。这些不当的帖子共保留了 36 小时。

+   一旦账户重新控制，快乐熊将如何应对？

+   在建立长期解决方案之前，快乐熊将采取哪些立即措施来确保社交媒体账户的安全？

+   快乐熊将如何应对攻击者所声称的敏感信息已被泄露的说法？

##### 注入 7

事件响应团队提供了初步调查结果，其中包括对导致泄露的过程漏洞的检查。团队确认社交媒体账户没有使用多因素认证，而且多个员工共享一个简单的密码。这些做法与快乐熊的信息安全政策不符。

此外，攻击者是在一名市场营销员工点击了钓鱼邮件后获得了凭证。该员工曾多次未通过钓鱼测试，且一直未遵循安全计算实践。事件响应团队还确认没有证据表明数据被外泄。

+   人力资源团队在调查中的角色是什么？

+   即使事件响应团队没有发现数据外泄的证据，是否需要通知监管机构？

+   快乐熊将如何通知家长以安抚他们，确保没有信息丢失？公司能做些什么来重新建立信任？

+   假设公司发布最终报告，谁负责执行纠正措施？ #### 可能的修改

为了调整情境，可以考虑进行以下修改：

+   据称被外泄的数据集属于进行此次演练的组织，如果丢失，可能会引发公众的重大担忧。

+   攻击者展示了一份被盗信息样本，这使得组织相信数据确实被盗。

+   应急响应团队发现了敏感数据确实被窃取的证据，因此需要做出更大的响应。

+   父母或其他受影响的个人威胁提起诉讼，迫使组织采取法律保护措施。

+   被窃取的敏感数据属于跨国客户群，复杂了合规性通知的问题。

+   该组织是上市公司，数据丢失对其财务状况有重大影响，需要公司通知其他相关方。

### 内部威胁

大多数组织在安全投资上专注于防范外部威胁行为者，但内部威胁同样是一个不可忽视的重要风险，应当在桌面演练中加以探讨。

内部威胁有多种形式：疏忽大意的员工未能认真对待安全问题、决心对雇主造成伤害的员工，或者想通过出售知识产权获利的员工，等等。

如果你聘请了外部顾问来处理内部威胁情境，那么特别重要的一点是利用组织中的可信代理来帮助你制定一个现实的情景。大多数内部威胁发生在员工滥用之前获得的特权时，而可信代理比组织协调员更可能理解这些潜在的控制失效点。

在情境演练中，务必考虑技术性和非技术性威胁。互联网充斥着关于敏感数据丢失的故事，原因往往只是某人盗取了打印件或用手机拍照了数据。

最后，尽管情境可能涉及技术控制，但也可能涉及各种政策和程序，需要法律或其他团队的参与。

#### 情境

Mica 的 Fleet Repair 提供大型商业车队的维修服务，服务非常定制化。其最有价值的资产之一是广泛的客户联系人名单，其中包括为每个客户提供的个性化定价。许多企业都会遇到这样的情境：内部人员窃取了关键的知识产权，意图开设竞争性公司。

在情境开始时，David，Mica Fleet Repair 的资深客户经理，刚刚与 Mica 的原始客户之一——Central Delivery Services 开完会。Central 最近决定结束与 Mica 的合作关系。被问及原因时，Central 表示他们对 Mica 的服务很满意，但收到了来自由 Mica 前员工 Ajay 成立的新公司 NYFleet 的报价，比 Mica 便宜了 10%。

令 David 非常沮丧的是，这是 Mica 最近因竞标价格低于对方近 10%的报价而失去的第五个客户。David 怀疑 Ajay 离开时可能带走了某些信息。

+   是否有报告知识产权被盗的流程？应向谁报告？

+   这是否属于 Mica 应急响应计划定义的网络安全事件？

+   谁必须被告知？

##### 注入 1

账户丢失问题足够严重，已经引起 Mica 高层管理的关注，他们怀疑 Ajay 可能带走了 Mica 的知识产权，比如价格清单和合同。Mica 的法律顾问开始审查 Ajay 离职的相关事实，以及 Mica 的离职流程。

+   是否有一个离职流程，Mica 会在员工最后一天前对其进行简报？

+   在员工入职时以及之后的定期检查中，是否告知员工有关敏感信息的政策？

+   是否对敏感信息进行了标记，并采取了额外的安全控制措施加以保护？

+   是否对曾经接触过敏感信息的员工设立了独特的离职流程？

##### 注入 2

Mica 的法律顾问要求提供所有敏感账户信息的位置，包括合同、关键联系人和其他数据。

+   组织是否定义了一个数据分类方案，明确区分了敏感商业信息和无需保护的信息？

+   是否有一个敏感账户信息的清单及其存储位置？

+   是否有访问控制措施限制对这些数据的访问，并记录哪些用户访问过？

##### 注入 3

Mica 的信息技术团队报告称，大部分敏感账户信息都存储在一个系统中，Ajay 和其他 30 名账户经理有权限访问这些信息。

+   是否有日志记录每位账户经理的登录情况及其执行的活动？这些日志保存多长时间？

+   现有的控制措施是否防止用户下载敏感商业信息或将其传输到网络外部（例如通过电子邮件）？

##### 注入 4

Mica 的法律顾问要求信息技术团队提供 Ajay 在职期间使用的所有信息系统的清单。他们希望保留 Ajay 的任何信息，以备调查目的和潜在诉讼使用。

+   接收被终止员工的电脑、手机或其他设备的流程是怎样的？

+   设备在重新发放或销毁前会存放多长时间？

+   在设备重新分配给新员工之前，是否会清除数据？

##### 注入 5

Ajay 的前同事 Martin 在听说 Ajay 正在接受调查的传闻后，主动找到了他的经理。Martin 告诉经理，Ajay 曾经吹嘘过他如何轻松地将客户信息通过电子邮件发送给自己，并且可以开始自己的竞争性业务。自 Ajay 离职已经过去四个月。

+   Mica 在员工离职后会保留电子邮件账户多长时间？是否有保留或销毁政策？

+   四个月后，哪些剩余的调查资料可以帮助验证 Ajay 是否将文件通过电子邮件发送给自己？

##### 注入 6

随着调查的展开，越来越明显的是，多个政策和技术上的漏洞曾使 Ajay 能够窃取知识产权。高层管理人员希望做出改变，确保这种情况不会再次发生。

+   鉴于故障发生在多个团队之间，是否应该由某个角色负责主导解决？如果是，应该是谁？也许是审计或风险管理？

+   Mica 将如何验证已识别的差距是否已被修正？具体而言，谁能判断实施的解决方案是否足够？

#### 可能的修改

为了调整场景，考虑进行以下修改：

+   用于窃取敏感信息的手段包括打印文件、使用手机相机或将文件下载到 USB 驱动器中。

+   敏感信息与进行演练的组织相关。例如，可能包括化学公式、原型图纸或研究数据。

+   不再是丢失客户信息，内部人员窃取了受监管的数据（如健康信息）或需要通知其他企业的信息。

+   内部人员是现任员工，且他们的角色使得他们对信息技术流程有深入了解。这意味着他们能够通过删除日志来掩盖痕迹。（此外，如果此类员工的离职会造成重大困难，可以在演练中讨论是否可以通过使一些员工任务冗余的方式，确保权力和知识不完全掌握在一个人手中。）
