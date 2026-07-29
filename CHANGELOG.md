# Changelog

## v0.1.0 (2026-07-29)

### 新增
- HTTP/1.1 服务器：路由、中间件、静态资源服务
- JSON 请求/响应处理、表单解析与 URL 解码
- Session 认证与权限控制（`requireUser` / `requirePermission`）
- CORS 支持
- 文件上传与落盘（`saveUpload` → `data/uploads/`）
- 静态资源自动加载（`data/uploads/` 目录）
- `.lpkg` 库包分发，显式 `public` 可见性
- `HttpRoute.handler` 支持 `action`（impure）类型，可调用文件 I/O
- 完整的 percent-encoding URL 解码（`urlDecode`）

### 库包
- `loong-web`（21 模块）：HTTP 服务器、路由、中间件、JSON、静态资源、认证、Session、CORS、上传
- `loong-shared`（2 模块）：共享数据模型（User、Post、DocPage、Comment 等）
