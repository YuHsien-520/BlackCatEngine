# BlackCat Engine 1.0 Architecture

## Dependency direction

```text
Gameplay / Feature Modules
          |
          v
     BlackCat API
          |
          v
  Runtime Services
          |
          v
    Microkernel Core
          |
          v
Forge Adapter / Compatibility Layer (next integration layer)
          |
          v
Minecraft 1.12.2 / Forge
```

The current foundation intentionally has **no Forge or Minecraft dependency**. This keeps Kernel behavior deterministic and testable. Forge integration is expected to depend on `BlackCatEngine-API` and `BlackCatEngine-Core`; Kernel must never depend back on Forge.

## Runtime composition

`BlackCatRuntime` is the composition root. It creates and publishes:

- `DiagnosticSink`
- `EngineProfiler`
- `CompatibilityRegistry`
- `EngineScheduler`
- `AssetRuntime`
- `ModuleRuntime`

The public `ServiceRegistry` is the stable access boundary. Modules should depend on service interfaces, not concrete classes.

## Asset smoothness model

BC asset work is split into two phases:

1. **Prepare** — performed on a BC-owned IO worker. File IO, decoding, hashing, decompression, model parsing, and future compilation stages belong here.
2. **Commit** — queued as a small operation and executed by the caller of `AssetRuntime.processCommits(budgetNanos)`. The Forge client adapter will call this from the render/main thread with a strict frame budget.

Properties already enforced by the foundation:

- preparation does not run on the requesting/render thread;
- duplicate in-flight requests share one future;
- scheduler queues are bounded;
- commit queue is bounded;
- a zero budget performs no commit work;
- completed assets are memory-cached until invalidated;
- commit processing stops when its time budget is consumed.

Later BC resource milestones will layer VAFS mounts, SHA-256 content-addressed disk cache, resource priorities, prefetch hints, decoded/compiled model caches, reference accounting, VRAM budgeting, and Forge/OpenGL upload adapters on this contract.

## Runtime handles

Human-readable IDs such as `bc:dragon_sword` are resolved once into `RuntimeHandle<T>`. Handles carry a registry identity and integer index, preventing accidental cross-registry use. Hot paths can therefore use indexed storage instead of repeated string parsing or nested hash maps.

## Module isolation

Each `BlackCatModule` owns a lifecycle state. A failure during lifecycle execution marks only that module `FAILED` and emits a structured diagnostic (`BC-MODULE-*`). The Runtime does not silently continue a partially initialized module.

## Compatibility model

`EnvironmentProfile` and `CompatibilityAdapter` live behind an isolated compatibility registry. Future Pixelmon, OptiFine, CatServer, JEI, CustomNPCs, and other adapters will be separate integration modules rather than Kernel dependencies.

## Java baseline

All production and test code is compiled using `javac --release 8`. The packaging verification checks for Java classfile major version 52 so the core remains valid for the Java 8 ecosystem used by Minecraft 1.12.2.
