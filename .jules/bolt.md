## 2026-03-04 - Incremental object compilation for fast verification
**Learning:** Running `make tests` or building the full `game` target times out in the sandbox because compiling all game/server sources at once takes over 400 seconds.
**Action:** Use target-specific object compilation (e.g. `cd build/src/server/game && make Maps/Map.cpp.o`) for rapid build and syntax verification.
