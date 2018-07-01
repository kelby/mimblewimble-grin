## Server

```rust
/// P2P server implementation, handling bootstrapping to find and connect to
/// peers, receiving connections from other peers and keep track of all of them.
pub struct Server {
    pub config: P2PConfig,
    capabilities: Capabilities,
    handshake: Arc<Handshake>,
    pub peers: Arc<Peers>,
    stop: Arc<AtomicBool>,
}
```

#### Server &gt; Peers &gt; Peer

#### Handshake

```rust
/// Handles the handshake negotiation when two peers connect and decides on
/// protocol.
pub struct Handshake {
	/// Ring buffer of nonces sent to detect self connections without requiring
	/// a node id.
	nonces: Arc<RwLock<VecDeque<u64>>>,
	/// The genesis block header of the chain seen by this node.
	/// We only want to connect to other nodes seeing the same chain (forks are
	/// ok).
	genesis: Hash,
	config: P2PConfig,
}
```



