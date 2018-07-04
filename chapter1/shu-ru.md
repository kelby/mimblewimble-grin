## \#\# Input

A reference to an output being spent by a transaction.

```
/// The input for a transaction, which spends a pre-existing unspent output.
/// The input commitment is a reproduction of the commitment of the output
/// being spent. Input must also provide the original output features and the
/// hash of the block the output originated from.
```

OutputFeatures \# 来源标记。来自普通交易，还是 Coinbase？根据来源不同，成熟时间不同。

Commitment \# 之前输出的 Commitment

block\_hash \# 之前的输出来源于哪个块？非必选

MerkleProof \# 证明之前存在且本块其它交易未花费（这里是第一次使用）。非必选

```rust
/// A transaction input.
///
/// Primarily a reference to an output being spent by the transaction.
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Input {
    /// The features of the output being spent.
    /// We will check maturity for coinbase output.
    pub features: OutputFeatures,
    /// The commit referencing the output being spent.
    pub commit: Commitment,
    /// The hash of the block the output originated from.
    /// Currently we only care about this for coinbase outputs.
    pub block_hash: Option<Hash>,
    /// The Merkle Proof that shows the output being spent by this input
    /// existed and was unspent at the time of this block (proof of inclusion
    /// in output_root)
    pub merkle_proof: Option<MerkleProof>,
}
```

## An input must provide -

* the commitment \(to lookup the output in the MMR\)
* the output features \(hash in output MMR dependent on features\|commitment\)
* a merkle proof showing inclusion of the output in the originating block
* the block hash of originating blocks
  * \[tbd - maintain index based on merkle proof?\]

## 重要操作

verify\_maturity

```
    /// Verify the maturity of an output being spent by an input.
    /// Only relevant for spending coinbase outputs currently (locked for 1,000
    /// confirmations).
    ///
    /// The proof associates the output with the root by its hash (and pos) in
    /// the MMR. The proof shows the output existed and was unspent at the
    /// time the output_root was built. The root associates the proof with a
    /// specific block header with that output_root. So the proof shows the
    /// output was unspent at the time of the block and is at least as old as
    /// that block (may be older).
    ///
    /// We can verify maturity of the output being spent by -
    ///
    /// * verifying the Merkle Proof produces the correct root for the given
    /// hash (from MMR) * verifying the root matches the output_root in the
    /// block_header * verifying the hash matches the node hash in the Merkle
    /// Proof * finally verify maturity rules based on height of the block
    /// header
```



