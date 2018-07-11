## PMMR

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



