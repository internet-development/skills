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

### Ask Your Agent

The easiest way to install a skill is to give your agent the link and ask it to set it up. For example:

> Install this skill into my project: https://github.com/internet-development/skills/tree/main/skills/server-mono

Your agent will fetch the `SKILL.md`, create the directory, and place it in the right location.

### Individual Skills

Each skill is a self-contained folder. Download just the ones you need directly into your project or global skills directory:

```bash
# Download a single skill into your project
curl -sL https://raw.githubusercontent.com/internet-development/skills/main/skills/server-mono/SKILL.md \
  --create-dirs -o .claude/skills/server-mono/SKILL.md

# Or download to your global skills (applies to all projects)
curl -sL https://raw.githubusercontent.com/internet-development/skills/main/skills/server-mono/SKILL.md \
  --create-dirs -o ~/.claude/skills/server-mono/SKILL.md
```

This works with Claude Code (`.claude/skills/`), OpenCode (`.opencode/skills/`), and any tool that supports the [Agent Skills specification](https://agentskills.io/specification).

For skills with reference files (like `sacred-computer`), extract the folder from the repo tarball:

```bash
curl -sL https://github.com/internet-development/skills/archive/refs/heads/main.tar.gz \
  | tar xz --strip-components=2 skills-main/skills/sacred-computer
mv sacred-computer .claude/skills/
```

### All Skills (Plugin Marketplace)

Install everything at once via the Claude Code plugin marketplace:

```
/plugin marketplace add internet-development/skills
/plugin install intdev-tools@intdev-skills
/plugin install intdev-ops@intdev-skills
```

Skills are grouped into two bundles:

- **`intdev-tools`** — nextjs-sass-starter, nextjs-sass-base, sacred-computer, server-mono, intdev-brand-guidelines, intdev-api
- **`intdev-ops`** — intdev-deployment, intdev-accessibility, daedalus

## Creating a Skill

Use the [template](./template/SKILL.md) as a starting point. See the [Agent Skills specification](https://agentskills.io/specification) for the full format reference.

## Open Source

All skills in this repository are open source under the [MIT License](./LICENSE). Built by the team at [Internet Development Studio Company](https://internet.dev) in Seattle, Washington.

- [INTDEV on GitHub](https://github.com/internet-development)
- [INTDEV on Telegram](https://t.me/internetdevelopmentstudio)
- [Explore INTDEV open source](https://wireframes.internet.dev)
