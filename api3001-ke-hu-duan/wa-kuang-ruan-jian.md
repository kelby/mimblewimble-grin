## Miner

```rust
pub struct Miner {
    config: StratumServerConfig,
    chain: Arc<chain::Chain>,
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    stop: Arc<AtomicBool>,

    // Just to hold the port we're on, so this miner can be identified
    // while watching debug output
    debug_output_id: String,
}
```





