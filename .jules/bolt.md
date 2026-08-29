## 2026-07-16 - Avoid value copy in hot Map::Update loops
**Learning:** Iterating over multimaps/maps like `player->GetAppliedAuras()` using value types (`std::pair<K, V>`) causes hidden value copy overhead on every map tick for every active player. Using `auto const& [_, val]` eliminates value copies in hot loops.
**Action:** When inspecting map iteration loops in core tick functions, verify structured bindings or const references are used instead of value copies.
