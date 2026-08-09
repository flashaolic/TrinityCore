## 2025-05-15 - [Container Reuse in Map::Update]
**Learning:** The `Map::Update` method is a critical hot path executed for every player on every map every tick. Local allocations of `std::vector` and `std::unordered_set` in this loop cause significant heap churn.
**Action:** Use class-member scratchpad containers and `.clear()` them for reuse. This is safe because `Map` updates are sequential and thread-pinned in the `MapUpdater`.
