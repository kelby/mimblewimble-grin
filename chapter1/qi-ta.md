## ShortId

Short id for identifying inputs/outputs/kernels

可根据 hash 和 nonce 生成。

## OutputIdentifier

```rust
/// An output_identifier can be build from either an input _or_ an output and
/// contains everything we need to uniquely identify an output being spent.
/// Needed because it is not sufficient to pass a commitment around.
#[derive(Serialize, Deserialize, Debug, Clone, PartialEq)]
pub struct OutputIdentifier {
    /// Output features (coinbase vs. regular transaction output)
    /// We need to include this when hashing to ensure coinbase maturity can be
    /// enforced.
    pub features: OutputFeatures,
    /// Output commitment
    pub commit: Commitment,
}
```

它是数据结构 TxHashSet 里的一部分。作用也和 TxHashSet 类似，仅是为了方便数据处理，方便开发。并非核心数据结构。

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

process\_block\_header

sync\_block\_header

rewind\_and\_apply\_fork

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

