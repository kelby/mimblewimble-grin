## PMMR

一种数据结构。

```
/// Prunable Merkle Mountain Range implementation. All positions within the tree
/// start at 1 as they're postorder tree traversal positions rather than array
/// indices.
///
/// Heavily relies on navigation operations within a binary tree. In particular,
/// all the implementation needs to keep track of the MMR structure is how far
/// we are in the sequence of nodes making up the MMR.
pub struct PMMR<'a, T, B>
where
    T: PMMRable,
    B: 'a + Backend<T>,
{
    /// The last position in the PMMR
    pub last_pos: u64,
    backend: &'a mut B,
    // only needed to parameterise Backend
    _marker: marker::PhantomData<T>,
}
```

这里的 Backend 就是数据存储里的 PMMRBackend

```
//! This implementation is built in two major parts:
//!
//! 1. A set of low-level functions that allow navigation within an arbitrary
//! sized binary tree traversed in postorder. To realize why this us useful,
//! we start with the standard height sequence in a MMR: 0010012001... This is
//! in fact identical to the postorder traversal (left-right-top) of a binary
//! tree. In addition postorder traversal is independent of the height of the
//! tree. This allows us, with a few primitive, to get the height of any node
//! in the MMR from its position in the sequence, as well as calculate the
//! position of siblings, parents, etc. As all those functions only rely on
//! binary operations, they're extremely fast. For more information, see the
//! doc on bintree_jump_left_sibling.
//! 2. The implementation of a prunable MMR tree using the above. Each leaf
//! is required to be Writeable (which implements Hashed). Tree roots can be
//! trivially and efficiently calculated without materializing the full tree.
//! The underlying Hashes are stored in a Backend implementation that can
//! either be a simple Vec or a database.
```

Prunable Merkle Mountain Range

merkle\_proof

```
/// Build a Merkle proof for the element at the given position in the MMR
```

validate

```
/// Walks all unpruned nodes in the MMR and revalidate all parent hashes
```

可能过 txhaseset Extension 进而与系统交互，实现其功能。

## PMMRHandle

通过 PMMRHandle 提供给 TxHashSet 使用，进而影响整个系统。

```
struct PMMRHandle<T>
where
    T: PMMRable,
{
    backend: PMMRBackend<T>,
    last_pos: u64,
}
```

TxHashSet 会用到它，这是数据存储与区块链核心业务的链接之处（TxHashSet 被包含于 Chain）。

存储数据：

```rust
const BLOCK_HEADER_PREFIX: u8 = 'h' as u8;
const BLOCK_PREFIX: u8 = 'b' as u8;
const HEAD_PREFIX: u8 = 'H' as u8;
const HEADER_HEAD_PREFIX: u8 = 'I' as u8;
const SYNC_HEAD_PREFIX: u8 = 's' as u8;
const HEADER_HEIGHT_PREFIX: u8 = '8' as u8;
const COMMIT_POS_PREFIX: u8 = 'c' as u8;
const BLOCK_MARKER_PREFIX: u8 = 'm' as u8;
const BLOCK_SUMS_PREFIX: u8 = 'M' as u8;
const BLOCK_INPUT_BITMAP_PREFIX: u8 = 'B' as u8;
```

## 两个概念解析

PMMR 和 PMMRHandle 差不多，都是 &lt;T, B&gt; 结构，T 表示要存储的数据，B 表示存储实现。不同点在于前者还没有明确 B，而后者明确了，就是用 PMMRBackend。

它们的数据结构能直接证明上述描述，Extension 和 TxHashSet 能间接证明上述描述。

Backend 约等于 PMMRBackend，前者是接口，后者是具体实现。它们就是上述描述里的“存储实现”。

MerkleProof 来源于 MMR，但高于 MMR。具体是其数据来源于 MMR，但其用于及意义高于 MMR。

