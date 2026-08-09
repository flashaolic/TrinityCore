## 2026-07-11 - Scratchpad containers in Map::Update
**Learning:** In TrinityCore's MapUpdater, each Map instance is updated sequentially by a single thread at a time. This allows for the use of Map member variables as scratchpad containers (e.g., for unit visitation) without requiring thread synchronization. This pattern significantly reduces heap churn in the Map::Update hot path.
**Action:** When optimizing hot paths in Map or similar objects, check if they are guaranteed to be accessed by a single thread at a time to utilize member-level scratchpads instead of local allocations.
