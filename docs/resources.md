---
title: Resources
nav_order: 6
has_toc: true
permalink: /docs/resources/
---

# Resources
{: .no_toc }

Tools, links, communities, prompting patterns, and a glossary of every term that confused me the first time I hit it.
{: .fs-5 .fw-300 }

<details markdown="block">
<summary><strong>Table of contents</strong></summary>

1. TOC
{:toc}

</details>

---

## Tools (in the order you'll meet them)

### For chatting with Claude

| Tool | What | Why | Cost |
|---|---|---|---|
| [Claude.ai](https://claude.ai) | Web app to chat with Claude | Best for first-time users. No install. | Free tier; Pro $20/mo |
| [Claude Desktop](https://claude.ai/download) | Desktop app to chat with Claude | Same as Claude.ai but feels more like a real tool. Connects to file system. | Same as above |

### For building with Claude

| Tool | What | Why | Cost |
|---|---|---|---|
| [Claude Code](https://claude.ai/code) | Terminal-based AI agent | **What this guide teaches.** Anthropic's official agent. You give it a goal, it figures out the steps. Used to build Call Intelligence. | Subscription via Claude.ai (Pro $20/mo) or pay-per-use via API |
| [Cursor](https://cursor.com) | AI code editor (GUI) | Alternative if you prefer a visual editor over the terminal. Familiar feel if you've ever seen VS Code. | Free tier; Pro $20/mo |
| [VS Code](https://code.visualstudio.com) | General-purpose code editor | Useful as a "visual companion" alongside Claude Code, see your file tree and read code with syntax highlighting. | Free |
| [Anthropic Console](https://console.anthropic.com) | Get an API key, monitor usage | Required for any code that *calls* Claude programmatically (your scripts, not your dev tool) | Pay-per-token; pennies for small projects |
| [OpenRouter](https://openrouter.ai) | One API for many LLMs | Useful when you want to swap models without changing code | Pay-per-token; transparent pricing dashboard |

### For storing data

| Tool | What | Why | Cost |
|---|---|---|---|
| [Supabase](https://supabase.com) | Postgres + auth + storage, hosted | Default database for small teams. Free tier covers most personal projects. | Free tier; Pro $25/mo |
| [Neon](https://neon.tech) | Serverless Postgres | Alternative to Supabase if you want pure Postgres without the extras | Free tier; pay-as-you-go |

### For running scheduled jobs and background work

| Tool | What | Why | Cost |
|---|---|---|---|
| [Vercel Cron](https://vercel.com/docs/cron-jobs) | Scheduled HTTP requests to your own API routes | **What Call Intelligence uses.** Lowest-overhead path: add a `crons` array to `vercel.json` and Vercel pings your endpoints on the schedule. Built into Vercel hosting. | Included in Vercel hosting tiers |
| Webhooks (provider-specific) | Source system POSTs to your URL on events | **What Call Intelligence uses for Fireflies.** Real-time ingestion when the source supports it. Each integration is custom. | Free (you build the receiver) |
| [Inngest](https://www.inngest.com) | Job scheduler + workflow engine | Used elsewhere in Base Camp (CRM workflows, deal sync). Worth graduating to when you need retries, parallelism, or a debug UI for complex orchestration. | Free tier; paid above 50k runs/mo |
| [Trigger.dev](https://trigger.dev) | Alternative to Inngest | Similar, different style. Worth comparing if Inngest doesn't fit. | Free tier; paid above limits |

### For hosting your app

| Tool | What | Why | Cost |
|---|---|---|---|
| [Vercel](https://vercel.com) | Next.js hosting | Push to GitHub → auto-deploy. Easiest path. | Hobby tier free; Pro $20/mo |
| [Netlify](https://netlify.com) | Alternative to Vercel | Older, similar feel | Free tier; Pro $19/mo |
| [Railway](https://railway.app) | Full-stack hosting incl. databases | Useful if you want everything in one place | Pay-as-you-go |

### For version control

| Tool | What | Why | Cost |
|---|---|---|---|
| [GitHub](https://github.com) | Where your code lives | The default. Free for public and personal projects. | Free for individuals |
| [GitHub Desktop](https://desktop.github.com) | Visual git client | Way friendlier than the command line for beginners | Free |

### For "the polish"

| Tool | What | Why | Cost |
|---|---|---|---|
| [Tailwind CSS](https://tailwindcss.com) | Utility-first CSS framework | What Claude defaults to. Quick polished UIs. | Free |
| [shadcn/ui](https://ui.shadcn.com) | Copy-paste UI components | Most popular React component set. Looks professional out of the box. | Free |
| [Lucide](https://lucide.dev) | Icon set | Clean, consistent icons. | Free |
| [Plausible](https://plausible.io) / [PostHog](https://posthog.com) | Privacy-friendly analytics | Know who uses your tool and how | Plausible $9/mo+; PostHog has free tier |

---

## Recommended reading

For the absolute beginner who finished the 101 and wants to think about what they're doing:

- 🎥 **[Every Level of Claude Code Explained in 39 Minutes](https://www.youtube.com/watch?v=Y09u_S3w2c8)**, The single most useful Claude Code video I've found. Walks through Claude Code at increasing levels of depth, from "I just installed it" to "I'm running it as an agent on my codebase." Worth watching all the way through.
- **[Anthropic's "Prompt Engineering" guide](https://docs.anthropic.com/claude/docs/intro-to-prompting)**, Official, short, useful.
- **[How I use AI to write code](https://crawshaw.io/blog/programming-with-llms)** by David Crawshaw, A working engineer describes the actual workflow.
- **[Simon Willison's blog](https://simonwillison.net/)**, Best running commentary on LLM tooling. Skim the tag for "llm-tools".
- **[Geoffrey Litt, Malleable software](https://www.geoffreylitt.com/)**, Why this is a bigger shift than tutorials let on.

For the 201/301 reader who's actually building things:

- **[Next.js Learn](https://nextjs.org/learn)**, Official Next.js tutorial. Do this if you want one structured walkthrough.
- **[Supabase docs](https://supabase.com/docs)**, Genuinely good. The "build a database" guide is enough to start.
- **[Just enough TypeScript](https://www.totaltypescript.com/)** by Matt Pocock, Free intros that actually click.
- **[The Pragmatic Engineer](https://www.pragmaticengineer.com/)**, Newsletter on how real software teams work. Read it to understand the industry around you.

For the CS leader thinking about *why* this tool exists in the first place:

- **[How to Create an Effective Feedback Loop Between Customer Success and Product Teams](https://gaingrowretain.com/kb/articles/116-how-to-create-an-effective-feedback-loop-between-customer-success-and-product-teams)**, I wrote this for [Gain Grow Retain](https://gaingrowretain.com) in 2023, back when I was Director of Success at LiveSchool. It walks through the manual playbook we built using [Canny.io](https://canny.io), centralizing requests, setting a monthly cadence with Product, training the whole company to log things in one place. **Read this first for the human-driven version of the feedback loop, then come back here for the automated next step.**

---

## Communities

- **[Claude Discord](https://discord.com/invite/anthropic)**, Active, friendly, lots of people building.
- **[r/ClaudeAI](https://reddit.com/r/ClaudeAI)**, Casual discussion, tips, gotchas.
- **[Cursor Discord](https://discord.com/invite/cursor)**, Cursor-specific questions, often answered by Cursor staff.
- **[Indie Hackers](https://www.indiehackers.com)**, For when you start thinking *"what if I shipped this as a product"*.

---

## Prompting patterns that work for me

A few patterns I use over and over. None of these are revolutionary. The combination is what matters.

### "Walk me through it before writing code"

When starting anything non-trivial:

> Before writing any code, walk me through the design. What files do you plan to create? What's the data model? What's the API surface? What are the trade-offs?

This catches a huge fraction of "Claude built the wrong thing" failures.

### "Don't write the whole thing at once"

For multi-file work:

> Walk me through it file by file. Show me each one before applying. I want to understand what's happening as we go.

Lower-context LLM runs sometimes try to write the whole feature in one go. Slowing it down forces you to actually read along.

### "Pretend I'm a beginner"

When the response uses jargon you don't follow:

> Re-explain that as if I've never written code before. What does [term] mean? Why do we need it?

Claude is happy to do this. It's the single best way to learn the vocabulary.

### "Show me an example before generalizing"

When designing a schema or API:

> Before writing the schema, give me 3 example rows of what the data would look like, in JSON. I want to see what I'm describing before we make it abstract.

This is the design-by-example pattern from the [101](../101-your-first-ai-tool/#step-3-iterate--make-the-output-better) applied to bigger things.

### "What would you do differently if this had to scale to 100,000 users?"

When you want to think ahead:

> Right now this is a personal tool. What would change if this had to handle 100,000 users? Don't change the code yet, just tell me what the major issues would be and how I'd address each.

You learn architecture patterns by hearing what *would* break. Way more efficient than building it and watching it fail.

### "What's the dumbest possible version?"

When scope is creeping:

> What's the simplest version of this feature that gets 80% of the value? I want to start there.

Almost always, the dumbest version is enough. The complicated version is for later.

---

## Glossary

Terms I tripped on. Defined casually.

**API**, A way for code to talk to other code. When Claude has an "API," it means there's a URL you can send text to and get a response back. Same idea for HubSpot, Fireflies, Slack, etc.

**Auth / OAuth**, Authentication: proving who you are. OAuth specifically: a standard way to let "App A" act on your behalf in "App B" without giving away your password. Google sign-in is OAuth.

**Backend / Frontend**, Frontend is what runs in the user's browser (the page, the buttons). Backend is what runs on a server (database queries, sensitive logic, API calls to other services). In Next.js they're in the same project, but conceptually split.

**Cron / Scheduled job**, Code that runs on a schedule, not in response to a user action. "Every 6 hours, fetch new transcripts" is a cron job.

**Database migration**, A script that changes the structure of your database (add a column, create a table, etc.). Migrations get committed to your repo so the changes are tracked.

**Embedding / Vector**, A numeric representation of a piece of text that captures its meaning. Two texts with similar meaning have similar vectors. Used for "find similar items" features (like dedup).

**Environment variable**, A piece of config (like an API key) stored *outside* your code. Lives in a `.env` file locally and in your hosting platform's settings in production. Keeps secrets out of git.

**Inngest / Job queue**, A service that lets you write functions and have them run on a schedule, in response to events, or in the background. Handles retries and parallelism. Heavier than Vercel Cron; worth it for complex orchestration.

**JSON**, A simple text format for structured data. What Claude outputs when you say "return as JSON." Looks like `{"key": "value", "list": [1, 2, 3]}`.

**Migration**, See "Database migration."

**Node.js**, The runtime that lets you run JavaScript on your computer (instead of just in a browser).

**npm / pnpm / yarn**, Package managers. They install the libraries your code depends on. `npm install` reads `package.json` and downloads everything.

**Next.js**, The most popular React framework. Lets you write both the UI and the API in the same project.

**Postgres**, A relational database. Storage for structured data. Supabase is built on Postgres.

**Prompt**, The text you send to Claude. The art of writing prompts well is "prompt engineering."

**React**, The most popular JavaScript library for building UIs. Components, state, props. Next.js is built on React.

**Repo / Repository**, A folder of code tracked by git. Usually pushed to GitHub.

**REST API**, The most common style of API. URLs like `GET /features/123` or `POST /features`. Most third-party services (HubSpot, Fireflies, etc.) provide REST APIs.

**Row-Level Security (RLS)**, A Postgres feature that enforces per-row access rules inside the database. "Users can only read rows they own." Critical for multi-user apps.

**Schema**, The shape of your data. What tables exist, what columns each has, what types they hold.

**SDK**, A library that wraps an API in a convenient interface. `@anthropic-ai/sdk` is the official SDK for Claude, easier than calling the raw API yourself.

**Supabase**, Hosted Postgres + auth + storage. The default "backend in a box" for personal-scale projects.

**Token**, Roughly, a chunk of text (about ¾ of a word). LLMs charge by token, both for input and output.

**TypeScript**, JavaScript with types. Lets the editor catch errors before you run the code. Slightly more setup, much fewer bugs.

**Vercel**, A hosting platform that auto-deploys Next.js apps from GitHub. Push to main → live in 60 seconds.

**Vercel Cron**, A scheduling feature built into Vercel hosting. You add a `crons` array to `vercel.json` listing `path` + `schedule` pairs, and Vercel pings those URLs on the schedule. The handler is just a regular API route. Simplest cron path on Vercel.

**Webhook**, An API in reverse: when something happens in another system (a new Fireflies call, a HubSpot deal update), they call *your* URL to notify you. The opposite of polling.

---

## Models I use, and when

You don't need to think about this in the 101 or 201. By the time you're in the 301 it starts to matter.

| Use case | Model | Why |
|---|---|---|
| Extraction from transcripts (high volume) | Claude Haiku 4.5 | Fast, cheap, good enough for structured extraction |
| Deduplication judgment (low volume, high stakes) | Claude Sonnet 4.6 | More accurate on subtle "are these the same thing" judgments |
| Code generation in Claude Code | Claude Sonnet 4.6 or Opus 4.7 | Worth paying for the better reasoning |
| Quick one-off chat ("what does this error mean") | Whatever's default | Doesn't matter for ad hoc questions |

These will change as new models ship. Anthropic releases a new model every few months. **The pattern stays the same: cheap-and-fast for high-volume routine work, smart-and-expensive for low-volume judgment work.**

---

<div style="display: flex; justify-content: space-between; margin-top: 3em;">
<a href="../case-study/">← Case Study</a>
<a href="../../">Home →</a>
</div>
