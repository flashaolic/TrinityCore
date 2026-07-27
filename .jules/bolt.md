## 2026-07-27 - Optimizing Map::Update Heap Allocations
**Learning:** Dynamic allocation of containers (like `std::vector` and `std::unordered_set`) in the `Map::Update` hot path introduces significant heap churn and performance overhead during map updates.
**Action:** Keep reusable collections as private scratchpad members of the `Map` class (`_unitsToVisit` and `_unitsToVisitSet`), clearing them prior to each use. Since each Map instance is updated sequentially by a single thread at a time, thread safety is preserved.
