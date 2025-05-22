---
title: Hello World
---

# Hello, world!

Let’s get your first vroom app running.

## 1. Install dependencies

Add to your `Cargo.toml`:

```toml
vroom = { git = "https://github.com/yourname/vroom" }
tokio = { version = "1", features = ["full"] }
```

## 2. Write your app

```rust
use vroom::{App, Response};
#[tokio::main]
async fn main() -> Result<(), vroom::BoxError> {
    let mut app = App::new("templates");
    app.route("/")
        .get(|_, ctx| async move {
            Ok(Response::html("<h1>Hello, vroom!</h1>"))
        })
        .register();
    app.run("0.0.0.0:8443", "cert.pem", "key.pem").await
}
```

## 3. Run

```bash
cargo run
```

Visit [https://localhost:8443/](https://localhost:8443/) in your browser.

---

[Next: Routing](02-routing.md)