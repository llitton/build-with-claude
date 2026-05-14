---
title: 101 — Your first AI tool
nav_order: 2
has_toc: true
permalink: /docs/101-your-first-ai-tool/
---

# 101 — Your first AI tool
{: .no_toc }

**Time: about 30 minutes. Cost: free. Prior experience required: none.**
{: .fs-5 .fw-300 }

By the end of this page you'll have used Claude to read a customer call and pull out every feature request as structured data. That's the seed of Call Intelligence. Everything we build later is "the same idea, scaled up."
{: .fs-5 .fw-300 }

<details markdown="block">
<summary><strong>Table of contents</strong></summary>

1. TOC
{:toc}

</details>

---

## What you need

One thing: **Claude Desktop**. It's a free app from Anthropic.

1. Go to [claude.ai/download](https://claude.ai/download)
2. Download the app for your operating system (Mac, Windows, or Linux)
3. Install it like any other app
4. Open it and sign in (you can use Google to sign up — it's free to start)

That's it. No GitHub. No coding tools. No accounts. Just one app.

{: .tip }
> **Why the desktop app and not the website?** They both work. The desktop app is slightly faster and feels more like "a real tool" psychologically, which matters for getting in the habit.

---

## Step 1: Meet Claude

Open Claude Desktop. You'll see a text box. That's it. That's the whole interface.

Type:

> Hi! I'm a beginner. I want to use you to read customer call transcripts and pull out feature requests. Can you walk me through how that would work, in plain English, before we try?

Send it. (Press Enter, or click the up arrow.)

Claude will respond with something like: *"Sure! I can help with that. Here's how it would work..."*

Read the response. **This is the most important part of the whole guide.** You just had a conversation with the tool you're going to use to build software. You didn't write any code. You explained what you wanted. Claude explained back.

That's the entire job.

<details markdown="block">
<summary><strong>Wait, but how does Claude actually know what I'm asking?</strong></summary>

Claude is a Large Language Model — an AI that's read a huge amount of text and learned to predict what response would be helpful given some input. You don't need to know how it works under the hood to use it, the same way you don't need to know how your car's engine works to drive.

The mental model that works: **Claude is a very smart, very fast intern who has read everything ever written, has no ego, doesn't get tired, and will do anything you ask — but only exactly what you ask.** If you're vague, you get vague work back. If you're specific, you get great work back.

That's the entire skill. Specificity.

</details>

---

## Step 2: Your first extraction

Now we'll do the real thing. We're going to:

1. Paste a sample call transcript into Claude
2. Ask Claude to extract feature requests as structured data
3. See what comes back

### The sample transcript

Copy this whole block (yes, the whole thing — including the speaker labels):

```
[Call: ABC Elementary — Renewal conversation — 2026-03-12]

Sarah (Customer Success): Hi Maria, thanks for jumping on. I wanted to walk through the renewal and hear how this year has gone.

Maria (Principal, ABC Elementary): Yeah, happy to. Overall — really positive. The teachers are using it daily, the kids love the points, and our discipline referrals are down maybe 30% from last year.

Sarah: That's amazing. Anything that's been frustrating?

Maria: Honestly, the biggest thing is the parent app. Parents want to see their kid's points history, but right now they can only see the current week. A bunch of parents have asked me if there's a way to see the whole year. That's been a constant complaint.

Sarah: Got it. I'll write that up.

Maria: Also — and this is smaller — but when teachers give a behavior award, there's no way to attach a photo. Like, if a kid does something amazing and the teacher wants to capture the moment, they have to take a photo separately and text it to the parent. It would be cool if the photo could just live in the app, attached to the award.

Sarah: Oh that's a good one. We've heard that from a few other schools too actually.

Maria: And then the other thing — the reporting. Right now when I run a report it only shows me the current month. I want to be able to pick a date range. Like, "show me September through December." Especially for parent conferences, I need to be able to pull a specific window.

Sarah: Yeah, custom date ranges have been on the roadmap for a while. I'll mark you as another vote for it.

Maria: Cool. Other than that, things are great. Oh — one bug actually. Sometimes when a teacher logs in on the iPad, the app crashes the first time. They have to close it and reopen it and then it works. It only happens the first time of the day.

Sarah: Weird, I'll file that with engineering. Anything else?

Maria: No, I think that's everything.

Sarah: Great. So for renewal — same package as last year?

Maria: Yep, sounds good. Send me the paperwork and I'll get it signed this week.
```

### The prompt

Now paste this into Claude *along with* the transcript (you can put them in the same message — Claude will figure it out):

> I'm going to paste a customer call transcript below. Please extract every distinct feature request, bug report, or piece of product feedback. Return your answer as a JSON array. Each item should have:
>
> - `type` ("feature_request", "bug", or "feedback")
> - `summary` (one short sentence, in the customer's voice)
> - `detail` (a few sentences with full context)
> - `urgency` ("low", "medium", or "high") — your best guess based on tone
>
> Here is the transcript:
>
> [paste the transcript here]

Send it.

### What you should see

Claude will return something close to this:

```json
[
  {
    "type": "feature_request",
    "summary": "Parents want to see their child's full point history, not just the current week.",
    "detail": "Parents have been repeatedly asking the principal for visibility into the whole year of points. Currently the parent app only shows the current week, which is a constant source of complaints.",
    "urgency": "high"
  },
  {
    "type": "feature_request",
    "summary": "Teachers want to attach a photo to a behavior award.",
    "detail": "When a teacher gives an award for something special, they currently have to take a photo separately and text it to the parent. It would be more useful if the photo could be attached to the award inside the app.",
    "urgency": "medium"
  },
  {
    "type": "feature_request",
    "summary": "Reports should support custom date ranges, not just the current month.",
    "detail": "The principal needs to pull specific date ranges (e.g., September through December) especially for parent conferences. Currently the reporting only shows the current month.",
    "urgency": "medium"
  },
  {
    "type": "bug",
    "summary": "iPad app crashes on first launch of the day.",
    "detail": "Teachers report that the app reliably crashes the first time they open it each day on iPad. Closing and reopening resolves it. Occurs once per day, only on iPad.",
    "urgency": "medium"
  }
]
```

**Stop and look at that.** You just turned a wall of conversational text into clean, structured data. The principal mentioned four things in passing. Claude pulled them all out, labeled them, and rated their urgency. **That's the entire job of Call Intelligence.** Every call we process — hundreds a week — runs through a version of that one prompt.

The whole tool, conceptually, is: *do that, but automatically, in the background, on every call that comes in, and put the results in a dashboard.*

{: .story }
> **From the build:** The very first version of Call Intelligence was *literally this prompt*, in Claude Desktop, run by hand on call transcripts the customer success team would paste in one at a time. I did that for two weeks before writing any code. It told me the idea worked. Most "build the real thing" mistakes come from skipping this step.

---

## Step 3: Iterate — make the output better

Here's the part nobody teaches you: **the first response from Claude is rarely the final answer.** You make it better by asking for changes in plain English. This is the single most important skill in this whole guide.

Try each of these as a follow-up message in the same Claude conversation:

### Try this

> Can you also tag each item with a `category` (e.g., "parent_app", "reporting", "teacher_experience", "stability")?

Claude will re-output the JSON with categories added. **You didn't have to know what categories you wanted in advance.** You saw the output and noticed they were missing.

### Try this

> For each item, add a `quote` field with the exact words the customer used. I want to be able to show the verbatim quote as evidence.

This is huge. **You're now extracting evidence, not just summaries.** That's the difference between "trust me, customers want X" and "here's the customer saying X, with timestamp."

### Try this

> I'd also like a `school_name` field at the top level. Apply "ABC Elementary" to every item. (Eventually I'd extract this from the transcript header, but for now I'll provide it.)

Now your output looks like real production data. School name, type, summary, detail, urgency, category, verbatim quote.

<details markdown="block">
<summary><strong>What just happened, conceptually</strong></summary>

You designed a data schema. Without knowing what a data schema is.

A "schema" is just "the shape of the data" — what fields exist, what types they are. Every database, every API, every spreadsheet has one. You usually have to design it up front, on paper, before you build anything. With Claude, you can design it iteratively by looking at examples and saying "add this field, remove that one, rename this."

This is a recurring pattern: **design by example.** You'll do it over and over as you build real software with Claude. Show it something concrete. React. Refine.

</details>

---

## Step 4: Try it with your own content

The exercise so far was useful but contrived. Now try it on something from your life.

Some ideas:

- **Paste a long email thread.** Ask Claude to extract every action item, who owns it, and the deadline.
- **Paste meeting notes.** Ask for decisions made, open questions, and next steps as separate lists.
- **Paste customer reviews from a Google Maps listing.** Ask for sentiment, recurring praise, recurring complaints.
- **Paste a contract.** Ask for every dollar amount, every date, and every obligation.

For each one, you're doing exactly what Call Intelligence does — turning unstructured text into structured data. The only difference between "an experiment in Claude" and "a real tool" is whether it runs once, by hand, or automatically, in the background, every day.

**That gap is what 201 and 301 close.**

---

## What you actually just did

Take a second to appreciate this.

You took a 700-word conversation. You wrote one prompt. You got back clean, labeled, structured data with evidence. **You did data extraction.** That's a thing engineers used to spend weeks building bespoke code for. You did it in two minutes by typing what you wanted.

The reason this matters: most of the value in software is *not* in the fancy parts. It's in things exactly like this — taking messy input, turning it into structured output, doing something useful with it. Once you can do that, you can build most "internal tools" any company needs.

Call Intelligence is just this, scaled up.

---

## What's next

You have three options.

<div class="code-example" markdown="1">

### Stay here for a while.

Spend a week running real call transcripts (or emails, or meetings) through this prompt by hand. You'll learn what works, what doesn't, and what fields you actually care about. The next level becomes way easier if you've already played here.

### Go to [201 — Make it real](../201-make-it-real/).

You'll build a tiny web app that does this automatically. Paste a transcript in one side, see a table of extracted items on the other. You'll install one new tool and write your first lines of "code" — except Claude writes them, you direct.

### Skip ahead to the [Case Study](../case-study/).

If you want to see how I went from this exact prompt to the live tool product managers use weekly, the case study walks the whole arc.

</div>

[Go to 201 →](../201-make-it-real/){: .btn .btn-primary .fs-5 }
[See the Case Study →](../case-study/){: .btn .fs-5 }

---

## Cheat sheet

For when you come back to this page later.

- **Tool**: Claude Desktop, free, from claude.ai/download
- **Pattern**: Paste unstructured text → ask for structured JSON → iterate on the schema
- **Key prompt fragments**:
  - *"Extract every distinct [X] as a JSON array with these fields..."*
  - *"Add a field called [Y] that captures..."*
  - *"For each item, include the verbatim quote..."*
- **Mindset**: Show, don't tell. Get something rough. Refine by example.

---

<div style="display: flex; justify-content: space-between; margin-top: 3em;">
<a href="../../">← Home</a>
<a href="../201-make-it-real/">201 — Make it real →</a>
</div>
