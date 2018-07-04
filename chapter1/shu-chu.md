## Output

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

#### OutputIdentifier

```
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

#### ProofMessageElements

```
/// A structure which contains fields that are to be committed to within
/// an Output's range (bullet) proof.
#[derive(Serialize, Deserialize, Debug, Clone, PartialEq)]
pub struct ProofMessageElements {
	/// The amount, stored to allow for wallet reconstruction as
	/// rewinding isn't supported in bulletproofs just yet
	/// This is going to be written 3 times, to facilitate checking
	/// values on rewind
	/// Note that rewinding with only the nonce will give you back
	/// the first 32 bytes of the message. To get the second
	/// 32 bytes, you need to provide the correct blinding factor as well
	value: u64,
	/// another copy of the value, to check on rewind
	value_copy_1: u64,
	/// another copy of the value
	value_copy_2: u64,
	/// the first 8 bytes of the blinding factor, used to avoid having to grind
	/// through a proof each time you want to check against key possibilities
	bf_first_8: Vec<u8>,
	/// unused portion of message, used to test whether we have both nonce
	/// and blinding correct
	zeroes: Vec<u8>,
}
```



