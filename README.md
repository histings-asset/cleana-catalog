# cleana-catalog

> Cleana macOS 客户端在线拉取的远程目录 + 模板库。

这个仓库**全部是数据**——JSON 目录、Markdown 模板、规则文件。Cleana 客户端从 raw.githubusercontent.com 直接 HTTPS 拉取，不需要服务器，不需要域名（Phase 1）。

## 内容

| 文件 / 目录 | 客户端用途 |
|---|---|
| `ai-tools.json` | AI Stack 工具栈的 12+ 工具元数据（安装命令、检测命令、主页等） |
| `agents-md-templates/` | AI 配置教练用来打分的「Top 1%」模板库（CLAUDE.md / .cursorrules / AGENTS.md） |
| `agents-md-rules.json` | 配置评分规则（结构 / 权限 / 路径 / 坑 / 跨工具一致性 5 维） |
| `hardware-table.json` | 硬件评估器用的 Mac 机型 vs AI 工作流匹配表 + 二手市场价 |
| `discover-feed.json` | 发现新工具的本周精选（人工 + 抓 awesome-list 半自动维护） |

## 编辑 / 发版流程

直接 push main 就生效——客户端拉的是 `https://raw.githubusercontent.com/histings-asset/cleana-catalog/main/<filename>`。

## 客户端默认 URL

写在 `Sources/Cleana/Services/AIHubCatalog.swift` 的 `catalogURL`。如果迁移到自有域名（cleana.app），改一行 + 套 Cloudflare Pages 即可。

## 许可

数据 / 模板 = MIT。安装命令均来自每个项目的官方文档，是客观事实。
