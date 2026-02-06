# Skills

[Agent Skills](https://agentskills.io) for the [Internet Development Studio Company](https://internet.dev) open source tools. These skills teach AI agents how to build with INTDEV's stack — from scaffolding a new project with [nextjs-sass-starter](https://github.com/internet-development/nextjs-sass-starter) to deploying it on Render.

## Skills

| Skill | Description |
|-------|-------------|
| [nextjs-sass-starter](./skills/nextjs-sass-starter/) | Scaffold and build projects using INTDEV's full Next.js + SASS + TypeScript template |
| [nextjs-sass-base](./skills/nextjs-sass-base/) | Scaffold minimal projects with the lightweight Next.js + SASS base template |
| [sacred-computer](./skills/sacred-computer/) | Build UIs with SRCL React components and terminal aesthetics |
| [server-mono](./skills/server-mono/) | Set up and use Server Mono, INTDEV's open-source monospace typeface |
| [intdev-brand-guidelines](./skills/intdev-brand-guidelines/) | Apply INTDEV's visual identity — colors, themes, typography, SVG logos |
| [intdev-api](./skills/intdev-api/) | Integrate with api.internet.dev for auth, payments, data, and organizations |
| [intdev-deployment](./skills/intdev-deployment/) | Deploy and maintain INTDEV websites on Render, Vercel, and AWS |
| [intdev-accessibility](./skills/intdev-accessibility/) | Build WCAG 2.1 AA compliant interfaces following INTDEV's approach |
| [daedalus](./skills/daedalus/) | Plan and orchestrate work with the Daedalus CLI and Talos daemon |

## Usage

### Claude Code (Plugin Marketplace)

Install all skills at once via the plugin marketplace:

```
/plugin marketplace add internet-development/skills
/plugin install intdev-tools@intdev-skills
/plugin install intdev-ops@intdev-skills
```

Skills are grouped into two bundles:

- **`intdev-tools`** — nextjs-sass-starter, nextjs-sass-base, sacred-computer, server-mono, intdev-brand-guidelines, intdev-api
- **`intdev-ops`** — intdev-deployment, intdev-accessibility, daedalus

### Claude Code / OpenCode / Any Agent (Individual Skills)

To install individual skills, clone this repo and copy or symlink just the ones you need into your project or global skills directory:

```bash
git clone https://github.com/internet-development/skills.git ~/intdev-skills

# Project-level (applies to one project)
mkdir -p .claude/skills
ln -s ~/intdev-skills/skills/server-mono .claude/skills/
ln -s ~/intdev-skills/skills/sacred-computer .claude/skills/

# User-level (applies to all your projects)
ln -s ~/intdev-skills/skills/server-mono ~/.claude/skills/
```

This works with Claude Code (`.claude/skills/`), OpenCode (`.opencode/skills/`), and any tool that supports the [Agent Skills specification](https://agentskills.io/specification). Each skill is a self-contained folder with a `SKILL.md` file.

## Creating a Skill

Use the [template](./template/SKILL.md) as a starting point. See the [Agent Skills specification](https://agentskills.io/specification) for the full format reference.

## Open Source

All skills in this repository are open source under the [MIT License](./LICENSE). Built by the team at [Internet Development Studio Company](https://internet.dev) in Seattle, Washington.

- [INTDEV on GitHub](https://github.com/internet-development)
- [INTDEV on Telegram](https://t.me/internetdevelopmentstudio)
- [Explore INTDEV open source](https://wireframes.internet.dev)
