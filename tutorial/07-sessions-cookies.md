---
title: Sessions & Cookies
---

# Sessions & Cookies

Sessions are per-client state, managed with secure cookies.

## Access Session

```rust
let username = ctx.session("username");
```

## Set/Remove Session

```rust
let mut res = Response::html("Welcome!");
let mut session = HashMap::new();
session.insert("username".to_string(), "bob".to_string());
res.set_session(session);
// or
res.destroy_session();
```

## Cookies

```rust
let mut res = Response::html("Cookie set!");
res.set_cookie(Cookie::new("flavor", "mint").http_only().secure());
```

---

[← Templates](06-templates.md) | [Next: Streaming](08-streaming.md)