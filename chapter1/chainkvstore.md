## ChainKVStore

```rust
/// An implementation of the ChainStore trait backed by a simple key-value
/// store.
pub struct ChainKVStore {
	db: grin_store::Store,
	header_cache: Arc<RwLock<LruCache<Hash, BlockHeader>>>,
	block_input_bitmap_cache: Arc<RwLock<LruCache<Hash, Vec<u8>>>>,
}
```

#### Store

```rust
/// Thread-safe rocksdb wrapper
pub struct Store {
	rdb: RwLock<DB>,
}
```

> 这里的 DB 来源于 rocksdb





