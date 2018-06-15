**hyper** HTTP 相关库。

**iron** Web 框架。

输入参数+调用内部接口，目前看是3个服务+重要数据结构及其方法。

**3 个服务：**

chain::Chain 链

p2p::Peers 节点

pool::TransactionPool 交易池

**信息包括：**

blocks

chain

status

txhashset

pool

peers

可以根据客户端需要，组合不同的数据结构。目前主要还是 GET 获取信息，没有 POST 等修改操作。



