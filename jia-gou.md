## 架构

分为五个部分：

* 区块链（核心部分，其中又以区块、交易为重点）

* API/客户端（通过RPC交互）

* 网络传输（一般就是P2P）

* 数据存储（运用数据库，保存、管理数据）

* 数学/密码学

模块之间，可通过创建其关联对象进行互相调用。

API/客户端 - 调用 chain::Chain、p2p::Peers、pool::TransactionPool、pool::BlockChain

区块链 - 调用 store::ChainStore（store::Store）、ChainAdapter、PMMRBackend（PMMR）

