## 2026-07-16 - Map::Update Scratchpad Container Reuse
**Learning:** In TrinityCore, `Map::Update` runs on a per-Map basis sequentially per tick. Local `std::vector` and `std::unordered_set` allocations inside per-player update loops cause continuous heap allocation/deallocation churn on hot paths.
**Action:** Promote local iteration containers to `Map` class member scratchpads and call `.clear()` before and after use to preserve allocated heap capacity without retaining dangling references.
