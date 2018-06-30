```rust
pub struct Peer {
	pub info: PeerInfo,
	state: Arc<RwLock<State>>,
	// set of all hashes known to this peer (so no need to send)
	tracking_adapter: TrackingAdapter,
	connection: Option<conn::Tracker>,
}
```



