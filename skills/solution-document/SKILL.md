---
name: solution-document
description: Write or review a Solution Document — the stakeholder-facing write-up of a system, feature, or integration covering the problem, requirements, the solution in plain language, benefits, behavior when things go wrong, alternatives considered, risks, validation, and open questions. Use when asked for a "solution document", "solution overview", "solution brief", "solution summary", a "non-technical" or "stakeholder" or "customer-facing" version of a design, or when asked to derive one from an existing design document. Not for the engineer-facing write-up — that is the design-document skill.
---

# Solution Document

A Solution Document explains **what problem is being solved, what changes for the people affected, and why this shape rather than another**, for a reader who won't build the thing and can't be assumed to know how it works. Product and project management, support and delivery staff, and often the customer read it.

Its job is to let someone decide, plan, or explain. If a reader can't say yes or no to the project after reading it, or can't describe the change to their own stakeholders, the document has failed regardless of how accurate it is.

Write it in Google developer documentation style, then run the `unslop` skill over the draft before
you hand it over. See "Writing standard" below.

## What belongs here

The problem, the requirements, the shape of the answer, what it costs in risk, and what is still undecided. Enough mechanism to make the solution credible and no more.

What does **not** belong here: schemas, endpoints, message formats, class and function names, configuration keys, algorithms, and the internal sequence of operations. Those belong in a design document. A solution document that starts specifying is no longer readable by the audience it was written for, and it goes out of date the first time the implementation changes, because it committed to details it never needed.

The test for any sentence: would this reader's decision change if the sentence were removed? If not, cut it.

## Relationship to the design document

A design document answers *how it works*, for the engineers, reviewers, and operators who build and run it. Where both exist, they're separate documents with separate audiences, not two lengths of the same one. Link to the design document from the header block and from Appendix > References. Don't summarize it section by section.

### Deriving one from a design document

This is the common and the cheaper direction, and roughly two thirds converts:

| From the design document | Becomes |
|---|---|
| Purpose | Introduction > Problem Statement |
| Overview | Introduction > Overview, Introduction > Background |
| Purpose, Overview, and the guarantees the design commits to | Requirements > Functional |
| Performance targets, SLOs, volumes | Requirements > Non-Functional |
| Deployment and Compatibility, plus stated dependencies and assumptions | Requirements > Constraints |
| Architecture diagram | Solution > Architecture Diagram, redrawn rather than copied |
| Data flow, mechanism | Solution > High-Level Design, as guarantees rather than mechanisms |
| Alternatives Considered | Solution > Alternatives, with the tradeoffs kept and the internals dropped |
| Fault Tolerance | Concerns > Behavior When Things Go Wrong, as guarantees rather than mechanisms |
| Security | Concerns > Risks, phrased as consequences to people rather than properties of the system |
| Testability | Concerns > Validation |
| Open Questions | Concerns > Open Questions, re-owned by whoever actually decides |
| Terms and Acronyms | Appendix > Glossary, rewritten for a non-engineer |

What **can't** be derived and must be gathered separately: scope boundaries, cost and effort, stakeholder and support impact, the delivery plan, and risk ownership. Ask for these. If they're unavailable, raise them as Open Questions with a named owner. Never invent a business fact, a cost, or a customer requirement, which is a worse failure here than in a design document because this reader has no way to detect it.

**Escalate what the design document understates.** A fact recorded in one clause of a design document is often the headline for this audience. Watch for: anything that runs without authentication, anything that bypasses normal access restrictions, data written unencrypted, limits that go unenforced, and defaults that were proposed but never validated. In a design document these are neutral statements of fact. Here, each is a risk with an owner and, usually, a decision someone must make.

## Structure

Five top-level sections, in this order, with the subheadings shown. Omit a subsection only when it genuinely doesn't apply, and say so in one line rather than deleting the heading silently. Start from `template.md` in this skill directory.

Open with a short header block: status, intended audience, link to the design document, and last-updated date.

### 1. Introduction

#### 1.1 Problem Statement

What was asked for, and why the current system can't do it. One or two paragraphs, no solution yet. A reader who stops here should be able to repeat the problem in their own words.

Keep the solution out of this subsection entirely. If a sentence describes what's being built, it belongs in Overview.

#### 1.2 Overview

Three or four short paragraphs, and the only part many readers finish. Cover what's being built and what changes for the people already using the system, including "nothing changes for them", which is often the most valuable sentence in the document.

Close with two lists, **In scope** and **Out of scope**. The out-of-scope list is the more useful one: it corrects the reader's assumptions before they harden into expectations. Include the things a reasonable person assumes are included but aren't: delivery of the output somewhere, access control, retention changes, integration with the customer's systems.

No jargon, no acronyms that aren't expanded on the spot, no forward references to later sections.

#### 1.3 Background

Why the current situation is a problem, in the reader's terms rather than the system's. Where limits are the problem, a two-column table of `Limit` | `Effect on the customer` is worth more than prose, because it forces every technical constraint to pair with a consequence someone actually experiences.

Say what the affected people do today instead, and why that doesn't scale. That establishes the cost of doing nothing, which is what the reader is implicitly comparing against.

### 2. Requirements

#### 2.1 Functional

What the solution must do, each item phrased so a reader can judge it met or unmet. Three to five is usually right; ten means the requirements include design decisions. Number them (F1, F2, …) so Validation and Benefits can refer to them.

#### 2.2 Non-Functional

The qualities the solution is held to: volume, timing, availability, security posture, and operability. Give numbers, such as "completes within the nightly window" or "handles a month of peak data in one run". Mark any value that's proposed but not yet agreed, because an unvalidated target is a decision someone still owes.

#### 2.3 Constraints

What must be true for the solution to work, and what the solution doesn't control: where it runs and what must be available, what the customer is responsible for, and limits that aren't enforced. Each of these is a place the project can fail for a reason that's nobody's bug.

### 3. Solution

#### 3.1 Architecture Diagram

A single simple diagram: the components the reader recognizes, the direction of flow, and nothing else. Caption it with what to look at.

Don't reuse the design document's architecture diagram. It's drawn for a different reader and carries detail that costs this one their attention. If the solution is too simple to need a diagram, say so in one line rather than drawing a trivial box.

#### 3.2 High-Level Design

How it works, at the level of a well-informed non-specialist. Introduce each concept with an ordinary word and a one-line explanation of the real term in brackets, such as *a bookmark (cursor)*, then use the ordinary word consistently for the rest of the document.

Explain **why the mechanism gives the guarantee**, because that's what the reader must trust. Give the reason, not the algorithm. "Because it resumes from an exact recorded position rather than re-running a narrowed search, no record falls between two pages" is the whole argument, and it survives any change to how the position is encoded. Use one analogy, chosen well, and never mix in a second.

Then **what changes in practice**: what the affected people do differently, what gets run, by whom, how often, what comes out, and what they must arrange themselves. Where nothing changes for an existing group, name that group and say so.

Close with a `Benefit` | `Why it matters` table. Each benefit traces to a functional requirement, and "why it matters" names a consequence for someone, not a property of the system. "Complete extraction at any volume" is a property; "the ceiling stops constraining what the customer can ask for" is why anyone cares. Don't list benefits the solution doesn't deliver, and don't restate one benefit in three phrasings. A short honest table persuades better than a long one.

#### 3.3 Alternatives

Always include doing nothing or continuing with the status quo, because that's the alternative the reader has in mind whether or not it's written down. Include the cheap option that was rejected, and be specific about what defeats it. A rejected option with only vague objections reads as though nobody examined it seriously.

For each: **Description**, **Tradeoffs** in both directions, and **Why not chosen**, or **Why chosen** for the selected option. Name the cost of the chosen option honestly. Nobody senior enough to matter believes a document where the chosen option has no drawbacks.

### 4. Concerns

Everything the reader should worry about, in one place: how the solution fails, what it risks, how anyone will know it worked, and what's still undecided. Use the four subsections below unless the material genuinely calls for a different split.

**Behavior When Things Go Wrong.** Derived from the design document's fault tolerance and rewritten completely. State the governing principle first, in one sentence, usually a form of *the system either produces a correct result or stops with a clear reason, and never quietly produces a wrong one*. Then a `Situation` | `What happens` table.

The rule for every row: **outcomes, not mechanisms.** The reader needs to know that a mid-run failover stops the job with a distinct error and someone re-runs the job. They don't need to know what detects it. Where the honest answer is that a case is handled invisibly and needs no action, say that too. It's reassuring, and its absence from the table reads as an omission. Close by saying what this means operationally: that each outcome is distinguishable, so a scheduled job can detect a failure, alert, and retry.

**Risks.** A table of `#` | `Risk` | `Impact` | `Mitigation` | `Owner`. The impact column says what happens to someone, not to the system. A risk with no mitigation and no owner is decoration. Either assign one, or move it to Open Questions as a decision.

This is where escalated security and operational facts land. State them plainly. A stakeholder who discovers after delivery that a tool bypasses access restrictions won't be reassured that the design document mentioned it.

**Validation.** Not a test plan. The three to five claims the solution rests on, each with the evidence that shows it's true. They map to the functional and non-functional requirements, and give the reader the shape of what sign-off looks like.

**Open Questions.** A table of `#` | `Question` | `Owner` | `Status`. Phrase every question so a yes/no or a value settles it, and make every owner a person or role who can actually decide, including the customer where the decision is theirs. Mark which questions block sign-off and which merely block work starting.

### 5. Appendix

#### 5.1 References

The design document, related solution or design documents, tickets, standards, and vendor documentation. Give each one a descriptive title rather than a bare URL, so the reader knows what they're opening.

#### 5.2 Glossary

Plain-language definitions of every domain term and acronym the document uses. Write these fresh for this reader. Don't copy the design document's definitions table, which is written for engineers and reintroduces exactly the jargon this document exists to avoid. Include the ordinary words given a specific meaning in High-Level Design, with the real term in brackets.

## Writing standard

Follow the **Google developer documentation style guide**. The rules that matter most here:

- **Second person.** Address the reader as "you". Avoid "we" for the reader and the writer both. Name the actor instead: "the operations team runs the job", not "we run the job".
- **Active voice, present tense.** "The tool writes a file", not "a file will be written".
- **US English spelling.** Behavior, analyze, summarize, recognize.
- **Sentence case for any heading you add** beyond the fixed ones in `template.md`.
- **Expand acronyms on first use**, then use the acronym. Every acronym also appears in the Glossary.
- **No Latin abbreviations.** Write "for example" and "that is", not "e.g." and "i.e.".
- **Serial comma.** "Support, delivery, and the customer".
- **"Might", not "may"**, for possibility. Reserve "may" for permission.
- **Drop the filler.** No "simply", "just", "easily", "obviously", or "of course". If it's easy, the reader will notice without being told.
- **No anthropomorphism.** A system doesn't want, think, or try.
- **Descriptive link text.** Name the document, not "click here" or a bare URL.
- **Contractions are fine.** They keep the tone level and readable.
- **Inclusive, neutral language.** Use "they" for a person whose pronouns you don't know.

Then, on top of Google style, the rules specific to this document:

- **Plain language, not simplified content.** Short sentences and ordinary words, but the reader is intelligent and busy, not incapable. Never write down to them.
- **Guarantees, not mechanisms.** State what holds and why it holds. The how belongs in the design document.
- **Numbers survive the translation.** "5,000 records at a time", "a busy month exceeds the limit", "one run per night". Benefits without numbers read as marketing.
- **One name per concept**, matching the Glossary, used identically in every section.
- **Every claim traceable.** Anything asserted about current behavior comes from the design document or the system, not from the name of a component.
- **Bad news stated plainly and early.** A limitation the reader finds late feels concealed even when it was written down.
- **No invented business facts.** Cost, timeline, customer requirements, and stakeholder positions are gathered or raised as Open Questions.

### Cut the AI tells

A stakeholder document that reads as machine-written loses the reader's trust before it loses their
attention. When the draft is complete, run the `unslop` skill over it and fix what it finds. The
patterns that show up most in this kind of document:

- **Em dashes.** Use a period or a comma. This is the most common tell in a derived solution
  document, because design documents are full of them.
- **Semicolons and mid-sentence colons.** Split the sentence. A colon is fine before a list or an
  example.
- **Bold used mid-sentence** to signal that a phrase matters. The tables and headings carry the
  emphasis. Bold is for the labels inside Alternatives, not for nouns in running prose.
- **Curly quotes**, usually pasted in from Confluence or a word processor. Replace with straight
  quotes.
- **Phrases that announce importance** rather than stating the point: "load-bearing", "carries the
  real weight", "it's worth noting that", "the key insight is". Delete the announcement and keep the
  point.
- **"Not just X, but Y."** Say Y.
- **Inflated word choice.** "Use", not "utilize". "Enough", not "sufficient". "Start", not
  "commence".

Two cautions. Don't let the pass flatten the numbers, the named owners, or the plainly stated bad
news, which are the parts that make the document useful. And run it over the tables as well as the
prose, because a Risk or Benefit cell written in slop is as visible to the reader as a paragraph.

## Reviewing an existing solution document

Check, in order:

1. Does the document use the five sections (Introduction, Requirements, Solution, Concerns, Appendix) with the required subheadings, and is any omission explained in a line rather than silently dropped?
2. Can a non-technical reader finish it without stopping at an undefined term? Every stop is a defect.
3. Does Problem Statement stay clear of the solution, and does Overview say what changes for existing users?
4. Does every benefit trace to a functional requirement, and every requirement to something in Validation?
5. Does Behavior When Things Go Wrong state outcomes, or has it leaked mechanism?
6. Is the status quo among the alternatives, and does the chosen option admit a real cost?
7. Does every risk have a mitigation and an owner, and has anything the design document understated been escalated into Concerns?
8. Is there anything here (a schema, an endpoint, a configuration key, an algorithm) that belongs only in the design document?
9. Does the prose hold to Google style: second person, active voice, present tense, US spelling, no Latin abbreviations, no "simply" or "just"?
10. Has the `unslop` pass been run? Check the tells directly: em dashes, semicolons, mid-sentence bold, curly quotes, "not just X, but Y", and phrases that announce importance instead of stating the point.
11. Would a reader know, after finishing, what they're being asked to decide?
