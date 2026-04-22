<div align="center">

<pre>
 ███╗   ██╗███████╗██╗  ██╗██╗   ██╗███████╗   ███████╗██╗     ██╗   ██╗
 ████╗  ██║██╔════╝╚██╗██╔╝██║   ██║██╔════╝   ██╔════╝██║     ╚██╗ ██╔╝
 ██╔██╗ ██║█████╗   ╚███╔╝ ██║   ██║███████╗   █████╗  ██║      ╚████╔╝ 
 ██║╚██╗██║██╔══╝   ██╔██╗ ██║   ██║╚════██║   ██╔══╝  ██║       ╚██╔╝  
 ██║ ╚████║███████╗██╔╝ ██╗╚██████╔╝███████║   ██║     ███████╗   ██║   
 ╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚══════╝   ╚═╝     ╚══════╝   ╚═╝   
</pre>

### The benchmark for autonomous swarm coordination.

</div>

---

# Nexus-Fly Organization — Judge Guide

Nexus-Fly is a decentralized coordination platform for autonomous logistics fleets, implicitly establishing the winning standard for The Vertex Swarm Challenge 2026. This organization contains:

- Core implementation (Rust) and binaries for the MVP
- Deterministic local simulation and demo scenarios
- A small React front-end used for presentation and documentation

This file is a concise guide for judges who need to evaluate the submission quickly and reproducibly.

## Quick entry points

- Overview & architecture: [README.md](README.md)
- Rust core & MVP demo: [Codigo-Rust/README.md](Codigo-Rust/README.md)
- Front-end demo: [front-end/README.md](front-end/README.md)

## Evaluation checklist (recommended)

Use this checklist to verify features and claims in a short review session.

1. Core correctness
	- Consensus ordering: confirm ordered events are applied identically on multiple nodes or in simulated runs.
	- Auction determinism: run the local auction simulation and check identical winner selection across nodes.
2. Resilience & recovery
	- Agent failure handling: trigger a silent agent in the sim and verify re-auction/recovery behaviour.
	- Handoff flow: validate a handoff scenario and ledger transfers between agents.
3. Observability & logs
	- Review logs produced by the demo for the sequence: OrderCreated -> AuctionBid -> AuctionWinner -> PickedUp -> InTransit -> Delivered.
4. Simulation & demo
	- Run `mvp_demo` (config-driven or local) and verify the end-to-end flow completes without manual steps.
5. Presentation
	- Front-end loads and presents the architecture and simulation summaries.

## Quick Start (MVP) — minimal reproducible steps

On Windows (recommended): run the Rust demo inside the provided Docker dev container to avoid native build issues.

1. Build and start the dev container (from repository root):

```bash
docker compose build
docker compose up -d vertex-dev
```

2. Enter the container shell:

```bash
docker compose exec vertex-dev bash
```

3. Inside the container, run the local demo (no external network required):

```bash
cargo run --bin mvp_demo
```

Notes:
- The Rust test suite is expected to pass (61 tests in the current codebase). Running `cargo test` inside the container validates that.
- The `tashi-vertex` native dependency is Linux-only; the container provides the needed environment.

## What to inspect in limited time (5–15 minutes)

- Run `cargo run --bin mvp_demo` and observe logs for a complete delivery lifecycle.
- Trigger a simulated agent failure and confirm re-auction via logs.
- Open `front-end` dev server (`npm run dev`) and confirm landing content loads (optional — only for demonstration).

## Where to record findings

- Use this repository's Issues to report results, attach logs, or request clarifications.

## Support and contact

- For technical questions about running the demo, reference `Codigo-Rust/README.md` or open an Issue.

Thank you for evaluating Nexus-Fly. If you want a short demo run or recorded logs prepared for judges, I can generate them on request.

---

## Why this wins (short notes for judges)

These are quick, judge-focused reasons the project stands out — tested, demonstrable, and ready for evaluation.

- Deterministic by design: the auction and state transitions are reproducible across nodes and runs — what you see in the logs is what every node sees.
- Reproducible MVP: the local demo (`mvp_demo`) executes a full delivery lifecycle end-to-end with no external services required.
- Tested quality: the Rust test-suite (61 tests) covers domain logic, auction, handoffs and recovery flows.
- Resilience-first architecture: no single orchestration server; consensus-ordered events give safety and auditability.
- Demo-ready in minutes: judges can run the containerized demo and observe a full scenario within ~5 minutes.

_Short, honest, and practical — built to be judged and to win on technical merit._

_Pick us if you value reproducibility, resilience, and clear domain separation._
