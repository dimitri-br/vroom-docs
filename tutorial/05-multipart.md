---
title: Multipart Forms & File Uploads
---

# Multipart Forms & File Uploads

vroom supports safe, async multipart form parsing via `multer`.

## Example

```rust
app.route("/upload")
    .post(|mut req, ctx| async move {
        if let Some(mut mp) = vroom::get_multipart(&mut req).await? {
            while let Some(field) = mp.next_field().await? {
                let name = field.name().unwrap_or("unnamed");
                let filename = field.file_name().unwrap_or("file.bin");
                let bytes = field.bytes().await?;
                // Save to disk, validate, etc.
            }
        }
        Ok(Response::html("Done!"))
    })
    .register();
```

*Multipart uploads are streamed to RAM/disk, so you can handle huge files.*

---

[← Static Files](04-static-files.md) | [Next: Templates](06-templates.md)