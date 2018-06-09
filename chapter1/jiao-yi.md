## Input

List of inputs spent by the transaction.

## Output

List of outputs the transaction produces.

## TxKernel

List of kernels that make up this transaction \(usually a single kernel\).

## BlindingFactor

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



