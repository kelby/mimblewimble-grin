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

其功能有限。

process\_block

```
/// Runs the block processing pipeline, including validation and finding a
/// place for the new block in the chain. Returns the new
/// chain head if updated.
```

process\_block\_header

```
/// Process block header as part of "header first" block propagation.
/// We validate the header but we do not store it or update header head based
/// on this. We will update these once we get the block back after requesting
/// it.
```

sync\_block\_header

```
/// Process the block header.
/// This is only ever used during sync and uses a context based on sync_head.
```

rewind\_and\_apply\_fork

```
/// Utility function to handle forks. From the forked block, jump backward
/// to find to fork root. Rewind the txhashset to the root and apply all the
/// forked blocks prior to the one being processed to set the txhashset in
/// the expected state.
```

validate\_header

```
/// First level of block validation that only needs to act on the block header
/// to make it as cheap as possible. The different validations are also
/// arranged by order of cost to have as little DoS surface as possible.
/// TODO require only the block header (with length information)
```

等。

