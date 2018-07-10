## ~~rocksdb~~

RocksDB is an embeddable persistent key-value store for fast storage.

The RocksDB library provides a persistent key value store. Keys and values are arbitrary byte arrays. The keys are ordered within the key value store according to a user-specified comparator function.

Rust wrapper for Facebook's RocksDB embeddable database.

```rust
use rocksdb::{DBCompactionStyle, DBIterator, Direction, IteratorMode, WriteBatch, DB};
```

## Roaring Bitmap

Bitmap 索引在数据库和搜索引擎里使用的很广泛。

## LMDB

Storage of core types using LMDB.



