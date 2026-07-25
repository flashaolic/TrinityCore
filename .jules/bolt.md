## 2026-07-24 - Map::Update heap allocation optimizations
**Learning:** Re-allocating `std::vector` and `std::unordered_set` instances on every Map update tick for each active player creates substantial heap allocation churn on game server hot paths.
**Action:** Replaced local containers in `Map::Update` with reusable member variables `_unitsToVisit` and `_unitsToVisitSet`. Clear them at the start of each scope to reuse capacity safely without multi-threading issues since maps are updated sequentially per instance.
