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

主要工作由它封装的 NetAdapter 完成。

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

#### Protocol

```
pub struct Protocol {
    adapter: Arc<NetAdapter>,
    addr: SocketAddr,
}
```

#### Message

```
/// A message as received by the connection. Provides access to the message
/// header lazily consumes the message body, handling its deserialization.
pub struct Message<'a> {
    pub header: MsgHeader,
    conn: &'a mut TcpStream,
}
```

#### Response

    /// Response to a `Message`
    pub struct Response<'a> {
        resp_type: Type,
        body: Vec<u8>,
        conn: &'a mut TcpStream,
        attachment: Option<File>,
    }

#### Tracker

```
// TODO count sent and received
pub struct Tracker {
	/// Bytes we've sent.
	pub sent_bytes: Arc<Mutex<u64>>,
	/// Bytes we've received.
	pub received_bytes: Arc<Mutex<u64>>,
	/// Channel to allow sending data through the connection
	pub send_channel: mpsc::SyncSender<Vec<u8>>,
	/// Channel to close the connection
	pub close_channel: mpsc::Sender<()>,
	/// Channel to check for errors on the connection
	pub error_channel: mpsc::Receiver<Error>,
}
```



