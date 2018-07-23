Utility structs to handle the 3 hashtrees \(output, range proof, kernel\) more conveniently and transactionally.

## 主要是 3 个哈希的集合

output\_pmmr\_h OutputIdentifier

rproof\_pmmr\_h RangeProof

kernel\_pmmr\_h TxKernel

commit\_index ChainStore

方便某些情况下管理“交易”。

可用于快速检索、校验、验证。

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

和下面的 Extension 差不多，只不过它更加具体一点，因为它所使用的 PMMRHandle 本身已经包含 PMMRBackend，所以这里不用指定。

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

它是数据结构 TxHashSet 里的一部分。作用也和 TxHashSet 类似，仅是为了方便数据处理，方便开发。并非核心数据结构。

#### PMMRBackend

xxx

#### croaring Bitmap

xxx

## Extension

扩展 TxHashSet，大大增强了其功能。

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

#### 操作

is\_unspent

```
    /// Check if an output is unspent.
    /// We look in the index to find the output MMR pos.
    /// Then we check the entry in the output MMR and confirm the hash matches.
```

compact

```
/// Compact the MMR data files and flush the rm logs
```

apply\_raw\_tx

```
    /// Apply a "raw" transaction to the txhashset.
    /// We will never commit a txhashset extension that includes raw txs.
    /// But we can use this when validating txs in the tx pool.
    /// If we can add a tx to the tx pool and then successfully add the
    /// aggregated tx from the tx pool to the current chain state (via a
    /// txhashset extension) then we know the tx pool is valid (including the
    /// new tx).
```

validate\_raw\_txs

```
    /// Validate a vector of "raw" transactions against the current chain state.
    /// We support rewind on a "dirty" txhashset - so we can apply each tx in
    /// turn, rewinding if any particular tx is not valid and continuing
    /// through the vec of txs provided. This allows us to efficiently apply
    /// all the txs, filtering out those that are not valid and returning the
    /// final vec of txs that were successfully validated against the txhashset.
    ///
    /// Note: We also pass in a "pre_tx". This tx is applied to and validated
    /// before we start applying the vec of txs. We use this when validating
    /// txs in the stempool as we need to account for txs in the txpool as
    /// well (new_tx + stempool + txpool + txhashset). So we aggregate the
    /// contents of the txpool into a single aggregated tx and pass it in here
    /// as the "pre_tx" so we apply it to the txhashset before we start
    /// validating the stempool txs.
    /// This is optional and we pass in None when validating the txpool txs
    /// themselves.
```

apply\_block

```
    /// Apply a new set of blocks on top the existing sum trees. Blocks are
    /// applied in order of the provided Vec. If pruning is enabled, inputs also
    /// prune MMR data.
```

merkle\_proof

```
    /// Build a Merkle proof for the given output and the block by
    /// rewinding the MMR to the last pos of the block.
    /// Note: this relies on the MMR being stable even after pruning/compaction.
    /// We need the hash of each sibling pos from the pos up to the peak
    /// including the sibling leaf node which may have been removed.
```

rewind

```
    /// Rewinds the MMRs to the provided block, rewinding to the last output pos
    /// and last kernel pos of that block.
```

validate

```
/// Validate the txhashset state against the provided block header.
```



