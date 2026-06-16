# Guide: How to Write Your Input for the Prompt Optimizer

## The Most Important Thing First

You need **no fixed format**. The optimizer is designed to work with raw text. But: the more context you provide, the more precise the result.

---

## The `prompt:` Trigger (Recommended)

If you want to **guarantee** an optimization — even when your input looks like a question or references attached documents — start your message with the `prompt:` prefix.

**Example:**

```
prompt: Explain, based on the attached PDF, what GDPR risks
exist for our CRM and how we can mitigate them.
```

Without the prefix, the optimizer might in some cases try to answer the question substantively or analyze the PDF directly. With the prefix, you **always** get an optimized prompt back — including placeholders for the document.

The prefix is case-insensitive: `prompt:`, `Prompt:`, `PROMPT:` all work.

**Rule of thumb:**
- Content is clearly an optimization task? → Prefix is optional.
- Content sounds like a question, contains document references, or contains direct instructions? → **Use the prefix.**

---

## Minimal Version (Always Works)

Just write what you want:

```
Write me a Python script that merges CSV files
```

The optimizer automatically recognizes intent, domain, and complexity and fills in the gaps.

---

## Better Version: The Four-Sentence Method

For better results, answer these four questions in one to two sentences each:

**1. WHAT should Claude do?** — the concrete task
**2. FOR WHOM / WHY?** — audience and purpose
**3. HOW should the result look?** — format, length, style, language
**4. WHAT SHOULD BE AVOIDED?** (optional) — explicit no-gos

**Example:**

```
Write a blog post about AI in recruiting.
Audience: HR leadership at mid-sized companies.
Around 1,500 words, practical focus with concrete tool recommendations.
No marketing speak, no inflated promises.
```

---

## Pro Version: Context Block

For complex tasks you can provide additional context in a structured way. You do **not** need to write XML tags — the optimizer adds them automatically. Just write naturally:

```
Task: Develop a migration strategy from our on-premise Exchange to Microsoft 365.

Context: Mid-sized company with 200 employees,
3 locations in the US, currently running Exchange 2016.
Budget around $50,000. IT team: 4 people.

Result: Structured document with a phased plan,
risk assessment, cost breakdown, and checklist.

Important: Data privacy compliance is required.
Works council exists — change management is relevant.
```

---

## Special Cases

### Coding Prompts
Name the language, use case, and quality requirements:

```
Python function that merges multiple PDFs.
Should handle large files (500+ pages), with error handling,
usable as a CLI tool.
```

### Creative Prompts
Specify tone, mood, audience, and length:

```
Short story in sci-fi noir style.
Protagonist: AI forensics detective in Neo-Chicago 2087.
Around 3,000 words, dark tone, plot twist at the end.
```

### Analysis Prompts
Name the data source, the question, and the desired output:

```
Analyze the attached quarterly figures and identify
the three biggest cost drivers. Result as an executive summary
for leadership, one page maximum.
```

### System Prompt Optimization
If you want to optimize your own system prompt, say so explicitly:

```
Optimize the following system prompt for my support project:
[your system prompt here]
The system should classify tickets and provide suggested responses.
```

---

## What You Do NOT Need to Do

- You don't need to write XML tags — the optimizer sets them.
- You don't need to define a role — the optimizer picks the right one.
- You don't need to know any prompt engineering techniques — that's exactly what this tool is for.
- You don't need to write polished text — bullet points and rough notes are fine.

---

## What Happens After Optimization?

1. You receive the optimized prompt in a code block — **one click to copy**.
2. Paste it into a new Claude conversation, a project, or your API call.
3. If something doesn't fit: tell the optimizer. It will revise accordingly.

**Tips for iterative feedback:**
- "Make the prompt shorter."
- "Add few-shot examples."
- "Change the role to [XYZ]."
- "Calibrate the verbosity: this should be a deep analysis."
- "Recommend an appropriate effort level for API usage."

**Good to know for API users:**
Opus 4.8 has Thinking off by default on the API. If the optimized prompt requires multi-step reasoning, enable `thinking: {"type": "adaptive"}` in your API request. 
The default effort is `high` and applies on all surfaces (Claude API and Claude Code) — for difficult or long-running async tasks, step up to `xhigh` (in claude.ai this level is called "extra"); 
for simple or narrowly scoped tasks, step down to `low`/`medium`. For very long agentic loops, the Beta feature `task_budget` is worth a look; 
in long, multi-turn conversations you can also inject updated instructions via a mid-conversation system message without breaking the prompt cache.
