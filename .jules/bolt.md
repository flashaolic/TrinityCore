## 2026-06-30 - Reducing heap churn in Map::Update
**Learning:** Map::Update is a primary hot path in TrinityCore. Frequently creating local containers like std::vector and std::unordered_set for unit visitation causes unnecessary heap allocations and deallocations. Each Map instance is updated sequentially by a single thread at a time, allowing for the use of Map member variables as reusable scratchpads.
**Action:** Use Map member variables for temporary containers in Map::Update and clear them instead of reallocating.
