## ChainStore

```
/// All chain-related database operations
pub struct ChainStore {
    db: store::Store,
    header_cache: Arc<RwLock<LruCache<Hash, BlockHeader>>>,
    block_input_bitmap_cache: Arc<RwLock<LruCache<Hash, Vec<u8>>>>,
}
```

主要对和“链”相关的元素进行增、删、查。

相关元素：

```
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

## Batch

```
/// An atomic batch in which all changes can be committed all at once or
/// discarded on error.
pub struct Batch<'a> {
    store: &'a ChainStore,
    db: store::Batch<'a>,
}
```



