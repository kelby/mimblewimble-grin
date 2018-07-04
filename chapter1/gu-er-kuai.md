## OrphanBlockPool &gt; Orphan &gt; 块

孤儿块，也是块。事后确认，也需要添加。

```rust
struct Orphan {
    block: Block,
    opts: Options,
    added: Instant,
}

struct OrphanBlockPool {
    // blocks indexed by their hash
    orphans: RwLock<HashMap<Hash, Orphan>>,
    // additional index of height -> hash
    // so we can efficiently identify a child block (ex-orphan) after processing a block
    height_idx: RwLock<HashMap<u64, Vec<Hash>>>,
}
```

#### 操作

添加

移除

等



