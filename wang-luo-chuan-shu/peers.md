## Peers

```rust
pub struct Peers {
    pub adapter: Arc<ChainAdapter>,
    store: PeerStore,
    peers: RwLock<HashMap<SocketAddr, Arc<RwLock<Peer>>>>,
    dandelion_relay: RwLock<HashMap<i64, Arc<RwLock<Peer>>>>,
}
```

主要工作由封装的 store、peers, 以及 adapter 完成。

两部分工作：

peers 网络（核心工作）

store 存储（网络配置等需要存储起来）

adapter 区块链（核心业务）



