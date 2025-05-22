---
title: Routing
---

# Routing

vroom routes are path-aware and method-aware.  
You can match paths with parameters, and specify handlers per HTTP method.

## Example

```rust
app.route("/users/:id")
    .get(|_, ctx| async move {
        let id = ctx.param("id").unwrap_or("unknown");
        Ok(Response::html(format!("<p>User: {id}</p>")))
    })
    .register();
```

## HTTP Methods

```rust
app.route("/posts")
    .get(|_, ctx| async move { /* GET /posts */ })
    .post(|_, ctx| async move { /* POST /posts */ })
    .put(|_, ctx| async move { /* PUT /posts */ })
    .delete(|_, ctx| async move { /* DELETE /posts */ })
    .register();
```

## Params

Path params (e.g. `:id`) are available in `ctx.param("id")`.

---

[← Hello World](01-hello-world.md) | [Next: Middleware](03-middleware.md)