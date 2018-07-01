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

#### P2PConfig

```rust
/// Configuration for the peer-to-peer server.
#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct P2PConfig {
	pub host: IpAddr,
	pub port: u16,

	pub peers_allow: Option<Vec<String>>,

	pub peers_deny: Option<Vec<String>>,

	pub ban_window: Option<i64>,

	pub peer_max_count: Option<u32>,

	pub peer_min_preferred_count: Option<u32>,
}
```

#### msg

MsgHeader

Hand

Shake

GetPeerAddrs

PeerAddrs

PeerError

SockAddr

Locator

Headers

Ping

Pong

BanReason

TxHashSetRequest

TxHashSetArchive

