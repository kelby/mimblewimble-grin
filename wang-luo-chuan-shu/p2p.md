## TcpStream

std::net::TcpStream

Peer-to-peer protocol that can handle transaction merging

```rust
/// A message as received by the connection. Provides access to the message
/// header lazily consumes the message body, handling its deserialization.
pub struct Message<'a> {
	pub header: MsgHeader,
	conn: &'a mut TcpStream,
}
```

```rust
/// Response to a `Message`
pub struct Response<'a> {
	resp_type: Type,
	body: Vec<u8>,
	conn: &'a mut TcpStream,
	attachment: Option<File>,
}
```



