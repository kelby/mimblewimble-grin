## ShortId

Short id for identifying inputs/outputs/kernels

可根据 hash 和 nonce 生成。

## Committed

/// Implemented by types that hold inputs and outputs \(and kernels\)

/// containing Pedersen commitments.

/// Handles the collection of the commitments as well as their

/// summing, taking potential explicit overages of fees into account.

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

## ChainKVStore

数据存储 ORM

封装的 grin\_store::Store

/// An implementation of the ChainStore trait backed by a simple key-value store.

各个 key

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

## Committed

```
/// Implemented by types that hold inputs and outputs (and kernels)
/// containing Pedersen commitments.
/// Handles the collection of the commitments as well as their
/// summing, taking potential explicit overages of fees into account.
```

sum\_kernel\_excesses

```
/// Gather the kernel excesses and sum them.
```

sum\_commitments

```
/// Gathers commitments and sum them.
```

verify\_kernel\_sums

```
    /// Verify the sum of the kernel excesses equals the
    /// sum of the outputs, taking into account both
    /// the kernel_offset and overage.
```



