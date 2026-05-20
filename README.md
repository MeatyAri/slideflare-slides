# SlideFlare Slides — AI Agent Skill

> Create beautiful presentations effortlessly with your AI agent.

[SlideFlare](https://github.com/MeatyAri/slideflare) is a blazing-fast, interactive presentation tool built with Rust + SvelteKit. This agent skill lets your AI agent generate, edit, and style polished slide decks — complete with LaTeX math, HTML components, Tailwind CSS styling, and embedded media — all from natural language prompts.

## What You Can Do

Tell your agent to create slides on any topic, and it'll produce a complete, styled presentation. You can also ask it to edit existing decks, add or remove slides, or tweak styling — all through conversation.

## Installation

### Using npx (Recommended)

```bash
npx skills add MeatyAri/slideflare-slides
```

This downloads and sets up the skill in your agent's skills directory automatically.

### Manual Installation

Drop the `slideflare-slides` folder into your agent's skills directory:

```bash
cp -r slideflare-slides ~/.agents/skills/
```

Your agent will automatically pick up the skill and use it when you ask about slides, presentations, or SlideFlare.

## Supported Agents

This skill works with any agent that supports installing skills — including Claude Code, OpenCode, PI, and many others.

## File Extension

SlideFlare presentations use the `.md` extension — they're just markdown files. Drag and drop them into the SlideFlare app to view them.

## License

[Apache 2.0](https://github.com/MeatyAri/slideflare/blob/main/LICENSE) — Part of the SlideFlare ecosystem.

