# Skill: Internship Outreach Personalizer

## Trigger
`/internship-outreach`

## Purpose
Take the hardcoded message template below and personalize it for every company in the user's list. For each company, research the founder/CEO, YC status, what the company does, and any recent milestones — then fill in all placeholders with specific, authentic content.

---

## Sender Context (Hardcoded)

The sender is **Nhi**, a self-taught developer/data science student with the following background:
- Started coding from zero ~9 months ago (didn't know how to use Finder)
- Now writes code for data science
- Built a **video analysis project and automated temperature alert** for Bearcat Motorsports FSAE Formula 1 Electric Vehicle Student Team
- **Vice President of Vietnamese Student Associates** — organized 9 events in 1 year
- Also worked simultaneously as a **Math Tutor** and **Lab Assistant**
- Currently works at **Starbucks** to develop customer service skills
- Dreams of founding her own venture and getting into YC
- Tone: warm, direct, genuine, with a quiet confidence

---

## Message Template

> **Note:** This is the fixed base message. Do NOT rewrite it. Only fill in the placeholders.

```
Hi [FOUNDER_FIRST_NAME].

I'll run main() since you're busy:

I want to work with a YC founder like yourself
Because it is my dream to start my own venture and get into YC [INSERT reason - founder].
I want to intern at [COMPANY_NAME] because [INSERT reason - company].
9 months ago, I did not know how to use Finder. Now I write code to do data science.
If you give me a shot, I will go all in on my abilities to contribute to the company.

Proof:
- [Video analysis project](https://github.com/nyle06dn/VideoAnalysis) and automated temperature alert for Bearcat Motorsports FSAE Formula 1 Electric Vehicle Student Team.
- I am a Vice President for Vietnamese Student Associates. We hosted 9 events in 1 year. I worked as a Math Tutor and Lab Assistant simultaneously that year.
- I am working at Starbucks to learn customer service.

My resume is attached. I am looking forward to hearing your feedback.

With gratitude,
Nhi
```

---

## Inputs Required from User

The user only needs to provide:
1. **Company List** — Pasted text, HTML, PDF, or a URL with company names.

If missing, ask for it before proceeding.

---

## Placeholder Spec

| Placeholder | Where it appears | What to fill in |
|---|---|---|
| `[FOUNDER_FIRST_NAME]` | Greeting line | First name only of the founder or CEO |
| `[COMPANY_NAME]` | Line 4 | Official company name |
| `[INSERT reason - founder]` | End of line 3, after "get into YC" | **A few words only** — a short inline phrase that completes the sentence naturally. e.g. *"just like you did with Invert W22"*. If NOT YC: rewrite line 3 entirely with an alternative short motivation. |
| `[INSERT reason - company]` | End of line 4, after "because" | **A few words only** — one punchy clause that completes "I want to intern at X because...". e.g. *"you're turning messy bioprocess data into AI-powered decisions"*. |

> **Critical:** Each reason is **a short phrase — 5 to 10 words max**. It finishes a sentence already in the template. Do NOT write a paragraph. Do NOT add new sentences. Think of it like filling in a blank.

---

## Execution Steps (Per Company)

For **each company** in the list, do the following in order:

### Step 1 — Research the Company (go deep)

Do NOT stop at a homepage tagline. Use `read_url_content` on the company website, their blog, and their product pages to understand:
- **Exactly what problem they solve** — in plain English, as if explaining to a non-expert
- **Who their customers are** (e.g. pharma scientists, bank compliance teams, small restaurant owners)
- **What the customer was doing before** this product existed (spreadsheets? manual processes? expensive consultants?)
- **What the product specifically does** — not "AI-powered platform" but the actual workflow it replaces or automates
- **YC status**: batch, year
- **Recent concrete milestones**: a specific product launch with a name, a funding round with a dollar amount, a named customer win, a conference talk, a blog post about a new feature

Suggested steps:
1. `search_web`: `"[Company Name]" YC Y Combinator founder`
2. `read_url_content`: company homepage
3. `read_url_content`: company `/blog` or `/about` page
4. `search_web`: `"[Company Name]" launch funding 2024 2025 milestone`

### Step 2 — Research the Founder / CEO (go deep)

Do NOT stop at a name. Find:
- Full name and first name
- Their background **before** founding this company (previous jobs, research, prior startups)
- Their educational path — did they drop out? Change fields?
- Anything they've written or said publicly (blog posts, tweets, conference talks, interviews)
- YC personal alumni status

Suggested steps:
1. `read_url_content`: their LinkedIn profile URL
2. `search_web`: `"[Founder Name]" "[Company Name]" background story`
3. `search_web`: `"[Founder Name]" YC interview OR blog OR talk`

### Step 3 — Find a Recent Blog Post and Generate the Subject Line

This step is required. Every message must have a subject line.

**Where to look (in order):**
1. CEO / founder's personal blog, LinkedIn posts, or Twitter/X — did they write about something they find interesting, a problem they're thinking about, a lesson they learned, or something they think is cool?
2. Company blog — a recent post about a product launch, a new feature, an industry opinion, or a challenge they explored
3. A conference talk or interview they gave

**What to do with it:**
- Read the actual post/article using `read_url_content`, not just the title
- Find a specific thing they expressed: a belief, a frustration, a want, a finding, something they said was "cool" or unsolved
- The subject line must do **two things at once**:
  1. Reference the blog/post (shows you actually read it)
  2. Position the sender as **the answer** to what the founder wrote about or expressed needing
- Think: *"they wrote about wanting X → subject line says: X has arrived / here's your X"*

**Subject line rules:**
- **Short**: 5–10 words max
- **Specific**: reference the actual topic from the post
- **Position the sender as the solution**, not just a fan of the post
- **Never use**: "Internship Application", "Reaching Out", "Excited About", "Love What You're Building", "Re: [post title]" (too passive)

**Good subject line examples:**
- *"Your DataOps Agent has arrived"* — after reading a post about needing an AI DataOps agent
- *"The bioreactor scale-up person you need"* — after reading a post about scale-up bottlenecks
- *"Here's the data person your ELN blog needed"* — after reading a post on ELN limitations
- *"Your next hire just read your Berlin talk"* — after finding a conference talk they gave

**Bad subject line examples:**
- *"Re: why ELNs aren't enough for PD teams"* ❌ — just echoes the title, doesn't position the sender
- *"Internship Application at Invert"* ❌ — generic
- *"Saw your blog post"* ❌ — says nothing

**If no blog or post is found:**
- Fall back to a subject line based on the most specific thing you know about the company or founder
- Flag it in the output as "Subject (no blog found — fallback)"
- Do NOT use a generic subject line like "Internship at [Company]"

### Step 4 — Write `[INSERT reason - founder]`

**Rule: a short phrase, ~5–12 words, completing the sentence "...get into YC [phrase]"**

**If YC-backed:**
- Reference the specific batch: e.g. *"just like you did with [Company] W22"*
- Or reference something they specifically did: *"after betting on yourself and dropping out to build [Company]"*
- Do NOT say "your journey" or "your path" — those are vague. Name the actual thing.

**If NOT YC-backed:**
- Rewrite line 3 of the template entirely.
- Replace with a short, specific motivation tied to the founder's real story.
- Example: *"I want to work with a founder like yourself who left [Previous Company] to solve [Specific Problem] no one else was tackling."*
- Still ~1 short sentence. No flattery without substance.

**Banned phrases:** "your journey", "your path", "your vision", "inspiring story", "innovative approach", "exciting space"

### Step 5 — Write `[INSERT reason - company]`

**Rule: a short clause, ~8–15 words, completing "I want to intern at [X] because [clause]"**

- Describe the **specific thing** the product does that a person could picture.
- It must answer: *what did the user/customer do before, and what does this product let them do instead?*
- Reference a real, named feature or recent milestone if found.
- Do NOT use: "AI-powered decisions", "innovative platform", "cutting-edge technology", "meaningful impact", "disrupting the industry"

**Good examples:**
- *"you replaced weeks of scientists cleaning bioreactor data in Excel with a chat interface"*
- *"you let solo founders generate legal contracts in 30 seconds instead of hiring a lawyer"*
- *"you help restaurants predict which menu items to cut before they lose money on them"*

**Bad examples (do not do this):**
- *"you're building AI-powered solutions for the biotech space"* ❌
- *"your innovative platform is transforming the industry"* ❌
- *"you're doing something really exciting in bioprocessing"* ❌

### Step 6 — Assemble the Message

- Use the exact template above.
- Slot in `[FOUNDER_FIRST_NAME]`, `[COMPANY_NAME]`, `[INSERT reason - founder]`, `[INSERT reason - company]`.
- Do not alter any other line in the template.
- Keep the casual, energetic, first-person tone.
- **Always output the complete message, every line, including the Proof section and sign-off. Never truncate. Never use "..." to skip lines.**

### Step 7 — Output Format

For each company, output the full block below — no shortcuts:

```
---
## [Company Name]
**To:** [Full Founder Name] — [Title]
**YC:** [Yes — Batch / No]
**Recent Milestone:** [1-line summary, or "None found"]
**Blog/Post Used:** [Title or description of post, or "None found"]

**Subject:** [Subject line here]

### Message:
Hi [FOUNDER_FIRST_NAME].

I'll run main() since you're busy:

I want to work with a YC founder like yourself
Because it is my dream to start my own venture and get into YC [INSERT reason - founder].
I want to intern at [COMPANY_NAME] because [INSERT reason - company].
9 months ago, I did not know how to use Finder. Now I write code to do data science.
If you give me a shot, I will go all in on my abilities to contribute to the company.

Proof:
- [Video analysis project](https://github.com/nyle06dn/VideoAnalysis) and automated temperature alert for Bearcat Motorsports FSAE Formula 1 Electric Vehicle Student Team.
- I am a Vice President for Vietnamese Student Associates. We hosted 9 events in 1 year. I worked as a Math Tutor and Lab Assistant simultaneously that year.
- I am working at Starbucks to learn customer service.

My resume is attached. I am looking forward to hearing your feedback.

With gratitude,
Nhi
```

After all companies, output a summary table:

| # | Company | Founder | YC? | Milestone Found? |
|---|---|---|---|---|
| 1 | ... | ... | ... | ... |

---

## Quality Rules

- **Never be generic.** Every reason must reference something specific to that founder or company.
- **Never fabricate.** If you can't verify a fact, don't include it. Say "None found" and work with what you have.
- **Keep the voice.** The template has an informal, energetic, slightly unconventional tone. Don't sanitize it.
- **One founder per company.** Pick the CEO or most public-facing co-founder.
- **Flag if stuck.** If there's genuinely not enough info to write a good reason, flag the company and ask the user before producing a weak message.

---

## Notes for Agent

- Use `search_web` at least 2–3 times per company.
- YC lookup: search `site:ycombinator.com "[Company Name]"` or check `https://www.ycombinator.com/companies`.
- If the company list is in HTML or PDF form, extract the company names first before starting the loop.
- Process companies **one at a time**.
- If the list is 10+ companies, ask the user if they want to batch or go all at once.
