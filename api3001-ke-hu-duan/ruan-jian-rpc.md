Communicates with the Grin server

```
SUBCOMMANDS:
    ban                   Ban peer
    help                  Prints this message or the help of the given subcommand(s)
    listconnectedpeers    Print a list of currently connected peers
    status                Current status of the Grin chain
    unban                 Unban peer
```

## Web 框架

**iron**

输入参数+调用内部接口，目前看是3个服务+重要数据结构及其方法。

Iron is a high level web framework built in and for Rust, built on **hyper**. Iron is designed to take advantage of Rust's greatest features - its excellent type system and its principled approach to ownership in both single threaded and multi threaded contexts.

## HTTP 相关库

**hyper**

High level JSON/HTTP client API

发送 GET、POST 请求。

hyper is a fast, safe HTTP implementation written in and for Rust.

hyper offers both an HTTP client and server which can be used to drive complex web applications written entirely in Rust.

## RESTful API

```rust
/// Gets block details given either a hash or height.
/// Optionally return results as "compact blocks" by passing "?compact" query param GET /v1/blocks/<hash>?compact
get blocks

/// Chain handler. Get the head details.
get chain

/// Chain compaction handler. Trigger a compaction of the chain state to regain storage space.
get chain/compact

/// Chain validation handler.
get chain/validate
get chain/outputs

/// Temporary - fix header by height index.
post chain/height-index

/// Status handler. Post a summary of the server status
get status

// Sum tree handler. Retrieve the roots:
get txhashset/roots

// Last inserted nodes::
get txhashset/lastoutputs?n=10
get txhashset/lastrangeproofs
get txhashset/lastkernels

// UTXO traversal::
get txhashset/outputs?start_index=1&max=100

// Build a merkle proof for a given pos
get txhashset/merkleproof?n=1

// Get basic information about the transaction pool.
get pool

// Push new transaction to our local transaction pool.
post pool/push

/// Peer operations
post peers/a.b.c.d:p/ban
post peers/a.b.c.d:p/unban

get peers/all
get peers/connected
get peers/a.b.c.d
```

每个请求都有对应的 Handler 进行处理。

#### 信息包括

blocks

chain

status

txhashset

pool

peers

可以根据客户端需要，组合不同的数据结构。目前主要还是 GET 获取信息，没有 POST 等修改操作。

> 钱包CMD也可以封装调用这里已经实现的方法。

#### 主要涉及功能模块

主要和以下几个模块进行交互：

* chain::Chain 链（链和区块）

* p2p::Peers 网络节点

* pool::TransactionPool 交易池



