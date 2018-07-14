## LMDBBackend

```
pub struct LMDBBackend<C, K> {
    db: store::Store,
    config: WalletConfig,
    /// passphrase: TODO better ways of dealing with this other than storing
    passphrase: String,
    /// Keychain
    keychain: Option<K>,
    /// client
    client: C,
}
```

C 可以是 WalletClient

K 可以是 Keychain

存储数据：

```
const OUTPUT_PREFIX: u8 = 'o' as u8;
const DERIV_PREFIX: u8 = 'd' as u8;
const CONFIRMED_HEIGHT_PREFIX: u8 = 'c' as u8;
```

## Batch

```
/// An atomic batch in which all changes can be committed all at once or
/// discarded on error.
pub struct Batch<'a, C: 'a, K: 'a>
where
    C: WalletClient,
    K: Keychain,
{
    store: &'a LMDBBackend<C, K>,
    db: RefCell<Option<store::Batch<'a>>>,
}
```



