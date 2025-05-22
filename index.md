---
title: vroom — Minimalist HTTP/2 Web Framework for Rust
---

![vroom logo](assets/vroom-logo.png)

# vroom

**vroom** is a fast, minimalist async web framework for Rust, focused on performance, security, and clear code.  
- **Modern**: HTTP/2, async/await, TLS-first
- **Simple**: Explicit routing, no "magic"
- **Safe**: RAM-safe streaming and upload
- **Productive**: Templates, sessions, static, multipart

**Why vroom?**

- Outruns most frameworks on static, streaming, and form workloads
- Predictable: you always know what’s happening
- No unnecessary dependencies or bloat

---

## Features

| Feature                | Description                                 |
|------------------------|---------------------------------------------|
| HTTP/2 + TLS           | Modern, secure, and highly concurrent       |
| Routing                | Path, param, and method-based               |
| Middleware             | Global and per-route, before/after hooks    |
| Static Files           | Serve securely, no traversal attacks        |
| Multipart/Form         | Async-safe, RAM-efficient uploads           |
| Templates              | MiniJinja for fast dynamic pages            |
| Sessions & Cookies     | Built-in, secure session management         |
| Compression            | gzip/deflate/brotli out of the box          |
| Streaming              | Serve large files, video, or audio easily   |

---

## Quick Start

```rust
use vroom::{App, Response};
#[tokio::main]
async fn main() -> Result<(), vroom::BoxError> {
    let mut app = App::new("templates");
    app.route("/")
        .get(|_, ctx| async move {
            Ok(Response::html("<h1>Hello, world!</h1>"))
        })
        .register();
    app.run("0.0.0.0:8443", "cert.pem", "key.pem").await
}
```

*See [Tutorials](tutorial/01-hello-world.md) for more!*

---

## 📚 Docs

- [Architecture](architecture.md)
- [Components](components.md)
- [Tutorials](tutorial/01-hello-world.md)

---