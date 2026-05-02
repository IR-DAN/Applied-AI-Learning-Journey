# Applied AI Learning Diary

> A day-by-day record of my applied AI learning journey, shared openly to encourage others.
>
> *If we put in the time and effort, we can learn anything.*

---

## Table of Contents

- [May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful](#may-2-2026--why-github-over-notion-and-posthogs-guide-to-making-claude-code-actually-useful)
- [May 3, 2026 - How AI Is Changing the Product Manager's Job, and What to Do About It](#may-3-2026--how-ai-is-changing-the-product-managers-job-and-what-to-do-about-it)

---

## May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful

I decided to document my learnings in Applied AI and create a centralised place for all the resources, publicly available to everyone.

I went with GitHub over Notion because it's easier to distribute. People can follow the repo and get notified when things change. It also feels more techie and I like it here more than Notion.

My first documented learning is a blog post from **PostHog** on how to make Claude Code actually useful. I use PostHog a lot, basically daily, so when they wrote about their own experience adopting it I paid attention. Up until now I had been playing more with OpenClaw and its extensive possibilities, but Claude Code seems to be a superior solution in terms of stability, UX and security.

The article is written from a team context (the author is a manager at PostHog), but the setup is practical for anyone using Claude Code seriously. Here is what I took from it.

**Start by asking the agent what to use it for.** The single most useful thing the author did was ask Claude to come up with use cases for his specific job. Not "top AI use cases for managers" from some listicle, but literally: here is what I do, here is what my team does, here is what I care about, now tell me where you would actually help. That question alone surfaces things you would never think to ask for yourself. Generic advice is written for someone whose job is not your job, so it rarely lands right.

**Build context files before you do anything else.** Claude Code does not know anything about you by default. The author solves this with a set of markdown files the agent reads before every task. The main one is CLAUDE.md, which works like a personal index: who you are, your direct reports with their GitHub handles and Slack IDs, what you are currently focused on, and your preferences. Alongside that there is a glossary.md with company-specific acronyms and the Slack channels that matter. Without this layer, every conversation starts from zero. With it, the agent already knows your world before you type a single word.

**Scheduled tasks are more valuable than chat.** This one surprised me. The author uses Claude Code less as a chatbot and more as a background worker that runs tasks on a schedule. One example he shares: on the 8th of every month, a task reads a GitHub issue called "Things Charles cares about", a list he keeps updated with his current priorities, and uses it to refresh CLAUDE.md automatically. The context never goes stale and he never has to do it manually. The idea is that the agent is not just answering questions, it is doing work while you are doing other things.

**MCPs connect the agent to your actual stack.** MCP stands for Model Context Protocol and it is the layer that plugs Claude Code into the rest of your tools, PostHog, Slack, GitHub, whatever you use day to day. PostHog even ships their own official MCP so the agent can pull analytics data directly without you copying and pasting anything. Think of it as the difference between an assistant who only knows what you tell them in the moment, and one who can actually look things up in the systems you already use.

The article lists several concrete MCP use cases the author actually runs:

- **Slack: morning digest.** Every morning the agent surfaces Slack threads where the author was tagged but never replied, so nothing falls through the cracks without having to scroll back through the whole day.
- **GitHub: objectives coherence check.** Every Monday it pulls the quarterly objectives from around 50 teams out of the GitHub repo, reads them all in one pass, and flags contradictions or teams using the same word to mean different things. That would take hours to do manually.
- **GitHub: 1:1 prep.** Before each weekly 1:1, it searches every direct report's RFC and pull request activity for the week and writes the talking points directly into a subtask in the task manager, one per person.
- **PostHog MCP: customer lookups.** Any question like "who is the TAM for this customer?" goes through the PostHog MCP, which runs a SQL query against their data warehouse and returns the answer. No more digging through spreadsheets or pinging someone on Slack.
- **Linear / Notion: task writing.** The 1:1 prep output gets written straight into subtasks inside a recurring task in Linear or Notion, so the prep and the meeting notes live in the same place.
- **Calendar: scheduling tasks.** The agent can read your calendar and factor it into scheduling-related tasks, though the author mentions this one is less central to their setup than the others.

### People

- **Charles Cook**, VP Operations & Marketing at PostHog · [LinkedIn](https://www.linkedin.com/in/wololo/)

### Companies & Tools

- **PostHog**: Open-source product analytics platform I use daily. They also publish an official MCP that plugs directly into Claude Code · [posthog.com](https://posthog.com)
- **Claude Code**: Anthropic's CLI for Claude. The AI coding tool I am moving focus to after finding it more stable, polished and secure than alternatives · [claude.ai/code](https://claude.ai/code)

### Resources

- [Making Claude Code Actually Useful](https://posthog.com/blog/making-claude-cowork-actually-useful) - PostHog's practical guide to context files, scheduled background tasks and MCPs

---

## May 3, 2026 - How AI Is Changing the Product Manager's Job, and What to Do About It

I came across a guide on Every called "A Guide to Agent-native Product Management" by Marcus Moretti, who runs Spiral, Every's AI writing product, largely as a solo operator. The premise hit close to home: a lot of what product managers do every day is routine, screen-based work that LLMs can now do just as well or better. The question is what to do with the time that frees up.

The guide is built around a simple observation. In any software development cycle, product management mostly happens at two stages: planning and review. Marcus maps out how to hand those stages to AI agents, from writing your strategy all the way through to checking whether your shipped features are actually working. Here is what I found most useful.

**Strategy comes first, and an agent should interview you to write it.** Every other part of the process (feature ideas, prioritization, specs) only works well if your strategy document is solid. The strategy answers four things: what problem you are solving and how, who the product is for, how you measure success, and what the main tracks of work are. The recommended way to write it is not to sit down and write it yourself. You run a command, the agent asks you questions section by section, and out comes a strategy.md file. It works better than writing it solo because the agent has built-in guidance on what a good answer looks like and pushes back if you are being vague.

**Once your strategy is written, every other planning skill reads it automatically.** The guide describes a set of installable agent skills for ideating, brainstorming, planning and prioritizing. All of them pull from strategy.md as their grounding context before they do anything. That means you are not re-explaining your product to the agent every time you want to brainstorm a feature or write a spec. The strategy is the single source of truth and everything downstream inherits it.

**Prioritization runs as a daily command, not a quarterly meeting.** Instead of doing big prioritization exercises every few months, the workflow includes a /prioritize command that runs every day. Because the agent already knows your strategy and has access to your backlog, it can surface what matters right now without you needing to set up a scoring framework or run a meeting to align the team on it.

**Review is built into the loop, not bolted on at the end.** The guide includes a "product pulse" skill that checks your metrics after a feature has been live for a while. The output is a pulse report, and the planning skills are meant to read those reports when you kick off a new planning cycle. So the loop is genuinely closed: what you shipped and how it performed feeds directly into what you plan next, rather than sitting in an analytics tab that nobody checks.

**One person can run a full product with this setup.** Marcus mentions his own situation here. He handles product, coding, customer support and marketing for Spiral himself. The workflow does not replace the thinking, it handles enough of the mechanical work that one person can cover ground that would normally need a whole team behind it.

### People

- **Marcus Moretti**, GM of Spiral at Every · [Every Profile](https://every.to/@marcus_fd8302_1)

### Companies & Tools

- **Every**: Media and product company publishing writing about AI, tools and business. Home to Spiral and several newsletters by founders and operators · [every.to](https://every.to)
- **Spiral**: Every's AI co-writing product, built and run by Marcus as a solo operator

### Resources

- [A Guide to Agent-native Product Management](https://every.to/guides/ai-product-management-guide) - Marcus Moretti's practical guide to running the full PM workflow with AI agents: strategy, ideation, prioritization, specs and review
