# Bolt's Journal - Critical Performance Learnings

## 2026-06-20 - Thread execution guarantees and sequentially-updated map scratchpads
**Learning:** In TrinityCore's MapUpdater, each Map instance is updated sequentially by a single thread at a time. This thread execution guarantee allows us to use Map member variables as scratchpad containers (e.g., for unit visitation in Map::Update) without requiring thread synchronization. This avoids expensive heap allocation and deallocation churn on the hot path (Map::Update).
**Action:** When optimizing hot paths in Map::Update or similar sequentially-updated contexts, look for transient heap allocations (like std::vector or std::unordered_set inside loops) and pull them into class member variables as scratchpads. Remember to document them with comments stating they are for temporary use in specific methods to avoid misuse as persistent state.
