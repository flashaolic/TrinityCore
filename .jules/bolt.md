## 2026-07-16 - Reusable Map Scratchpads for Hot Update Loops

**Learning:** In TrinityCore's Map update loop (`Map::Update`), each `Map` instance is updated sequentially on a worker thread. Creating local `std::vector` and `std::unordered_set` instances inside player update loops causes repeated heap allocations on every tick. Promoting these scratchpads to `Map` class member variables and calling `clear()` reuses vector capacity across iterations without thread synchronization overhead.

**Action:** Whenever iterating over players/entities in `Map::Update` or grid visitors, use class-level scratchpad containers cleared via `.clear()` rather than declaring local stack/heap containers in hot loops.
