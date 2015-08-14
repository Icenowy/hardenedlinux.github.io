---
layout: post
title:  "Brad Spengler( Pax Team/grsecurity)访谈, 2010年1月1日"
date:   2015-05-17 16:49:45
summary: Shawn：PaX/Grsecurity是在OS安全上的一个开创性的贡献，没有PaX/Grsecurity的GNU/Linux的安全性只能防御脚本小子，过去的14年里Pax/Grsecurity为Linux内核做出了巨大出贡献的贡献，但到今天Linux内核社区都不愿意承认，这可能的确是受商业厂商控制了主流媒体的后果，在后棱镜时代，这种现象有极端的阴谋论甚至认为NSA也是推手，当然这也并非完全没有道理，毕竟SELinux项目早已成为Five-Eyes国家的标配。

categories: system-security
---


## 原文：[Brad Spengler (PaX Team/grsecurity) interview， Jan 1 2010](https://slo-tech.com/clanki/10001en)
  
  
## 译者：Shawn the R0ck, May 16 2015

Shawn：PaX/Grsecurity是在OS安全上的一个开创性的贡献，没有
PaX/Grsecurity的GNU/Linux的安全性只能防御脚本小子，过去的14年里
Pax/Grsecurity为Linux内核做出了巨大出贡献的贡献，但到今天Linux内核社区
都不愿意承认，这可能的确是受商业厂商控制了主流媒体的后果，[在后棱镜时代](https://raw.githubusercontent.com/citypw/DNFWAH/master/3/d3_0x06_hacker_nsa_free-software.txt)，
这种现象有极端的阴谋论甚至认为NSA也是推手，当然这也并非完全没有道理，毕
竟[SELinux项目](http://www.solidot.org/story?sid=43483)早已成为Five-Eyes国家的标配。

我尝试翻译这篇5年前的访谈是为了让更多的人了解到历史，因为反观今天的
Linux内核社区对于安全的态度相比5年前可能是更糟糕，[offset2lib](http://www.solidot.org/story?sid=42174)的远程利用
方式轻松绕过了GNU/Linux厂商们宣称的完美防御，相信就算是智商只有85的人也
能明白“抗爆破”机制只能抗不到1秒的时间是在扯淡;-) 即使offset2lib所带来的
风险巨大，Linux内核社区的态度也是极度傲慢，他们也不认为这个
PaX/Grsecurity在2001年就已经加固的攻击平面而他们在2015年还存在有什么问
题，而BadiRET漏洞里我们更能清晰的看到SMEP虽然被绕过，但SMAP依然有效，而这两个Intel CPU的特性也是源于2007年PaX/Grsecurity的其中一个特性UDEREF的启发，自从有了OS的攻防历史，就有了PaX/Grsecurity，如果Linux内核社区继续傲慢自大，最终的受害者是企业用户和个人用户。

在Anarchist看来，这样的Linux内核社区正是数字军火商，斯拉夫兵工厂甚至
NSA所喜欢的。


## 标题：Brad Spengler( PaX Team/grsecurity)访谈

### Slo-Tech：向我们的读者介绍一下你自己（工作，教育背景以及兴趣），也请你解释一下你的真名是Spender还是Spengler;-) 请问Brad是否是任何黑帽组织的成员？

Brad Spengler: Brad Spengler(不是Brad Spender)，虽然相似的名字并非偶然，
我改了改姓氏作为别名。我毕业于Bucknell大学，获得了计算机与工程（混杂了
计算机科学和电子硬件的课程）学士学位和一个应用数学的学士学位。数学/物理
学/经济学/哲学都是我最有兴趣的课程。我在学习操作系统课程之前就已经有4年
的学习Linux内核和编程的经历，所以计算机科学课程并不是那么的有趣。我从来
没有参加过任何黑帽组织。自从高中开始我总是对创造有趣的事物有兴趣。

......................(未翻译）


### Slo-Tech：你能用简单描述一下什么是PaX和GRSecurity以及有多少人参与这些项目吗？

Brad Spengler：[PaX](http://en.wikipedia.org/wiki/PaX)是一头戏剧性的改变了整个安全的形态的野兽，而且对未来
安全的影响甚至会更多。PaX专注于一次性的解决一堆各种类型的漏洞利用，有一
些工作还没有完成，但希望能有所改变，也希望8年后（Shawn：现在已经是5年后
了，愚蠢的大众还是宁愿相信商业厂商和NSA;-)）所有人都能明白PaX的前瞻性。
PaX完全专注于内存的漏洞利用，[grsecurity](http://www.grsecurity.net/)则增加了主机层的防御和基于现有的
PaX特性进行了一系列的改进，包括抗爆破，ASLR的抗信息泄漏，不允许文件系统
级别的任意代码执行等。Grsecurity包括了很多简单的自动化特性，比如RBAC系
统可以通过学习模式（你可以选择基于进程/用户或者整个系统）来自动化创建规
则，这些规则都是人类可读的纯文本格式（Shawn：SELinux是使用难以审计的二
进制的格式。），报错信息有助于根据攻击类型来制定相应的规则。

PaX项目的参与人数是未知的！因此PaX Team至少有一个人:) 对于grsecurity这
边就我一个人。偶尔我也收到一些patch提交（比如来自Zbyniu Krzystolik），
赞助者和朋友有时也会告诉我他们想要加入一些新功能。


### Slo-Tech：只有一些人真正了解PaX Team开发了一些安全机制（比如ASLR）后来被用于Linux内核里，至少目前来看主要的Linux内核社区开发者和参与者并不打算承认PaX所带来的贡献，你认为这些机制对于Linux安全贡献最大的是什么。

Brad Spengler：好吧，对我而言很搞笑的是聪明的[Ingo Molnar](http://en.wikipedia.org/wiki/Ingo_Molnar)多年前对于
paxtest测试（包括检查不同区域的地址空间是否有能力执行任意代码）非常不爽，
因为第2组测试中mprotect用于标记一些内存为可写和可执行。Ingo称这个测试是
"破坏" -- mprotect检测多少有些不公平（因为exec-shield完全失效了）。往前
看几年你会发现SELinux基本上把PaX的[MPROTECT](http://pax.grsecurity.net/docs/mprotect.txt)加入了它的规则语言。在
Windows的世界里你能找到所有人都在尝试日等价于Linux上的mprotect，glibc曾
经有一个make_stack_executable()函数也是ret2libc攻击的对象，Windows上也
有类似的函数。PaX team早在很多年前就认识到攻击者会找最薄弱的环节下手，
而这正是今天正在发生的事情。

我不能说哪一个特性是对Linux安全贡献最大，因为这些特性都是叠加式的让
Linux内核更安全。同样，我认为下一个最具革命性的贡献将同样来自PaX team。

![PaX/Grsecurity](/images/pax_grsec_graph.jpg)


### Slo-Tech：看起来Brad和Linux内核开发者的“口水战”还在继续。什么是主要原因导致了这种不愉快的情况？你不认为其实GNU/Linux的终端用户才是遭受损失的吗？

Brad Spengler：我从来都没有发过一封邮件到LKML（Linux内核邮件列表），所
以我并没有参与任何”口水战“。PaX Team曾经发过邮件到LKML（比如让Linux内核
开发者承认他们的不愿意让外界关注的不披露漏洞的官方政策和安全漏洞信息模
糊化以及Linus为此多次赢得pwnie奖项的"a bug is bug"的安全哲学）。8个公开
的空指针引用的漏洞利用才被作为提权威胁来处理，在第一个公开漏洞利用后几
个月，mmap_min_addr被引入，但并不懂安全的Linux开发者开发的这个安全机制
导致了至少6个不同的绕过。Linux内核的ASLR有大量的弱点。SSP被攻破了多次最
终导致他们强行限制其工作范围。所有这些破事都来自于一个商业源头: Red
Hat -- 对于公司重要的是为了赚钱你要说你有X特性（比如反病毒厂商会宣称：
“我们将会保护你不受病毒的侵害。”，至于这个特性是否有用并不是公司关心的
（但有些人会去验证厂商的宣传 --- 安全研究人员或者黑帽）。


### Slo-Tech：谁是你尊重的Linux内核开发者？或者说，你不觉得在安全问题上Linux需要重新组织一下关于处理安全事件和安全开发的流程（很多回归测试代码）。比如微软的SDL...你觉得SDL怎么样？

Brad Spengler：基于有很多公司和个人用户使用微软的产品，我很尊重微软对安
全的态度。Windows大量的二进制软件的生态系统的基础上，去实现安全功能的同
时还要保证应用程序的兼容性。这些工程的真实难度很容易被误认为是简单的事
情。

Linux确实需要一些集中的领导者或者组织来处理安全。Linux开发者就算知道他
们在修复安全漏洞，但他们也不会通知任何人（包括厂商）。选择性的通知厂商
特定的安全问题，而不通知小的厂商和GNU/Linux发行版社区。Upstream基本上让
厂商难受，每个厂商都必须去做重复的劳动，因为没有标准化流程。这个Linux内
核社区官方的"a bug is just a bug"政策是在伤害所有的GNU/Linux用户。一些
很优秀的加固补丁很少被内核社区接受，因为他们过度看中安全机制造成的性能
影响。


### Slo-Tech：你觉得Linux Torvalds能胜任Linux的安全工作吗？我的意思是，他是一个优秀的开发者，但不是一个安全研究人员。那其他的著名Linux内核开发者呢？他们有相关的技能吗？

Brad Spengler：我不认为他能，他没有安全思维，也无法理解安全。我不确定为
什么很多人都感觉在安全问题上Linus是否参与很重要。一些开发者"理解"安全，
但通常他们只修复bug。Upstream通常不关心系统加固方面的内容。


### Slo-Tech：Dave Aitel写了一封名为“需要中心平台让多厂商合作来改善Linux内核安全问题“的邮件到他的邮件列表。你同意他的观点吗？这是正确的一步吗？你愿意为这样的中心平台工作吗？

Brad Spengler：这点上[Dave](http://en.wikipedia.org/wiki/Dave_Aitel)是对的，但我并没看到这种事情在发生。最重要的是
Linus对安全的态度必须改变才行。只要一天他还是upstream内核的看门人，不论
他的观点对还是错都会直接影响Linux的安全。同时，PaX team和我只能继续做我
们所一直在做的事情，改善Linux的安全只有一条路：单干。

![1](/images/1.jpg)


### Slo-Tech：内核维护者悄然无声的修复一些内核bug是真的吗？"悄然无声的修复“是否意味着不正确的BUG分类和低估安全风险或者其他什么的？

Brad Spengler：是的，他们已经承认这么干过。如果你回去读读LWN上我的文章
有一堆这样的例子。厂商在漏洞分类的问题上也非常糟糕 -- 所有都是DoS。我认
为这个事情现在有所改善是因为他们被曝光和受到了公众的批评。部分的问题原
因是没有统一的bug管理造成了对于同一个bug有不同的解释。通常不同的厂商的
bug分析也不一样，而现在有一些厂商发的安全公告并不是安全漏洞（比如NOMMU
是用于嵌入式系统，由于用户空间和内核空间没有隔离所以根本没有安全的设计，
但至少有2个CVE是有关这种系统的BUG）。这些事情可能会促使商业公司更愿意招
聘软件开发人员而不是安全人员来完成安全有关的工作。在每天都会报无数漏洞
的年代，集中处理平台和管理流程是能减轻很多工作量的。


### Slo-Tech：这是个恶心的问题，所以你不愿意的话你可以不回答。你愿意为微软（像Crispin Cowan）或者Red Hat工作吗？

Brad Spengler：在我大学的最后一年微软曾经邀请我去面试，但我拒绝了，因为
HR在弄丢了我的简历1年后他们才想起我，而我那时已经失去去那里工作的兴趣。
为Red Hat工作？我确定你知道答案的;)


### Slo-Tech：众所周知你使用Windows Vista作为你的主要操作系统。这对于一个Linux内核安全研究者很奇怪。你为什么会这样选择呢？你尝试去找过Windows的bug吗？

Brad Spengler：事实上我使用的是Windows 7 -- Cheddar Bay的视频里应该是
RC版。因为Linux对我而言只是用来测试和改进grsecurity的。在高中和大学的时
候，我曾经使用GNU/Linux作为我的主要桌面系统，但现在GNU/Linux都是在虚拟
机里。以前的Linux的内核和用户态都简单很多。你知道那些众所周知的配置文件，
如果你修改他们，一些"智能"的进程会背着你把配置改回去，你不会因为想要不
同的默认配置而一定要修改SELinux规则。那是更多的是感受到GNU/Linux的自由
（Shawn：个人认为Brad说的问题应该是针对RedHat/CentOS/Fedora的，至少目前
来看Debian和Gentoo是享有高度的自由），而自由的缺失我认为是因为商业化造
成的。而游戏是我用Windows的主要原因。如果Pidgin通知我有一个新版本更新，
我只是下载一个去执行，而不需要强制的更新另外100+个包，那样会增加系统的
风险的。


### Slo-Tech：为什么你会公布漏洞利用而不是把它们卖给像iDefense，ZDI，Immunity这样的公司... 类似像本地root提权漏洞像cheddarbay, ingom0wnar, wundebar的市场价值是什么？

Brad Spengler：我不确定他们是否关心Linux的本地提权漏洞 -- 首先，这些漏
洞已经在某些版本的Linux内核开发分支上被修复了。其次这些漏洞利用太容易编
写了。所以这些漏洞利用是用于提醒大家安全的重要性的（以前的一堆讨论无法
改善Linux内核社区的看法，但那8个漏洞利用做到了）。第1个成果是帮助到了人
们去理解风险的等级（有一些人联系我说那些漏洞利用帮助他们说服了他们的老
板更关注安全），因为Linux内核公开的漏洞利用并不是那么多，不是因为漏洞不
存在，而是因为黑帽们都用于自己的目的了。第2个成果是让所有主要的的
GNU/Linux厂商和发行版都把空指针引用的攻击平面给默认防御住了，SELinux的
漏洞也修复了，厂商更注重关于mmap\_min\_addr的问题。用户也注意到了这个特性
和开启它的重要性（Shawn: mmap\_min\_addr成为今天的标准安全基线），很多人
也都升级了Linux内核。这些都是好事。我想整件事情唯一的"创新"应该是
enlightenment框架了（下一个问题跟这个有关）。


### Slo-Tech：最近你发布的针对Linux内核漏洞利用的框架叫Englightenment。你是否有计划继续改进这个框架并且希望它成为像Metasploit一样？

Brad Spengler：我一直在改进这个框架因为她让我以攻击者的方式来思考，这会
帮助我有多种思路去考虑针对特定攻击的防御机制（我最近在grsecurity里实现
的加固就是来源于此）。我也想让她变得尽量通用：她已经支持x86和x8\6_64平台
的所有2.4和2.6内核上关闭所有LSM模块。我最近也增加了Xen特性的支持，这个
特性会更恰当的让hyppercall去修改内核代码。我也在考虑关于
namespace/container(Shawn：就是lxc，以及后来docker用的底层模块），这些
都在TODO list上。[Enlightenment](http://grsecurity.net/~spender/enlightenment.tgz)会仅仅针对Linux内核漏洞利用。

![2](/images/2.jpg)


### Slo-Tech：大多数人都不把本地漏洞利用提权当成真正的威胁。我知道SuSE的Sebastian Krahmer写过相关的观点而我也同意他的观点，但事实上现在已经没有任何公开的远程漏洞利用了（Sgrakkyu是最后一名勇士），远程漏洞利用标准Linux内核真的已经是不可能还是在不远的将来会有所改变？

Brad Spengler：远程内核漏洞利用非常困难，特别是针对运行PaX的内核和定制
过的内核。只要读读sgrakkyu/twiz在Phrack上的论文Attacking the core:
Kernel exploitation notes（Shawn：发表于Phrack Issue 64，2007年）就知道
所涉及的复杂性。他们都是热衷于挑战高难度的人，而其他大部分人会选择更简
单的方式，比如从Web进入然后使用本地内核提权漏洞的方式。如果系统运行了最
新的PaX，漏洞利用会变得极度困难，而不是更简单。我仍然能看到现有的威胁会
在可预见的未来存在下去，因为GNU/Linux发行版都把时间浪费在了不太可能出现
严重bug的SUID程序上，而新的内核提权漏洞几乎每个礼拜都在曝光。还有就是
web开发人员（ 那些编写的第三方代码运行在公共的服务器上，让远程用户能进
入"非信任的本地用户"）并没有变得更聪明。


### Slo-Tech：GNU/Linux能依然被认为是安全的操作系统吗？你觉得政府或者其他对安全性要求高的基础架构应该使用GNU/Linux吗？

Brad Spengler：我希望在高安全要求的环境中有其他的系统可以使用(Shawn: 经
过加固的GNU/Linux或者Quebes OS/MirageOS?)。作为建议，一个安全的操作系统
可能会犯下非常不安全愚蠢的错误，而一个不安全的操作系统可以变得安全如果
不跑任何业务的话。


### Slo-Tech：你有任何私人的0-day漏洞利用在你的硬盘上吗;)

Brade Spenger：有的，[ext4\_own.tgz](http://grsecurity.net/~spender/ext4_own.tgz)，它小于1000bytes。

感谢Brad Spengler的访谈。
