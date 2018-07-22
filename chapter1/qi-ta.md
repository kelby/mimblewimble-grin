## ShortId

Short id for identifying inputs/outputs/kernels

可根据 hash 和 nonce 生成。

## BlockSums

```
/// The output_sum and kernel_sum for a given block.
```

```rust
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

* save\_block\_sums
* get\_block\_sums

会存储到数据，标识为 BLOCK\_SUMS\_PREFIX

主要用于区块验证、交易验证。

Verify the sum of the kernel excesses equals the sum of the outputs, taking into account both the kernel\_offset and overage.

## TxHashSetRoots

A helper to hold the roots of the txhashset in order to keep them readable



