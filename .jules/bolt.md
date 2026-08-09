## 2025-05-15 - Reducing Heap Churn in Map::Update
**Learning:** High-frequency hot paths like Map::Update in TrinityCore frequently allocate temporary containers (std::vector, std::unordered_set) for unit visitation. These allocations cause significant heap churn. Since Map instances are updated sequentially by MapUpdater, we can safely use Map member variables as scratchpads.
**Action:** Always check for local container allocations in high-frequency loops and consider promoting them to member variables if thread safety (sequential access) is guaranteed. Use .clear() to preserve capacity.
