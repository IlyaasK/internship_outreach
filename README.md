# internship_outreach

An Antigravity skill for personalizing cold internship outreach emails to startup founders.

## What it does

Given a list of companies, this skill:
1. Researches each company (YC status, product, what problem it actually solves)
2. Researches the founder/CEO (background, unconventional path, public writing)
3. Finds a recent blog post or talk from the CEO or company
4. Generates a **subject line** that references the post AND positions the sender as the answer to what the founder expressed needing
5. Fills in a fixed message template with a specific, non-generic reason for the founder and company
6. Outputs the full personalized message + subject line for every company

## Usage

Trigger: `/internship-outreach`

Paste your company list after the trigger. The skill will process them one at a time and output a full personalized message for each.

## Skill file

[`skills/internship-outreach.md`](skills/internship-outreach.md)

## Message Template

```
Hi [FOUNDER_FIRST_NAME].

I'll run main() since you're busy:

I want to work with a YC founder like yourself
Because it is my dream to start my own venture and get into YC [INSERT reason - founder].
I want to intern at [COMPANY_NAME] because [INSERT reason - company].
9 months ago, I did not know how to use Finder. Now I write code to do data science.
If you give me a shot, I will go all in on my abilities to contribute to the company.

Proof:
- Video analysis project and automated temperature alert for Bearcat Motorsports FSAE Formula 1 Electric Vehicle Student Team.
- I am a Vice President for Vietnamese Student Associates. We hosted 9 events in 1 year. I worked as a Math Tutor and Lab Assistant simultaneously that year.
- I am working at Starbucks to learn customer service.

My resume is attached. I am looking forward to hearing your feedback.

With gratitude,
Nhi
```

## Key Rules

- **Subject line** = references a real blog post + positions sender as the answer to what the founder wrote about
- **Founder reason** = 5–12 words, specific to their actual story (batch, path, decision)
- **Company reason** = 8–15 words, describes what the customer did *before* vs. what they can do *now*
- **No buzzwords**: "AI-powered decisions", "innovative platform", "exciting space" are banned
- **Full message always output** — never truncated

## Deploying to another Antigravity instance

Copy `skills/internship-outreach.md` to `~/.gemini/antigravity/skills/` on the target machine.
