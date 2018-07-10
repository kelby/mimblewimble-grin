```
/// All chain-related database operations
pub struct ChainStore {
	db: store::Store,
	header_cache: Arc<RwLock<LruCache<Hash, BlockHeader>>>,
	block_input_bitmap_cache: Arc<RwLock<LruCache<Hash, Vec<u8>>>>,
}
```

```
/// An atomic batch in which all changes can be committed all at once or
/// discarded on error.
pub struct Batch<'a> {
	store: &'a ChainStore,
	db: store::Batch<'a>,
}
```



