OutputData

```
/// Information about an output that's being tracked by the wallet. Must be
/// enough to reconstruct the commitment associated with the ouput when the
/// root private key is known.

#[derive(Serialize, Deserialize, Debug, Clone, PartialEq, PartialOrd, Eq, Ord)]
pub struct OutputData {
	/// Root key_id that the key for this output is derived from
	pub root_key_id: Identifier,
	/// Derived key for this output
	pub key_id: Identifier,
	/// How many derivations down from the root key
	pub n_child: u32,
	/// Value of the output, necessary to rebuild the commitment
	pub value: u64,
	/// Current status of the output
	pub status: OutputStatus,
	/// Height of the output
	pub height: u64,
	/// Height we are locked until
	pub lock_height: u64,
	/// Is this a coinbase output? Is it subject to coinbase locktime?
	pub is_coinbase: bool,
	/// Optional corresponding internal entry in tx entry log
	pub tx_log_entry: Option<u32>,
}
```

BlockIdentifier

```
/// Block Identifier
#[derive(Debug, Clone, PartialEq, PartialOrd, Eq, Ord)]
pub struct BlockIdentifier(pub Hash);
```

BlockFees

```
/// Fees in block to use for coinbase amount calculation
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct BlockFees {
	/// fees
	pub fees: u64,
	/// height
	pub height: u64,
	/// key id
	pub key_id: Option<Identifier>,
}
```

CbData

```
/// Response to build a coinbase output.
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct CbData {
	/// Output
	pub output: String,
	/// Kernel
	pub kernel: String,
	/// Key Id
	pub key_id: String,
}
```

WalletInfo

```
/// a contained wallet info struct, so automated tests can parse wallet info
/// can add more fields here over time as needed
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct WalletInfo {
	/// height from which info was taken
	pub last_confirmed_height: u64,
	/// total amount in the wallet
	pub total: u64,
	/// amount awaiting confirmation
	pub amount_awaiting_confirmation: u64,
	/// coinbases waiting for lock height
	pub amount_immature: u64,
	/// amount currently spendable
	pub amount_currently_spendable: u64,
	/// amount locked via previous transactions
	pub amount_locked: u64,
}
```

WalletDetails

```
/// Separate data for a wallet, containing fields
/// that are needed but not necessarily represented
/// via simple rows of OutputData
/// If a wallet is restored from seed this is obvious
/// lost and re-populated as well as possible
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct WalletDetails {
	/// The last block height at which the wallet data
	/// was confirmed against a node
	pub last_confirmed_height: u64,
	/// The last child index used
	pub last_child_index: u32,
}
```

TxLogEntry

```
/// Optional transaction information, recorded when an event happens
/// to add or remove funds from a wallet. One Transaction log entry
/// maps to one or many outputs
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct TxLogEntry {
	/// Local id for this transaction (distinct from a slate transaction id)
	pub id: u32,
	/// Slate transaction this entry is associated with, if any
	pub tx_slate_id: Option<Uuid>,
	/// Transaction type (as above)
	pub tx_type: TxLogEntryType,
	/// Time this tx entry was created
	/// #[serde(with = "tx_date_format")]
	pub creation_ts: DateTime<Utc>,
	/// Time this tx was confirmed (by this wallet)
	/// #[serde(default, with = "opt_tx_date_format")]
	pub confirmation_ts: Option<DateTime<Utc>>,
	/// Whether the inputs+outputs involved in this transaction have been
	/// confirmed (In all cases either all outputs involved in a tx should be
	/// confirmed, or none should be; otherwise there's a deeper problem)
	pub confirmed: bool,
	/// number of inputs involved in TX
	pub num_inputs: usize,
	/// number of outputs involved in TX
	pub num_outputs: usize,
	/// Amount credited via this transaction
	pub amount_credited: u64,
	/// Amount debited via this transaction
	pub amount_debited: u64,
	/// Fee
	pub fee: Option<u64>,
}
```

TxWrapper

```
/// Dummy wrapper for the hex-encoded serialized transaction.
#[derive(Serialize, Deserialize)]
pub struct TxWrapper {
	/// hex representation of transaction
	pub tx_hex: String,
}
```

SendTXArgs

```
/// Send TX API Args
#[derive(Clone, Serialize, Deserialize)]
pub struct SendTXArgs {
	/// amount to send
	pub amount: u64,
	/// minimum confirmations
	pub minimum_confirmations: u64,
	/// destination url
	pub dest: String,
	/// Max number of outputs
	pub max_outputs: usize,
	/// whether to use all outputs (combine)
	pub selection_strategy_is_use_all: bool,
	/// dandelion control
	pub fluff: bool,
}
```



