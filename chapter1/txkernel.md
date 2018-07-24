The excess value is a multisig of all the input owners and all the output owners.

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
    pub excess: Commitment, // 相当于公钥（可由 Output 而来）
    /// The signature proving the excess is a valid public key, which signs
    /// the transaction fee.
    pub excess_sig: Signature, # 包含了 TxKernel 下面的其它 4 个元素，相当于签名
}
```

The excess value is a multisig but it's also a proof that the transaction adds up to zero at the same time.

#### excess\_sig

包含了 TxKernel 下面的其它 4 个元素

#### excess

交易有 offset: BlindingFactor，它对应 k = k1 + k2 这里的 k2

excess 对应 k1G

## 作用

* 元数据
* 见证&签名
* Trust model

## verify 验证

这里特指密码学上的验证。

```
    /// Verify the transaction proof validity. Entails handling the commitment
    /// as a public key and checking the signature verifies with the fee as
    /// message.
```

fee 和 lock\_height 做为消息，excess\_sig 做为签名，excess 做为公钥，用的是 secp 相关算法。

上面几个要素，已经完全符合密码学里“验证”条件。



