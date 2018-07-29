slate 是被管理“交易”的封装，下面几个方法主要围绕它进行；

updater 更新管理中心，与外部通讯，进行事件处理；

selection 选择器，选择合适的交易、输入、转出。

#### 相关方法

receive\_tx

```
/// Receive a transaction, modifying the slate accordingly (which can then be
/// sent back to sender for posting)
```

create\_send\_tx

```
/// Issue a new transaction to the provided sender by spending some of our
/// wallet
```

complete\_tx

```
/// Complete a transaction as the sender
```

cancel\_tx

```
/// Rollback outputs associated with a transaction in the wallet
```

issue\_burn\_tx

```
/// Issue a burn tx
```



