# BlackCat Engine Changelog

## 1.0.0-dev.1 — 2026-08-13

BC 1.0 第一份可追溯开发快照。

- 建立 Java 8 微内核与运行时组合根。
- 建立 Service Registry、Runtime Handle Registry、Event Pipeline。
- 建立有界 Scheduler 与 Backpressure。
- 建立异步 Asset Runtime：prepare 后台化、commit 分帧预算、请求去重。
- 增加五级资源优先级，并支持 in-flight PREFETCH 在变为可见资源时升级优先级。
- 建立 VAFS、安全目录挂载、SHA-256 内容寻址缓存与 Manifest 路由。
- 建立 Module Runtime、Compatibility Runtime、Diagnostics/Profiler 基础。
- 当前仍属于 Foundation / Runtime 开发阶段，不是 Forge 可安装最终版。
