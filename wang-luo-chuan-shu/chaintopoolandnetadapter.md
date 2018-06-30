## ChainToPoolAndNetAdapter

```rust
/// Implementation of the ChainAdapter for the network. Gets notified when the
/// blockchain accepted a new block, asking the pool to update its state and
/// the network to broadcast the block
pub struct ChainToPoolAndNetAdapter {
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    peers: OneTime<Weak<p2p::Peers>>,
}
```



