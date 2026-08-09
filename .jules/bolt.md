
## 2024-05-23 - Map Scratchpad Optimization
**Learning:** The TrinityCore MapUpdater processes each Map instance sequentially within a thread, which allows for the use of Map member variables as scratchpads without synchronization. This is a powerful pattern for avoiding heap churn in the extremely hot Map::Update path.
**Action:** Look for similar per-object update loops where local containers are used and can be moved to member variables to preserve capacity.
