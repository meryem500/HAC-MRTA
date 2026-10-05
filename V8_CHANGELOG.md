# V8 Changelog — Allocation and Optimization Repair

## Normal mission

- Restored a clean deterministic path: **CBBA → consensus → route optimization**.
- Removed normal-case dependence on LLM reasoning for task selection.
- CBBA bids now use **best feasible insertion** into the robot's current bundle instead of always evaluating a simple append-style travel cost.
- Bids are expressed as utilities: higher feasible utility wins.
- Hard constraints are evaluated before a robot can bid.
- Added a 20% minimum battery safety floor consistent with the unexpected-event test cases.
- Route optimization is now followed by a hard constraint validation.
- For small bundles, the route optimizer searches feasible permutations and selects the shortest feasible route.
- OR-Tools remains available as the larger-case route optimizer; its output is also validated.
- Added clearer robot-to-robot / consensus-style messages to the dashboard trace.

## Unexpected-event branch

- CBBA remains completely bypassed for unexpected events.
- TSP remains completely bypassed for unexpected events.
- Fixed sequential shadow-load accounting so newly assigned tasks consume capacity during the same replanning session.
- Candidate feasibility now considers the complete planned route, not only distance and a simple battery threshold.
- LLM-proposed routes are hard-validated before acceptance.
- If an LLM route is invalid, a safe deterministic route validator/fallback is used.
- The LLM remains responsible for reasoning, proposals, communication, and unexpected-event replanning rather than replacing the normal MRTA algorithm.

## Validation

Added `tests/test_allocation_quality.py` for:

- capacity and battery hard constraints
- best-insertion bidding
- final route feasibility

Existing unexpected-event tests remain in `tests/test_unexpected_llm_replan.py`.
