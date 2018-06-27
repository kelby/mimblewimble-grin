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

## **Block** 区块

BlockHeader

Input

Output

TxKernel

注意：区块头保存的是这几者的 Merklish root, 而这里是关联着具体的实体。

```rust
/// A block as expressed in the MimbleWimble protocol. The reward is
/// non-explicit, assumed to be deducible from block height (similar to
/// bitcoin's schedule) and expressed as a global transaction fee (added v.H),
/// additive to the total of fees ever collected.
#[derive(Debug, Clone)]
pub struct Block {
    /// The header with metadata and commitments to the rest of the data
    pub header: BlockHeader,
    /// List of transaction inputs
    pub inputs: Vec<Input>,
    /// List of transaction outputs
    pub outputs: Vec<Output>,
    /// List of kernels with associated proofs (note these are offset from
    /// tx_kernels)
    pub kernels: Vec<TxKernel>,
}
```

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

/// Compact representation of a full block.

/// Each input/output/kernel is represented as a short\_id.

/// A node is reasonably likely to have already seen all tx data \(tx broadcast

/// before block\) and can go request missing tx data from peers if necessary to

/// hydrate a compact block into a full block.

/// 区块里面主要包含交易，既然在产生区块之前就已经产生了交易（交易被打包成块之前已经进行广播了），并且交易数据已经传送，那么就不需要重复传送了。

/// 主要作用是减少网络请求所需要的传输数据

/// “压缩”与“修剪”是不同的概念。

/// 当前主要用在 传输、（交易池、API客户端）

/// 它即能完整表示区块里包含的信息，又能减少数据量

```rust
pub struct CompactBlock {

/// The header with metadata and commitments to the rest of the data

pub header: BlockHeader, // 完全复制

/// Nonce for connection specific short_ids

pub nonce: u64, // 随机产生，下面计算 ShortId 会用到

/// List of full outputs - specifically the coinbase output(s)

pub out_full: Vec<Output>, // 仅采用 coinbase 部分

/// List of full kernels - specifically the coinbase kernel(s)

pub kern_full: Vec<TxKernel>, // 仅采用 coinbase 部分

/// List of transaction kernels, excluding those in the full list

/// (short_ids)

pub kern_ids: Vec<ShortId>, // 除了 coinbase 外的 kernels，仅取头部，使用了上面的 nonce 进行哈希处理

}
```

## 重要操作：validate 区块校验

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

## 重要操作：修剪

cut\_through

```rust
	/// Matches any output with a potential spending input, eliminating them
	/// from the block. Provides a simple way to cut-through the block. The
	/// elimination is stable with respect to the order of inputs and outputs.
	/// Method consumes the block.
	///
	/// NOTE: exclude coinbase from cut-through process
	/// if a block contains a new coinbase output and
	/// is a transaction spending a previous coinbase
	/// we do not want to cut-through (all coinbase must be preserved)
```



