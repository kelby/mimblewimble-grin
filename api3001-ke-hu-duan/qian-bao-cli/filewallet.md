```
/// Wallet information tracking all our outputs. Based on HD derivation and
/// avoids storing any key data, only storing output amounts and child index.
#[derive(Debug, Clone)]
pub struct FileWallet<C, K> {
	/// Keychain
	pub keychain: Option<K>,
	/// Client implementation
	pub client: C,
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



