```rust
/// Block header, fairly standard compared to other blockchains.
#[derive(Clone, Debug, PartialEq)]
pub struct BlockHeader {
    /// Version of the block
    pub version: u16,
    /// Height of this block since the genesis block (height 0)
    pub height: u64,
    /// Hash of the block previous to this in the chain.
    pub previous: Hash,
    /// Timestamp at which the block was built.
    pub timestamp: time::Tm,
    /// Total accumulated difficulty since genesis block
    pub total_difficulty: Difficulty,
    /// Merklish root of all the commitments in the TxHashSet
    pub output_root: Hash,
    /// Merklish root of all range proofs in the TxHashSet
    pub range_proof_root: Hash,
    /// Merklish root of all transaction kernels in the TxHashSet
    pub kernel_root: Hash,
    /// Total accumulated sum of kernel offsets since genesis block.
    /// We can derive the kernel offset sum for *this* block from
    /// the total kernel offset of the previous block header.
    pub total_kernel_offset: BlindingFactor,
    /// Nonce increment used to mine this block.
    pub nonce: u64,
    /// Proof of work data.
    pub pow: Proof,
}
```

All block headers include the root hash of all unspent outputs in the chain at the time of that block.

> 虽然不是强制，但区块头没有类似"数组"这样的数据结构，下面的各个字段都相对比较固定。

## 区块校验

先检查版本和高度

再检查时间戳

检查上一个块的哈希

再次检查高度和时间戳

检查总难度

检查工作量证明

再根据上一个块的检查难度

