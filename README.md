# async-tls
[![license](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/async-std/async-tls/blob/master/LICENSE-MIT)
[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/async-std/async-tls/blob/master/LICENSE-APACHE)
[![docs.rs](https://docs.rs/async-tls/badge.svg)](https://docs.rs/async-tls/)

Asynchronous TLS/SSL streams using [Rustls](https://github.com/ctz/rustls).

### Simple Client

```rust
use async_tls::TlsConnector;
use async_std::net::TcpStream;

// ...

let tcp_stream = TcpStream::connect("rust-lang.org:443").await?;
let connector = TlsConnector::default();
let handshake = connector::connect("www.rust-lang.org", tcp_stream)?;
let mut tls_stream = handshake.await?;

// ...
```

### Client Example Program

See [examples/client](examples/client/src/main.rs). You can run it with:

```sh
cd examples/client
cargo run -- hsts.badssl.com
```

### Server Example Program

See [examples/server](examples/server/src/main.rs). You can run it with:

```sh
cd examples/server
cargo run -- 127.0.0.1:8080 --cert ../../tests/end.cert --key ../../tests/end.rsa 
```

and point the client at it with:

```sh
cd examples/client
cargo run -- 127.0.0.1 --port 8080 --domain localhost --cafile ../../tests/end.chain
```

**NOTE**: Don't ever use those certificate files anywhere but for testing!

## Safety

This crate uses ``#![deny(unsafe_code)]`` to ensure everything is implemented in
100% Safe Rust.

### License & Origin

This project is licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or
   http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or
   http://opensource.org/licenses/MIT)

at your option.

This started as a fork of [tokio-rustls](https://github.com/quininer/tokio-rustls).

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in async-tls by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
