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
    pub excess: Commitment,
    /// The signature proving the excess is a valid public key, which signs
    /// the transaction fee.
    pub excess_sig: Signature, # 包含了 TxKernel 下面的其它 4 个元素
}
```

The excess value is a multisig but it's also a proof that the transaction adds up to zero at the same time.

## 作用

* 元数据
* 见证&签名
* Trust model

## 验证

fee + lock\_height 是消息

excess\_sig 是签名

excess 是公钥

用的是 secp 相关算法。

