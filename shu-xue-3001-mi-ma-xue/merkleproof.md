## MerkleProof

默克尔树证明

来源于 MMR，高于 MMR

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

verify

```
    /// Verifies the Merkle proof against the provided
    /// root hash, element and position in the MMR.
```

verify\_consume

```
    /// Consumes the Merkle proof while verifying it.
    /// The proof can no longer beused by the caller after dong this.
    /// Caller must clone() the proof first.
```

来源

在 PMMR 里实现，具体 /// Build a Merkle proof for the element at the given position.

