**公钥签名 -&gt; 公钥验证**

3个步骤：

1. Setup
2. Commit
3. Open

示例：

```
example :: IO Bool
example = do
  -- Setup commitment parameters
  (a, cp) <- setup 256

  -- Commit to the message using paramaters: Com(msg, cp)
  let msg = 0xCAFEBEEF
  Pedersen c r <- commit msg cp

  -- Open and verify commitment: Open(cp,c,r)
  pure (open cp c r)
```

符合结合律：

```
Commit(m0; r0) * Commit(m1; r1) = Commit(m0 + m1; r0 + r1)
```

椭圆曲线版本：

```
example :: IO Bool
example = do
  -- Setup commitment parameters
  (a, cp) <- ecSetup Nothing -- SECP256k1 is used by default

  -- Commit to the message using paramaters: Com(msg, cp)
  let msg = 0xCAFEBEEF
  ECPedersen c r <- ecCommit msg cp

  -- Open and verify commitment: Open(cp,c,r)
  pure (ecOpen cp c r)
```

仍然满足结合律：

```
Commit(x, r1) + Commit(y, r2) = Commit(x + y, r1 + r2)
```

向量操作：

```
Commit(x,r) + n = Commit(x + n,r)
```



