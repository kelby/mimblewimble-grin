## ShortId

Short id for identifying inputs/outputs/kernels

可根据 hash 和 nonce 生成。

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

## Committed

/// Implemented by types that hold inputs and outputs \(and kernels\)

/// containing Pedersen commitments.

/// Handles the collection of the commitments as well as their

/// summing, taking potential explicit overages of fees into account.

## BlockSums

```
/// The output_sum and kernel_sum for a given block.
```

```rust
/// This is used to validate the next block being processed by applying
/// the inputs, outputs, kernels and kernel_offset from the new block
/// and checking everything sums correctly.
#[derive(Debug, Clone)]
pub struct BlockSums {
    /// The total output sum so far.
    pub output_sum: Commitment,
    /// The total kernel sum so far.
    pub kernel_sum: Commitment,
}
```

其作用在上面注释已经说清楚。

要保存到数据库？

Save blocks sums \(the output\_sum and kernel\_sum\) for the given block header.

* save\_block\_sums
* get\_block\_sums

会存储到数据，标识为 BLOCK\_SUMS\_PREFIX

主要用于区块验证、交易验证。

Verify the sum of the kernel excesses equals the sum of the outputs, taking into account both the kernel\_offset and overage.

## TxHashSetRoots

A helper to hold the roots of the txhashset in order to keep them readable

## ChainKVStore

数据存储 ORM

封装的 grin\_store::Store

/// An implementation of the ChainStore trait backed by a simple key-value store.

各个 key

```rust
const BLOCK_HEADER_PREFIX: u8 = 'h' as u8;
const BLOCK_PREFIX: u8 = 'b' as u8;
const HEAD_PREFIX: u8 = 'H' as u8;
const HEADER_HEAD_PREFIX: u8 = 'I' as u8;
const SYNC_HEAD_PREFIX: u8 = 's' as u8;
const HEADER_HEIGHT_PREFIX: u8 = '8' as u8;
const COMMIT_POS_PREFIX: u8 = 'c' as u8;
const BLOCK_MARKER_PREFIX: u8 = 'm' as u8;
const BLOCK_SUMS_PREFIX: u8 = 'M' as u8;
const BLOCK_INPUT_BITMAP_PREFIX: u8 = 'B' as u8;
```

## Committed

```
/// Implemented by types that hold inputs and outputs (and kernels)
/// containing Pedersen commitments.
/// Handles the collection of the commitments as well as their
/// summing, taking potential explicit overages of fees into account.
```



