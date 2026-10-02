# Loon 日语网页过滤

面向 Loon 3.5.2(1005) 的静态日语过滤插件。基于 AdGuard 日语过滤器和 Japanese Filters+EasyList 的日语作用域规则，未导入完整 EasyList。

## 安装

在 Loon 中导入以下插件地址：

```text
https://raw.githubusercontent.com/uposol/loon-japanese-filter/main/AdGuard_Japanese_Loon.plugin
```

插件会从同一仓库加载 `japanese.response.js`。开启 MitM 并信任证书；启用后关闭旧单文件版本，避免重复过滤。

## 设置

- 普通 CSS：默认开启。
- 扩展网页过滤：默认开启，包含扩展选择器与 Scriptlets。
- 上下文网络规则：默认关闭，通过 Referer / Sec-Fetch 近似匹配。

两份运行文件合计约 5.72 MiB。原生配置负责网络拦截与资源替代，共享 JS 负责正文替换、CSS 和浏览器脚本注入。普通 CSS 含通用规则，会处理匹配的 HTML；CSP 和响应脚本优先级可能影响效果。同一响应只会执行一个响应脚本，与其他网页过滤插件共同启用时需安排顺序。

411 条原生动作、58 份完整正文、33 份浏览器脚本和 27,639 个作用域案例对照通过。尚未在 Loon 3.5.2(1005) 真机导入验证。规则为静态快照，非自动更新的 AdGuard 订阅。

## 来源与许可

- [AdGuard Japanese Filter](https://github.com/AdguardTeam/AdGuardFilters)：2.0.77.2，2026-10-01。
- [Japanese Filters](https://gitlab.com/eyeo/filterlists/japanesefilters)：202609280703 日语作用域补充。
- [AdGuard Scriptlets](https://github.com/AdguardTeam/Scriptlets)：2.5.1。
- [AdGuard ExtendedCss](https://github.com/AdguardTeam/ExtendedCss)：2.2.1。
- [Public Suffix List](https://publicsuffix.org/list/)：2026-10-01，MPL-2.0。

原规则与浏览器库著作权归各自作者；Loon 转换与模块化修改日期为 2026-10-02，依 GPL-3.0 分发，许可证见 `licenses/GPL-3.0.txt`。JS 内共享的 Public Suffix List 数据依 MPL-2.0 分发，许可证见 `licenses/MPL-2.0.txt`。
