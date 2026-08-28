## 2026-07-16 - Heap allocations in hot loop std::unordered_set vs std::vector
**Learning:** Instantiating `std::unordered_set` inside per-player `Map::Update` loops causes node heap allocations and hash table overhead on every tick. For small element collections (< 10 items), replacing `std::unordered_set` with `std::vector` and `std::find` prevents node heap allocations completely and provides better cache locality.
**Action:** Prefer `std::vector` with linear duplicate checks over `std::unordered_set` when working with small datasets in hot game loop updates.
