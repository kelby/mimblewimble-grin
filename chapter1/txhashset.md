## 主要是 3 个哈希的集合

output\_pmmr\_h OutputIdentifier

rproof\_pmmr\_h RangeProof

kernel\_pmmr\_h TxKernel

commit\_index ChainStore

方便某些情况下管理“交易”。

## TxHashSet

```rust
/// An easy to manipulate structure holding the 3 sum trees necessary to
/// validate blocks and capturing the Output set, the range proofs and the
/// kernels. Also handles the index of Commitments to positions in the
/// output and range proof pmmr trees.
///
/// Note that the index is never authoritative, only the trees are
/// guaranteed to indicate whether an output is spent or not. The index
/// may have commitments that have already been spent, even with
/// pruning enabled.

pub struct TxHashSet {
    output_pmmr_h: PMMRHandle<OutputIdentifier>,
    rproof_pmmr_h: PMMRHandle<RangeProof>,
    kernel_pmmr_h: PMMRHandle<TxKernel>,

    // chain store used as index of commitments to MMR positions
    commit_index: Arc<ChainStore>,
}
```

## Extension

```rust
/// Allows the application of new blocks on top of the sum trees in a
/// reversible manner within a unit of work provided by the `extending`
/// function.
pub struct Extension<'a> {
    output_pmmr: PMMR<'a, OutputIdentifier, PMMRBackend<OutputIdentifier>>,
    rproof_pmmr: PMMR<'a, RangeProof, PMMRBackend<RangeProof>>,
    kernel_pmmr: PMMR<'a, TxKernel, PMMRBackend<TxKernel>>,

    commit_index: Arc<ChainStore>,
    new_output_commits: HashMap<Commitment, u64>,
    new_block_markers: HashMap<Hash, BlockMarker>,
    rollback: bool,
}
```

#### OutputIdentifier

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

> 注意：它可以从输入，也可以从输出而来。

#### BlockMarker

```rust
/// The output and kernel positions that define the size of the MMRs for a
/// particular block.
#[derive(Debug, Clone)]
pub struct BlockMarker {
    /// The output (and rangeproof) MMR position of the final output in the
    /// block
    pub output_pos: u64,
    /// The kernel position of the final kernel in the block
    pub kernel_pos: u64,
}
```



