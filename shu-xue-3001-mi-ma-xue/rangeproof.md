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



