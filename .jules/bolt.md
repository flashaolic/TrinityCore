## 2026-07-16 - Sequential Map Updates and Scratchpad Reuse
**Learning:** In TrinityCore, each `Map` instance is updated sequentially on a single thread at a time by `MapUpdater`. This allows using `Map` member variables as thread-safe scratchpads across player loops inside `Map::Update`, avoiding heap allocations per tick per player.
**Action:** Reuse member containers on `Map` (clearing them via `.clear()`) for hot-path temporary collections instead of instantiating local `std::vector` or `std::unordered_set` instances on every iteration.
