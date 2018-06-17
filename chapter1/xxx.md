## **BlockHeader** 区块头

元数据。很通用的数据，本区块链特有的数据。

比较特殊的有：

output\_root: Hash \# 根据下面所有的 TxHashSet 而来

range\_proof\_root: Hash\# 根据下面所有的 TxHashSet 而来

kernel\_root: Hash\# 根据下面所有的 TxHashSet 而来

total\_kernel\_offset: BlindingFactor \# 从创世区块到当前的 kernel offsets

比特币只有 **mrkl\_root** 一个哈希，Grin 有三个，除此之外还有致盲因子。

## **Block** 区块

BlockHeader

Input

Output

TxKernel

注意：区块头保存的是这几者的 Merklish root, 而这里是关联着具体的实体。

## A block is simply built from:

* A block header.
* The list of inputs remaining after cut-through.
* The list of outputs remaining after cut-through.
* The transaction kernels containing, for each transaction:
  * The public key`r*G`obtained from the summation of all the commitments.
  * The signatures generated using the excess value.
  * The mining fee.

## **CompactBlock** 压缩区块

区块头

nonce

Output

TxKernel

ShortId \# 一个标识

对比标准的区块，把“输入”去掉了，多了唯一标识 ShortId

## validate 区块校验

verify\_weight

verify\_sorted

verify\_cut\_through

verify\_coinbase

verify\_inputs

verify\_kernel\_lock\_heights

verify\_kernel\_sums

verify\_rangeproofs

verify\_kernel\_signatures

## 特殊区块\(最简单的区块\)

创世区块

