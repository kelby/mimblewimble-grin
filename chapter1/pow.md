Cuckoo Cycle

使用概念：环和边

```rust
/// An edge in the Cuckoo graph, simply references two u64 nodes.
#[derive(Debug, Copy, Clone, PartialEq, PartialOrd, Eq, Ord, Hash)]
struct Edge {
	u: u64,
	v: u64,
}

/// Cuckoo cycle context
pub struct Cuckoo {
	mask: u64,
	size: u64,
	v: [u64; 4],
}
```



