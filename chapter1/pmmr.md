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



