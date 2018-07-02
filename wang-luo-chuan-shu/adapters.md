P2P网络传输与区块链核心业务之间产生联系的枢纽。

## ChainToPoolAndNetAdapter

```rust
/// Implementation of the ChainAdapter for the network. Gets notified when the
/// blockchain accepted a new block, asking the pool to update its state and
/// the network to broadcast the block
pub struct ChainToPoolAndNetAdapter {
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    peers: OneTime<Weak<p2p::Peers>>,
}
```

## PoolToNetAdapter

```rust
/// Adapter between the transaction pool and the network, to relay
/// transactions that have been accepted.
pub struct PoolToNetAdapter {
    peers: OneTime<Weak<p2p::Peers>>,
}
```

## PoolToChainAdapter

```rust
/// Implements the view of the blockchain required by the TransactionPool to
/// operate. Mostly needed to break any direct lifecycle or implementation
/// dependency between the pool and the chain.
pub struct PoolToChainAdapter {
    chain: OneTime<Weak<chain::Chain>>,
}
```

## NetToChainAdapter

```rust
/// Implementation of the NetAdapter for the blockchain. Gets notified when new
/// blocks and transactions are received and forwards to the chain and pool
/// implementations.
pub struct NetToChainAdapter {
    currently_syncing: Arc<AtomicBool>,
    archive_mode: bool,
    chain: Weak<chain::Chain>,
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    peers: OneTime<Weak<p2p::Peers>>,
    config: ServerConfig,
}
```



