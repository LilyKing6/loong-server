# loong-server

Loong 语言的 Web 框架——从零构建，无外部运行时依赖（仅依赖 Loong 标准库）。

## 特性

- HTTP/1.1 服务器，支持路由、中间件、静态资源
- JSON 请求/响应处理
- 表单解析与 URL 解码（含 percent-encoding）
- Session 认证与权限控制
- CORS 支持
- 文件上传与落盘
- `.lpkg` 库包分发，显式 `public` 可见性
- 支持 `impure` 路由处理器（`action` 类型），可调用文件 I/O

## 库包

| 包 | 路径 | Target | 说明 |
|----|------|--------|------|
| `loong-web` | `loong-web/` | `web` (lib) | HTTP 服务器、路由、中间件、JSON、静态资源、认证、Session、CORS、上传 |
| `loong-shared` | `loong-shared/` | `shared` (lib) | 共享数据模型（User、Post、DocPage、Comment 等） |

## 快速开始

### 构建

```bash
# 构建库包
loc build --manifest loong-web/loong.toml
loc build --manifest loong-shared/loong.toml

# 校验
loc validate --manifest loong-web/loong.toml
loc validate --manifest loong-shared/loong.toml

# 检查 .lpkg 完整性
loc inspect loong-web/dist/loong.web-0.1.0.lpkg
loc inspect loong-shared/dist/loong.shared-0.1.0.lpkg
```

### 在下游项目中使用

```toml
# loong.toml
[dependencies]
std = { builtin = true }
web = { path = "../loong-server/loong-web" }
shared = { path = "../loong-server/loong-shared" }
```

```loong
import web.server using;
import web.routing using;
import web.context using;

impure fn myRoutes() -> List<HttpRoute> {
  routeGroup(
    "/api",
    HttpRoute(HttpMethod.Get, "/hello", impure [](ctx: RouteContext) -> HttpResp {
      jsonOk(jsonObject(jsonField("msg", "Hello, Loong!")))
    })
  )
}

impure fn serve(s: ServerSettings) -> Option<Error> {
  serveWithRoutes(s, myRoutes())
}
```

## 模块一览

```
loong-web/src/web/
  app.lo              框架演示路由（健康检查、登录、上传）
  auth.lo             权限检查
  config.lo           CLI/env 配置加载
  context.lo          请求/路由上下文、HttpRoute
  cors.lo             CORS 处理
  errors.lo           统一 JSON 错误响应
  form.lo             表单/URL 解析（含 percent-encoding）
  http.lo             HTTP 模块聚合
  http_content_type   内容类型
  http_header         HTTP 头解析/写入
  http_method         HTTP 方法
  http_response       HTTP 响应构造
  http_statuscode     HTTP 状态码
  json.lo             JSON 构造与解析
  logging.lo          请求/响应日志
  middleware.lo       中间件管道
  routing.lo          路由匹配与分发
  server.lo           TCP 服务器、静态资源加载
  session.lo          Cookie session
  static.lo           静态资源服务
  upload.lo           文件上传与落盘
```

## 可见性

所有导出 API 均使用显式 `public` 修饰符（语言规范 §14.5）。内部辅助函数保持默认可见，不导出。

## 技术要求

- Loong 编译器 `loc` v2.0.1+
- Loong 运行时 `lort`

## 许可证

MIT
