## PMMRBackend

Implementation of the persistent Backend for the prunable MMR tree.

```rust
/// PMMR persistent backend implementation. Relies on multiple facilities to
/// handle writing, reading and pruning.
///
/// * A main storage file appends Hash instances as they come.
/// This AppendOnlyFile is also backed by a mmap for reads.
/// * An in-memory backend buffers the latest batch of writes to ensure the
/// PMMR can always read recent values even if they haven't been flushed to
/// disk yet.
/// * A leaf_set tracks unpruned (unremoved) leaf positions in the MMR..
/// * A prune_list tracks the positions of pruned (and compacted) roots in the
/// MMR.
pub struct PMMRBackend<T>
where
    T: PMMRable,
{
    data_dir: String,
    hash_file: AppendOnlyFile, // 两个文件之一
    data_file: AppendOnlyFile, // 两个文件之一
    leaf_set: LeafSet, // 未修剪数据
    prune_list: PruneList, // 已修剪数据
    _marker: marker::PhantomData<T>, // 临时存储。（自动操作）
}
```

不仅要实现 core pmmr 给出的 trait Backend，还要实现自身希望提供的功能，可以说任务艰巨。

#### LeafSet

未修剪数据

```rust
/// Compact (roaring) bitmap representing the set of positions of
/// leaves that are currently unpruned in the MMR.
pub struct LeafSet {
    path: String,
    bitmap: Bitmap,
    bitmap_bak: Bitmap,
}
```

#### PruneList

已修剪数据

```rust
/// Maintains a list of previously pruned nodes in PMMR, compacting the list as
/// parents get pruned and allowing checking whether a leaf is pruned. Given
/// a node's position, computes how much it should get shifted given the
/// subtrees that have been pruned before.
///
/// The PruneList is useful when implementing compact backends for a PMMR (for
/// example a single large byte array or a file). As nodes get pruned and
/// removed from the backend to free space, the backend will get more compact
/// but positions of a node within the PMMR will not match positions in the
/// backend storage anymore. The PruneList accounts for that mismatch and does
/// the position translation.
pub struct PruneList {
    path: Option<String>,
    /// Bitmap representing pruned root node positions.
    bitmap: Bitmap,
}
```

#### AppendOnlyFile

文件存储

```rust
/// Wrapper for a file that can be read at any position (random read) but for
/// which writes are append only. Reads are backed by a memory map (mmap(2)),
/// relying on the operating system for fast access and caching. The memory
/// map is reallocated to expand it when new writes are flushed.
///
/// Despite being append-only, the file can still be pruned and truncated. The
/// former simply happens by rewriting it, ignoring some of the data. The
/// latter by truncating the underlying file and re-creating the mmap.
pub struct AppendOnlyFile {
    path: String,
    file: File,
    mmap: Option<memmap::Mmap>,
    buffer_start: usize,
    buffer: Vec<u8>,
    buffer_start_bak: usize,
}
```





