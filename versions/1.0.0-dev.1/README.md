# BlackCat Engine 1.0.0-dev.1

这是 BlackCat Engine 1.0 的第一份开发归档。

**状态：Foundation / Runtime Development Snapshot**

当前 JAR 仅为 API/Core 运行时产物，尚未包含 Forge 1.12.2 Bootstrap，因此不能直接作为最终 `mods/BlackCatEngine-1.0.0.jar` 使用。

本快照重点验证 BC 的长期底层架构：Java 8 兼容、微内核、服务注册、模块隔离、异步资源准备、按帧预算提交、资源优先级/in-flight 优先级升级、VAFS 与 SHA-256 内容缓存。

下一开发阶段继续完成服务器辅助 Prefetch、引用追踪/内存预算、Forge Bootstrap、OpenGL Render Commit Adapter 与 Network Runtime。
