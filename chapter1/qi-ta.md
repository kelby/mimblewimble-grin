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

