## **BlockHeader** 区块头

元数据。很通用的数据，本区块链特有的数据。

比较特殊的有：

output\_root: Hash \# 根据下面所有的 TxHashSet 而来

range\_proof\_root: Hash\# 根据下面所有的 TxHashSet 而来

kernel\_root: Hash\# 根据下面所有的 TxHashSet 而来

total\_kernel\_offset: BlindingFactor \# 从创世区块到当前的 kernel offsets

比特币只有 **mrkl\_root** 一个哈希，Grin 有三个，除此之外还有致盲因子。

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
	/// Total accumulated sum of kernel commitments since genesis block.
	/// Should always equal the UTXO commitment sum minus supply.
	pub total_kernel_sum: Commitment,
	/// Total size of the output MMR after applying this block
	pub output_mmr_size: u64,
	/// Total size of the kernel MMR after applying this block
	pub kernel_mmr_size: u64,
	/// Nonce increment used to mine this block.
	pub nonce: u64,
	/// Proof of work data.
	pub pow: Proof,
}
```

All block headers include the root hash of all unspent outputs in the chain at the time of that block.

> 虽然不是强制，但区块头没有类似"数组"这样的数据结构，下面的各个字段都相对比较固定。

## 区块校验

We're able to verify the whole chain, the total work, the validity of each block, their full content, etc. In addition, with MimbleWimble and full UTXO set commitments, even more integrity validation can be performed.

区块（以及交易）的验证，都可分为两部分：自证（根据自身数据进行验证）；他证（借助与之相关的外部数据进行验证）。

先检查版本和高度

再检查时间戳

检查上一个块的哈希

再次检查高度和时间戳

检查总难度

检查工作量证明

再根据上一个块的检查难度

