## Transaction

输入是输出的简单引用，输出包含了交易金额，TxKernel 包含了手续费和签名。

```rust
/// A transaction
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Transaction {
    /// List of inputs spent by the transaction.
    pub inputs: Vec<Input>,
    /// List of outputs the transaction produces.
    pub outputs: Vec<Output>,
    /// List of kernels that make up this transaction (usually a single kernel).
    pub kernels: Vec<TxKernel>,
    /// The kernel "offset" k2
    /// excess is k1G after splitting the key k = k1 + k2
    pub offset: BlindingFactor, // 随机数，供加密、签名、验证、计算用
}
```

#### Input（输入）

List of inputs spent by the transaction.

#### Output（输出）

List of outputs the transaction produces.

#### TxKernel（元数据 + 签名）

List of kernels that make up this transaction \(usually a single kernel\).

#### BlindingFactor（额外数据）

The kernel "offset" k2 excess is k1G after splitting the key k = k1 + k2

## 校验

Verification of zero sums. 输入与输出之差为0，不能额外产生或者销毁。

Possession of private keys. 确保私钥的拥有者才能发起交易。

```
    /// Validates all relevant parts of a fully built transaction. Checks the
    /// excess value against the signature as well as range proofs for each
    /// output.
```

## A Grin transaction consists of the following

* A set of inputs, each referencing a previous output being spent.
* A set of new outputs that include -
  * A value`v`and a blinding factor \(private key\)`r`multiplied on a curve and summed to be`rG+vH`
  * A range proof that shows that v is non-negative.
* An explicit transaction fee in the clear.
* A signature, computed by taking the excess blinding value \(the sum of all outputs plus the fee, minus the inputs\) and using it as the private key.

## 组成

门罗币的组成是：前缀、后缀。后缀就是签名，前缀又拆分为输入、输出、元数据、额外数据。

比特币的，则更简单。输入、输出、元数据、额外数据、签名。

这里呢？

类比过来，同样的道理。

备注：这里的签名，包含了见证（不拆分，方便理解）。

## 运用

聚合签名（数学、密码学）

构建交易（核心业务）

证明（Proof）

Slate（核心业务。用于构建交易所需的公开数据）

## fee

是下面所有 kernels 的手续费（fee）之和

## lock\_height

下面所有 kernels 的被锁高度（lock\_height）取最大值

## 合并 aggregate

```
/// Aggregate a vec of transactions into a multi-kernel transaction with
/// cut_through
```

aggregate 已经实现。

inputs

outputs

kernels

kernel\_offsets

有这 4 者就能重新创建一个交易。可以将原来多个交易，合并成一个！

#### offset

```
			// tx has an offset k2 where k = k1 + k2
			// and the tx is signed using k1
			// the kernel excess is k1G
```

```
sum := BlindSum::new()

blind_sum = ctx.keychain.blind_sum(&sum)?

split = blind_sum.split(&keychain.secp())?
k1 = split.blind_1
k2 = split.blind_2

// store the kernel offset (k2) on the tx itself
// commitments will sum correctly when including the offset
tx.offset = k2.clone()
```

split 介绍

```
	/// Split a blinding_factor (aka secret_key) into a pair of
	/// blinding_factors. We use one of these (k1) to sign the tx_kernel (k1G)
	/// and the other gets aggregated in the block_header as the "offset".
	/// This prevents an actor from being able to sum a set of inputs, outputs
	/// and kernels from a block to identify and reconstruct a particular tx
	/// from a block. You would need both k1, k2 to do this.
```



