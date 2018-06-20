当前一个“证明”（Proof）超过1w多字符，按一字节等于两字符计算，约5k大小。

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



