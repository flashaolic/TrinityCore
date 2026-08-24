# Bolt's Journal

## 2026-07-16 - Sequential Map Updates and Scratchpad Reusability
**Learning:** In TrinityCore, each Map instance is updated sequentially by a single thread at a time. Local heap allocations (`std::vector`, `std::unordered_set`) in `Map::Update` player loops cause heap churn on hot paths.
**Action:** Use class member scratchpads for temporary collections during `Map::Update` and clear them after use.
