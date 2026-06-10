# CC Operation Log

> Owner: CC (Codex)
> Created: 2026-06-10
> Purpose: CC's project handoff notes and operation history for Project Astra.

## How CC Should Use This File

- Read `ASTRA_CORE.md` first, then `PROGRESS.md`, then the task-specific document under `docs/`.
- Record every meaningful action in the operation history below.
- Keep entries short, factual, and useful for future continuation.
- When a design change affects project state, also update `PROGRESS.md`, `CHANGELOG.md`, and if needed `ASTRA_CORE.md`.
- Preserve Project Astra's emotional core: "Even if the whole world forgets you, I will find you again."

## Current Understanding

Project Astra is a third-person open-world action RPG in pre-production/design phase. Its core theme is reincarnation, memory, sacrifice, pure love, and resisting fate. The emotional center is not simply saving the world, but the protagonist gradually remembering the heroine, who carries the cost of being forgotten by the world.

The project currently prioritizes story and design documentation before playable implementation. Unity 2022.3 LTS + URP + cel shading is the chosen technical direction, but the Unity project itself has not been created yet.

## Repository Snapshot

- Repository: `Darlingyyyy/Project-Astra`
- Default branch: `main`
- Local Git workspace: `C:\Users\20807\Documents\Codex\2026-06-10\cc\Project-Astra-git`
- Temporary zip/API workspace: `C:\Users\20807\Documents\Codex\2026-06-10\cc\Project-Astra`
- The repository was first retrieved by public GitHub zip/API on 2026-06-10 because local Git was not available.
- Git for Windows 2.54.0 was later installed successfully.
- Original SSH private key generated in `work\cc_github_ed25519` became unreadable to Windows OpenSSH due local ACL restrictions.
- Current working SSH key:
  - Public key path: `C:\Users\20807\.ssh\cc_github_ed25519_v3.pub`
  - Private key path: `C:\Users\20807\.ssh\cc_github_ed25519_v3`
  - GitHub Deploy Key authentication: confirmed.

## Important Documents

| File | Role |
|------|------|
| `ASTRA_CORE.md` | Compressed game design DNA and AI handoff protocol |
| `PROGRESS.md` | Current module progress and next tasks |
| `CHANGELOG.md` | Versioned design change history |
| `docs/GDD.md` | Main game design document |
| `docs/skill-system.md` | Skill system and class skill trees |
| `docs/class-system.md` | Six-class positioning |
| `docs/level-design/prologue.md` | Detailed prologue beat design |
| `docs/level-design/village-01.md` | Starter village level design |
| `greybox/prologue-greybox.html` | Three.js prologue greybox prototype |

## Current Project State

Completed or mostly complete:

- World framework for Eldra and the three origin forces.
- Core trio: protagonist, heroine, and great mage.
- Seven-act story outline.
- Prologue beat design v0.3, built around a three-person squad and heroine sacrifice scene.
- Starter village level design.
- Combat frame: three-person real-time party action, switching, six skill keys, elemental links.
- Skill system v3.0 framework.
- Paladin skill tree fully redesigned with 18 skills and tank/magic-warrior routes.
- Three.js greybox prototype.

Known next tasks:

- Rewrite the remaining five class skill trees under v3.0: Berserker, Mage, Priest, Assassin, Hunter.
- Fill Paladin numeric placeholders only after playable prototype testing.
- Build Unity 2022.3 LTS + URP project and migrate greybox concepts.
- Create combat/economy/growth data tables.
- Design 3-5 adventure companions with independent arcs.
- Write detailed Chapter 1 beats.
- Produce concept art directions for protagonist, heroine, and Godtree Village.

## Design Rules CC Must Preserve

- Every design decision should serve memory, reunion, sacrifice, or the heroine's remembered/unremembered existence.
- Do not add systems only because they are cool.
- Keep numbers as `[PLACEHOLDER]` until a playable prototype exists.
- The heroine's silence is meaningful; do not casually make her talk.
- Every controllable companion needs an independent arc, not just a combat function.
- Avoid complexity that does not create meaningful player choice.

## Operation History

### 2026-06-10

- Accepted the user-defined assistant name `CC`.
- Generated an initial GitHub SSH key pair:
  - Public key label: `cc-codex-github-2026-06-10`
  - Private key path: `work\cc_github_ed25519`
- Attempted to clone `git@github.com:Darlingyyyy/Project-Astra.git`.
- Found local `git` was not installed or not on PATH.
- Verified the repository is public and default branch is `main` through the GitHub API.
- Downloaded repository contents by GitHub zip/API into local workspace.
- Read and summarized `README.md`, `PROGRESS.md`, `CHANGELOG.md`, `ASTRA_CORE.md`, and `docs/skill-system.md`.
- Generated replacement SSH key pair after the original private key became unreadable due Windows ACL restrictions:
  - Public key label: `cc-codex-github-2026-06-10-v3`
  - Public key path: `C:\Users\20807\.ssh\cc_github_ed25519_v3.pub`
  - Private key path: `C:\Users\20807\.ssh\cc_github_ed25519_v3`
- Created this file as CC's ongoing operation log.
- Confirmed the v3 Deploy Key authenticates as `Darlingyyyy/Project-Astra`.
- Installed Git for Windows 2.54.0.
- Cloned the repository through SSH into `Project-Astra-git`.
- Committed and pushed this operation log to `main`.
