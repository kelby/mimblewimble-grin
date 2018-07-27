#### 相关方法

receive\_tx

create\_send\_tx

complete\_tx

cancel\_tx

issue\_burn\_tx

#### selection

build\_send\_tx\_slate

build\_recipient\_output\_with\_slate

select\_send\_tx

inputs\_and\_change

select\_coins

#### sigcontext

```
/// Holds the context for a single aggsig transaction
pub struct Context {
	/// Secret key (of which public is shared)
	pub sec_key: SecretKey,
	/// Secret nonce (of which public is shared)
	/// (basically a SecretKey)
	pub sec_nonce: SecretKey,
	/// store my outputs between invocations
	pub output_ids: Vec<Identifier>,
	/// store my inputs
	pub input_ids: Vec<Identifier>,
	/// store the calculated fee
	pub fee: u64,
}
```

#### updater

retrieve\_outputs

retrieve\_txs

refresh\_outputs

map\_wallet\_outputs

cancel\_tx\_and\_outputs

apply\_api\_outputs

retrieve\_info

build\_coinbase

receive\_coinbase

#### keys

next\_available\_key

retrieve\_existing\_key



