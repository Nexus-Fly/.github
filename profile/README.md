# Nexus-Fly Organization

Nexus-Fly is a decentralized coordination platform for autonomous logistics fleets. This organization hosts the core Rust implementation, simulation demos, and a front-end landing experience.

## For Judges

If you are evaluating the project, these are the fastest entry points:

1. High-level overview, architecture, and roadmap:
	- Repository root README
2. Rust core, simulations, and how to run the MVP:
	- Codigo-Rust README
3. Front-end landing experience:
	- front-end README

## What to Look For

- Consensus-driven event ordering for coordination without a central server.
- Deterministic auction, handoff, and recovery logic in the Rust domain layer.
- Local simulation that exercises the full delivery lifecycle.
- Clear separation between consensus, domain logic, and UI.

## Quick Start (MVP)

On Windows, run the Rust demo from the Docker dev container:

1. Build and start the container.
2. Enter the container shell.
3. Run the MVP demo binary.

Detailed steps are in the Rust README.

## Support

Please use repository Issues for questions, feedback, or evaluation notes.
