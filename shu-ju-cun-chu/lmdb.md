## Store

//! Storage of core types using LMDB.

```
/// LMDB-backed store facilitating data access and serialization. All writes
/// are done through a Batch abstraction providing atomicity.
pub struct Store {
	env: Arc<lmdb::Environment>,
	db: Arc<lmdb::Database<'static>>,
}
```



