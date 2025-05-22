---
title: Core Components
---

# Core Components

vroom is organized around several clear concepts.  
Below is an overview of each, with usage snippets.

---

## Routing

Explicit path/method matching, REST-style.

```rust
app.route("/users/:id")
    .get(|_, ctx| async move { /* ... */ })
    .post(|_, ctx| async move { /* ... */ })
    .register();
```
- Named parameters (e.g. `:id`) auto-populate `ctx.param("id")`.

---

## Middleware

Middleware can intercept **before** and/or **after** a handler.

```rust
struct Logger;
impl vroom::Middleware for Logger {
    fn before(&self, req, ctx) -> Result<Option<Response>, vroom::BoxError> {
        println!("Request from {}", ctx.remote_addr);
        Ok(None) // continue
    }
    fn after(&self, method, uri, ctx, res) {
        println!("Responded with {}", res.status);
    }
}
app.use_middleware(Logger);
```
- Register global (`use_middleware`) or per-route (`.middleware()`).

---

## Static Files

Serve entire directories securely.

```rust
app.static_dir("/static", "public");
```
- `/static/app.js` → `public/app.js`
- Directory traversal (e.g. `/static/../../etc/passwd`) is blocked.

---

## Multipart Forms

Async file uploads, zero-copy RAM.

```rust
if let Some(mut mp) = vroom::get_multipart(&mut req).await? {
    while let Some(field) = mp.next_field().await? {
        // field.name(), field.file_name(), field.bytes().await, etc.
    }
}
```
- Handles big uploads with no memory spike.

---

## Templates

MiniJinja for rendering dynamic HTML.

```rust
let html = template!("user.html", &minijinja::context!{ name => "Alice" }, ctx);
Ok(Response::html(html))
```

---

## Sessions & Cookies

Secure, convenient state.

```rust
let sid = ctx.session_id();
let username = ctx.session("username");
res.set_session(new_session_data);
res.set_cookie(Cookie::new("foo", "bar").http_only().secure());
```
- Session store is in-memory by default.

---

## Compression

Automatic gzip, brotli, or deflate via middleware.

```rust
res.compress_gzip();
res.compress_brotli();
```

---

## Streaming

RAM-safe, seekable file or video endpoints.

```rust
vroom::stream_file_range(&req, "video.mp4", "video/mp4").await
```
- Accepts HTTP range headers for video scrubbing.

---

[← Home](index.md)