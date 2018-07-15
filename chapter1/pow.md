```
/// Miner for the Cuckoo Cycle algorithm. While the verifier will work for
/// graph sizes up to a u64, the miner is limited to u32 to be more memory
/// compact (so shift <= 32). Non-optimized for now and and so mostly used for
/// tests, being impractical with sizes greater than 2^22.
pub struct Miner {
	easiness: u64,
	proof_size: usize,
	cuckoo: Cuckoo,
	graph: Vec<u32>,
	sizeshift: u8,
}
```

Cuckoo Cycle 知识参考数学/密码学对应部分。

具体步骤：略.

