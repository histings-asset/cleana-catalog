# {{PROJECT_NAME}}

> 一句话产品定位：{{ELEVATOR_PITCH}}

技术栈：**Swift X.Y / SwiftUI / SwiftPM**，最低 macOS XX。`open Package.swift` 或 `swift run {{TARGET}}`。

---

## 运行 / 打包

```sh
cd /path/to/{{PROJECT}}

# 开发：跑 swift run（无图标）
swift run {{TARGET}}

# 打 release .app（带 Info.plist + 图标）
./scripts/bundle-app.sh
open build/{{TARGET}}.app
```

`killall Dock` 强刷图标缓存。

---

## 技术栈 / 架构总览

- **Swift X.Y / SwiftUI**，最低 macOS XX
- **SwiftPM**：`Package.swift` 一个 `executableTarget`
- **{{SANDBOX_STATE}}** —— 写明白沙盒状态（无 sandbox / 启用 App Sandbox / 部分 entitlements）
- **{{XCODE_OR_SPM}}** —— 写明白 Xcode 工程文件 vs SwiftPM only

### 重要架构决定（举几个项目独有的）

1. **Singleton VM**：长任务 VM 用 `.shared`，视图用 `@ObservedObject`，扫描状态不随视图销毁丢失
2. **Task 取消链**：每个长任务 VM 持有 `private var scanTask: Task<Void, Never>?`
3. **{{ACTIVITY_REGISTRY}}**：全局任务寄存器 / Activity Center 等模式

---

## 目录结构

```
{{PROJECT}}/
├── Package.swift
├── CLAUDE.md                          # 你正在看
├── README.md
├── scripts/                           # 打包 / 工具脚本
└── Sources/{{TARGET}}/
    ├── {{TARGET}}App.swift            # @main + AppDelegate
    ├── AppState.swift                 # 全局状态
    ├── Theme/                         # 设计语言 token
    ├── Components/                    # 可复用 SwiftUI 组件
    ├── Views/                         # 一个 Feature 一个 View
    ├── Services/                      # actor 业务逻辑
    └── ...
```

---

## 关键约定 / 坑

### {{PITFALL_1_TITLE}}
（写出项目踩过的具体坑 + 修复办法。例：「ByteCountFormatter(.file) 0 值会返 'Zero KB'，所以 formatBytes() 必须早退」）

### {{PITFALL_2_TITLE}}
…

### Singleton VM + @ObservedObject（不是 @StateObject）
视图里写 `@ObservedObject private var vm = XxxVM.shared`。如果写成 `@StateObject`，SwiftUI 会按视图生命周期管理，导致 view 销毁时 StateObject 被释放。

### actor 内部 await 点之间必须有 isCancelled 检查
否则 `cancel()` 是无效的——actor 会跑完整个方法。

---

## 权限 / 首次运行

- 首次跑 macOS 的 TCC 会弹授权框 —— 要做什么决定一下
- 需要 **完全磁盘访问权限**（系统设置 → 隐私与安全）的功能列出来
- 从 `swift run` 启动时被授权的是 `swift` 命令——日常用打包出来的 .app

---

## 设计语言

- 配色 / 字体 / 玻璃拟态 / 动效 都在 `Theme/`
- 文案语气：（写明白产品的人格设定）

---

## 已知限制 / 下一轮候选

- **还没做**：列出未实现但值得做的功能
- **已知瑕疵**：列出当前的小毛病
- **依赖外部资源**：如远程 catalog 等

---

## IP 注意

- 不复制竞品 / 不复刻艺术资源
- 信息架构可参考行业，每屏视觉 / 文案 / 图标必须原创

---

> 这份 CLAUDE.md 是 {{PROJECT_NAME}} 项目级 Claude Code 指令。
> 进入目录后 Claude / Cursor / OpenCode / Codex 会自动加载。
> 修改后 push 到 main，所有协作者下次 pull 自动同步。
