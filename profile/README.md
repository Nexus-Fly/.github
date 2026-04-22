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

---

![Built with Rust](https://img.shields.io/badge/Built%20with-Rust-orange?style=for-the-badge&logo=rust)
![Containerized](https://img.shields.io/badge/Docker-Ready-blue?style=for-the-badge&logo=docker)
![Tests](https://img.shields.io/badge/Tests-61%20passing-brightgreen?style=for-the-badge&logo=github-actions)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Functional%20%26%20Running-success?style=for-the-badge)

---

### Pitch

[![Watch the Nexus-Fly Pitch](https://img.youtube.com/vi/BnBTw9CslL0/maxresdefault.jpg)](https://youtu.be/BnBTw9CslL0)

> *Click the image above to watch the pitch video.*

</div>

---

# Evaluation Guide — Nexus-Fly

**Nexus-Fly** is a decentralized coordination platform for autonomous delivery fleets, designed to show how drones, ground robots, and e-bikes can operate as a single resilient network without relying on a central orchestrator. The project addresses one of the most important challenges in autonomous logistics: coordinating heterogeneous agents in real time in a way that is auditable, fault-tolerant, and reproducible.

This organization includes:

* The **core Rust implementation** and fully functional MVP binaries
* A **deterministic local execution flow** and reproducible operational scenarios
* A **live execution server** for observing the system running continuously
* A **React front-end** for architecture presentation and system visualization
* A **Docker-containerized environment**, ready for fast deployment and frictionless validation

This document is intended as a concise and practical guide for reviewing the project efficiently, technically, and reproducibly.

---

## Recommended Entry Points

* **Project overview and architecture:** `README.md`
* **Rust core, MVP flow, and execution details:** `Codigo-Rust/README.md`
* **Front-end presentation layer:** `front-end/README.md`

---

## Recommended Review Checklist

Use this checklist to validate the project's main claims during a short review session.

### 1. Distributed Core Correctness

* **Consensus ordering:** confirm that critical events are applied consistently and identically across nodes or simulated executions.
* **Auction determinism:** verify that the winner selection logic produces the exact same result across runs and nodes.

### 2. Resilience and Recovery

* **Agent failure handling:** trigger an inactive or silent agent and observe how the system detects the failure and re-routes the workflow through re-auction.
* **Handoff flow:** validate that a delivery can be transferred between agents and that the ledger reflects the transition correctly.

### 3. Observability and Traceability

* Review the logs and confirm the expected operational sequence:
  `OrderCreated -> AuctionBid -> AuctionWinner -> PickedUp -> InTransit -> Delivered`

### 4. Functional Execution

* Run `mvp_demo` and verify that a complete delivery lifecycle executes end-to-end without manual intervention.
* Run `mvp_server` and confirm that the system stays active, continuously generating activity and real-time logs.

### 5. Presentation Layer

* Confirm that the front-end loads correctly and communicates the architecture, capabilities, and system scenarios clearly.

---

## Quick Start — Minimal Reproducible Execution

### Recommended on Windows

To avoid native build issues, the Rust execution flow should be run inside the provided Docker development container.

### 1. Build and start the development container

From the repository root:

```bash
docker compose build
docker compose up -d vertex-dev
```

### 2. Enter the container

```bash
docker compose exec vertex-dev bash
```

### 3. Run the local functional workflow

Inside the container:

```bash
cargo run --bin mvp_demo
```

### 4. Run the live execution server

Inside the container:

```bash
cargo run --bin mvp_server
```

---

## Execution Notes

* The Rust test suite is expected to pass successfully (**61 tests in the current codebase**).
  You can validate this by running:

```bash
cargo test
```

* The native **tashi-vertex** dependency requires a Linux environment; the Docker container already provides everything needed.
* Because the project is already **containerized with Docker**, it is straightforward to deploy, reproduce, and inspect without dealing with local environment inconsistencies.

---

## What to Inspect in a Short Review (5-15 minutes)

If review time is limited, this is the recommended flow:

1. Run `cargo run --bin mvp_demo`
2. Confirm the complete delivery lifecycle in the logs
3. Run `cargo run --bin mvp_server`
4. Observe continuous system activity, event generation, and live behavior
5. Inspect auction logic, handoffs, and settlement behavior
6. Trigger or review an agent failure and re-auction path
7. Open the front-end (`npm run dev`) to inspect architecture and visual summaries
   *(Optional, but useful for context and presentation)*

---

## Where to Record Findings

Use this repository's **Issues** to report findings, attach logs, or request clarification.

---

## Support and Contact

For technical questions about execution or architecture, refer to:

* `Codigo-Rust/README.md`
* or open an **Issue** in this repository.

If a guided run-through or a packaged set of execution logs is needed, it can be prepared quickly.

---

# Why Nexus-Fly Stands Out

These are some of the reasons Nexus-Fly represents a strong, technically mature, and highly inspectable submission:

* **Deterministic by design**
  Auction behavior, event ordering, and state transitions are reproducible across nodes and executions. What is observed is not dependent on arbitrary or manual conditions.

* **Reproducible functional workflow**
  The local execution path (`mvp_demo`) runs a full delivery lifecycle end-to-end without requiring external services, making validation fast and reliable.

* **Live execution server for continuous observation**
  `mvp_server` allows the system to be observed as an ongoing functional process, generating activity and logs in real time.

* **Quality backed by tests**
  The current Rust test suite (**61 tests**) covers domain logic, auctions, handoffs, recovery flows, and core system behavior.

* **Resilience-first architecture**
  Nexus-Fly removes the single point of failure by replacing centralized orchestration with a coordination layer based on consensus-ordered events.

* **Direct, frictionless deployment**
  The project is already prepared to run inside a **Dockerized environment**, which reduces setup overhead and makes review fast, clean, and consistent.

* **Clear observability**
  Logs and execution flow make it possible to verify exactly how an order is created, assigned, transferred, and completed.

* **Ready to run in minutes**
  The project can be built, launched, and inspected quickly, allowing attention to stay on system behavior rather than environment setup.

* **Real technical substance**
  The system combines distributed systems, robotics, BFT consensus, multi-agent coordination, and autonomous logistics in a modular and extensible architecture.

---

# Conclusion

**Nexus-Fly represents a concrete and functional vision of how autonomous coordination should work in the future.**
It combines reproducibility, resilience, traceability, and architectural clarity into a system that can already be deployed, executed, and inspected with minimal setup.

Rather than presenting only a concept, Nexus-Fly provides a **running functional codebase** that shows how drones, ground robots, and e-bikes can operate as a distributed logistics network without relying on a central orchestrator. Its architecture demonstrates a credible path toward real-world autonomous fleet coordination: **distributed, fault-tolerant, auditable, and built for heterogeneous agents.**

**Nexus-Fly is not just a proposal — it is functional code already running.**
