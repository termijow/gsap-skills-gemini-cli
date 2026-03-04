# gsap-skills

Official AI skills for GSAP. These skills teach AI coding agents how to correctly use the GSAP (GreenSock Animation Platform), including best practices, common animation patterns, and plugin usage.

Skills follow the [Agent Skills](https://agentskills.io) format and work with the [skills](https://github.com/vercel-labs/skills) CLI (Cursor, Claude Code, Codex, Windsurf, GitHub Copilot, and others).

## Installation

Install all GSAP skills with the skills CLI:

```bash
npx skills add <owner>/gsap-skills
```

Replace `<owner>` with the GitHub org or username (e.g. `greensock/gsap-skills`). To list skills without installing:

```bash
npx skills add <owner>/gsap-skills --list
```

To install a single skill by name:

```bash
npx skills add <owner>/gsap-skills --skill gsap-core
```

Agents use each skill when the task matches the skill’s `description` (e.g. “scroll animation” → gsap-scrolltrigger).

## Skills

| Skill | Description |
|-------|-------------|
| **gsap-core** | Core API: `gsap.to()` / `from()` / `fromTo()`, easing, duration, stagger, defaults |
| **gsap-timeline** | Timelines: sequencing, position parameter, labels, nesting, playback |
| **gsap-scrolltrigger** | ScrollTrigger: scroll-linked animations, pinning, scrub, triggers, refresh & cleanup |
| **gsap-react** | React: useGSAP hook, refs, `gsap.context()`, cleanup, SSR |
| **gsap-performance** | Performance: transforms over layout props, will-change, batching, ScrollTrigger tips |

## Structure

```
gsap-skills/
  README.md
  AGENTS.md          # Guidance for agents editing this repo
  skills/
    gsap-core/       SKILL.md
    gsap-timeline/   SKILL.md
    gsap-scrolltrigger/ SKILL.md
    gsap-react/      SKILL.md
    gsap-performance/  SKILL.md
```

## Compatibility

- **[skills CLI](https://github.com/vercel-labs/skills)** — installs into Cursor, Claude Code, Codex, Windsurf, GitHub Copilot, and [40+ agents](https://github.com/vercel-labs/skills#supported-agents)
- **[Agent Skills spec](https://agentskills.io/specification.md)** — SKILL.md format and discovery