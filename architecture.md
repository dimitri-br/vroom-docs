---
title: Architecture
---

# Architecture

## Overview

vroom is designed for **transparency, speed, and reliability**.  
All I/O is async, all endpoints are routed by explicit patterns and HTTP method, and all state (sessions, templates) is managed in clear containers.

## High-Level Flow

```
TLS (rustls) 
   ↓
HTTP/2 (h2)
   ↓
Routing (PathTree)
   ↓
Middleware (global + per-route)
   ↓
Handler
   ↓
Response (headers/body/stream/session/cookies)
```

## Main Components

- **App**: Main entry point, holds all routes, global middleware, templates, config.
- **Routing**: Uses a `PathTree` to match routes and params. All HTTP methods supported, including 405 handling.
- **Middleware**: Any number, global or per-route. Before/after hooks.
- **Response**: Can be full (RAM) or streaming (file/video).
- **Sessions**: Built-in in-memory store, designed for easy swap-out.
- **Static**: Secure file serving, no directory traversal.
- **Multipart**: Async, RAM-safe file uploads.

## TLS, HTTP/2

vroom **requires** TLS.  
It speaks HTTP/2 by default, offering many parallel streams per connection and modern browser support.

## Streaming & RAM Safety

- Large files (e.g. video) are streamed via `tokio::fs::File` and `AsyncRead`, not loaded fully into RAM.
- Multipart upload handler streams to disk/file, RAM never spikes.

## Sessions & Cookies

- Session IDs are cryptographically random, base64-url.
- All session state is per-process, with a simple interface for replacement (e.g. Redis, SQL).
- Cookie helpers are RFC 6265 compliant.

## Security

- Directory traversal is blocked when serving static files.
- TLS/HTTP/2 is always-on.
- Sessions/cookies are Secure/HttpOnly by default.

---

[← Home](index.md)