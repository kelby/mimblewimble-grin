## PMMR

Prunable Merkle Mountain Range

```rust
/// Prunable Merkle Mountain Range implementation. All positions within the tree
/// start at 1 as they're postorder tree traversal positions rather than array
/// indices.
///
/// Heavily relies on navigation operations within a binary tree. In particular,
/// all the implementation needs to keep track of the MMR structure is how far
/// we are in the sequence of nodes making up the MMR.
```

merkle\_proof

```
/// Build a Merkle proof for the element at the given position in the MMR
```

validate

```
/// Walks all unpruned nodes in the MMR and revalidate all parent hashes
```

## MerkleProof

```rust
/// A Merkle proof.
/// Proves inclusion of an output (node) in the output MMR.
/// We can use this to prove an output was unspent at the time of a given block
/// as the root will match the output_root of the block header.
/// The path and left_right can be used to reconstruct the peak hash for a
/// given tree in the MMR.
/// The root is the result of hashing all the peaks together.
#[derive(Clone, Debug, Eq, Ord, PartialEq, PartialOrd, Serialize, Deserialize)]
pub struct MerkleProof {
    /// The root hash of the full Merkle tree (in an MMR the hash of all peaks)
    pub root: Hash, // 根
    /// The hash of the element in the tree we care about
    pub node: Hash, // 叶子
    /// The size of the full Merkle tree
    pub mmr_size: u64, // 总数据大小
    /// The full list of peak hashes in the MMR
    pub peaks: Vec<Hash>, // 枝干
    /// The sibling (hash, pos) along the path of the tree
    /// as we traverse from node to peak
    pub path: Vec<(Hash, u64)>, // 路径
}
```

verify

```
    /// Verify the Merkle proof.
    /// We do this by verifying the following -
    /// * inclusion of the node beneath a peak (via the Merkle path/branch of
    /// siblings) * inclusion of the peak in the "bag of peaks" beneath the
    /// root
```



