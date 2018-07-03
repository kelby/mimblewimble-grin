## StratumServer

矿池挖矿模式。

```rust
// Grin Stratum Server

pub struct StratumServer {
    id: String,
    config: StratumServerConfig,
    chain: Arc<chain::Chain>,
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    current_block: Block,
    current_difficulty: u64,
    minimum_share_difficulty: u64,
    current_key_id: Option<keychain::Identifier>,
    workers: Arc<Mutex<Vec<Worker>>>,
    currently_syncing: Arc<AtomicBool>,
}
```

#### Worker

```rust
// Worker Object - a connected stratum client - a miner, pool, proxy, etc...

pub struct Worker {
    id: String,
    agent: String,
    login: Option<String>,
    stream: BufStream<TcpStream>,
    error: bool,
    authenticated: bool,
}
```

```rust
use common::adapters::PoolToChainAdapter;
use common::stats::{StratumStats, WorkerStats};
use common::types::StratumServerConfig;
```



