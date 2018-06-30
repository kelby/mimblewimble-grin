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



