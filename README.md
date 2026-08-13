# BlackCat Engine

**BlackCat Engine（BC）** 是面向 Minecraft Java Edition **1.12.2** 的全新高性能双端 Runtime Engine / Module Platform。

BC 是从零设计的新引擎，不继承旧引擎的架构包袱。核心目标是：更低的资源加载卡顿、更高的运行时性能、更强的 Forge/大型整合包兼容性，以及能够长期演进的模块、资源、网络与诊断基础设施。

> 当前正在开发 **1.0.0**。现有产物属于 Forge-independent Core Foundation，还不是可直接放入 `mods/` 的最终 Forge 1.12.2 安装包。

## 当前已经落地

- Java 8 classfile（major 52）
- Microkernel 生命周期与 Service Registry
- Indexed Runtime Handle Registry
- Stage / Priority / Cancellation Event Pipeline
- 有界 Scheduler 与 Backpressure
- 异步 Asset Prepare + 分帧 Budget Commit
- 五级 Asset Priority：Immediate / Visible / Nearby / Prefetch / Background
- Prepare 与 Commit 双阶段优先级队列
- In-flight Prefetch 自动升档，保持同 Future 且不重复加载
- VAFS、安全目录 Mount、路径穿越与 Symlink Escape 防护
- 流式 SHA-256 Content Addressed Store
- Immutable Manifest → Content Hash 资源路由
- Module Runtime 异常隔离
- Compatibility Runtime 基础
- Structured Diagnostics / Profiler 基础
- Network Protocol Foundation：安全 VarInt/VarLong、受限 UTF-8、Protocol/Capability Negotiation

## 资源加载原则

BC 将明显的资源加载冻结视为缺陷。非必要 IO、Hash、Decompress、Decode、Parse、Compile 禁止阻塞 Minecraft Client/Render Thread；必须进入渲染线程的提交工作使用优先级、批处理与每帧时间预算控制。

## 版本归档

仓库参考 YXLand 的可追溯版本结构：

```text
versions/
└── <version>/
    ├── README.md
    ├── CHANGELOG.md
    ├── TEST_REPORT.md
    └── SHA256SUMS.txt
```

源码以仓库主树为准；版本目录记录该版本的状态、验证结果、变更与构建校验信息。

## 1.0 仍需完成

Forge 1.12.2 Bootstrap、FML Transport Bridge、Render/OpenGL Commit Adapter、Snapshot/Delta/RPC Network Runtime、完整 Module Loader、内存/VRAM Budget 与驱逐、诊断 UI、Compatibility Adapters，以及真实 Minecraft 1.12.2 整合包压力测试。

详见 [`docs/NEXT_MILESTONES.md`](docs/NEXT_MILESTONES.md)。
