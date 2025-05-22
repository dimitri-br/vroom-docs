---
title: Middleware
---

# Middleware

Middleware can run code before or after every request.

## Global Middleware

```rust
struct Logger;
impl vroom::Middleware for Logger {
    fn before(&self, req, ctx) -> Result<Option<Response>, vroom::BoxError> {
        println!("Request: {} {}", req.method(), req.uri().path());
        Ok(None)
    }
    fn after(&self, method, uri, ctx, res) {
        println!("Response: {} {}", method, res.status);
    }
}
app.use_middleware(Logger);
```

## Per-route Middleware

```rust
app.route("/secure")
    .get(|_, ctx| async move { /* ... */ })
    .middleware(Logger)
    .register();
```

---

[← Routing](02-routing.md) | [Next: Static Files](04-static-files.md)