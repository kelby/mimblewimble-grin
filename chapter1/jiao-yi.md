## Input（输入）

List of inputs spent by the transaction.

## Output（输出）

List of outputs the transaction produces.

## TxKernel（元数据 + 签名）

List of kernels that make up this transaction \(usually a single kernel\).

## BlindingFactor（额外数据）

The kernel "offset" k2 excess is k1G after splitting the key k = k1 + k2

## 两个校验

Verification of zero sums. 输入与输出之差为0，不能额外产生或者销毁。

Possession of private keys. 确保私钥的拥有者才能发起交易。

## A Grin transaction consists of the following -

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

build\_input





