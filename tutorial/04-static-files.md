---
title: Static Files
---

# Static Files

Serve entire directories with a single call:

```rust
app.static_dir("/static", "public");
```

Now requests to `/static/foo.js` map to `public/foo.js`.

## Directory Traversal

vroom blocks traversal attacks like `/static/../../etc/passwd`.

---

[← Middleware](03-middleware.md) | [Next: Multipart Uploads](05-multipart.md)