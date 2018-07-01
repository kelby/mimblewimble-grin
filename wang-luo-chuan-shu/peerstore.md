## PeerStore

所用数据库。

```rust
/// Storage facility for peer data.
pub struct PeerStore {
    db: grin_store::Store,
}
```

#### PeerData

被存储数据：peer

```rust
/// Data stored for any given peer we've encountered.
#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct PeerData {
    /// Network address of the peer.
    pub addr: SocketAddr,
    /// What capabilities the peer advertises. Unknown until a successful
    /// connection.
    pub capabilities: Capabilities,
    /// The peer user agent.
    pub user_agent: String,
    /// State the peer has been detected with.
    pub flags: State,
    /// The time the peer was last banned
    pub last_banned: i64,
    /// The reason for the ban
    pub ban_reason: ReasonForBan,
}
```



