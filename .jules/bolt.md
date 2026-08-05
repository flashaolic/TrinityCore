# Bolt's Journal - Critical Learnings

## 2026-08-04 - TrinityCore Sequentially-Updated Map Scratchpads
**Learning:** Each Map instance in TrinityCore is updated sequentially by a single thread at a time inside MapUpdater. This means we can safely reuse class member variables as scratchpads for heavy performance loops (like unit visitation in `Map::Update`) without needing any thread synchronization or incurring heap allocation churn.
**Action:** When optimizing hot loops in `Map` or other sequentially-updated contexts, introduce reusable member containers (e.g., `std::vector` and `std::unordered_set`) as scratchpads, and ensure they are cleared at the end of the method to prevent dangling pointer retention.
