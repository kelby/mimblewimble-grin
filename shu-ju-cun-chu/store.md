PMMRHandle

```rust
struct PMMRHandle<T>
where
    T: PMMRable,
{
    backend: PMMRBackend<T>,
    last_pos: u64,
}
```



