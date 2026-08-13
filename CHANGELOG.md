# BlackCat Engine Changelog

## 1.0.0 Foundation — 2026-08-13

- Established the Java 8-compatible BlackCat microkernel foundation.
- Added lifecycle, service registry, indexed runtime handles, staged event pipeline and bounded scheduler.
- Added asynchronous asset preparation with in-flight deduplication and frame-budgeted commit processing.
- Added module fault isolation, compatibility environment registry and structured diagnostics/profiling foundations.
- Added BlackCatRuntime as the composition root for core services.
- Added VAFS directory mounts with traversal and symlink-escape protection.
- Added streaming SHA-256 content-addressed storage and immutable manifest-backed resource routing.
- Added five-level asset priorities: IMMEDIATE, VISIBLE, NEARBY, PREFETCH and BACKGROUND.
- Added bounded priority preparation and commit queues so visible resources can overtake queued background work.
- Added in-flight asset priority promotion so queued prefetch work can become immediate without duplicate loading.
- Added Network Protocol Foundation with bounded VarInt/VarLong and UTF-8 codecs.
- Added protocol major/minor and capability negotiation with required-capability rejection.
- Verified 10/10 foundation tests and Java classfile major version 52.

This snapshot is the BC 1.0 foundation and is not yet the final Minecraft-installable Forge 1.12.2 release.
