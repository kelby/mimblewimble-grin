## PoolToChainAdapter

```rust
/// Implements the view of the blockchain required by the TransactionPool to
/// operate. Mostly needed to break any direct lifecycle or implementation
/// dependency between the pool and the chain.
pub struct PoolToChainAdapter {
    chain: OneTime<Weak<chain::Chain>>,
}
```



