## 2026-07-16 - Map::Update Per-Player Iteration Heap Allocation Scratchpad
**Learning:** In TrinityCore's core loop (`Map::Update`), allocating temporary containers like `std::vector` and `std::unordered_set` inside the per-player loop causes recurring heap allocation overhead on every map tick. Reusing class member containers as scratchpads preserves internal array/bucket capacity and avoids repeated heap allocations in hot paths.
**Action:** Use class member containers as scratchpads for iteration loops in sequentially updated objects (such as `Map`), clearing them before and after use.
