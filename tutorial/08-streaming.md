---
title: Streaming Files & Video
---

# Streaming Files & Video

Stream large files (audio, video) efficiently and safely.

## Range Requests

Use `stream_file_range` to serve files supporting HTTP range headers:

```rust
app.route("/video/:file")
    .get(|req, ctx| async move {
        let fname = ctx.param("file").unwrap_or("demo.mp4");
        let path = format!("videos/{fname}");
        vroom::stream_file_range(&req, &path, "video/mp4").await
    })
    .register();
```

*Clients can scrub or seek without re-downloading the entire file.*

---

[← Sessions](07-sessions-cookies.md)