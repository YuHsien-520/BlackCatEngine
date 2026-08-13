# BlackCat Engine 1.0 Remaining Milestones

The current repository is the verified Core/Foundation layer. The installable Minecraft 1.12.2 1.0 release still requires these layers, in this order:

1. **Forge Bootstrap** — Forge 1.12.2 entrypoint, sided lifecycle bridge, game/render thread bridge, environment scanner, safe shutdown.
2. **VAFS + content-addressed cache** — mount `module://`, `server://`, `cache://`, `minecraft://`; SHA-256 object store; manifest mapping; secure path resolution.
3. **Advanced Asset Scheduler** — priority classes, server-assisted prefetch hints, bounded decode queues, decoded/compiled caches, reference tracking, eviction and memory budgets.
4. **OpenGL/Render Commit Adapter** — frame-budgeted texture/mesh upload, upload batching, render-thread assertions, fallback resources, stall diagnostics.
5. **Network Runtime** — protocol negotiation, capabilities, binary codec, state snapshot/delta, RPC/events/control channels, authority validation hooks.
6. **Module Loader** — manifest parser/schema, dependency graph, API/capability negotiation, classloader isolation for trusted local modules, sandbox boundary for data modules.
7. **Diagnostics UI / Profiler bridge** — in-game inspection, subsystem timing, queue depth, asset cache hit rate, module fault reports.
8. **Compatibility adapters** — CatServer, OptiFine, Pixelmon, JEI, CustomNPCs and other required integrations kept outside Kernel.
9. **Release hardening** — stress tests, malformed module tests, disconnect/reconnect tests, large resource burst tests, long-run memory/queue tests, and a real Forge client/server integration suite.

A final `BlackCatEngine-1.0.0.jar` should only be called installable once milestones 1-9 have been integrated and tested in an actual Minecraft 1.12.2 environment.

## Current progress (2026-08-13)

- [x] Foundation microkernel/runtime
- [x] VAFS directory mounts with traversal + symlink escape protection
- [x] Streaming SHA-256 content-addressed disk cache
- [x] Manifest-backed logical resource routing
- [x] Bounded priority asset preparation queue
- [x] Priority-aware frame-budgeted asset commit queue
- [ ] Server-assisted prefetch hints and predictive region preloading
- [ ] Reference tracking, memory/VRAM budgets and eviction
- [ ] Forge 1.12.2 bootstrap and render-thread bridge
- [ ] OpenGL texture/mesh upload adapter
- [~] Network runtime foundation complete (protocol negotiation + bounded binary codec); snapshot/delta/RPC/transport remain
- [ ] Full module loader
- [ ] In-game integration/compatibility test matrix
