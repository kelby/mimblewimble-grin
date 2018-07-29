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

new

```
/// Create a new context with defaults
```

add\_output

```
	/// Tracks an output contributing to my excess value (if it needs to
	/// be kept between invocations
```

get\_outputs

```
/// Returns all stored outputs
```

add\_input

```
	/// Tracks IDs of my inputs into the transaction
	/// be kept between invocations
```

get\_inputs

```
/// Returns all stored input identifiers
```

get\_private\_keys

```
/// Returns private key, private nonce
```

get\_public\_keys

```
/// Returns public key, public nonce
```



