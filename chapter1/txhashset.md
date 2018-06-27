## 主要是 3 个哈希的集合

output\_pmmr\_h OutputIdentifier

rproof\_pmmr\_h RangeProof

kernel\_pmmr\_h TxKernel

commit\_index ChainStore

方便某些情况下管理“交易”。

## Extension

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
```

```rust
/// Allows the application of new blocks on top of the sum trees in a
/// reversible manner within a unit of work provided by the `extending`
/// function.
pub struct Extension<'a> {
    output_pmmr: PMMR<'a, OutputIdentifier, PMMRBackend<OutputIdentifier>>,
    rproof_pmmr: PMMR<'a, RangeProof, PMMRBackend<RangeProof>>,
    kernel_pmmr: PMMR<'a, TxKernel, PMMRBackend<TxKernel>>,
}
```



