```rust
/// The output_sum and kernel_sum for a given block.
/// This is used to validate the next block being processed by applying
/// the inputs, outputs, kernels and kernel_offset from the new block
/// and checking everything sums correctly.
#[derive(Debug, Clone)]
pub struct BlockSums {
	/// The total output sum so far.
	pub output_sum: Commitment,
	/// The total kernel sum so far.
	pub kernel_sum: Commitment,
}
```

其作用在上面注释已经说清楚。

要保存到数据库？

Save blocks sums \(the output\_sum and kernel\_sum\) for the given block header.

