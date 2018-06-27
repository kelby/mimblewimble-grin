**两部分：**

元数据

关联对象

MVC 里一个功能比较综合的“控制器”。

```rust
/// Facade to the blockchain block processing pipeline and storage. Provides
/// the current view of the TxHashSet according to the chain state. Also
/// maintains locking for the pipeline to avoid conflicting processing.
pub struct Chain {
    db_root: String,
    store: Arc<ChainStore>,
    adapter: Arc<ChainAdapter>,

    head: Arc<Mutex<Tip>>,
    orphans: Arc<OrphanBlockPool>,
    txhashset_lock: Arc<Mutex<bool>>,
    txhashset: Arc<RwLock<txhashset::TxHashSet>>,

    // POW verification function
    pow_verifier: fn(&BlockHeader, u8) -> bool,
}
```

## 元数据

db\_root String

head Tip

等

## 关联对象

store ChainStore

adapter ChainAdapter

orphans OrphanBlockPool

txhashset txhashset::TxHashSet

等

## 作用

“元数据”这部分不是很重要，主要是对其“关联对象”的处理。如：OrphanBlockPool、BlockContext、ChainStore、TxHashSet 等（注意：这里的部分概念仅是为了方便“链”进行管理，在其它模块，或者说在整个区块链上，意义不大）。

“链”是大脑、是协调者。协调下面的“软件”的多个模块，让它们协作起来。

对其它区块链项目而言，“链”在概念上可以借鉴，但实现上不能直接参考。

## 链的压缩

compact

```rust
    /// Triggers chain compaction, cleaning up some unnecessary historical
    /// information. We introduce a chain depth called horizon, which is
    /// typically in the range of a couple days. Before that horizon, this
    /// method will:
    ///
    /// * compact the MMRs data files and flushing the corresponding remove logs
    /// * delete old records from the k/v store (older blocks, indexes, etc.)
    ///
    /// This operation can be resource intensive and takes some time to execute.
    /// Meanwhile, the chain will not be able to accept new blocks. It should
    /// therefore be called judiciously.
```



