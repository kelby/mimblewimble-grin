## A reference to an output being spent by a transaction.

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



