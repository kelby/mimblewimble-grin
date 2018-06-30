## PoolToNetAdapter

```rust
/// Adapter between the transaction pool and the network, to relay
/// transactions that have been accepted.
pub struct PoolToNetAdapter {
	peers: OneTime<Weak<p2p::Peers>>,
}
```



