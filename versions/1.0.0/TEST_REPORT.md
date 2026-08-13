# BlackCat Engine 1.0.0 Foundation Test Report

Date: 2026-08-13

## Verification

- Java 8 target bytecode verified (`classfile major 52`).
- Full foundation test suite: 10 / 10 PASS.
- Kernel/runtime composition starts and stops cleanly.
- Asset preparation executes off the caller/render thread.
- Duplicate in-flight asset requests are deduplicated.
- Asset commits respect an explicit nanosecond frame budget.
- Asset preparation and commit queues are bounded and priority-aware.
- `IMMEDIATE` work can overtake queued `BACKGROUND` work in both preparation and commit stages.
- In-flight `PREFETCH` work can be promoted without duplicate loading and keeps the shared future.
- VAFS rejects traversal and symlink escapes outside the canonical mount root.
- SHA-256 storage supports streaming writes/reads and survives store recreation.
- Manifest-backed VFS mounts resolve logical paths to content-addressed objects.
- Network codec rejects malformed overlong VarInt and oversized remote UTF-8 lengths before allocation.
- Protocol negotiation rejects major-version mismatch and missing required capabilities.
- Module failures are isolated and recorded as structured diagnostics.

## Tests

1. LifecycleServiceRegistryTest
2. RuntimeRegistryTest
3. EventPipelineTest
4. SchedulerTest
5. AssetRuntimeTest
6. ModuleRuntimeTest
7. CompatibilityDiagnosticsTest
8. BlackCatRuntimeTest
9. VafsContentStoreTest
10. NetworkRuntimeTest

## Scope

This verifies the Forge-independent BC 1.0 foundation plus VAFS/content cache, priority asset scheduling and the first network protocol layer. It does not yet certify a Minecraft-installable Forge 1.12.2 mod JAR. Forge bootstrap, render-thread/OpenGL adapter, state snapshot/delta/RPC transport, full module loader, memory/VRAM eviction and in-game compatibility testing remain required before the final 1.0 release.
