---
title: "I Hired 4 AI Coworkers. They Built an App in 5 Minutes."
description: "I gave four AI helpers four different jobs — planning, design, coding, and testing — and they built ping-monitor, a small tool that checks whether websites are up."
pubDate: 2026-11-18
tags: ["DevOps", "AI Agents", "Python", "Automation", "Claude Code"]
---

As a DevOps engineer, my superpower has always been automation. But what happens when you scale that automation from infrastructure up to the way software gets built itself?

Instead of hiring a traditional engineering team for a quick weekend project, I decided to test a new idea: **can one person, acting as the manager, run an entire virtual software company using specialized AI helpers?**

To test it, I built **`ping-monitor`** — a lightweight, clean Python CLI tool that takes a list of URLs, checks their HTTP status and latency in milliseconds, outputs a clean summary table, and exits with code `1` if any endpoint is dead.

Here is how I structured my virtual company, and how the AI team built the tool from scratch in minutes.

---

### Step 1: Designing the Virtual Company Roster

To keep the AI helpers from stepping on each other's toes, I gave each one a strict, isolated role using **Claude Code** and a modular subagent configuration (`.claude/agents/`):

1. **The Business Analyst (BA):** Translates raw ideas into structured Product Requirements Documents (`docs/prd.md`).
2. **The Solution Architect:** Takes the PRD and maps out the technical blueprint, module layout, and function signatures (`docs/architecture.md`).
3. **The Lead Developer:** Implements the exact specifications into production-ready Python code (`src/`).
4. **The QA Engineer:** Writes comprehensive `pytest` suites, executes test runs, and flags edge cases.

---

### Step 2: The Workflow in Action

Instead of writing boilerplate myself, writing tests, or configuring argument parsers, I gave my main session a single prompt:

> *"We need to build `ping-monitor`, a CLI tool that takes a list of URLs, checks HTTP status and response times, prints a summary table, and exits with code 1 on failure. Kick off our full team workflow starting with the BA, then Architect, then Developer, then QA."*

#### 1. The BA Phase (`docs/prd.md`)
The BA immediately spun up and generated a concise PRD outlining the user stories, CLI flags (`--file`, `--timeout`), and exact acceptance criteria (Given/When/Then format).

#### 2. The Architecture Phase (`docs/architecture.md`)
The Solution Architect reviewed the PRD and designed a modular structure keeping dependencies minimal (using standard library `urllib` or lightweight `httpx` along with `pytest`):
* `src/monitor.py`: Core ping logic and timing engine.
* `src/cli.py`: Command-line interface and table formatting.
* `tests/test_monitor.py`: Automated test suite with mocked HTTP responses.

#### 3. The Code & QA Phase (`src/` & `tests/`)
The Lead Developer generated clean, type-hinted Python code matching the architecture blueprint. Immediately after, the QA Engineer stepped in, wrote the test suite, executed `pytest` via the terminal, and verified that everything passed cleanly.

---

### What I Learned

1. **Context Isolation is Everything:** By restricting the BA and Architect so they *cannot* write code or run bash commands, they are forced to focus purely on planning. This prevents "hallucinated scope creep."
2. **Deterministic Handoffs:** Using shared files (`docs/prd.md` and `docs/architecture.md`) acts like a version-controlled contract between team members. The developer never has to guess *what* to build because the architecture spec is explicit.
3. **Speed to Prototype:** What normally takes a few hours of boilerplate scaffolding happened in under 5 minutes, leaving me free to focus on architecture, CI/CD integration, and deployment.

### What's Next?
Now that `ping-monitor` is locally built and tested, the next step is writing a Dockerfile and a GitHub Actions CI pipeline to run it automatically on a cron schedule.

*(Curious how to set this up yourself? Drop a comment or check out the repository structure!)*
