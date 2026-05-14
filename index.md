---
title: Home
layout: home
nav_order: 1
description: "A complete beginner's guide to building real AI tools by talking to Claude. Featuring the story of Call Intelligence."
permalink: /
---

# You don't need to know how to code.
{: .fs-9 }

I'm the VP of Success at an EdTech company. A year ago, I'd never written a real program. Today, the tool I'm about to show you — **Call Intelligence** — reads every customer call, extracts every feature request, and gives our product team a live roadmap of what customers actually want.
{: .fs-5 .fw-300 }

<p class="pull-quote">I built it by talking to Claude.</p>

<div class="byline">
  <div class="byline-avatar">
    <img src="assets/images/laura-headshot.png" alt="Laura Litton" onerror="this.style.display='none'; this.parentElement.innerHTML='LL';">
  </div>
  <div class="byline-text">
    <p class="byline-name">Laura Litton</p>
    <p class="byline-role">VP of Success · LiveSchool</p>
  </div>
</div>

<div class="hero-ctas">
<a href="docs/101-your-first-ai-tool/" class="btn btn-primary mr-2">Start at the very beginning →</a>
<a href="docs/case-study/" class="btn">See the case study</a>
</div>

<div class="stat-strip">
  <div class="stat-item">
    <p class="stat-number">4</p>
    <p class="stat-label">customer data sources<br>flowing in automatically</p>
  </div>
  <div class="stat-item">
    <p class="stat-number">50K+</p>
    <p class="stat-label">customer mentions<br>extracted and deduplicated</p>
  </div>
  <div class="stat-item">
    <p class="stat-number">0</p>
    <p class="stat-label">lines of code<br>I wrote by hand</p>
  </div>
</div>

<figure class="hero-image">
  <img src="assets/images/dashboard-hero.png" alt="The Call Intelligence dashboard — feature requests sorted by mention count">
</figure>
<p class="hero-image-caption">The live Call Intelligence dashboard. Every row is a deduplicated feature request, sorted by how many customers have asked for it.</p>

---

## Pick your starting point

The guide is layered. Pick the layer that matches your patience and ambition right now. You can come back for the next one whenever.

<div class="level-cards">
  <a class="level-card level-card-101" href="docs/101-your-first-ai-tool/">
    <span class="level-card-badge">101 · Beginner</span>
    <h3 class="level-card-title">Your first AI tool</h3>
    <p class="level-card-meta">⏱ 30 minutes &nbsp;·&nbsp; Never used Claude</p>
    <p class="level-card-outcome">A working AI extraction running in Claude Desktop on a real call transcript. You'll know whether this is worth more of your time.</p>
    <p class="level-card-cta">Start here →</p>
  </a>
  <a class="level-card level-card-201" href="docs/201-make-it-real/">
    <span class="level-card-badge">201 · Intermediate</span>
    <h3 class="level-card-title">Make it real</h3>
    <p class="level-card-meta">⏱ A weekend &nbsp;·&nbsp; Has a GitHub account</p>
    <p class="level-card-outcome">A tiny app running on your laptop. Paste a transcript in one side, see a clean table of feature requests come out the other.</p>
    <p class="level-card-cta">Read 201 →</p>
  </a>
  <a class="level-card level-card-301" href="docs/301-build-the-real-thing/">
    <span class="level-card-badge">301 · Advanced</span>
    <h3 class="level-card-title">Build the real thing</h3>
    <p class="level-card-meta">⏱ A few weeks &nbsp;·&nbsp; Wants the full thing</p>
    <p class="level-card-outcome">Your own deployed version of Call Intelligence. Real database, scheduled jobs, live dashboard, real users.</p>
    <p class="level-card-cta">Read 301 →</p>
  </a>
</div>

Inside each layer, anything you don't want to read is hidden behind a toggle. The visible path is short. The deep path is one click away.

---

## Why this exists

Every customer success team is sitting on a goldmine of product feedback they can't quite use. Calls happen. Customers ask for things. The CS rep promises to "pass it along." Sometimes it gets to product. Usually it gets lost — buried in a Slack thread, mentioned once in a 1:1, or summarized into oblivion by the time anyone with priority-setting authority hears it.

<div class="context-box" markdown="1">

**The broader context**

This is the classic CS↔Product feedback loop problem. [Gain Grow Retain has a great primer on it](https://gaingrowretain.com/kb/articles/116-how-to-create-an-effective-feedback-loop-between-customer-success-and-product-teams) — the short version is: when customer-facing teams and product teams aren't tightly connected, customers shout requests in, insights come out at random, and product prioritization ends up based on the loudest internal voice rather than the data.

**Call Intelligence is a concrete answer to that question.** It's the implementation behind "create a structured feedback loop." Built by a CS leader, for a CS team, with evidence flowing straight from every customer conversation into a product-facing dashboard.

</div>

This guide is how you build your own version — even if you've never written code before.

---

## How it works

The flow, in plain English:

```mermaid
flowchart LR
    A[Customer calls<br/>and emails] --> B[AI reads everything]
    B --> C[Extracts feature<br/>requests, bugs,<br/>questions]
    C --> D[Deduplicates<br/>against past mentions]
    D --> E[Product team<br/>dashboard]
    E --> F[Decide what<br/>to build]
```

Calls come in from four sources (Fireflies, HubSpot emails, Intercom chats, NPS surveys). Claude reads each one and pulls out structured items. A simple matching algorithm groups duplicate mentions of the same feature. The dashboard shows the product team what customers actually want, with evidence.

That's it. The whole thing.

But it's not really about Call Intelligence. It's about a method: **describe what you want, let Claude write the code, and learn just enough to direct it intelligently.**

---

## A note before you start

The hard part of building software isn't the code. The hard part is **knowing what you want and explaining it clearly.** If you can write a clear email describing a problem, you can build software with Claude.

You're going to make mistakes. You're going to ask Claude for something and get back code that doesn't work. You're going to spend an hour confused before realizing you forgot to save a file. **All of that is normal.** It happened to me too. It still happens to me.

Ready? [Start with the 101 →](docs/101-your-first-ai-tool/){: .btn .btn-primary }

---

<small>Source for this guide and Call Intelligence are both on <a href="https://github.com/llitton">GitHub</a>. Questions? Open an issue.</small>
