## Peer

```rust
pub struct Peer {
    pub info: PeerInfo,
    state: Arc<RwLock<State>>,
    // set of all hashes known to this peer (so no need to send)
    tracking_adapter: TrackingAdapter,
    connection: Option<conn::Tracker>,
}
```

#### TrackingAdapter

```rust
/// Adapter implementation that forwards everything to an underlying adapter
/// but keeps track of the block and transaction hashes that were received.
#[derive(Clone)]
struct TrackingAdapter {
    adapter: Arc<NetAdapter>,
    known: Arc<RwLock<Vec<Hash>>>,
}
```

#### PeerInfo

```rust
/// General information about a connected peer that's useful to other modules.
#[derive(Clone, Debug, Serialize, Deserialize)]
pub struct PeerInfo {
	pub capabilities: Capabilities,
	pub user_agent: String,
	pub version: u32,
	pub addr: SocketAddr,
	pub total_difficulty: Difficulty,
	pub height: u64,
	pub direction: Direction,
}
```



