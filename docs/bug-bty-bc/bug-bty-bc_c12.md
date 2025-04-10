# 第十二章：竞争条件

![](img/chapterart.png)

竞争条件是现代 Web 应用中最有趣的漏洞之一。它们源于开发人员常犯的简单编程错误，这些错误已经证明是代价高昂的：攻击者利用竞争条件从在线银行、电子商务网站、股票经纪公司和加密货币交易所窃取资金。

让我们深入了解这些漏洞是如何发生的，为什么会发生，以及你如何找到它们并加以利用。

## 机制

*竞争条件*发生在两个原本设计为按顺序执行的代码块被打乱顺序执行时。要理解这一点，首先需要了解并发的概念。在计算机科学中，*并发*指的是在不影响程序结果的情况下同时执行程序的不同部分。并发可以显著提高程序的性能，因为程序的不同部分可以同时运行。

并发有两种类型：多处理和多线程。*多处理*指的是使用多个*中央处理单元（**CPU**）*，即计算机中执行指令的硬件，来进行并行计算。另一方面，*多线程*是指单个 CPU 提供多个*线程*或并发执行的能力。这些线程并不会真正同时执行，而是轮流使用 CPU 的计算能力。当一个线程处于空闲状态时，其他线程可以继续利用未被使用的计算资源。例如，当一个线程在等待用户输入时挂起，另一个线程可以接管 CPU 执行计算。

安排多个线程的执行顺序被称为*调度*。不同的系统根据其性能优先级使用不同的调度算法。例如，有些系统可能通过优先执行最高优先级的任务来调度任务，而另一些系统则可能通过轮流分配计算时间来执行任务，无论任务的优先级如何。

这种灵活的调度恰恰是竞争条件发生的原因。竞争条件发生在开发人员未遵循某些安全的并发原则时，我们将在本章后面讨论这些原则。由于调度算法可以随时在两个线程的执行之间切换，因此你无法预测线程执行每个操作的顺序。

为了理解执行顺序为何重要，我们来看一个例子（感谢维基百科：[`en.wikipedia.org/wiki/Race_condition`](https://en.wikipedia.org/wiki/Race_condition)）。假设两个并发执行的线程各自试图将一个全局变量的值增加 1。如果变量初始值为 0，那么它应该最终值为 2。理想情况下，线程应该按照表 12-1 中所示的阶段执行。

表 12-1：两个线程操作同一变量的正常执行

|  | **线程 1** | **线程 2** | **变量 A 的值** |
| --- | --- | --- | --- |
| **阶段 1** |  |  | 0 |
| **阶段 2** | 读取 A 的值 |  | 0 |
| **阶段 3** | 将 A 增加 1 |  | 0 |
| **阶段 4** | 写入 A 的值 |  | 1 |
| **阶段 5** |  | 读取 A 的值 | 1 |
| **阶段 6** |  | 将 A 增加 1 | 1 |
| **阶段 7** |  | 写入 A 的值 | 2 |

但如果两个线程同时运行，且没有考虑访问相同资源时可能发生的冲突，执行可能会如表 12-2 所示。

表 12-2：由于竞争条件导致的错误计算

|  | **线程 1** | **线程 2** | **变量 A 的值** |
| --- | --- | --- | --- |
| **阶段 1** |  |  | 0 |
| **阶段 2** | 读取 A 的值 |  | 0 |
| **阶段 3** |  | 读取 A 的值 | 0 |
| **阶段 4** | 将 A 增加 1 |  | 0 |
| **阶段 5** |  | 将 A 增加 1 | 0 |
| **阶段 6** | 写入 A 的值 |  | 1 |
| **阶段 7** |  | 写入 A 的值 | 1 |

在这种情况下，最终的全局变量值变为 1，这是不正确的。结果值应该是 2。

总结来说，竞争条件发生在一个线程的执行结果依赖于另一个线程的执行结果，并且当两个线程在没有考虑其他线程也在使用这些资源的情况下操作相同的资源时。当这两个线程同时执行时，可能会发生意外结果。某些编程语言，如 C/C++，因为管理内存的方式，更容易发生竞争条件。

## 当竞争条件成为漏洞时

竞争条件成为安全漏洞，当它影响到安全控制机制时。在这种情况下，攻击者可以引发一种情况，使得敏感操作在安全检查完成之前执行。因此，竞争条件漏洞也被称为*检查时*或*使用时*漏洞。

假设前面的两个线程正在执行一些更敏感的操作：在银行账户之间转账。该应用程序必须执行三个子任务才能正确地转账。首先，它必须检查发起账户是否有足够的余额。然后，它必须将钱存入目标账户。最后，它必须从发起账户中扣除相同的金额。

假设你拥有两个银行账户，账户 A 和账户 B。账户 A 中有 500 美元，账户 B 中有 0 美元。你同时发起了两笔从账户 A 到账户 B 的 500 美元转账。理想情况下，当同时发起两笔转账请求时，程序应如表 12-3 所示。

表 12-3：两个线程操作同一银行账户的正常执行

|  | **线程 1** | **线程 2** | **账户 A + B 的余额** |
| --- | --- | --- | --- |
| **阶段 1** | 检查 A 账户余额（$500） |  | $500 |
| **阶段 2** | 向 B 账户添加 $500 |  | $1,000（A 账户 $500，B 账户 $500） |
| **阶段 3** | 从 A 账户扣除 $500 |  | $500（A 账户 $0，B 账户 $500） |
| **阶段 4** |  | 检查 A 账户余额（$0） | $500（A 账户 $0，B 账户 $500） |
| **阶段 5** |  | 转账失败（余额不足） | $500（A 账户 $0，B 账户 $500） |

最终你会得到正确的资金数额：你在两个银行账户中共 $500。但如果你能同时发送这两个请求，你可能会诱发一个执行情况，像表 12-4 中所示。

表 12-4：由于竞争条件导致的错误转账结果

|  | **线程 1** | **线程 2** | **A 和 B 账户的余额** |
| --- | --- | --- | --- |
| **阶段 1** | 检查 A 账户余额（$500） |  | $500 |
| **阶段 2** |  | 检查 A 账户余额（$500） | $500 |
| **阶段 3** | 向 B 账户添加 $500 |  | $1,000（A 账户 $500，B 账户 $500） |
| **阶段 4** |  | 向 B 账户添加 $500 | $1,500（A 账户 $500，B 账户 $1,000） |
| **阶段 5** | 从 A 账户扣除 $500 |  | $1,000（A 账户 $0，B 账户 $1,000） |
| **阶段 6** |  | 从 A 账户扣除 $500 | $1,000（A 账户 $0，B 账户 $1,000） |

请注意，在这个场景中，你最终拥有的资金比你开始时多。你的账户中原本有 $500，但现在你总共拥有 $1,000。你通过利用竞争条件漏洞，让额外的 $500 似乎凭空出现！

尽管竞争条件通常与金融网站有关，攻击者也可以在其他情况下利用它们，比如操纵在线投票系统。假设一个在线投票系统执行三个子任务来处理一次在线投票。首先，它检查用户是否已经投过票。然后，它会将选票数增加到所选候选人的票数中。最后，它记录用户已投票，以防止他们再次投票。

假设你同时为候选人 A 投两次票。理想情况下，应用程序应当拒绝第二次投票，按照表 12-5 中的程序操作。

表 12-5：两个线程操作同一用户投票的正常执行

|  | **线程 1** | **线程 2** | **候选人 A 的投票数** |
| --- | --- | --- | --- |
| **阶段 1** |  |  | 100 |
| **阶段 2** | 检查用户是否已经投票（尚未投票） |  | 100 |
| **阶段 3** | 增加候选人 A 的投票数 |  | 101 |
| **阶段 4** | 标记用户为已投票 |  | 101 |
| **阶段 5** |  | 检查用户是否已经投票（已投票） | 101 |
| **阶段 6** |  | 拒绝用户的投票 | 101 |

但如果投票应用程序存在竞争条件漏洞，执行可能会变成表 12-6 中展示的场景，这会使得用户能够投出潜在无限的选票。

表 12-6：用户通过滥用竞争条件能够投两次票

|  | **线程 1** | **线程 2** | **候选人 A 的投票数** |
| --- | --- | --- | --- |
| **阶段 1** |  |  | 100 |
| **阶段 2** | 检查用户是否已经投票（他们尚未投票） |  | 100 |
| **阶段 3** |  | 检查用户是否已经投票（他们尚未投票） | 100 |
| **阶段 4** | 增加候选人 A 的票数 |  | 101 |
| **阶段 5** |  | 增加候选人 A 的票数 | 102 |
| **阶段 6** | 将用户标记为已投票 |  | 102 |
| **阶段 7** |  | 将用户标记为已投票 | 102 |

攻击者可以按照以下步骤同时发送两个、十个，甚至是数百个请求，然后查看哪些投票请求在用户被标记为已投票之前先被处理。

大多数竞态条件漏洞被用来操控金钱、礼品卡积分、投票、社交媒体点赞等。但竞态条件也可以用来绕过访问控制或触发其他漏洞。你可以在 HackerOne 的 Hacktivity feed 上阅读一些实际的竞态条件漏洞案例（[`hackerone.com/hacktivity?querystring=race%20condition/`](https://hackerone.com/hacktivity?querystring=race%20condition/)).

## 预防措施

防止竞态条件的关键是在执行过程中通过使用*同步*方法来保护资源，或者使用机制确保使用相同资源的线程不会同时执行。

资源锁是其中一种机制。它们通过*锁定*资源来阻止其他线程对同一资源进行操作。在银行转账的例子中，线程 1 可以在修改账户 A 和 B 的余额之前先锁定它们，这样线程 2 就必须等线程 1 完成操作后才能访问这些资源。

大多数具有并发能力的编程语言也都内建了一些同步功能。你必须意识到你应用中的并发问题，并相应地采取同步措施。除了同步，遵循安全编码实践，如最小特权原则，可以防止竞态条件发展成更严重的安全问题。

*最小特权原则*意味着应用程序和进程只应获得完成任务所需的特权。例如，当一个应用程序仅需要对文件进行读取访问时，它不应被授予任何写入或执行权限。你应当精确授予应用程序所需的权限。这可以降低在攻击过程中整个系统被攻陷的风险。

## 寻找竞态条件

寻找竞态条件很简单，但通常它也涉及一些运气因素。通过遵循这些步骤，你可以确保最大化成功的机会。

### 步骤 1：找到容易发生竞态条件的功能

攻击者利用竞态条件来破坏访问控制。从理论上讲，任何依赖访问控制机制来执行敏感操作的应用程序都可能存在漏洞。

大多数时候，竞态条件发生在处理数字的功能中，例如在线投票、在线游戏得分、银行转账、电子商务支付和礼品卡余额。请在应用程序中查找这些功能，并注意涉及更新这些数字的请求。

例如，假设你在代理中发现了一个用于从银行网站转账的请求。你应该复制这个请求用于测试。在 Burp Suite 中，你可以通过右键点击该请求并选择**复制为 curl 命令**来复制请求。

### 步骤 2：发送同时请求

然后，你可以通过同时向服务器发送多个请求来测试和利用目标中的竞态条件。

例如，如果你在银行账户中有 $3,000 并想查看是否能够转账超过你所拥有的金额，你可以通过 `curl` 命令同时发送多个转账请求到服务器。如果你已经从 Burp 中复制了命令，你可以将命令粘贴到终端中多次，并在每个命令之间插入 `&` 字符。在 Linux 终端中，`&` 字符用于同时在后台执行多个命令：

```
curl (transfer $3000) & curl (transfer $3000) & curl (transfer $3000)
& curl (transfer $3000) & curl (transfer $3000) & curl (transfer $3000)
```

一定要测试那些应该只允许一次，但不能多次执行的操作！例如，如果你的银行账户余额是 $3,000，测试转账 $5,000 是没有意义的，因为单个请求是无法允许的。但是，测试将 $10 转账多次也是没有意义的，因为即使没有竞态条件，你也应该能够完成这项操作。关键是通过执行那些不应该重复的操作来测试应用程序的限制。

### 步骤 3：检查结果

检查你的攻击是否成功。在我们的示例中，如果目标账户在同时请求后出现超过 $3,000 的余额增加，那么攻击就成功了，你可以确定转账余额端点存在竞态条件。

请注意，攻击是否成功取决于服务器的进程调度算法，这是运气问题。然而，在短时间内发送更多请求，攻击成功的可能性会更大。此外，许多竞态条件测试第一次不会成功，因此建议在放弃之前再尝试几次。

### 步骤 4：创建概念验证

一旦你发现了竞态条件，你需要在报告中提供该漏洞的证明。最好的方式是列出利用该漏洞所需的步骤。例如，你可以按如下方式列出利用步骤：

1.  创建一个余额为 $3,000 的账户和一个余额为零的账户。余额为 $3,000 的账户将作为我们转账的源账户，余额为零的账户将作为目标账户。

1.  执行此命令：

    ```
    curl (transfer $3000) & curl (transfer $3000) & curl (transfer $3000)
    & curl (transfer $3000) & curl (transfer $3000) & curl (transfer $3000)
    ```

    这将尝试同时多次将 $3,000 转账到另一个账户。

1.  你应该在目标账户中看到超过$3,000 的金额。如果目标账户中没有超过$3,000，反向转账并尝试几次攻击。

由于竞态条件攻击的成功取决于运气，确保在第一次测试失败时，提供再次尝试的说明。如果漏洞存在，经过几次尝试后，攻击最终应该会成功。

## 升级竞态条件

竞态条件的严重性取决于受影响的功能。在确定特定竞态条件的影响时，要注意攻击者在金钱奖励或社会影响方面可能获得的收益。

例如，如果在像现金提取、资金转账或信用卡支付这样的重要功能上发现竞态条件，这个漏洞可能导致攻击者获得无限的经济收益。在报告中证明竞态条件的影响，并阐明攻击者将能够实现的目标。

## 找到你的第一个竞态条件！

现在你准备好找到你的第一个竞态条件了。按照以下步骤，使用这一巧妙的技术来操作 Web 应用：

1.  找出目标应用程序中容易出现竞态条件的功能，并复制相应的请求。

1.  同时向服务器发送多个此类关键请求。你应该构造那些应该允许一次但不允许多次的请求。

1.  检查结果，看看你的攻击是否成功。如果攻击没有成功，尝试多次执行该攻击以最大化成功的机会。

1.  考虑你刚刚发现的竞态条件的影响。

1.  起草你的第一个竞态条件报告！
