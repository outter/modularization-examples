## Autonomy

所有人似乎都在修改同一个文件，例如 order.php。所有需求似乎都堆积在少数几个人的身上。所有团队似乎都等着同一个模块的上线，但是一天只有24小时，没有足够的时间去在生产环境验证新部署的可靠性。公司里的 PMO 越来越多，项目的感谢名单越来越长。

## Consistency

很多地方都在写非常类似的代码，比如每个 RPC 调用之后，都要手工再写一行日志。所有的列表页面，都要重复实现一次分页，排序等非常类似的功能。当出现性能问题，稳定性问题的时候，似乎需要修改一亿个地方才能改完。每当你发现 ctrl-c / ctrl-v 的代码的时候，代码已经被复制过 N 份了，甚至已经上线了。这个时候让人家去返工，纯属没事找事。所有的产品经理都视你为敌，因为你总是以复用之名，漠视他们的体验微创新的巨大价值。

## Feedback

单元测试不要说一个函数了。就是一个 git 仓库也往往是跑不起来的。不要说在开发笔记本上跑不起来了，就是在机房的测试环境里都经常跑不起来的，依赖联调作战。全球全宇宙的孤本可能就是那个所谓的生产环境了。出了错也无法很快定位到是哪个模块出的问题。要么是没有足够的日志，要么是日志太多了，把信号淹没在噪音的海洋里了。获得 Feedback 的时间以天为单位，甚至以周为单位。

# 模块化的三个优化目标

这三个优化目标分别是

* Autonomy：减少沟通成本，一个需求改的模块数尽可能的少，一个模块的负责团队需要的知识边界尽可能的小。
* Consistency：在保障 Autonomy 的情况下，减少不必要的不一致性。引入额外的不一致性，需要获得足够额外的业务收益。
* Feedback：增加人员流动性，能够让新人快速上手。最有效的“文档”是可工作的软件本身提供的交互式学习环境。

Modularization 是很容易达成的，可以以任意地方式切分出各种形态的模块。然而评判 Modularization 的收益是非常困难的，大致可以归纳为以上三个难以量化的方面。这也就使得 Modularization 更像一门艺术而不是科学，谁也无法说服别人自己的 Modularization 方案比他们的要“好”。同时这三个方面的收益都是“降低成本”的收益，以下是常见的不切实际的预期：

* 降低新需求的交付时间：这很难达到，新需求往往是全新的。不能为了快而强行复用。
* 增加收入：降本和增收是两码事
* 获得比较竞争优势，达成业务成功：相比内燃机，集成电路等技术带来的成本急剧下降，Modularization 的改良对象是人类的协作，是不可能有特别大幅度的成本降低的。

既然只是降低有限成本的技术，为什么还值得软件开发人员去追求呢? 因为人不是没有情感的机器，从 Autonomy, Consistency, Feedback 三个方面，从业者可以收获人类本能的喜悦。对于从业者自身的情感价值，恐怕要远大于对资本方的价值。没有证据可以证明，把人异化为螺丝钉，996 的工作制不能交付出有商业价值的软件。也没有证据证明，高市值的软件企业不用堆人的方式工作，可以获得更高的市场估值。

假定 Modularization 仍然是值得追求的技术，那么为什么是 Autonomy, Consistency, Feedback，而不是其他的分法呢? 可以看如下的模块依赖关系图

![shape](./shape.drawio.svg)

假设对于 B 来说

* Autonomy：是指不用关心自己边界之外的事情。比如 C 和 D，相对 B 来说，就是完全没有关系的模块。也就是“确保不应该产生依赖的模块，不产生依赖”
* Consistency：是指一个模块改了，所有依赖的地方都连着变了。比如改了 A，也就是改了 B、C、D。也就是“确保应该复用的模块，被复用”
* Feedback：是指每个模块能多高效率的获得反馈。B是连着A，就可以获得反馈，还是要ABCDE都集成到一起才能获得反馈。如果获得整体反馈之后，是否可以把反馈拆解到模块。也就是“模块如何集成起来工作，又如何把反馈拆解回模块”

可见 Autonomy, Consistency, Feedback 完整覆盖了依赖的上游，下游，以及集成。这里剥离了具体的业务，是为了从抽象的层面看到这个分类法的完备性。接下来我们以具体的案例来看，从 Autonomy, Consistency, Feedback 三个视角，如何优化。