```
//! Aggsig helper functions used in transaction creation.. should be only
```

```
//! interface into the underlying secp library
```

create\_secnonce

```
/// exports a secure nonce guaranteed to be usable
/// in aggsig creation
```

calculate\_partial\_sig

```
/// Calculate a partial sig
```

verify\_partial\_sig

```
/// Verifies a partial sig given all public nonces used in the round
```

sign\_from\_key\_id

```
/// Just a simple sig, creates its own nonce, etc
```

verify\_single\_from\_commit

```
/// Verifies a sig given a commitment
```

verify\_sig\_build\_msg

```
/// Verify a sig, with built message
```

verify\_single

```
/// Verifies an aggsig signature
```

add\_signatures

```
/// Adds signatures
```

sign\_with\_blinding

```
/// Just a simple sig, creates its own nonce, etc
```



