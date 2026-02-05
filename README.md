# Skills

[Agent Skills](https://agentskills.io) for the [Internet Development Studio Company](https://internet.dev) open source tools. These skills teach AI agents how to build with INTDEV's stack — from scaffolding a new project with [nextjs-sass-starter](https://github.com/internet-development/nextjs-sass-starter) to deploying it on Render.

## Skills

| Skill | Description |
|-------|-------------|
| [nextjs-sass-starter](./skills/nextjs-sass-starter/) | Scaffold and build projects using INTDEV's Next.js + SASS + TypeScript template |
| [sacred-computer](./skills/sacred-computer/) | Build UIs with SRCL React components and terminal aesthetics |
| [intdev-brand-guidelines](./skills/intdev-brand-guidelines/) | Apply INTDEV's visual identity — Server Mono, brand colors, SVG logos |
| [intdev-api](./skills/intdev-api/) | Integrate with api.internet.dev for auth, payments, data, and organizations |
| [intdev-deployment](./skills/intdev-deployment/) | Deploy and maintain INTDEV websites on Render, Vercel, and AWS |
| [intdev-accessibility](./skills/intdev-accessibility/) | Build WCAG 2.1 AA compliant interfaces following INTDEV's approach |
| [daedalus](./skills/daedalus/) | Plan and orchestrate work with the Daedalus CLI and Talos daemon |

## Usage

### Claude Code

Register this repository as a Claude Code Plugin marketplace:

```
/plugin marketplace add internet-development/skills
```

Then install a skill bundle:

```
/plugin install intdev-tools@intdev-skills
/plugin install intdev-ops@intdev-skills
```

Or browse and install individual skills:

1. Select `Browse and install plugins`
2. Select `intdev-skills`
3. Choose `intdev-tools` or `intdev-ops`
4. Select `Install now`

### OpenCode

OpenCode discovers skills from `.opencode/skills/`, `.claude/skills/`, or `.agents/skills/` directories. Clone this repo and symlink the skills you want:

```bash
# From your project root
mkdir -p .opencode/skills
ln -s /path/to/skills/skills/nextjs-sass-starter .opencode/skills/
ln -s /path/to/skills/skills/sacred-computer .opencode/skills/
```

### Other Agent Skills-compatible tools

Any tool that supports the [Agent Skills specification](https://agentskills.io/specification) can use these skills. Each skill is a self-contained folder with a `SKILL.md` file containing YAML frontmatter and markdown instructions.

## Creating a Skill

Use the [template](./template/SKILL.md) as a starting point. See the [Agent Skills specification](https://agentskills.io/specification) for the full format reference.

## Open Source

All skills in this repository are open source under the [MIT License](./LICENSE). Built by the team at [Internet Development Studio Company](https://internet.dev) in Seattle, Washington.

- [INTDEV on GitHub](https://github.com/internet-development)
- [INTDEV on Telegram](https://t.me/internetdevelopmentstudio)
- [Explore INTDEV open source](https://wireframes.internet.dev)
