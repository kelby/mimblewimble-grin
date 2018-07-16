## Chain

**两部分：**

元数据

关联对象

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
	store: Arc<store::ChainStore>, // 数据存储
	adapter: Arc<ChainAdapter>, // 网络传输

	head: Arc<Mutex<Tip>>, // 基本信息
	orphans: Arc<OrphanBlockPool>, // 孤儿，分叉链管理
	txhashset: Arc<RwLock<txhashset::TxHashSet>>, // 关键信息
	// Recently processed blocks to avoid double-processing
	block_hashes_cache: Arc<RwLock<VecDeque<Hash>>>,
	// Recently processed headers to avoid double-processing
	header_hashes_cache: Arc<RwLock<VecDeque<Hash>>>,
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

等

## 作用

“元数据”这部分不是很重要，主要是对其“关联对象”的处理。如：OrphanBlockPool、BlockContext、ChainStore、TxHashSet 等（注意：这里的部分概念仅是为了方便“链”进行管理，在其它模块，或者说在整个区块链上，意义不大）。

“链”是大脑、是协调者。协调下面的“软件”的多个模块，让它们协作起来。

对其它区块链项目而言，“链”在概念上可以借鉴，但实现上不能直接参考。

#### 重要操作

init

```
    /// Initializes the blockchain and returns a new Chain instance. Does a
    /// check on the current chain head to make sure it exists and creates one
    /// based on the genesis block if necessary.
```

process\_block\_no\_orphans

```
    /// Attempt to add a new block to the chain. Returns the new chain tip if it
    /// has been added to the longest chain, None if it's added to an (as of
    /// now) orphan chain.
```

validate

```
    /// Validate the current chain state.
```

compact

```
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

txhashset\_read

```
    /// Provides a reading view into the current txhashset state as well as
    /// the required indexes for a consumer to rewind to a consistent state
    /// at the provided block hash.
```

txhashset\_write

```
    /// Writes a reading view on a txhashset state that's been provided to us.
    /// If we're willing to accept that new state, the data stream will be
    /// read as a zip file, unzipped and the resulting state files should be
    /// rewound to the provided indexes.
```

其它操作也很重要，只是篇幅有限，这里挑几个出来讲解。

