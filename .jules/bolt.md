## 2026-07-16 - Reusable Map Scratchpads for Unit Visitation in Hot Loops
**Learning:** In TrinityCore, `Map::Update` is executed sequentially for each `Map` instance. Local `std::vector` and `std::unordered_set` instantiations in the player update loop cause frequent dynamic memory allocations on every tick. Reusing class member scratchpads with `.clear()` preserves allocated capacity across updates safely without thread contention.
**Action:** Replace temporary stack collections in hot loop methods like `Map::Update` with dedicated, cleared member scratchpad containers.
