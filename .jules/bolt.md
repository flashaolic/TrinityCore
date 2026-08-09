## 2025-06-30 - Heap churn in Map::Update
**Learning:** The `Map::Update` function is a primary hot path where temporary `std::vector` and `std::unordered_set` were being allocated for every player during each tick. In TrinityCore's architecture, each `Map` is updated sequentially by a single thread, making it safe to use member variables as reusable scratchpad containers.
**Action:** Use member variables (e.g., `_unitsToVisit`) and `clear()` them before use in hot path loops to preserve allocated capacity and avoid repeated heap allocations.
