# Applied AI Learning Diary

> A day-by-day record of my applied AI learning journey, shared openly to encourage others.
>
> *If we put in the time and effort, we can learn anything.*

---

## Table of Contents

- [May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful](#may-2-2026--why-github-over-notion-and-posthogs-guide-to-making-claude-code-actually-useful)

---

## May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful

I decided to document my learnings in Applied AI and create a centralised place for all the resources, publicly available to everyone.

I chose GitHub over Notion because it's easier to distribute — people can follow the repo and get notified when things change. It also feels more techie, and I like it here more than Notion.

My first documented learning is an interesting blog post from **PostHog** on how to make Claude Code actually useful. I use PostHog a lot — basically daily — so when they wrote about their own experience adopting it, I paid attention. Up until now I had been playing more with **OpenClaw** and its extensive possibilities, but Claude Code seems to be a superior solution in terms of stability, UX, and security.

The article is written from a team context (the author is a manager at PostHog), but the practical setup applies to anyone using Claude Code seriously.

**The key insight**: the highest-leverage thing you can do is ask the agent to come up with use cases tailored specifically to your work. Generic "top AI use cases" listicles are written for someone whose job is not your job — they don't help.

**Context files are the foundation.** Before you can automate anything, you need to give the agent context about who you are, your team, and your company. The author uses:
- **CLAUDE.md** as the main index — who they are, their team's GitHub handles and Slack IDs, current focus areas, and standing preferences
- **glossary.md** for company-specific acronyms and relevant Slack channels

**Scheduled tasks beat on-demand chat.** The author finds background scheduled tasks far more valuable than the conversational interface. One concrete example: on the 8th of each month, a task reads a GitHub issue called "Things Charles cares about" — a running list of current priorities — and automatically refreshes CLAUDE.md with it. The context stays current without any manual upkeep.

**MCPs are the plumbing.** If scheduled tasks are the output layer and memory files are the context layer, MCPs (Model Context Protocols) are what connects the agent to the rest of your stack — PostHog, Slack, GitHub, and so on. PostHog even ships their own official MCP for Claude Code.

### Companies & Tools

- **PostHog**: Open-source product analytics platform I use daily. They also publish a PostHog MCP that plugs directly into Claude Code · [posthog.com](https://posthog.com)
- **Claude Code**: Anthropic's CLI for Claude. The AI coding tool I'm moving focus to after finding it more stable, polished, and secure than alternatives · [claude.ai/code](https://claude.ai/code)

### Resources

- [Making Claude Code Actually Useful](https://posthog.com/blog/making-claude-cowork-actually-useful) - PostHog's practical guide: context files, scheduled background tasks, and MCPs for getting real leverage from Claude Code
