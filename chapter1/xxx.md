## **BlockHeader** 区块头

元数据。

比较特殊的有：

output\_root: Hash

range\_proof\_root: Hash

kernel\_root: Hash

total\_kernel\_offset: BlindingFactor

pow: Proof

## **CompactBlock** 压缩区块

区块头

nonce

Output

TxKernel

ShortId

## **Block** 区块

BlockHeader

Input

Output

TxKernel

## A block is simply built from:

* A block header.
* The list of inputs remaining after cut-through.
* The list of outputs remaining after cut-through.
* The transaction kernels containing, for each transaction:
  * The public key`r*G`obtained from the summation of all the commitments.
  * The signatures generated using the excess value.
  * The mining fee.



