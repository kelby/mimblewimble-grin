## MerkleProof

```
/// A Merkle proof that proves a particular element exists in the MMR.
#[derive(Serialize, Deserialize, Debug, Eq, PartialEq, Clone, PartialOrd, Ord)]
pub struct MerkleProof {
    /// The size of the MMR at the time the proof was created.
    pub mmr_size: u64,
    /// The sibling path from the leaf up to the final sibling hashing to the
    /// root.
    pub path: Vec<Hash>,
}
```



