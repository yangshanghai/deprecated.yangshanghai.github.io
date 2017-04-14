---
layout: post
title: (译)facebook是如何管理代码的
category: tech
tag: 技术
---

<a href="http://framethink.wordpress.com/2011/01/17/how-facebook-ships-code/">原文在此</a>，看完之后，终于明白为什么优秀的工程师都去了/想去facebook，因为那里是工程师们的天堂。

译文:

我对facebook的运转着迷。这是一个很独特的环境，不容易被复制（他们的体系并不适合所有的公司，即使他们努力尝试过）。下面是我和facebook的朋友们关于他们如何开发和管理项目的记录。

现在距离我收集的这些信息又过去6个月了，我相信facebook肯定又对他们的项目开发实践进行了改进。所以这些记录可能会有点过时。同时facebook的工程师驱动文化也越来越为大众所知。非常感谢那些帮助我整理这篇文章的facebook的朋友们。

记录：

* 截止到2010年6月，facebook有将近2000名员工，10个月前只有1100名，一年之间差不多翻了一番。
* 两个最大的部门是工程师和运维，每个部门大概都是400-500人。这两个部门人数大约占了公司的一半。
* 产品经理与工程师的比例大约为1-7到1-10。
* 每个工程师入职时，都要接收4-6周的培训，通过修补bugs和听高级开发工程师的课程来熟悉facebook。
* 培训结束后，每个工程师都可以接触线上的数据库(更大的权力意味着更大的责任，也有一份"勿做清单"，不然可能会被开，比如共享用户的隐私数据)。
* 有非常牢靠的安全体系，以免有人不小心/故意做了些不好的事。
* 每个工程师可以修改facebook的任何代码，随时可以迁入。
* 浓厚的工程师驱动文化。"产品经理基本可以被忽略"，这是facebook一名员工的话。工程师可以修改流程的细节，重新安排工作任务，随时植入自己的想法。
* 在每月的跨部门会议上，由工程师来汇报工作进度，市场部和产品经理会出席会议，也可以做些简短的发言，但如果说得太多，很可能就会被打小报告。他们确实想让工程师来主导产品的开发，对自己的产品负责。
* 项目需要的资源都是自愿的
** 一个产品经理把工程师们召集到一起，让他们对他的想法产生兴趣。
** 工程师们决定开发那些让他们感兴趣的特性。
** 工程师跟他们的经理说："我下周想开发这5个新特性"。
** 经理会让工程师独立开发，可能有时会让他优先完成一些特性。
** 工程师独立完成所有的特性——前端/后端/数据库，等等所有相关的部分。如果需要得到设计人员的帮助，需要先让设计人员对你的想法产生兴趣。其他如架构之类的也一样。但总体来说，工程师要独立完成所有的任务。
* 对于某个特性是否值得开发的争论，通常是这么解决的：花一个星期的时间完成他，并在小部分人群中(如1%)进行测试。
* 工程师常常希望解决难题，这能获得声望和尊敬。他们很难对前端项目或UI设计产生太大的兴趣。这跟其他公司可能正好相反。在facebook，后端任务，比如新的feed算法，广告投放算法，memcache优化等等，是工程师真正感兴趣的。
* 所有的代码修改都要进行审核(通过一个或多个工程师)，但News Feed是个例外，因为太重要了，Zuckerberg会亲自review。
* 所有的修改至少要被一个人审核，而且这个系统可以让任何人很方便地审核其他人的代码，即使你没有邀请他
* 工程师负责测试，代码修复，和维护自己的项目。
* 每个办公室或通过VPN连接的员工会使用下一版的facebook，这个版本的facebook会经常更新，通常比公开的早1-12小时。所有的员工被强烈建议提交bugs，而且通常会很快被修复。
* 很奇怪只有很少的QA或自动测试——"大部分工程师都能写出基本没有bug的代码，只是在其他公司他们不需要这么做。如果有QA部门，他们只要把代码写完，扔给他们就行了"
* [针对上一条]我们有自动测试，代码发布前必须要通过测试。我们不相信"所有的工程师都能写出没有bug的代码"，毕竟这是一个商业公司。
* 很奇怪，缺少产品经理的影响和控制——产品经理是很独立的和自由的。产生影响力的关键是与工程师和工程师的领导们们搞好关系。需要大致了解技术，不要提一些愚蠢的想法。
* 所有提交的代码每周二打包一次。
* 只要多一分努力，终于一天会发生改变。
* 星期二的代码发布，需要所有的提交过代码的工程师在场。
* 代码打包前，工程师必须在一个特殊的IRC channel上。
* 运维执行打包过程
** facebook有大约60000台服务器
** 有9个代码发布级别
** 最小的级别只有6台服务器
** 星期二的代码发布会先发布到6台服务器上，运维组会检测这6台服务器的反应，保证代码正常工作，然后再提交到下一级
** 如果发布出现了一些问题（如报错等等），那么就停止下一级的部署，提交出错代码的工程师负责修复问题，然后从头继续发布。
** 所以一次发布可能会经历几次重复：1-2-3-fix. 回到1. 1-2-3-4-5-fix. 回到1. 1-2-3-4-5-6-7-8-9
* 运维组是受过严格训练，倍受尊敬，而且有商业意识的。他们的工作包括分析错误日志，负载和内存状态等等。还包括用户行为。
* 代码发布期间，运维组使用IRC-based页面系统，可以通过facebook/email/irc/im/sms ping每一个工程师，如果需要他们注意的话。对运维组不做回应是一件很羞愧的事。
* 代码一旦发布到第9级，并且稳定运行，就算发布成功了。
* 如果一个特性没有按时完成，也没什么大不了的，下次完成时一并发布即可。
* 如果被svn-blamed,public shamed或工作经常疏忽就很可能被开除。"这是一个高效的文化"。不够高效或者不够聪明的员工会被剔除。管理层会在6个月的时间里观察你表现，如果不合格，只能说再见。每一级都是这个待遇，即使是C级别和VP级别，如果不够高效，也会被开除。
* 被责骂不会导致解雇。我们特别尊重别人，原谅别人。大部分高级工程师都或多或少犯过一些严重的错误，包括我。但没有人因此被解雇。
* 我也没有遇到过因为上面提到过的犯错误而被解雇。有些人犯了错，他们会非常努力地去修复，也让其他人得到了学习。