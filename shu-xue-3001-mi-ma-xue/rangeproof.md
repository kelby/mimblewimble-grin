## RangeProof

\# 使用频率次之

```
/// A range proof. Typically much larger in memory that the above (~5k).
#[derive(Copy)]
pub struct RangeProof {
    /// The proof itself, at most 5134 bytes long
    pub proof: [u8; constants::MAX_PROOF_SIZE],
    /// The length of the proof
    pub plen: usize,
}
```

ProofMessage

ProofInfo

当前一个“证明”（Proof）超过1w字符，按一字节等于两字符计算，约5k大小。

范围：

```
// import com.ing.blockchain.zk.dto.*
ClosedRange range = new ClosedRange.of(lower, upper);
```

证明：

```
// import com.ing.blockchain.zk.HPAKErangeProof
RangeProof rangeProof = HPAKErangeProof.calculateRangeProof(ttpMessage, range);
```

校验：

```
HPAKErangeProof.validateRangeProof(rangeProof, ttpMessage.getCommitment(), range);
```

Smaller range proofs? Aggregation of range proofs?

