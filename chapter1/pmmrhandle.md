## PMMRHandle

通过 PMMRHandle 提供给 TxHashSet 使用，进而影响整个系统。

```
struct PMMRHandle<T>
where
    T: PMMRable,
{
    backend: PMMRBackend<T>,
    last_pos: u64,
}
```

TxHashSet 会用到它，这是数据存储与区块链核心业务的链接之处（TxHashSet 被包含于 Chain）。

存储数据：

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



