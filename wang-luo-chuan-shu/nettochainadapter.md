## NetToChainAdapter

```rust
/// Implementation of the NetAdapter for the blockchain. Gets notified when new
/// blocks and transactions are received and forwards to the chain and pool
/// implementations.
pub struct NetToChainAdapter {
	currently_syncing: Arc<AtomicBool>,
	archive_mode: bool,
	chain: Weak<chain::Chain>,
	tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
	peers: OneTime<Weak<p2p::Peers>>,
	config: ServerConfig,
}
```



