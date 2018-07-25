## 如何计算出\(非挖矿\)下一难度值？

```
/// The difficulty is defined as the maximum target divided by the block hash.
#[derive(Debug, Clone, Copy, PartialEq, PartialOrd, Eq, Ord)]
pub struct Difficulty {
	num: u64,
}
```

难度调整

```
difficulty = (diff_sum / DIFFICULTY_ADJUST_WINDOW) * BLOCK_TIME_WINDOW / adj_ts
```

相关概念：证明 Proof



