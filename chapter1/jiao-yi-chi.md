“交易池”最终要关联到“交易”

## TransactionPool &gt; Pool &gt; PoolEntry &gt; Transaction

元数据+其它关联对象

#### TransactionPool

包含两种“池子”\(txpool 和 stempool，结构是一样的，作用略有不同\)

作用主要是管理它们

```rust
/// Transaction pool implementation.
pub struct TransactionPool<T> {
    /// Pool Config
    pub config: PoolConfig,

    /// Our transaction pool.
    pub txpool: Pool<T>,
    /// Our Dandelion "stempool".
    pub stempool: Pool<T>,

    /// The blockchain
    pub blockchain: Arc<T>,
    /// The pool adapter
    pub adapter: Arc<PoolAdapter>,
}
```

#### Pool

主要包含“池子实例”\(PoolEntry\)

作用主要是管理它们

```rust
pub struct Pool<T> {
    /// Entries in the pool (tx + info + timer) in simple insertion order.
    pub entries: Vec<PoolEntry>,
    /// The blockchain
    pub blockchain: Arc<T>,
    pub name: String,
}
```

添加，查询、过滤。

#### PoolEntry

除了自身一些数据外，主要是关联着“交易”

交易池相关最小单位，和交易一一对应。

它是被管理者

```rust
/// Represents a single entry in the pool.
/// A single (possibly aggregated) transaction.
#[derive(Clone, Debug)]
pub struct PoolEntry {
    /// The state of the pool entry.
    pub state: PoolEntryState,
    /// Info on where this tx originated from.
    pub src: TxSource,
    /// Timestamp of when this tx was originally added to the pool.
    pub tx_at: Timespec,
    /// The transaction itself.
    pub tx: Transaction,
}
```

状态共有 5 种，主要是 stem 和 fluff，用标识及后续查询、过滤，相关知识可查看 Dandelion 协议。

来源主要起标识作用。

时间戳为交易关联（加入）本 PoolEntry 的时间

交易就是交易

## 要做的事

数据进来

数据出去

数据是合理的：自证（根据自身数据进行验证）、他证（借助与之有关联的外部数据进行验证）

数据处理（聚合交易；选择指定状态的交易，然后设置为另一指定状态等）





