# SmartCity MRTA V5 – Improvement Changelog

## Main goals
V5 keeps the deterministic MRTA pipeline authoritative while making the workflow visible and explainable in the UI.

## Implemented
- Scenario Builder redesigned with responsive agent/task cards; adding many tasks no longer forces a wide overflowing table.
- Dashboard battery terminology standardized to **Avg Remaining Battery**.
- Allocation page now exposes allocation summary, unassigned tasks, CBBA rounds, candidate bids, winners, conflicts, bundle state, and FIPA/ACL message breakdown.
- Constraint validation now warns when aggregate one-trip fleet capacity is lower than total waste demand.
- Unassigned tasks include deterministic per-agent feasibility reasons in the graph state.
- TSP results distinguish multi-task OR-Tools optimization from single-task routes where ordering optimization is not required.
- Results page no longer contains the “For PFE analysis” label.
- Results page now includes task execution history by robot for the current simulation run.
- Agents page shows each robot's completed task history.
- Live Simulation page adds live summary metrics, clearer status states, route progress, task state visualization, and cleaner Cartesian map labels.
- Logs page adds filters for System, CBBA, FIPA/ACL, TSP and Simulation events, plus communication and TSP summaries.
- LLM backend now has a real analysis path using the configured OpenAI API key, with deterministic MRTA data supplied as context. The LLM is explicitly prevented from replacing or overriding constraints, CBBA, FIPA/ACL or TSP.
- LLM chatbot now answers questions from the current scenario/allocation/routes/metrics/unassigned-task context.
- Simulation completion now means all assigned routes have finished; if some tasks are intentionally unassigned, the run completes with an explicit warning instead of running forever.
- Robot state records `completed_tasks` for traceability.

## API key
No secret is included in this package. Configure `OPENAI_API_KEY` in your local `.env` and keep `LLM_ENABLED=true` when you want the real LLM.
