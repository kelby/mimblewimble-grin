OutputFeatures \# 来源标记

Commitment \# 见证（输出金额）

RangeProof \# 见证所涉及的金额没有负数

```rust
/// Output for a transaction, defining the new ownership of coins that are being
/// transferred. The commitment is a blinded value for the output while the
/// range proof guarantees the commitment includes a positive value without
/// overflow and the ownership of the private key. The switch commitment hash
/// provides future-proofing against quantum-based attacks, as well as providing
/// wallet implementations with a way to identify their outputs for wallet
/// reconstruction.
#[derive(Debug, Copy, Clone, Serialize, Deserialize)]
pub struct Output {
	/// Options for an output's structure or use
	pub features: OutputFeatures,
	/// The homomorphic commitment representing the output amount
	pub commit: Commitment,
	/// A proof that the commitment is in the right range
	pub proof: RangeProof,
}
```

## An output consists of

* features \(currently coinbase vs. non-coinbase\)
* commitment`rG+vH`
* rangeproof

## To spend an output we continue to need -

* `r`and`v`to build the commitment and to prove ownership



