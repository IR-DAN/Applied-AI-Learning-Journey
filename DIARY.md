# Applied AI Learning Diary

> A day-by-day record of my applied AI learning journey, shared openly to encourage others.
>
> *If we put in the time and effort, we can learn anything.*

---

## Table of Contents

- [May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful](#may-2-2026--why-github-over-notion-and-posthogs-guide-to-making-claude-code-actually-useful)
- [May 3, 2026 - How AI Is Changing the Product Manager's Job, and What to Do About It](#may-3-2026--how-ai-is-changing-the-product-managers-job-and-what-to-do-about-it)
- [May 3, 2026 - Qwen3.6-27B: Open Source Models Are Catching Up to Frontier Models Fast](#may-3-2026--qwen36-27b-open-source-models-are-catching-up-to-frontier-models-fast)

---

## May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful

I decided to document my learnings in Applied AI and create a centralised place for all the resources, publicly available to everyone.

I went with GitHub over Notion because it's easier to distribute. People can follow the repo and get notified when things change. It also feels more techie and I like it here more than Notion.

My first documented learning is a blog post from **PostHog** on how to make Claude Code actually useful. I use PostHog a lot, basically daily, so when they wrote about their own experience adopting it I paid attention. Up until now I had been playing more with OpenClaw, but Claude Code seems to be a superior solution in terms of stability, UX and security.

Here is what I took from it.

**Start by asking the agent what to use it for.** Ask Claude to come up with use cases for your specific job, not some generic listicle. What do you do, what does your team do, what do you care about. That question alone surfaces things you would never think to ask for yourself.

**Build context files before you do anything else.** The author keeps a CLAUDE.md as a personal index: who he is, his team's GitHub handles and Slack IDs, current focus areas, preferences. And a glossary.md for company-specific terms. Without these, every conversation starts from zero.

**Scheduled tasks beat on-demand chat.** He uses Claude Code less as a chatbot and more as a background worker. Example: on the 8th of every month a task reads a GitHub issue of his current priorities and refreshes CLAUDE.md automatically. No manual upkeep.

**MCPs connect the agent to your actual stack.** MCP (Model Context Protocol) is the layer that plugs Claude into your tools: PostHog, Slack, GitHub, whatever you use. PostHog even ships their own official MCP. Use cases the author actually runs:

- **Slack: morning digest.** Surfaces threads where he was tagged but never replied.
- **GitHub: objectives coherence check.** Every Monday, pulls quarterly objectives from ~50 teams and flags contradictions or conflicting language.
- **GitHub: 1:1 prep.** Searches each direct report's RFC and PR activity for the week and writes talking points directly into the task manager.
- **PostHog MCP: customer lookups.** "Who is the TAM for this customer?" runs a SQL query against the data warehouse and returns the answer instantly.
- **Linear / Notion: task writing.** Writes the 1:1 prep output directly into subtasks of a recurring task.
- **Calendar: scheduling.** Can read your calendar for scheduling-related tasks, though less central than the others.

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

---

## May 3, 2026 - Qwen3.6-27B: Open Source Models Are Catching Up to Frontier Models Fast

A week ago, on April 22, Alibaba's Qwen team released Qwen3.6-27B. I only caught it today and it is worth documenting because it is one of those releases that makes you stop and think about how fast open source is moving.

The short version: a 27 billion parameter model is now matching or beating models that are 14 times its size, and it is doing it on the kind of coding benchmarks that matter for real work. It is free to download, modify and deploy under the Apache 2.0 license. No API fees, no usage restrictions.

**What the benchmarks actually say.** On SWE-bench Verified, which tests whether a model can resolve real GitHub issues in real codebases, Qwen3.6-27B scores 77.2%. Claude Opus 4.6 scores 80.8%. That is a gap of 3.7 points between a fully open model you can run locally and Anthropic's current flagship. On Terminal-Bench 2.0, Qwen3.6-27B scores 59.3%, which is exactly the same as Claude 4.5 Opus. The most striking number is SkillsBench: 48.2% versus 30.0% for Alibaba's own previous 397B model. It scores 77% higher on coding tasks with 14.8 times fewer parameters.

One caveat worth keeping in mind: there have been proven cases of Chinese AI labs fine-tuning or pre-training their models specifically to score well on the benchmarks they then publish. The numbers look impressive, but they may not fully reflect how the model actually performs on real-world tasks outside of those tests. I am taking these results as a directional signal, not gospel. The honest test is using the model yourself.

**It is fully dense, not a mixture of experts.** A lot of large models save on compute by using a mixture-of-experts architecture, where only a fraction of the total parameters activate on any given input. Qwen3.6-27B does not do that. All 27 billion parameters run on every inference pass. Dense models are easier to fine-tune and behave more consistently than MoE models. The tradeoff is that they cost more to run per token, but at 27B on a single high-end GPU that cost is manageable.

**Thinking Preservation is the new capability to watch.** The model keeps its reasoning trace across multi-turn conversations. In a normal setup, each conversation turn starts fresh and the model reasons from scratch each time. With Thinking Preservation, the chain of thought from the previous turn carries over. This matters a lot for agentic workflows where the model is working through a problem over many steps. It is described as the first open-source model to introduce this, which means it was previously something only proprietary models could do.

**The context window is massive.** Native context is 262,144 tokens and it can be extended to 1,010,000 tokens. It also supports text, image and video inputs natively. Free, open, multimodal, and a million-token context window is a combination that did not exist in open source until now.

The bigger picture is that the gap between the best open source models and frontier proprietary models is closing faster than most people expected. This is a theme I want to keep tracking in this diary.

### Companies & Tools

- **Qwen (Alibaba)**: Alibaba's open-source AI research lab behind the Qwen model family, consistently releasing competitive open-weight models that challenge the proprietary frontier · [qwenlm.github.io](https://qwenlm.github.io)
- **HuggingFace**: Where the Qwen3.6-27B weights are hosted, free to download · [huggingface.co/Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)

### Resources

- [Qwen3.6-27B on HuggingFace](https://huggingface.co/Qwen/Qwen3.6-27B) - Model weights, architecture details and usage instructions
- [Qwen Blog: Qwen3.6-27B](https://qwen.ai/blog?id=qwen3.6-27b) - Official release post from the Qwen team
