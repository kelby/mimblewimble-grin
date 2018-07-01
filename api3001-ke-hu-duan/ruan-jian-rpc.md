## hyper

HTTP 相关库。发送 GET、POST 请求。

hyper is a fast, safe HTTP implementation written in and for Rust.

hyper offers both an HTTP client and server which can be used to drive complex web applications written entirely in Rust.

## iron

Web 框架。

输入参数+调用内部接口，目前看是3个服务+重要数据结构及其方法。

Iron is a high level web framework built in and for Rust, built on **hyper**. Iron is designed to take advantage of Rust's greatest features - its excellent type system and its principled approach to ownership in both single threaded and multi threaded contexts.

## 3 个服务

chain::Chain 链

p2p::Peers 节点

pool::TransactionPool 交易池

```rust
get blocks
get chain
get chain/compact
get chain/validate
get chain/outputs
post chain/height-index
get status
get txhashset/roots
get txhashset/lastoutputs?n=10
get txhashset/lastrangeproofs
get txhashset/lastkernels
get txhashset/outputs?start_index=1&max=100
get pool
post pool/push
post peers/a.b.c.d:p/ban
post peers/a.b.c.d:p/unban
get peers/all
get peers/connected
get peers/a.b.c.d
```

## 信息包括

blocks

chain

status

txhashset

pool

peers

可以根据客户端需要，组合不同的数据结构。目前主要还是 GET 获取信息，没有 POST 等修改操作。

