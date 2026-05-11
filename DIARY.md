# Applied AI Learning Diary

> A day-by-day record of my applied AI learning journey, shared openly to encourage others.
>
> *If we put in the time and effort, we can learn anything.*

---

## Table of Contents

- [May 2, 2026 - Why GitHub Over Notion, and PostHog's Guide to Making Claude Code Actually Useful](#may-2-2026--why-github-over-notion-and-posthogs-guide-to-making-claude-code-actually-useful)
- [May 3, 2026 - How AI Is Changing the Product Manager's Job, and What to Do About It](#may-3-2026--how-ai-is-changing-the-product-managers-job-and-what-to-do-about-it)
- [May 3, 2026 - Qwen3.6-27B: Open Source Models Are Catching Up to Frontier Models Fast](#may-3-2026--qwen36-27b-open-source-models-are-catching-up-to-frontier-models-fast)
- [May 3, 2026 - DESIGN.md: Taking Control of How AI Builds Your UI](#may-3-2026--designmd-taking-control-of-how-ai-builds-your-ui)
- [May 3, 2026 - The Scaling Era: An Oral History of the Years That Shaped AI](#may-3-2026--the-scaling-era-an-oral-history-of-the-years-that-shaped-ai)
- [May 3, 2026 - Anthropic Analyzed 1M Claude Conversations. Here Is What People Actually Use It For](#may-3-2026--anthropic-analyzed-1m-claude-conversations-here-is-what-people-actually-use-it-for)
- [May 4, 2026 - Boris Cherny's One Book Recommendation: Functional Programming in Scala](#may-4-2026--boris-chernys-one-book-recommendation-functional-programming-in-scala)
- [May 4, 2026 - Google CodeWiki: Drop Any GitHub Repo and Walk Through It Visually](#may-4-2026--google-codewiki-drop-any-github-repo-and-walk-through-it-visually)
- [May 8, 2026 - HTML Might Be a Better Format Than Markdown for Storing Knowledge](#may-8-2026--html-might-be-a-better-format-than-markdown-for-storing-knowledge)
- [May 11, 2026 - OpenAI Daybreak: AI That Helps Defenders, Not Just Attackers](#may-11-2026--openai-daybreak-ai-that-helps-defenders-not-just-attackers)

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

---

## May 3, 2026 - Qwen3.6-27B: Open Source Models Are Catching Up to Frontier Models Fast

On April 22, Alibaba's Qwen team released Qwen3.6-27B. I caught it last week and it is worth documenting because it is one of those releases that makes you stop and think about how fast open source is moving.

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

---

## May 3, 2026 - DESIGN.md: Taking Control of How AI Builds Your UI

I came across a tweet from Mike Bespalov, the founder of Refero, that put something into words I had been feeling for a while.

"Agents make ugly UIs because they've never seen good design."

That is the problem. When you vibe code a UI and just let the AI decide, you get something generic. It is functional but it looks like every other AI-generated interface. The reason is not that the model is bad at code, it is that the model has no taste. It has never been trained to study what makes Stripe's UI feel trustworthy, or why Linear's spacing feels so clean. So it defaults to average.

The solution Mike built is a collection of 2,000 DESIGN.md files from the world's best products, structured for a model to read and understand before it writes a single line of UI code.

**What a DESIGN.md file actually is.** It is a single markdown file that describes your entire design system: colors, typography, spacing, components, dos and donts. The format is an open spec originally from Google Labs. When you drop a DESIGN.md into your project, Claude Code or Cursor reads it before generating any UI. Every component it creates follows the rules in that file. Instead of the agent inventing the design from scratch, it is working from a defined visual language.

**How Refero Styles works.** The site is a catalog of DESIGN.md files extracted from real products like Stripe, Linear, Notion, Figma and Vercel. You browse the catalog, pick the design style closest to what you want, drop the file into your project, and the agent generates UI that matches that aesthetic. You are no longer at the mercy of whatever the model decides looks good.

**There is also an MCP.** Refero ships an MCP so Claude Code can search the catalog directly in natural language. You describe the vibe you are going for and the agent finds the closest matching style and drops a generated DESIGN.md into your project before it starts building. That means the design language is locked in from the very first component.

The broader point here is about taste. As vibe coding gets easier, the people who put thought into design and take control of it will stand out. If everyone just lets the AI decide, everything ends up looking the same.

### People

- **Mike Bespalov**, Founder of Refero · [LinkedIn](https://www.linkedin.com/in/bespalov-mike) · [X](https://x.com/bbssppllvv)

### Companies & Tools

- **Refero Styles**: Catalog of 2,000 DESIGN.md files from top products, ready to drop into any AI coding project · [styles.refero.design](https://styles.refero.design)
- **Refero MCP**: MCP server that lets Claude Code search Refero's design catalog and generate a DESIGN.md for your project · [refero.design/mcp](https://refero.design/mcp)

### Resources

- [Refero Styles](https://styles.refero.design) - Browse and download DESIGN.md files from the world's best products
- [Original tweet by Mike Bespalov](https://x.com/bbssppllvv/status/2049924037111841027) - The post that introduced this resource

---

## May 3, 2026 - The Scaling Era: An Oral History of the Years That Shaped AI

I stumbled across Leopold Aschenbrenner's X account today. If you do not know who he is, his story is worth looking into. He graduated as valedictorian from Columbia at 19, went to work at OpenAI's Superalignment team, and was fired in April 2024 in circumstances that are still disputed. He says it was for raising security concerns about foreign espionage. OpenAI says it was for leaking information. After getting fired he wrote "Situational Awareness", a 165-page manifesto predicting AGI by 2027 that went viral and even got praised by Ivanka Trump. He then used that attention to launch a hedge fund called Situational Awareness LP. In under a year he grew it from $225 million to $5.5 billion. He is 24 years old.

On his account he was recommending a book called "The Scaling Era: An Oral History of AI, 2019-2025", published by Stripe Press in 2025. Leopold actually appears in the book himself as one of the people interviewed.

I probably will not have time to read the whole thing, but I want to know what is in it. History matters here. AI is moving so fast that without knowing where it came from it is hard to understand where it is going.

**What the book is.** The Scaling Era is by Dwarkesh Patel, host of the Dwarkesh Podcast, which is one of the most respected interview shows in the AI and technology space. Dwarkesh spent years doing deeply researched conversations with the people who built and shaped modern AI. This book is the curated highlights from those interviews, organised into a coherent narrative covering the years when scaling became the dominant paradigm in machine learning.

**Who is in it.** The interviews include Dario Amodei (CEO of Anthropic), Demis Hassabis (CEO of Google DeepMind), Ilya Sutskever (OpenAI cofounder), Sam Altman (CEO of OpenAI), Eliezer Yudkowsky (AI safety, MIRI), Mark Zuckerberg (CEO of Meta), Jan Leike (former OpenAI alignment lead), Carl Shulman, and Leopold himself. These are the people who were actually in the room during those years, talking in their own words about what they were thinking and doing.

**What it covers.** The period 2019 to 2025 is when scaling became consensus: more data, more compute, bigger models. The book traces how that hypothesis became institutional dogma, what it produced, and what it means for the future. It covers alignment and the risk of misaligned AI, what AGI might look like economically and socially, and where things go next. It also comes with 170+ definitions and visualisations, technical explainers, classic essays, and some unpublished interviews.

The reason I want to document this even if I do not read it cover to cover is that primary sources like this are rare. Most writing about AI history comes from journalists on the outside. This is the people who built it, in their own words.

### People

- **Leopold Aschenbrenner**, Founder and CIO of Situational Awareness LP, former OpenAI Superalignment researcher · [LinkedIn](https://www.linkedin.com/in/leopold-aschenbrenner/) · [X](https://x.com/leopoldasch)
- **Dwarkesh Patel**, Author of The Scaling Era, Host of the Dwarkesh Podcast · [LinkedIn](https://www.linkedin.com/in/dwarkesh-sp/)

### Companies & Tools

- **Situational Awareness LP**: Leopold's AI-focused hedge fund. Grew from $225M to $5.5B in under a year, concentrated in AI infrastructure and power
- **Stripe Press**: Stripe's publishing arm, known for high-quality books at the intersection of technology, business and ideas · [press.stripe.com](https://press.stripe.com)

### Resources

- [The Scaling Era: An Oral History of AI, 2019-2025](https://press.stripe.com/scaling) - Dwarkesh Patel, Stripe Press 2025. Oral history of the AI scaling era through interviews with Dario Amodei, Ilya Sutskever, Demis Hassabis, Sam Altman, Eliezer Yudkowsky, Mark Zuckerberg and others
- [Leopold's recommendation on X](https://x.com/leopoldasch/status/1976019603236307367)

---

## May 3, 2026 - Anthropic Analyzed 1M Claude Conversations. Here Is What People Actually Use It For

Two days ago Anthropic published a research paper on how people use Claude for personal guidance. They sampled 1 million Claude.ai conversations from March and April 2026 and used a classifier to find conversations where people were asking not just for information, but for a perspective on what they personally should do: should I take this job, should I move, how do I handle this conflict.

6% of all Claude conversations are this. That sounds small but think about the scale of Claude's usage. One in every sixteen conversations is someone using an AI as a life advisor.

**Where people go for help.** Over 75% of guidance conversations fell into four domains. The breakdown from the full chart (10 clusters, 37,657 conversations):

| Domain | Share | Topics covered |
|---|---|---|
| Health / Wellness | 27.2% | Test results, injuries, calories & macros |
| Professional / Career | 25.9% | Job search, career transitions, salary negotiation |
| Relationships | 12.3% | Communication, romantic interests, leaving abusive relationships |
| Financial | 10.9% | Debt, home purchase, retirement planning |
| Personal Development | 6.3% | Study habits, self-improvement, digital addiction |
| Spirituality | 4.4% | Divination, religious & spiritual practice |
| Legal | 4.2% | Real estate disputes, employment disputes |
| Consumer | 3.9% | Product comparison, rental & housing decisions |
| Parenting | 3.1% | Child caregiving, school behavior, education planning |
| Other | 1.9% | Travel, immigration, relocation |

**The sycophancy problem.** This is the part I found most interesting. Sycophancy is when an AI tells you what you want to hear instead of what is actually true or useful. On average across all guidance conversations, Claude was sycophantic 9% of the time. That is not terrible. But it broke badly in two categories: spirituality at 38% and relationships at 25%. One in four relationship conversations ended with Claude flattering the person rather than giving them an honest perspective.

The reason relationships are so bad is specific: users push back in relationship conversations more than any other domain, in 21% of cases versus 15% on average. And when a user pushes back, Claude's sycophancy rate doubles from 9% to 18%. The model folds under social pressure. That is a real problem when someone is deciding whether to leave an abusive relationship and Claude is just agreeing with whatever they say.

**What Anthropic did about it.** They used these findings to create synthetic training data specifically targeting relationship guidance scenarios, and used it to train Opus 4.7 and Mythos Preview (a new model name that appeared here for the first time). The result: Opus 4.7 shows roughly half the sycophancy rate of Opus 4.6 on relationship guidance, dropping from 10.7% to 4.8%. And that improvement generalised across all domains, not just relationships.

The thing I keep thinking about is the scale of this. Millions of people are going to AI for advice on their health, their career, their relationships, their money. Whether the AI agrees with them or tells them the truth actually matters for their lives.

### Companies & Tools

- **Anthropic**: The AI safety company behind Claude. They published this research openly, which is not something every lab would do · [anthropic.com](https://www.anthropic.com)

### Resources

- [How People Ask Claude for Personal Guidance](https://www.anthropic.com/research/claude-personal-guidance) - Anthropic's full research paper with methodology, charts, and findings on sycophancy
- [Anthropic's tweet announcing the research](https://x.com/anthropicai/status/2049927618397614466)

---

## May 4, 2026 - Boris Cherny's One Book Recommendation: Functional Programming in Scala

I came across a post from Ryan Peterman quoting Boris Cherny, the creator of Claude Code. Boris was asked for the one technical book that had the greatest impact on him as an engineer. His answer was Functional Programming in Scala.

I probably will not have time to read it any time soon, but when the person who built Claude Code tells you a book completely changed the way he thinks about coding, it deserves to be documented.

Here is what Boris said in full:

> "The one technical book I would recommend to everyone that has had the greatest impact on me as an engineer is Functional Programming in Scala. You're probably never going to use Scala day to day, but the way it teaches you to think about coding problems is just such a change from the way that most people were taught coding, either practically or in school. It's going to completely change the way that you code. I think in types when I code. The thing that matters in your code the most is the type signatures. This is more important than the code itself."

**What the book actually teaches.** The book is by Paul Chiusano and Rúnar Bjarnason, published by Manning. The core idea is that you should build programs using only pure functions, meaning functions with no side effects. Everything is a transformation of data through the type system. The book teaches you how to use and design type classes like Monoids and Monads, and how to let the types guide your implementation. The insight Boris is pointing at is that if you get the types right, the code almost writes itself. If you are fighting the types, you are probably solving the wrong problem.

This is not a Scala book in the sense that you need to use Scala. It is a book about a way of thinking. Boris built Claude Code in TypeScript, not Scala. But the mental model he carries, thinking in types first, code second, clearly comes from somewhere.

This is probably overkill for most people. It requires a real coding foundation to get anything out of it, and some would argue that as coding itself gets automated, going this deep into how to write code is no longer worth the time. Maybe they are right. But I think people who understand the underlying concepts, not just the syntax, are going to be incredibly favored going forward. Knowing why code works a certain way, even if you are not the one writing it, is a very different skill from just prompting an agent to build something.

### People

- **Boris Cherny**, Head of Claude Code at Anthropic, creator of Claude Code, ex-Principal Engineer at Meta · [LinkedIn](https://www.linkedin.com/in/bcherny/)
- **Ryan Peterman**, ex-Staff Engineer at Instagram, newsletter writer for engineers · [LinkedIn](https://www.linkedin.com/in/ryanlpeterman/)

### Resources

- [Functional Programming in Scala](https://www.manning.com/books/functional-programming-in-scala-second-edition) - Paul Chiusano and Rúnar Bjarnason, Manning. Boris Cherny's single most recommended technical book
- [Ryan Peterman's post quoting Boris](https://x.com/ryanlpeterman/status/2044408902763114650)

---

## May 4, 2026 - Google CodeWiki: Drop Any GitHub Repo and Walk Through It Visually

Google just released something I think is genuinely incredible. It is called Code Wiki and it is at codewiki.google. You drop any public GitHub repo into it and it generates a full interactive documentation site for that codebase, automatically. Architecture diagrams, visual walkthroughs, a chat agent that can answer questions about the code. All of it.

This is huge for anyone trying to understand an unfamiliar codebase, which is something that used to take days.

**What it actually generates.** For any repo you submit, Code Wiki produces architecture diagrams, class diagrams, and sequence diagrams that show how the different parts of the code relate to each other. It also produces module-by-module written walkthroughs. Every section links directly to the exact lines of source code it is describing, so you can jump straight from the explanation to the thing being explained.

**The Gemini chat agent.** On top of the generated documentation, there is a Gemini-powered chat interface where you can ask questions in plain language. Things like "how does authentication work in this repo?" or "which services depend on the user database?" and it answers using the wiki as context, with links to the relevant parts of the code. This is the part that changes how you onboard to a new codebase.

**Video explainers.** It also creates short video walkthroughs of how specific parts of the codebase work, with each frame linking to the exact source code line it is referencing. So you can watch it being explained rather than read through it.

**It stays current.** Every time a pull request is merged, the documentation updates automatically. So the wiki does not go stale the way every other documentation always does.

The use case I immediately thought of: any time you want to understand a tool or library you are using, or before you fork something, or when you are onboarding to a new project at work. You used to have to read through the code yourself or find someone to explain it. Now you just drop it in here.

### Companies & Tools

- **Google Code Wiki**: Google's free tool for turning any public GitHub repo into interactive, always-current documentation with diagrams, walkthroughs, and a Gemini chat agent · [codewiki.google](https://codewiki.google)

### Resources

- [Google Code Wiki](https://codewiki.google) - Drop any public GitHub repo and get architecture diagrams, module walkthroughs, video explainers, and a Gemini chat agent
- [Google Developers Blog announcement](https://developers.googleblog.com/introducing-code-wiki-accelerating-your-code-understanding/) - The original launch post from Google

---

## May 8, 2026 - HTML Might Be a Better Format Than Markdown for Storing Knowledge

I came across a post from Thariq Shihipar, who works on Claude Code at Anthropic, arguing that HTML is actually a superior format to Markdown for storing and presenting information. It made me stop and think seriously about this repo.

Right now everything here is Markdown on GitHub. It works, but it is flat. No real layout, no visual hierarchy beyond headings and bullets, no way to make things scroll nicely or feel designed. The post made me think about whether a scrollable hosted HTML website would be a better home for this diary long term.

**Why Markdown became the default.** Markdown won because it is simple to write, renders cleanly on GitHub, diffs well in version control, and is easy for AI agents to read. It removes the overhead of thinking about presentation and lets you focus on content. That is genuinely valuable, and it is why this repo started in Markdown.

**What HTML can do that Markdown cannot.** HTML gives you spatial control. You can add margin notes alongside paragraphs, render call-graphs as actual boxes and arrows showing how things relate, embed inline SVG diagrams that illustrate a concept visually, and build side-by-side comparisons. None of this is possible in plain Markdown. Markdown is linear, top to bottom, full stop. HTML can show relationships, not just describe them.

**Richness of representation.** A well-structured HTML page can have collapsible sections, sticky navigation, scroll-linked animations, highlighted callouts, tables that actually look like tables, and images that sit in context rather than breaking the flow. The reading experience is just fundamentally different. A diary like this one, where each entry is a self-contained learning moment, could be much more navigable as a scrollable web page with a sidebar than as a long flat Markdown file.

**The honest tradeoff.** Markdown is still better for writing quickly, for version control diffs, and for AI agents that parse content. HTML requires more upfront work and some design decisions. But if the goal is a knowledge base people actually enjoy reading, not just a file they can grep through, HTML wins.

I am genuinely considering moving this repo to a hosted HTML website. The content would stay the same but the experience of reading it would be much better.

### People

- **Thariq Shihipar**, Engineer on Claude Code at Anthropic, previously founded a YC-backed gaming company, MIT Media Lab · [LinkedIn](https://www.linkedin.com/in/thariqshihipar/) · [X](https://x.com/trq212)

### Resources

- [The Unreasonable Effectiveness of HTML](https://thariqs.github.io/html-effectiveness/) - Thariq Shihipar's post with examples of what HTML can express that Markdown cannot
- [Thariq's tweet](https://x.com/trq212/status/2052809885763747935)

---

## May 11, 2026 - OpenAI Daybreak: AI That Helps Defenders, Not Just Attackers

OpenAI announced Daybreak, a cybersecurity initiative built on the premise that defense should be designed into software from the start, not bolted on after a breach. They are pairing it with GPT-5.5-Cyber, a variant of GPT-5.5 with fewer guardrails, available to vetted cybersecurity teams through a new Trusted Access for Cyber program.

I could not be more excited about this. So much of the AI risk conversation has focused on what these models could do for attackers. Daybreak is the first major step I have seen toward saying the same capabilities have to be put in the hands of defenders, and that defenders need first-class tools too. We have to keep up with adversaries, which means our LLMs have to evolve in a way that helps the people protecting systems, not just the people probing them.

**What Daybreak actually is.** Daybreak is OpenAI's vision for changing how software is built and defended: see risk earlier, act sooner, make systems resilient by design. The pitch is that AI can let defenders reason across whole codebases, find subtle vulnerabilities, validate fixes, and analyse unfamiliar systems at a speed that closes the gap with offensive work. Use cases listed include secure code review, threat modeling, patch validation, dependency risk analysis, detection, and remediation guidance, all folded into the everyday development loop.

**GPT-5.5-Cyber is a less-restricted model for vetted teams.** This is the part most worth flagging. OpenAI is rolling out a version of GPT-5.5 with fewer guardrails specifically to approved cybersecurity teams in the highest tier of the Trusted Access for Cyber program. With it, defenders can hunt for bugs, study malware, and reverse engineer attacks without the model refusing to engage with the kind of content that security work requires. Standard public models block a lot of that on principle, which makes them useless for the people who actually need them.

**Anthropic Mythos came first by about a month.** This follows Anthropic's Mythos preview, which I noted in the May 3 entry on the 1M Claude conversations study. Two of the three frontier labs now have dedicated cybersecurity model tracks. That feels like a meaningful turning point for the field.

**The accountability layer is the catch.** Capabilities like this are dual-use. OpenAI is gating access through vetting, verification and proportional safeguards, and says it is working with industry and government partners as it deploys progressively more cyber-capable models. How well that gating holds up under real-world pressure is the open question.

If you work in security and want to keep up with where the tooling is going, this is the announcement to read.

### Companies & Tools

- **OpenAI Daybreak**: OpenAI's cybersecurity initiative around defense-by-design and AI-assisted vulnerability work · [openai.com/daybreak](https://openai.com/daybreak/)
- **GPT-5.5-Cyber**: A less-restricted variant of GPT-5.5 available to vetted security teams via OpenAI's Trusted Access for Cyber program
- **Anthropic Mythos**: Anthropic's dedicated cybersecurity model line, which debuted about a month earlier

### Resources

- [Daybreak: OpenAI for cybersecurity](https://openai.com/daybreak/) - The official Daybreak page
- [Scaling Trusted Access for Cyber with GPT-5.5 and GPT-5.5-Cyber](https://openai.com/index/gpt-5-5-with-trusted-access-for-cyber/) - The OpenAI post detailing the tiered access program
- [CNBC: OpenAI rolls out new GPT-5.5-Cyber to vetted teams](https://www.cnbc.com/2026/05/07/openai-rolls-out-new-gpt-5point5-cyber-to-vetted-cybersecurity-teams.html) - News coverage of the GPT-5.5-Cyber release
