# 第七章：时间的掌控

你应该毫不拖延地开始行动，而不是过早开始，而是恰到好处的时机。

> 如果你打算攻打敌人的城堡或营地，你需要与盟友事先安排好点火的时间。
> 
> —百首义盛 #83

当忍者执行任务时，特别是在夜间，其中一个最关键且复杂的任务就是掌握时间。如果这个任务看起来很简单，请记住，忍者当时没有手表或钟表。直到 17 世纪初，他们甚至没有沙漏。^(1)为了在适当的时间发送和接收信号、协调攻击、了解敌人何时最脆弱等等，忍者们必须发展出可靠的时间感知方法。

历史上，一种标记时间的方法是点燃已知以恒定速度燃烧的香或蜡烛，然后在特定时间间隔敲响钟声以报时。*万川集海*建议使用环境线索，如星星的运动，或基于重量的仪器来标记时间。^(2)这些基于重量的仪器很可能是水钟，有时被称为*水漏*，利用平衡和水流/重量机制准确地标记时间间隔。其他卷轴中还包括一些更为复杂的选项，比如追踪猫眼睛虹膜的膨胀变化，或观察夜间房屋的微妙热胀冷缩，因为这些变化与特定的时间点相符合。^(3) 忍者们甚至被教导通过观察哪只鼻孔更活跃来推算时间。这些卷轴解释了呼吸是如何先从一个鼻孔明显进出，然后在规则的时间间隔后转到另一个鼻孔的。虽然这个想法可能看起来像伪科学，但在 1895 年，德国科学家理查德·凯瑟观察并记录到，在白天，血液会在人的鼻子两侧积聚，导致一个鼻孔的气流显著减少，然后再转到另一个鼻孔。^(4)不仅忍者们敏锐的观察能力在其西方科学出版三百多年之前就发现了这一现象，他们还为这一发现开发了实际应用。例如，他们可能需要躺在目标楼下的狭小空间中，在那里他们无法点燃蜡烛或香，也无法使用仪器来追踪时间，甚至不敢睁开眼睛，免得眼中的光芒通过地板的缝隙引起目标的注意。在这种不舒适的情况下，他们会保持静止，注意自己的鼻息，直到合适的时机到来——这正是忍者纪律、聪明才智和创造力的杰出例证。

忍者卷轴中对时间的众多提及，以及为追踪时间而开发的艰难方法，表明如果追踪时间对威胁行为者的有效运作不至关重要，这些技术就不可能被开发出来。现代社会中普遍存在廉价、简便且可靠的计时方法，这几乎肯定已经使我们习惯性地将时间及其测量视为理所当然。

在本章中，我们将重新审视时间在数字系统中的价值和重要性，同时简要回顾其生成、使用和现有最佳实践的安全措施。然后我们将提出以下问题：如果准确的时间对对手如此重要，那么如果我们能够将时间对他们保密，会发生什么呢？或者拒绝对手访问时间？甚至通过不准确的时间来欺骗他们，会怎样呢？

## 时间的重要性

时间对于几乎所有现代计算机系统的运行都是必要的。通过同步顺序逻辑并生成控制功能间隔的时钟信号，计算机建立了有限的时间脉冲。这些脉冲就像钟表的滴答声，系统在稳定、可靠的输入/输出环境中对数据进行操作。支撑我们政府、经济、企业和个人生活的庞大而复杂的网络和系统，依靠这些脉冲不断请求时间。如果没有时钟，它们将无法正常工作。

保护时间数据的安全控制措施有很多。网络时间协议（NTP）服务器上的身份验证可以验证攻击者是否伪装成系统的可信时间来源。加密和校验和——加密对通信进行编码，校验和用于检测传输过程中的错误——在 NTP 服务器的时间数据上验证其完整性并防止篡改。Nonce 是添加到时间通信中的一个任意随机数字，用于防止重复传输错误。时间戳和时间同步日志将系统的时间与权威时间源报告的时间进行比较。NTP 通过利用多个时间源和备用传播方法保持可用性和容错性，如果无法访问 NTP 或被拒绝访问，备用方法可以基于最后一次同步准确估算时间。其他安全最佳实践要求对审计记录进行时间戳标记，根据不活动锁定会话，限制基于时间的账户访问，基于时间和日期信息评估安全证书和密钥的有效性，确定何时创建备份，并衡量保留缓存记录的时长。

这些控制措施保护时间数据的完整性和可用性，但往往忽视了对时间数据机密性的保护。几乎任何现代应用都可以随时请求时间，且通常不仅可以访问日期和时间，还可以访问时钟库和相关功能。虽然 NTP 可以加密它传输的时间数据，但在限制对当前系统时间访问的控制措施方面明显存在缺失。识别这一控制空白很重要，因为时间是攻击者用来传播恶意软件的关键信息。例如，破坏性的 Shamoon 恶意软件，^(5) 就是在沙特阿拉伯周末开始时执行的，以造成最大破坏；它被设计成在任何人注意到之前，清除所有受感染的系统。

其他常见攻击包括泄露机密信息、造成竞争条件、强制死锁、操纵信息状态，以及执行计时攻击以发现加密秘密。更复杂的恶意软件可以利用其对时间的访问来：

+   设定特定的睡眠时间以避免被检测

+   计算π到 1000 万位，计时计算所需的时间，以确定受感染的系统是否处于沙盒/引爆环境中，旨在捕捉恶意软件

+   尝试根据特定的时间指令联系其指挥控制（C2）系统

+   通过计时攻击发现元数据和其他信息，揭示目标系统的状态、位置和能力

如果管理员能够拒绝对时间（本地时间、实际时间和线性时间）的访问，进行目标信息系统的操作将变得更加困难——并且可能对攻击者来说是不可行的。然而，重要的是要注意，随意限制时间查询可能会导致连锁故障和错误。因此，需要一种精确的方法来拒绝对时间的访问。

## 保持时间机密

记住，由于机密性不像其他形式的时间安全那样根深蒂固，实施这些安全控制将需要组织和更广泛的安全社区的特别努力。

### 确定基准

确定环境中需要访问时间的软件、应用程序、系统和管理命令。实施功能挂钩（拦截函数调用）和日志记录，以确定谁和什么在请求时间。在建立此基准后，利用它检测异常的时间查询，并开展基于时间的需求评估，以量身定制额外的安全控制（例如，及时[Just in Time] [JIT]）。

### 评估技术能力

联系硬件制造商和软件供应商，以确定可以启用哪些技术控制来限制对时间功能的访问。如果没有这样的控制措施，建议实施新功能，鼓励行业围绕时间机密性开发解决方案。

### 建立政策

否认对时间的访问是一种非传统的安全控制措施，但与更多常规控制措施一样，执行此措施需要建立战略性政策，详细说明要求——在此情况下，即限制对时间的访问并监控访问时间的尝试。尽可能将时间保密的概念融入所有变更管理决策、新硬件和软件的采购以及 SOC 优先级的安排中。正式记录新政策，并确保您组织的 CISO 批准这些政策。

## 推荐的安全控制措施和缓解措施

在相关的情况下，提供与 NIST 800-53 标准中适用的安全控制措施相关的建议。每项建议都应以时间保密的概念为依据进行评估。

1.  实施保护措施，阻止访问时间数据，如时间戳日志或其他信息监控日志。防止时间泄露或时间戳泄漏可能需要物理、环境、媒体和技术控制。[AU-9: 审计信息保护]

1.  审查您当前的信息架构，重点考虑时间方面的哲学、需求和实施访问及保密控制所需的策略。如果利益相关者同意时间限制，请在安全计划中记录，并确保有批准的预算、资源和实施时间。[PL-8: 信息安全架构]

1.  执行日志审查和内部排查，发现通过端口 123 与您环境中的任何非官方 NTP 服务器进行的通信。查找与外部 NTP 服务器的 NTP 通信，并考虑阻止对您无法控制的 NTP 服务器的访问。[SC-7: 边界保护]

## 简报

在本章节中，您了解了一些忍者用来计时的工具，以及他们如何利用对时间的理解来行动。我们讨论了时间对网络操作和安全性的重要性，指出当前的安全实践主要集中在确保系统中的时间可用性和完整性。您还参与了一个思维练习，探讨了如何通过时间操控来减轻忍者攻击。

在接下来的章节中，我们将讨论忍者如何将许多事物转化为工具来完成任务。理解这些工具的数字化“对应物”可能帮助您检测并防范这些工具的新型武器化，或者至少减少它们的使用。
