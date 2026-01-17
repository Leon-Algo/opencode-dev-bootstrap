# Opencode Dev Bootstrap (working title)

> AI-powered, one-command dev environment bootstrap for new machines, VMs and containers – powered by [Opencode](https://github.com/OpenCode-AI/).

> ⚠️ Status: **Early design / MVP stage**. Breaking changes expected.

---

## ✨ What is this?

`opencode-dev-bootstrap` is an opinionated, AI-assisted tool that turns a **brand new machine** into a **ready-to-code dev environment** with a single command.

It uses **Opencode** as the AI orchestrator and a set of **bootstrap skills** (best-practice recipes) to:

- Detect your OS and basic state
- Ask a few high-level questions (e.g. “Web dev”, “Python / AI dev”)
- Plan a sequence of installation / configuration steps
- Execute them locally with transparent logs

Target platforms (MVP):

- macOS (Intel / Apple Silicon)
- Windows 10+  
- Reusable flows in Docker / remote machines (for testing & CI)

---

## 🎯 Goals

- Make “new machine setup” **repeatable, shareable and observable**
- Give developers a **sane default** dev environment based on best practices
- Keep the surface simple:
  - For users: **one command + a few answers**
  - For contributors: a clear **skill specification** to extend behavior

---

## 🚫 Non-goals (for the MVP)

- Full dotfiles management or Nix-level system configuration
- Desktop / GUI tooling orchestration
- Managing secrets / production credentials
- User accounts, cloud sync, or web UI

We focus on **core dev fundamentals first**.

---

## 🧩 High-level architecture

### 1. Bootstrap installer

Minimal shell / PowerShell script that:

- Detects the platform
- Downloads the CLI
- Runs the initial bootstrap flow

Example (macOS):

```bash
/bin/bash -c "$(curl -fsSL https://opencode.dev/bootstrap.sh)"
```

Example (Windows, PowerShell):

```powershell
iex (iwr "https://opencode.dev/bootstrap.ps1" -UseBasicParsing)
```

> URLs are placeholders for now – to be updated once hosting is decided.

---

### 2. Local CLI

The CLI is responsible for:

- Inspecting the system (OS, arch, existing tools)
- Asking a few questions (dev role, preferences)
- Talking to Opencode API
- Executing the commands suggested by the skills
- Streaming logs & handling basic errors

MVP target stack:  
> Likely a Python-based CLI for fast iteration, with the option to migrate to Go/Rust later.

---

### 3. Opencode & skills

We use Opencode as:

- The **AI brain** that:
  - Reads environment context
  - Selects the right skills
  - Composes a safe, ordered set of actions

The project defines a set of **bootstrap skills**, e.g.:

- `setup_package_manager`
- `setup_git`
- `setup_ssh`
- `setup_node_env`
- `setup_python_env`

Each skill has:

- Platform constraints (macOS / Windows)
- Required inputs (e.g. git username/email)
- A reproducible sequence of commands
- Idempotent behavior where possible (safe to re-run)

In the long run, this skill layer should be **well-documented and contributor-friendly**.

---

## 🧪 MVP scope

For the first public MVP, the tool should be able to:

1. Run a single bootstrap command on macOS / Windows
2. Ensure:
   - a package manager is available (`brew` / `winget`)
   - `git` is installed and configured (name, email, default branch)
   - a basic `ssh` setup exists (generate key if missing)
   - one primary language runtime env is ready:
     - `node` (via `nvm` or equivalent), or
     - `python` (single default version)

3. Log clearly what was installed / changed
4. Be testable in a Docker / VM environment

---

## 📦 Roadmap (rough)

- **Milestone 0 – macOS-only internal prototype**
  - Minimal CLI
  - Opencode integration for a single “web dev” flow
- **Milestone 1 – Public MVP**
  - Windows support
  - Node + Python flows
  - Basic docs and examples
- **Milestone 2 – Extensible skills**
  - Stable skill spec for contributors
  - More languages / stacks
  - CI tests via containers

---

## 🛠 Contributing

> This repo starts with developers in mind.

Planned contributions (once initial scaffolding is ready):

- New skills for specific stacks
- Better defaults and best practices
- Improved error handling and logging
- Platform support & testing scenarios

A dedicated **“Skill Spec”** document will be added once the internal format stabilizes.

---

## ⚠️ Safety & trust

This tool ultimately executes shell / PowerShell commands on your machine.

- You should **always review** the installer script before running
- We aim to:
  - keep the bootstrap script small and auditable
  - make the planned actions **visible** before execution (future enhancement)
  - avoid handling secrets automatically in the MVP

Use at your own risk, especially on production / sensitive machines.

---

## 📄 License

TBD.  
(Most likely a permissive open-source license – MIT / Apache-2.0 – to be decided when the first code lands.)
