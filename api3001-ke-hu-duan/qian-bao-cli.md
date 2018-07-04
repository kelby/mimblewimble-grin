Wallet software for Grin

    SUBCOMMANDS:
        burn         ** TESTING ONLY ** Burns the provided amount to a known key. Similar to send but burns an output to
                     allow single-party transactions.
        help         Prints this message or the help of the given subcommand(s)
        info         basic wallet contents summary
        init         Initialize a new wallet seed file.
        listen       Runs the wallet in listening mode waiting for transactions.
        outputs      raw wallet info (list of outputs)
        owner_api    Runs the wallet's local web API.
        receive      Processes a JSON transaction file.
        restore      Attempt to restore wallet contents from the chain using seed and password. NOTE: Backup wallet.*
                     and run `wallet listen` before running restore.
        send         Builds a transaction to send coins and sends it to the specified listener directly.

## FileWallet

```rust
/// Wallet information tracking all our outputs. Based on HD derivation and
/// avoids storing any key data, only storing output amounts and child index.
#[derive(Debug, Clone)]
pub struct FileWallet<K> {
    /// Keychain
    pub keychain: Option<K>,
    /// Configuration
    pub config: WalletConfig,
    /// passphrase: TODO better ways of dealing with this other than storing
    passphrase: String,
    /// List of outputs
    pub outputs: HashMap<String, OutputData>,
    /// Details
    pub details: WalletDetails,
    /// Data file path
    pub data_file_path: String,
    /// Backup file path
    pub backup_file_path: String,
    /// lock file path
    pub lock_file_path: String,
    /// details file path
    pub details_file_path: String,
    /// Details backup file path
    pub details_bak_path: String,
}
```

#### Controller

OwnerAPIGetHandler

```rust
/// API Handler/Wrapper for owner functions

pub struct OwnerAPIGetHandler<T, K>
where
    T: WalletBackend<K>,
    K: Keychain,
{
    /// Wallet instance
    pub wallet: Arc<Mutex<T>>,
    phantom: PhantomData<K>,
}
```

OwnerAPIPostHandler

```rust
pub struct OwnerAPIPostHandler<T, K>
where
    T: WalletBackend<K>,
    K: Keychain,
{
    /// Wallet instance
    pub wallet: Arc<Mutex<T>>,
    phantom: PhantomData<K>,
}
```

OwnerAPIOptionsHandler

```rust
/// Options handler
pub struct OwnerAPIOptionsHandler {}
```

ForeignAPIHandler

```rust
/// API Handler/Wrapper for foreign functions

pub struct ForeignAPIHandler<T, K>
where
    T: WalletBackend<K> + WalletClient,
    K: Keychain,
{
    /// Wallet instance
    pub wallet: Arc<Mutex<T>>,
    phantom: PhantomData<K>,
}
```

#### API

//! Wrappers around library functions, intended to split functions

//! into external and internal APIs \(i.e. functions for the local wallet

//! vs. functions to interact with someone else\)

//! Still experimental, not sure this is the best way to do this

APIOwner

```rust
/// Wrapper around internal API functions, containing a reference to
/// the wallet/keychain that they're acting upon
pub struct APIOwner<'a, W, K>
where
    W: 'a + WalletBackend<K> + WalletClient,
    K: Keychain,
{
    /// Wallet, contains its keychain (TODO: Split these up into 2 traits
    /// perhaps)
    pub wallet: &'a mut W,
    phantom: PhantomData<K>,
}
```

APIForeign

```rust
/// Wrapper around external API functions, intended to communicate
/// with other parties
pub struct APIForeign<'a, W, K>
where
    W: 'a + WalletBackend<K> + WalletClient,
    K: Keychain,
{
    /// Wallet, contains its keychain (TODO: Split these up into 2 traits
    /// perhaps)
    pub wallet: &'a mut W,
    phantom: PhantomData<K>,
}
```

## WalletBackend

/// Wallets should implement this backend for their storage. All functions

/// here expect that the wallet instance has instantiated itself or stored

/// whatever credentials it needs

## WalletClient

/// Encapsulate all communication functions. No functions within libwallet

/// should care about communication details

## client

通过 hyper 提供的接口向服务端发送请求。（直接使用 hyper，或使用 api::client 里的 GET/POST）

//! Client functions, implementations of the WalletClient trait

//! specific to the FileWallet

## TX

aggsig

build

proof

reward

slate

## 关系

FileWallet &gt; WalletBackend/WalletClient &gt; OwnerAPIGetHandler/OwnerAPIPostHandler/OwnerAPIOptionsHandler/ForeignAPIHandler &gt; APIForeign/APIOwner

FileWallet &gt; client

FileWallet &gt; TX

