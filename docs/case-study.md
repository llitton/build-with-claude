---
title: Case Study — Call Intelligence
nav_order: 5
has_toc: true
permalink: /docs/case-study/
---

# Case Study: How Call Intelligence got built
{: .no_toc }

A linear story of how a non-engineer (me, Laura) turned a frustrating manual workflow into a tool the product team uses every week. Real timeline, real mistakes, real prompts.
{: .fs-5 .fw-300 }

<details markdown="block">
<summary><strong>Table of contents</strong></summary>

1. TOC
{:toc}

</details>

---

## The problem (before I built anything)

I work at [LiveSchool](https://liveschoolinc.com), an EdTech company. We make a behavior management tool used by hundreds of K-12 schools. Like every SaaS company, we have customer success calls, support tickets, NPS surveys, sales conversations. Customers told us what they wanted constantly.

**And we kept losing it.**

A principal would mention on a renewal call that they desperately needed a custom date range in reports. The CS manager would say *"oh yeah, we've heard that a lot."* It would never reach the product team. Or it would, but with no count, no evidence, no list of which other customers had said the same thing. Product would prioritize based on the loudest internal voice rather than the data.

Our customer-facing teams were a black hole. Customers shouted requests in. Insights came out only when someone happened to remember them.

I wanted to fix that. I'm not a software engineer. I knew SQL well enough to write a basic query and HTML well enough to embarrass myself. **I had never built anything close to what Call Intelligence is now.**

---

## Phase 1: Claude Desktop, by hand (2 weeks)

The first version of Call Intelligence wasn't software. It was a habit.

Every week, our CS team had 30-40 calls. We were already getting auto-generated transcripts from [Fireflies AI](https://fireflies.ai). I opened Claude Desktop, copied a transcript in, and typed something close to what's in [the 101 page](../101-your-first-ai-tool/#step-2-your-first-extraction):

> Extract every distinct feature request, bug, or piece of feedback from this transcript. Return as JSON with type, summary, detail, urgency, category, quote.

I did that for two weeks. Maybe 60 calls total, by hand, in a Notion page.

**Two weeks in, I had something the product team had never seen before.** A list of *every customer ask*, with the customer quoted verbatim, grouped by theme. I shared it in our weekly product meeting. Half the asks were ones the team had never heard of. **That's when I knew it was worth building.**

{: .story }
> **The lesson:** I almost skipped this phase. I almost jumped straight into "build a real tool." If I had, I would have built the wrong tool — I would have optimized for things that turned out not to matter (which sources to ingest, what fields to extract) and missed the things that *did* matter (deduplication, source linking, presenting evidence cleanly). Two weeks of doing it by hand is what told me what to build.

---

## Phase 2: The first script (one weekend)

The manual workflow didn't scale. Fireflies was producing more transcripts than I could process by hand, and my Notion page was a mess.

That weekend I:

1. Asked Claude (in Claude Desktop) to teach me about the Fireflies API
2. Got a Claude API key from `console.anthropic.com`
3. Installed Cursor
4. Asked Cursor to write me a Node script that:
   - Pulled the last 50 Fireflies transcripts via their API
   - Ran each through the same prompt I'd been using by hand
   - Dumped the results into a CSV

**The first version was about 80 lines of code.** It took me about 6 hours to get it working end-to-end, including the 4 hours I spent confused about why my `.env` file wasn't being read. (Spoiler: it was named `env`, not `.env`. The leading dot matters.)

I ran the script. It produced a 400-row CSV. I opened it in Google Sheets. I shared the sheet in our #product channel.

People lost their minds. *"How did you make this? Can we filter by school?"* The script ran once, by hand, on my laptop. There was no app. There was no dashboard. It was a CSV. It was already useful enough to be a thing people wanted.

![Placeholder: screenshot of the very first features.csv in Google Sheets](../assets/images/case-study-first-csv-placeholder.png)
*Add screenshot here: the first features.csv. Crude. Useful.*

---

## Phase 3: The first dashboard (a week of evenings)

A CSV in Google Sheets is fine for a week. Then people want filters, sorting, the ability to mark features as "shipped" or "in progress," a place to add comments.

I asked Cursor to:

1. Spin up a Next.js app
2. Use Supabase as the database (replacing the CSV)
3. Create the basic tables: `features` and `mentions`
4. Build a one-page dashboard listing features sorted by mention count

This took me about 8 evening-hours total over a week. **I had never touched Next.js or Supabase before.** Cursor walked me through every step.

By the end:

- Live URL on Vercel
- Google sign-in (only `@liveschoolinc.com` could log in)
- A table of features with mention counts, last-seen date, source links, and category filters

I posted the URL in #product. Within 48 hours, three different teams were using it.

{: .story }
> **The lesson:** I had a small panic-attack moment in week two when somebody asked me to "add a way to assign features to product managers." It sounded like a "real software" feature. I assumed it would take me weeks. It took me 45 minutes. Cursor scaffolded a `owner_id` column, a select dropdown, an API route to update it, and the UI to show owners in the dashboard. **Everything in software seems harder from the outside than it is from the inside, once you have Claude.**

---

## Phase 4: More sources, more pain (a month)

Fireflies covered customer success calls. But customers also send us:

- HubSpot emails (sales + CS threads)
- Intercom chats (in-product support)
- NPS surveys (every quarter, every customer)

Each one needed its own ingestion. Each had its own API, its own auth, its own pagination quirks. Each needed its own `*_sync_state` table to track where the last sync left off.

This was the slog phase. The phase where you realize software has a long tail of integration boilerplate. **Pulling data out of other systems is most of the work in building a system.**

I did this incrementally, one source per weekend:

- **Weekend 1**: HubSpot email sync. The HubSpot API for searching email threads is confusing. Took me longer than expected. Claude walked me through it but I had to actually understand the data model to get it right.
- **Weekend 2**: Intercom sync. Easier — their API is cleaner.
- **Weekend 3**: NPS survey ingestion. Different shape (single short text response, not a transcript), so the extraction prompt had to change. I added a `source_type` field that flows through to the prompt selection.

By the end of the month, four sources flowed in automatically every 6 hours via Inngest. **The dashboard now had ~10,000 mentions in it.**

That was the moment deduplication stopped being optional.

---

## Phase 5: Deduplication (the hardest two weeks)

With 10,000 mentions, you don't have a feature list. You have noise.

The same feature — *"parents want to see their child's full point history"* — was mentioned in 47 calls, 32 emails, 8 chats, and 14 surveys. Each was a separate row. The dashboard showed 100 entries that were all the same thing.

I asked Claude to design a dedup system. Here's the actual chat history from that conversation, paraphrased:

> **Me:** I have 10,000 mentions. Many are about the same underlying feature. I need to deduplicate them. What's the right approach?
>
> **Claude:** A few options, depending on how much LLM cost you want to spend. Cheapest is fuzzy string matching. Most accurate is calling an LLM for every pair. Best balance is usually: embed every summary with a vector model, find nearest neighbors with a similarity threshold, then run an LLM judgment only on the top few candidates per mention. Want me to walk through each?
>
> **Me:** Yes, walk through all three with pros, cons, and rough cost at our scale.

That conversation led to the two-stage approach described in [the 301 page](../301-build-the-real-thing/#two-stage-deduplication). It took two weeks of evenings to:

- Add pgvector embeddings to every feature summary
- Build the candidate-finding query
- Build the LLM judgment prompt and parser
- Build the triage UI for the "maybe" band

The triage UI was the unexpectedly satisfying part. I'd sit down with a coffee, click through 20 candidate pairs, and the dashboard would compress by 200 mentions. Every session made the data cleaner.

![Placeholder: screenshot of the dedup triage UI](../assets/images/case-study-dedupe-triage-placeholder.png)
*Add screenshot here: the dedup triage UI. Two cards side by side. Three buttons: merge, keep separate, skip.*

{: .story }
> **The lesson:** I tried to be clever first. My initial dedup attempt was "ask Claude to look at every new mention and pick the matching feature from a list of 500 options." It was slow ($$$) and wrong (it would invent matches that weren't there). Embedding-based pre-filtering — boring, mechanical, well-understood — outperformed the clever version by every metric. **The boring solution usually wins.**

---

## Phase 6: Polish, integrations, Slack

The system was working. Now it had to fit into how the team actually worked.

- **Slack notifications** when a feature crosses 5, 10, or 25 mentions
- **Email integration** so the team could send "we shipped what you asked for" announcements directly from the feature detail page
- **Owner assignment** so each feature has a product manager attached
- **Status workflow** (new → considering → planned → shipped)
- **Customer-facing announcements** for shipped features

Each of these was one to three evenings. The codebase had grown to maybe 5,000 lines but felt manageable because I knew the shape — I could ask Cursor to find the right file and modify it, and it could.

This phase taught me the most about code organization. Earlier I had everything jammed in one folder; refactoring it into `lib/call-intelligence/{fireflies, hubspot, intercom, gmail, slack, features, nps, autopilot}/` happened during this phase, mostly at Cursor's suggestion.

---

## Where it is today

- **16 Postgres tables** (`ci_*` prefix, plus shared CRM tables)
- **4 active data sources** with scheduled sync every 6 hours
- **~50,000 mentions** processed, deduplicated into ~3,500 canonical features
- **Used weekly** by product, customer success, and sales teams
- **~$40/month** in LLM costs (OpenRouter, mostly Haiku for extraction, Sonnet for dedup judgment)
- **~$25/month** in hosting (Vercel + Supabase + Inngest)

It's not a moonshot. It's a real internal tool that produces real decisions every week. **That's the bar I wish people aimed at more.**

---

## What I'd do differently

A few things, in order of how much pain they would have saved me.

### 1. Start with the data model, not the UI

I spent the first weekend on a beautiful dashboard with data that didn't fit it. The schema kept changing. The dashboard kept breaking. **Spend the first day asking Claude to design the schema. Argue with it. Push back on every choice.** Once the schema is right, the UI becomes obvious.

### 2. Set up TypeScript and tests on day one

I didn't. I told myself "I'll add them later when it matters." That was wrong. By the time it mattered, retrofitting them was painful. **Ask Cursor to scaffold TypeScript + a basic test setup as part of your initial project structure.** It's two prompts. It'll save you a month of confidence-erosion later.

### 3. Build the "what's broken right now" view before you have things break

A sync job that silently fails for three days is a special kind of pain. I added a sync health dashboard much too late — after I'd already missed data twice. **As soon as you have a scheduled job, ask Claude to add a "sync runs" table and a page that shows status.**

### 4. Don't trust your own dedup eyeballs

I spent a long time tweaking similarity thresholds based on "what feels right." It would have been more efficient to dump 200 candidate pairs into a spreadsheet, mark each one "match / not / unsure" myself, and use *that* to calibrate. **Build a labeled eval set for any subjective judgment in your system.**

### 5. Don't put off the integrations that scare you

I dragged my feet on HubSpot for two weeks because their API documentation was confusing. When I finally sat down with Cursor and asked it to walk through the doc, the integration was done in three hours. **Things look scarier from the outside than they are from the inside, every time.**

---

## What I want you to take from this

Three things:

1. **The hardest part is starting.** Two weeks of pasting transcripts into Claude Desktop by hand is what told me what to build. If I'd skipped that I would have built the wrong thing.

2. **Direction beats expertise.** I am not a software engineer. Cursor and Claude wrote essentially all the code. My job was to know what I wanted and to recognize when the output was wrong. That's a skill anyone can learn.

3. **Internal tools are the right starting place.** Don't try to build the next Notion. Build the thing your own team needs that's currently a manual Google Sheet. Internal tools have a forgiving user base (your coworkers), a defined problem (the manual thing they hate), and a fast feedback loop (you sit next to them). **They're the perfect on-ramp.**

If you've read this far, go back to the [101](../101-your-first-ai-tool/) and start. The hard part isn't the code.

---

<div style="display: flex; justify-content: space-between; margin-top: 3em;">
<a href="../301-build-the-real-thing/">← 301</a>
<a href="../resources/">Resources →</a>
</div>
