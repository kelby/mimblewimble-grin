“交易池”最终要关联到“交易”

## TransactionPool &gt; Pool &gt; PoolEntry &gt; Transaction

元数据+其它关联对象

#### TransactionPool

包含两种“池子”\(txpool 和 stempool，结构是一样的，作用略有不同\)

作用主要是管理它们

```rust
/// Transaction pool implementation.
pub struct TransactionPool<T> {
	/// Pool Config
	pub config: PoolConfig,

	/// Our transaction pool.
	pub txpool: Pool<T>,
	/// Our Dandelion "stempool".
	pub stempool: Pool<T>,

	/// The blockchain
	pub blockchain: Arc<T>,
	/// The pool adapter
	pub adapter: Arc<PoolAdapter>,
}
```

#### Pool

主要包含“池子实例”\(PoolEntry\)

作用主要是管理它们

```rust
pub struct Pool<T> {
	/// Entries in the pool (tx + info + timer) in simple insertion order.
	pub entries: Vec<PoolEntry>,
	/// The blockchain
	pub blockchain: Arc<T>,
	pub name: String,
}
```

#### PoolEntry

除了自身一些数据外，主要是关联着“交易”

它是被管理者

