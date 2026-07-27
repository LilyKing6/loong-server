# loong-server

The standards-track web framework for the [Loong](https://github.com/loong/loong) language.

Built from scratch — no external runtime dependencies except the Loong standard library.

## Packages

| Package | Path | Target | Description |
|---------|------|--------|-------------|
| `loong-web` | `loong-web/` | `web` (lib) | HTTP server, routing, middleware, JSON, static files, auth, sessions, CORS |
| `loong-shared` | `loong-shared/` | `shared` (lib) | Shared data models (User, Post, DocPage, Comment, etc.) |

## Quick start

```bash
# Build individual libraries
loc build --manifest loong-web/loong.toml
loc build --manifest loong-shared/loong.toml

# Inspect artifacts
loc inspect loong-web/dist/loong.web-0.1.0.lpkg
loc inspect loong-shared/dist/loong.shared-0.1.0.lpkg
```

### Consuming from a downstream project

```toml
# loong.toml
[dependencies]
std = { builtin = true }
web = { path = "../loong-server/loong-web" }
shared = { path = "../loong-server/loong-shared" }
```

## License

MIT
