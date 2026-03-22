# Bait Engine V3

> Automated engagement system with adaptive persona routing, mutation-driven evolution, and bite-gated targeting.

Bait Engine V3 is a fully-featured automation framework for analyzing online conversations, generating contextually appropriate responses, and managing multi-platform engagement with safety rails, observability, and evolution-driven improvement.

## What It Does

- **Analyzes** incoming messages for sentiment, contradiction, archetype signals, and opportunity scoring
- **Plans** tactical responses using persona-specific strategies and exit criteria
- **Generates** candidate replies with provider-backed LLM integration
- **Routes** through platform adapters (Reddit, X, Discord, Web) with transport-neutral envelopes
- **Evolves** via mutation loops that learn from high-performing responses
- **Monitors** with a built-in dashboard, autopsy tools, and engagement scoreboards

## Key Features

### Core Engine
- **Phase 1-3**: Analysis pipeline, decision engine, generation shell
- **Phase 4-5**: Persistence, replay, provider-backed generation
- **Phase 6-7**: Adapters, UI, execution rail, transport dispatch
- **Phase 8**: Rhetoric scoring, persona reputation tracking
- **Phase 9**: Hunt intake rail with target discovery
- **Phase 10**: Bite gate + mutation loop rail with winner evolution
- **Phase 11-13**: Optimization rail, auto persona router, autopilot hardening

### Safety & Control
- Deterministic scoring around models, not model-only magic
- Every decision inspectable via CLI and dashboard
- Approval workflows before dispatch
- Bite-gated targeting (requires qualification signals)
- Dead letter queue with retry/redrive capability

### Observability
- SQLite-backed run storage with full audit trail
- Autopsy tools for outcome analysis
- Scoreboard rollups by persona, platform, objective
- Report generation (markdown, CSV)
- Real-time dashboard with HTTP API

## Installation

```bash
git clone https://github.com/ethanheinrick01-ctrl/Bait-Engine-V3.git
cd Bait-Engine-V3

# Using uv (recommended)
uv sync
source .venv/bin/activate

# Or using pip
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

## Quick Start

```bash
# Analyze a comment for engagement opportunity
bait-engine analyze --text "Your take is garbage and you should feel bad"

# Draft a reply with a specific persona
bait-engine draft --text "Unpopular opinion: pineapple belongs on pizza" \
  --persona dry_midwit_savant --platform reddit --save

# Hunt for targets on Reddit
bait-engine hunt-preview --source reddit --persona auto --limit 10

# Run the web dashboard
bait-engine panel-serve --open

# View engagement scoreboard
bait-engine scoreboard

# Generate a report
bait-engine report-markdown --out report.md
```

## CLI Reference

### Analysis & Generation
| Command | Description |
|---------|-------------|
| `analyze` | Analyze text for signals, axes, archetypes, contradictions |
| `plan` | Build tactical plan from analysis |
| `draft` | Generate candidate replies with persona selection |
| `replay` | Replay a run with new parameters |

### Storage & Assessment
| Command | Description |
|---------|-------------|
| `runs` | List stored runs |
| `show-run` | Display specific run |
| `autopsy` | Inspect single run outcome |
| `autopsy-many` | Summarize recent runs |
| `scoreboard` | Rollup engagement outcomes |
| `report` | Bundle scoreboard + best bites + flops |
| `record-outcome` | Record engagement outcome |

### Hunt Intake (Phase 9+)
| Command | Description |
|---------|-------------|
| `hunt-preview` | Preview targets from hunt source |
| `hunt-list` | List available intake targets |
| `hunt-promote` | Promote target to active processing |
| `hunt-cycle` | Run staged hunt cycle |
| `hunt-run` | Execute full hunt with dispatch |

### Mutation & Evolution (Phase 10+)
| Command | Description |
|---------|-------------|
| `mutate-run` | Mutate winners from specific run |
| `mutate-winners` | Batch mutate recent winners |
| `mutation-report` | Inspect mutation inventory |

### Adapter & Dispatch
| Command | Description |
|---------|-------------|
| `adapters` | List registered platform adapters |
| `adapter-preview` | Compile run into transport-neutral envelope |
| `emit-preview` | Render transport-specific dry-run |
| `dispatch-emit` | Dispatch approved outbox entry |
| `dispatch-approved` | Batch-fire approved backlog |
| `dispatch-status` | Check dispatch lifecycle |
| `redrive-dispatch` | Retry failed dispatches |

### Panel & Dashboard
| Command | Description |
|---------|-------------|
| `panel-preview` | Build local inspection panel payload |
| `panel-serve` | Host panel as local HTTP app |
| `outbox` | Inspect emit outbox |

### Worker & Daemon
| Command | Description |
|---------|-------------|
| `worker-cycle` | Run one worker pass |
| `worker-run` | Run bounded worker cycles |
| `daemon` | Manage LaunchAgent-backed daemon |

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        HUNT INTAKE                          │
│  (target discovery → bite scoring → lane assignment)        │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                       ANALYSIS PIPELINE                     │
│  (signals → axes → archetypes → contradictions → score)    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      PLANNING ENGINE                        │
│  (persona selection → tactics → objectives → exit criteria) │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                     GENERATION PIPELINE                     │
│  (prompts → LLM writer → critic → ranker → candidates)     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                    ADAPTER & DISPATCH                       │
│  (transport-neutral envelope → platform adapter → emit)     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                    MUTATION & EVOLUTION                     │
│  (bite detection → winner mutation → next-gen prompts)      │
└─────────────────────────────────────────────────────────────┘
```

## Test Status

**146 tests passing**

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src/bait_engine
```

## Documentation

| Doc | Description |
|-----|-------------|
| `docs/00_build_order.md` | Architecture overview and build sequence |
| `docs/01_core_domain_model.md` | Domain models and schemas |
| `docs/02_analysis_pipeline.md` | Analysis pipeline design |
| `docs/03_decision_and_branching.md` | Decision engine and branching |
| `docs/14_phase9_hunt_intake.md` | Hunt intake rail (Phase 9) |
| `docs/15_phase10_bite_evolution.md` | Bite gate + mutation (Phase 10) |
| `docs/16_phase11_optimization_rail.md` | Optimization rail (Phase 11) |
| `docs/18_phase12_auto_persona_router.md` | Auto persona router (Phase 12) |
| `docs/19_phase13_autopilot_hardening.md` | Autopilot hardening (Phase 13) |
| `docs/operator_runbook.md` | Day-to-day operational guide |

## Configuration

Create `.env` or set environment variables:

```bash
# Required for provider-backed generation
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-...

# Optional: OpenRouter for alternative models
OPENROUTER_API_KEY=sk-...

# Optional: ElevenLabs for TTS
ELEVENLABS_API_KEY=...
```

## Development

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Run type checking
mypy src/bait_engine

# Run linting
ruff check src/bait_engine

# Format code
ruff format src/bait_engine
```

## Build Doctrine

1. Lock schemas before writing clever code
2. Separate analysis from generation
3. Make every decision inspectable
4. Prefer deterministic scoring around the model
5. Keep work chunked into small, durable files

## Phase Status

| Phase | Status | Description |
|-------|--------|-------------|
| 0-5 | ✅ Complete | Core engine, persistence, provider generation |
| 6 | ✅ Complete | Adapters and UI |
| 7 | ✅ Complete | Execution rail + transport dispatch |
| 8 | ✅ Complete | Rhetoric scoring + persona reputation |
| 9 | ✅ Complete | Hunt intake rail + target discovery |
| 10 | ✅ Complete | Bite gate + mutation loop rail |
| 11 | ✅ Complete | Optimization rail (arteries 1-6) |
| 12 | ✅ Complete | Auto persona router (arteries 1-4) |
| 13 | ✅ Complete | Autopilot hardening (arteries 1-7) |

## License

MIT License - See LICENSE file for details.

---

**Built with**: Python 3.14+, Pydantic, Click, pytest, SQLite

**Maintained by**: @ethanheinrick01-ctrl
