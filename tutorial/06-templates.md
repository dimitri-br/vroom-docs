---
title: Templates (MiniJinja)
---

# Templates (MiniJinja)

Use MiniJinja for rendering dynamic HTML.

## Render a Template

```rust
let html = template!("hello.html", &minijinja::context!{ name => "Alice" }, ctx);
Ok(Response::html(html))
```

## Context

Use a Rust struct, HashMap, or `minijinja::context!` macro for your context.

---

[← Multipart](05-multipart.md) | [Next: Sessions & Cookies](07-sessions-cookies.md)