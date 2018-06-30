## 链的基本信息

```rust
/// The tip of a fork. A handle to the fork ancestry from its leaf in the
/// blockchain tree. References the max height and the latest and previous
/// blocks
/// for convenience and the total difficulty.
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Tip {
    /// Height of the tip (max height of the fork)
    pub height: u64,
    /// Last block pushed to the fork
    pub last_block_h: Hash,
    /// Block previous to last
    pub prev_block_h: Hash,
    /// Total difficulty accumulated on that fork
    pub total_difficulty: Difficulty,
}
```

数据可以完全从 BlockHeader 复制而来。



