## Chain

**两部分：**

元数据 + 关联对象

MVC 里一个功能比较综合的“控制器”。

```rust
/// Facade to the blockchain block processing pipeline and storage. Provides
/// the current view of the TxHashSet according to the chain state. Also
/// maintains locking for the pipeline to avoid conflicting processing.

/// Facade to the blockchain block processing pipeline and storage. Provides
/// the current view of the TxHashSet according to the chain state. Also
/// maintains locking for the pipeline to avoid conflicting processing.
pub struct Chain {
    db_root: String,
    store: Arc<store::ChainStore>, // 数据存储（关联对象）
    adapter: Arc<ChainAdapter>, // 网络传输（关联对象）

    head: Arc<Mutex<Tip>>, // 基本信息（数据）
    orphans: Arc<OrphanBlockPool>, // 孤儿，分叉链管理（关联对象）
    txhashset: Arc<RwLock<txhashset::TxHashSet>>, // 关键信息（关联对象）
    // Recently processed blocks to avoid double-processing
    block_hashes_cache: Arc<RwLock<VecDeque<Hash>>>,
}
```

## 元数据

只有两项：

head Tip

txhashset TxHashSet

## 关联对象

store ChainStore

adapter ChainAdapter

orphans OrphanBlockPool

txhashset txhashset::TxHashSet

## 作用

“元数据”这部分不是很重要，主要是对其“关联对象”的处理。如：OrphanBlockPool、BlockContext、ChainStore、TxHashSet 等

（注意：这里的部分概念仅是为了方便“链”进行管理，在其它模块，或者说在整个区块链上，意义不大）。

“链”是大脑、是协调者。协调下面的“软件”的多个模块，让它们协作起来。

对其它区块链项目而言，“链”在概念上可以借鉴，但实现上不能直接参考。



