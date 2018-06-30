## Peers

```rust
pub struct Peers {
	pub adapter: Arc<ChainAdapter>,
	store: PeerStore,
	peers: RwLock<HashMap<SocketAddr, Arc<RwLock<Peer>>>>,
	dandelion_relay: RwLock<HashMap<i64, Arc<RwLock<Peer>>>>,
}
```



