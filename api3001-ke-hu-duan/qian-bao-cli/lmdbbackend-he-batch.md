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



