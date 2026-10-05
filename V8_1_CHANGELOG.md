# V8.1 — A2A Normal Mission + Balanced CBBA

## Normal mission
- Replaced the user-facing FIPA/ACL terminology with an A2A agent-to-agent communication layer.
- Added structured A2A message envelopes with sender, receivers, task/context, message type and content.
- Kept the normal mission deterministic: hard constraints → CBBA allocation → safe refinement → TSP/route optimization → validation → simulation.
- Fixed priority scoring so priority 5 is more important than priority 1.
- Hard capacity and battery constraints remain mandatory before a task can be proposed or awarded.
- Added one-award-per-robot-per-CBBA-round as a workload-balance guard for larger task sets.
- Added round-robin rotation for equivalent robot agents; robot IDs are not used as tie-breakers.
- Added a refinement fairness guard so distance improvement cannot collapse tasks onto one homogeneous robot.
- Final routes are revalidated against capacity and battery reserve constraints.

## Frontend
- Reworked the normal allocation page wording around A2A communication.
- Added a compact architecture strip showing Normal Mission vs Unexpected Event flows.
- Improved allocation rows with load/capacity information.
- Improved A2A communication trace with readable agent-style messages.
- Updated workflow/log/result labels to A2A and route optimization terminology.
- Kept the unexpected-event LLM branch separate from normal CBBA/TSP execution.

## Validation
- `python -m compileall -q .` — passed.
- `node --check web/static/app.js` — passed.
- `PYTHONPATH=. pytest -q tests/test_allocation_quality.py` — 7 passed.
- Full project pytest requires the project's installed `langgraph`, Flask and OR-Tools environment.
