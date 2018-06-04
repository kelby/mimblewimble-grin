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

