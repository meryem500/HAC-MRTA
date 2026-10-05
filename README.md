# SmartCity MRTA — V8 LLM-Enhanced Agentic Unexpected Replanning

This version deliberately separates two modes.

## 1. Normal mission

**CBBA remains the core allocation algorithm.**

```text
Robot Agents
    ↓
Feasibility / hard constraints
    ↓
CBBA bundle + bids
    ↓
Consensus
    ↓
Initial allocation
    ↓
Safe allocation refinement
    ↓
TSP / OR-Tools route optimization
    ↓
Route validation
    ↓
Simulation
```

The normal trace uses agent language to make the algorithm understandable, for example:

```text
[V1] 👋 Online. I am checking the mission board.
[V1] 💬 T1: Feasible. My CBBA utility = 4.32.
[V1] 📡 Broadcast bid → T1: utility=4.32
[V2] 📡 Broadcast bid → T1: utility=5.10
[CONSENSUS] ⚔️ T1: conflict → winner V2
[V2] 🏆 I won T1 with utility 5.10.
```

The wording is user-facing; the decision itself remains deterministic CBBA.

## 2. Unexpected event

Unexpected events use the agentic LLM branch:

```text
Unexpected event
    ↓
LLM Mission Manager
    ↓
Robot agents communicate
    ↓
LLM reasoning / proposals
    ↓
Manager coordination
    ↓
Hard constraint validation
    ↓
LLM route proposal
    ↓
Hard route validation
```

No CBBA or TSP is called in this branch.

## API-free mode

If no API key is configured, the unexpected-event branch uses a deterministic fallback so the complete architecture can be tested. This fallback is **not an LLM**.

With Claude/OpenAI configured, the same unexpected-event conversation uses the real LLM for agent reasoning and manager adjudication.

## Running

From the folder containing `main.py`:

```powershell
python main.py
```

Then open `http://127.0.0.1:5000`.

Install dependencies with:

```powershell
python -m pip install -r requirements.txt
```
