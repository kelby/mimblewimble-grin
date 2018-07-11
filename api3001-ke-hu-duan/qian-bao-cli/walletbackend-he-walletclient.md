## WalletBackend

```
/// Wallets should implement this backend for their storage. All functions
/// here expect that the wallet instance has instantiated itself or stored
/// whatever credentials it needs
```

## WalletClient

```
/// Encapsulate all communication functions. No functions within libwallet
/// should care about communication details
```

## controller

#### OwnerAPIGetHandler

```
/// API Handler/Wrapper for owner functions

pub struct OwnerAPIGetHandler<T: ?Sized, C, K>
where
	T: WalletBackend<C, K>,
	C: WalletClient,
	K: Keychain,
{
	/// Wallet instance
	pub wallet: Arc<Mutex<Box<T>>>,
	phantom: PhantomData<K>,
	phantom_c: PhantomData<C>,
}
```

#### OwnerAPIPostHandler

```
/// Handles all owner API POST requests
pub struct OwnerAPIPostHandler<T: ?Sized, C, K>
where
	T: WalletBackend<C, K>,
	C: WalletClient,
	K: Keychain,
{
	/// Wallet instance
	pub wallet: Arc<Mutex<Box<T>>>,
	phantom: PhantomData<K>,
	phantom_c: PhantomData<C>,
}
```

#### OwnerAPIOptionsHandler

```
/// Options handler
pub struct OwnerAPIOptionsHandler {}
```

#### ForeignAPIHandler

```
/// API Handler/Wrapper for foreign functions

pub struct ForeignAPIHandler<T: ?Sized, C, K>
where
	T: WalletBackend<C, K>,
	C: WalletClient,
	K: Keychain,
{
	/// Wallet instance
	pub wallet: Arc<Mutex<Box<T>>>,
	phantom: PhantomData<K>,
	phantom_c: PhantomData<C>,
}
```



