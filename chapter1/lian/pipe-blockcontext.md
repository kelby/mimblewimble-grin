## pipe BlockContext

方便某些情况下管理“区块”

模块化设计的产物。

数据结构和 Chain 链有几分相似，相当于子集。

```rust
/// Contextual information required to process a new block and either reject or
/// accept it.
pub struct BlockContext {
    /// The options
    pub opts: Options,
    /// The store
    pub store: Arc<ChainStore>,
    /// The head
    pub head: Tip,
    /// The POW verification function
    pub pow_verifier: fn(&BlockHeader, u8) -> bool,
    /// MMR sum tree states
    pub txhashset: Arc<RwLock<txhashset::TxHashSet>>,
}
```



