An implementation of the ChainStore trait backed by a simple key-value store.

## grin\_chain store

业务封装，与具体数据库无关，相当于 ORM

The full state of a Grin chain consists of all the following data:

1. The full unspent output \(UTXO\) set.
2. The range proof for each output.
3. All the transaction kernels.
4. A MMR for each of the above \(with the exception that the output MMR includes hashes for \_all \_outputs, not only the unspent ones\).

## Rust wrapper for CRoaring

A better compressed bitset

Roaring bitmaps are compressed bitmaps. They can be hundreds of times faster.

带有完全支持编译器\( GNU，llvm，Visual Studio \)的\( 还有 C++ \) 中的便携式Roaring位图。

Bitsets，也称为位图，通常用作快速数据结构。

## rust wrapper for rocksdb

具体使用数据库。

RocksDB is an embeddable persistent key-value store for fast storage.



