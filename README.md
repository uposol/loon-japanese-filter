# Loon 日语网页过滤

面向 Loon 3.5.2(1005) 的静态日语过滤插件。基于 AdGuard 日语过滤器和 Japanese Filters+EasyList 的日语作用域规则，未导入完整 EasyList。

## 安装

在 Loon 中导入以下插件地址：

```text
https://raw.githubusercontent.com/uposol/loon-japanese-filter/main/AdGuard_Japanese_Loon.plugin
```

插件会从同一仓库加载 `japanese.response.js`。开启 MitM 并信任证书；启用后关闭旧单文件版本，避免重复过滤。

## 2026-10-02 启动内存修正

旧版将默认关闭的上下文条件留在配置中，仍有大量原生正则声明。新版在构建时移除 353 条默认关闭动作并简化保留条件，原生正则声明由 9,752 次减至 163 次；普通 CSS、扩展网页过滤、正文替换和 MitM 范围不变。配置从约 3.18 MiB 减至约 373 KiB。

更新原插件地址后再启用；如果仍无法启动，请先禁用本插件并查看启动日志。

## 设置

- 普通 CSS：默认开启。
- 扩展网页过滤：默认开启，包含扩展选择器与 Scriptlets。
- 上下文网络近似匹配：固定关闭，相关分支在构建时消除，避免加载默认关闭规则的正则。

两份运行文件合计约 2.90 MiB。原生配置负责网络拦截与资源替代，共享 JS 负责正文替换、CSS 和浏览器脚本注入。普通 CSS 含通用规则，会处理匹配的 HTML；CSP 和响应脚本优先级可能影响效果。同一响应只会执行一个响应脚本，与其他网页过滤插件共同启用时需安排顺序。

修正后保留默认配置实际生效的 58 条原生动作（45 条网络拦截、13 条资源替代）。默认行为序列、58 份完整正文、33 份浏览器脚本和 27,639 个作用域案例对照通过。旧版已收到 iPhone VPN 无法启动反馈；修正后的真机启动结果待确认。规则为静态快照，非自动更新的 AdGuard 订阅。

## 来源与许可

- [AdGuard Japanese Filter](https://github.com/AdguardTeam/AdGuardFilters)：2.0.77.2，2026-10-01。
- [Japanese Filters](https://gitlab.com/eyeo/filterlists/japanesefilters)：202609280703 日语作用域补充。
- [AdGuard Scriptlets](https://github.com/AdguardTeam/Scriptlets)：2.5.1。
- [AdGuard ExtendedCss](https://github.com/AdguardTeam/ExtendedCss)：2.2.1。
- [Public Suffix List](https://publicsuffix.org/list/)：2026-10-01，MPL-2.0。

原规则与浏览器库著作权归各自作者；Loon 转换与模块化修改日期为 2026-10-02，依 GPL-3.0 分发，许可证见 `licenses/GPL-3.0.txt`。JS 内共享的 Public Suffix List 数据依 MPL-2.0 分发，许可证见 `licenses/MPL-2.0.txt`。
