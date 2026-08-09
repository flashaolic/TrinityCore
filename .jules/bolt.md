## 2026-06-30 - Reducing heap churn in Map::Update
**Learning:** In Map::Update, frequent local allocations of `std::vector` and `std::unordered_set` inside the player loop cause significant heap churn. Since each Map is updated by a single thread at a time in MapUpdater, these can be safely converted to member variables to reuse capacity.
**Action:** Always check high-frequency update loops (like Map::Update) for local container allocations that can be moved to class scope scratchpads.
