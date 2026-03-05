# gsap-skills

Official AI skills for GSAP. These skills teach AI coding agents how to correctly use the GSAP (GreenSock Animation Platform), including best practices, common animation patterns, and plugin usage.

Skills follow the [Agent Skills](https://agentskills.io) format and work with the [skills](https://github.com/vercel-labs/skills) CLI (Cursor, Claude Code, Codex, Windsurf, GitHub Copilot, and others).

## Installing

These skills work with any agent that supports the Agent Skills standard, including Claude Code, Cursor, and others.

### Claude Code

Install using the [plugin marketplace](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/plugins#add-from-marketplace):

```
/plugin marketplace add greensock/gsap-skills
```

### Cursor

Install from the Cursor Marketplace or add manually via **Settings > Rules > Add Rule > Remote Rule (Github)** with `greensock/gsap-skills`.

### npx skills

Install using the [`npx skills`](https://skills.sh) CLI:

```
npx skills add https://github.com/greensock/gsap-skills
```

### Clone / Copy

Clone this repo and copy the skill folders into the appropriate directory for your agent:

| Agent | Skill Directory | Docs |
|-------|-----------------|------|
| Claude Code | `~/.claude/skills/` | [docs](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/skills) |
| Cursor | `~/.cursor/skills/` | [docs](https://docs.cursor.com/context/rules) |
| OpenCode | `~/.config/opencode/skills/` | [docs](https://opencode.ai/docs/skills/) |
| OpenAI Codex | `~/.codex/skills/` | [docs](https://developers.openai.com/codex/skills/) |
| Pi | `~/.pi/agent/skills/` | [docs](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent#skills) |

## Skills

| Skill | Description |
|-------|-------------|
| **gsap-core** | Core API: `gsap.to()` / `from()` / `fromTo()`, easing, duration, stagger, defaults |
| **gsap-timeline** | Timelines: sequencing, position parameter, labels, nesting, playback |
| **gsap-scrolltrigger** | ScrollTrigger: scroll-linked animations, pinning, scrub, triggers, refresh & cleanup |
| **gsap-plugins** | Plugins: ScrollToPlugin, ScrollSmoother, Flip, Draggable, Inertia, Observer, SplitText, ScrambleText, SVG & physics plugins, CustomEase, EasePack, GSDevTools, etc. |
| **gsap-utils** | gsap.utils: clamp, mapRange, normalize, interpolate, random, snap, toArray, selector, wrap, pipe, and other helpers |
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
    gsap-plugins/    SKILL.md
    gsap-utils/      SKILL.md
    gsap-react/      SKILL.md
    gsap-performance/  SKILL.md
```

## Compatibility

- **[skills CLI](https://github.com/vercel-labs/skills)** — installs into Cursor, Claude Code, Codex, Windsurf, GitHub Copilot, and [40+ agents](https://github.com/vercel-labs/skills#supported-agents)
- **[Agent Skills spec](https://agentskills.io/specification.md)** — SKILL.md format and discovery

## License

MIT