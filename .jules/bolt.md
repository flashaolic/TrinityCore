## 2026-08-26 - Map Update Heap Allocation Optimization
**Learning:** Map::Update runs on every map tick. Using reusable member containers (`_unitsToVisit` std::vector and `_unitsToVisitSet` std::unordered_set) for visiting nearby units during player update in Map::Update eliminates recurring heap allocation/deallocation overhead in hot paths.
**Action:** When working on hot loops in sequential map update threads, prefer reusable class member containers over local stack-allocated vectors/sets, ensuring clear() is called after use.
