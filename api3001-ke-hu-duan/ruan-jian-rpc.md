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

简单封装，实现发送 GET、POST 请求。

hyper is a fast, safe HTTP implementation written in and for Rust.

hyper offers both an HTTP client and server which can be used to drive complex web applications written entirely in Rust.

## RESTful API

#### 信息包括

blocks

chain

status

txhashset

pool

peers

> /// Start all server HTTP handlers. Register all of them with Iron
>
> /// and runs the corresponding HTTP server.
>
> ///
>
> /// Hyper currently has a bug that prevents clean shutdown. In order
>
> /// to avoid having references kept forever by handlers, we only pass
>
> /// weak references. Note that this likely means a crash if the handlers are
>
> /// used after a server shutdown \(which should normally never happen,
>
> /// except during tests\).

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

// Supports retrieval of multiple outputs in a single request
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

可以根据客户端需要，组合不同的数据结构。目前主要还是 GET 获取信息，没有 POST 等修改操作。

> 钱包CMD也可以封装调用这里已经实现的方法。

#### 主要涉及功能模块

主要和以下几个模块进行交互：

* chain::Chain 链（链和区块）

* p2p::Peers 网络节点

* pool::TransactionPool 交易池

* pool::BlockChain 与交易池交互（间接与区块链交互）

#### 方便开发，创建数据结构

Tip /// The state of the current fork tip

Status /// Status page containing different server information

TxHashSet /// TxHashSet

TxHashSetNode /// Wrapper around a list of txhashset nodes, so it can be /// presented properly via json

Output

PrintableCommitment

OutputPrintable // As above, except formatted a bit better for human viewing

TxKernelPrintable // Printable representation of a block

BlockHeaderInfo // Just the information required for wallet reconstruction

BlockHeaderPrintable

BlockPrintable // Printable representation of a block

CompactBlockPrintable

BlockOutputs // For wallet reconstruction, include the header info along with the // transactions in the block

OutputListing // For traversing all outputs in the UTXO set // transactions in the block

PoolInfo

