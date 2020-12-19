# 问题

事件驱动是大家谈论解耦的时候寄予众望的技术。但是具体到实际的项目中，经常发现事件驱动没有发挥出什么作用。为什么会这样?

# 分析

## 基于事件的数据库同步

事件驱动经常变成一种数据库的同步技术。构造一个 Read Model 是有价值的，也是一种重要的解耦合手段。但是事件驱动的 Read Model 同步未必是最佳的实现技术。

【TODO，给个例子】

## 不要返回值?

核心的问题在于事件驱动是没有返回值的。那业务逻辑上这个返回值怎么反馈给用户呢? 除了发通知，发短信等天然的异步场景，大部分业务流程都是要反馈结果，通知用户下一步操作的。事件驱动最大的难题在于产品的交互设计上。

【TODO，给个例子】