```rust
/// A proof that a transaction sums to zero. Includes both the transaction's
/// Pedersen commitment and the signature, that guarantees that the commitments
/// amount to zero.
/// The signature signs the fee and the lock_height, which are retained for
/// signature validation.
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct TxKernel {
	/// Options for a kernel's structure or use
	pub features: KernelFeatures,
	/// Fee originally included in the transaction this proof is for.
	pub fee: u64,
	/// This kernel is not valid earlier than lock_height blocks
	/// The max lock_height of all *inputs* to this transaction
	pub lock_height: u64,
	/// Remainder of the sum of all transaction commitments. If the transaction
	/// is well formed, amounts components should sum to zero and the excess
	/// is hence a valid public key.
	pub excess: Commitment,
	/// The signature proving the excess is a valid public key, which signs
	/// the transaction fee.
	pub excess_sig: Signature,
}
```



```
X = 113*G + 3*H
```

```
Xi => Y
```

```
Y - Xi = (113*G + 3*H) - (113*G + 3*H) = 0*G + 0*H
```

```
Y - Xi = ((113+28)*G + 3*H) - (113*G + 3*H) = 28*G + 0*H
```

That signature, attached to every transaction, together with some additional data \(like mining fees\), is called a

_transaction kernel_.

