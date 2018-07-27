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

add\_output

get\_outputs

add\_input

get\_inputs

get\_private\_keys

get\_public\_keys

