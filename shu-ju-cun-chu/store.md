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

## LeafSet

```rust
/// Compact (roaring) bitmap representing the set of positions of
/// leaves that are currently unpruned in the MMR.
pub struct LeafSet {
	path: String,
	bitmap: Bitmap,
	bitmap_bak: Bitmap,
}
```

## PMMRBackend



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
	hash_file: AppendOnlyFile,
	data_file: AppendOnlyFile,
	leaf_set: LeafSet,
	prune_list: PruneList,
	_marker: marker::PhantomData<T>,
}
```

## PruneList

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

## RemoveLog

```rust
/// Log file fully cached in memory containing all positions that should be
/// eventually removed from the MMR append-only data file. Allows quick
/// checking of whether a piece of data has been marked for deletion. When the
/// log becomes too long, the MMR backend will actually remove chunks from the
/// MMR data file and truncate the remove log.
pub struct RemoveLog {
	path: String,
	/// Ordered vector of MMR positions that should get eventually removed.
	pub removed: Vec<(u64, u32)>,
	// Holds positions temporarily until flush is called.
	removed_tmp: Vec<(u64, u32)>,
	// Holds truncated removed temporarily until discarded or committed
	removed_bak: Vec<(u64, u32)>,
}
```

## AppendOnlyFile

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





