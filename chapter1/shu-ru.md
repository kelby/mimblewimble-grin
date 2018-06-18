## A reference to an output being spent by a transaction.

OutputFeatures \# 来源标记。来自普通交易，还是 Coinbase？根据来源不同，成熟时间不同。

Commitment \# 之前输出的 Commitment

block\_hash \# 之前的输出来源于哪个块？非必选

MerkleProof \# 证明之前存在且本块其它交易未花费（这里是第一次使用）。非必选

## An input must provide -

* the commitment \(to lookup the output in the MMR\)
* the output features \(hash in output MMR dependent on features\|commitment\)
* a merkle proof showing inclusion of the output in the originating block
* the block hash of originating blocks
  * \[tbd - maintain index based on merkle proof?\]



