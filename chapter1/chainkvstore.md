## ~~ChainKVStore~~



#### Store

```rust
/// Thread-safe rocksdb wrapper
pub struct Store {
    rdb: RwLock<DB>,
}
```

> 这里的 DB 来源于 rocksdb



