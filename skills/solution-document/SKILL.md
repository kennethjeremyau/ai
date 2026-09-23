---
name: solution-document
description: Write or review a Solution Document — the stakeholder-facing write-up of a system, feature, or integration covering the problem statement, executive summary, scope, requirements, constraints, the solution in plain language, concerns and open questions, risks, alternatives considered, data flow, and interfaces. Use when asked for a "solution document", "solution overview", "solution brief", "solution summary", a "non-technical" or "stakeholder" or "customer-facing" version of a design, or when asked to derive one from an existing design document. Not for the engineer-facing write-up — that is the design-document skill.
---

# Solution Document

A Solution Document explains **what problem is being solved, what changes for the people affected, and why this shape rather than another**. Its readers are product and project managers, support and delivery staff, and often the customer. They won't build the system and might not know how it works.

Its job is to let someone decide, plan, or explain. If a reader can't say yes or no to the project afterward, or explain the change to their own stakeholders, the document has failed.

## What belongs here

The problem, the requirements, the shape of the answer, the risks, and what is still undecided. Enough mechanism to make the solution credible, and no more.

Not schemas, endpoints, message formats, command-line options, code names, configuration keys, or algorithms. Those belong in the design document, and here they go out of date as the implementation changes. Data flow and Interfaces describe systems, people, and kinds of information, never fields or calls.

The test for any sentence: would the reader's decision change without it? If not, cut it.

## Deriving one from a design document

The design document is for the people who build and run the system. Link to it from References, and don't summarize it section by section. Most of it converts:

| From the design document | Becomes |
|---|---|
| Purpose | Problem Statement |
| Overview | Executive Summary |
| Scope | Scope |
| Scope, plus the guarantees the design commits to | Requirements > Functional |
| Operation targets | Requirements > Non-Functional |
| Deployment, dependencies, and assumptions | Constraints |
| Architecture Diagram | Architecture Diagram, redrawn |
| Design Overview and Modules | High-Level Design, as guarantees |
| Fault Tolerance, Disaster Recovery | Concerns > Behavior when things go wrong, as outcomes |
| `TBD` markers | Concerns > Open questions, owned by whoever decides |
| Security, Privacy | Risks, as consequences to people |
| Alternatives | Alternatives, internals dropped |
| Data flow | Data flow, kinds of information only |
| Interfaces | Interfaces, who and what connects |
| Testing | Requirements, as the evidence each is met |
| References, Glossary | References, Glossary, rewritten for this reader |

Gather what can't be derived: cost and effort, stakeholder and support impact, the delivery plan, risk ownership, and the decision the reader must make. If it's unavailable, raise it as an Open question with an owner. Never invent a business fact. This reader has no way to detect it.

**Escalate what the design document understates.** A neutral clause there is often the headline here. Look for anything that runs without authentication, bypasses access restrictions, writes data unencrypted, keeps personal data too long, leaves limits unenforced, or uses unvalidated defaults. Each is a risk with an owner.

## Structure

Copy `template.md` and fill it in. The template gives the headings, their order, and the fields each section needs. Keep every heading. If a section doesn't apply, say so in one line.

The guidance below covers what the template can't show.

### Problem Statement

The problem in the reader's terms, with no solution. Say what people do today instead and why that doesn't scale, which is the cost of doing nothing. The `Limit` | `Effect on the customer` table pairs each technical limit with a consequence someone feels.

### Executive Summary

The only part many readers finish. "Nothing changes for them" is often the most valuable sentence in the document. Put the bad news here too, because a limitation first found in Risks feels hidden.

### Scope

The out-of-scope list matters more. List what a reasonable person assumes is included but isn't, such as delivery of the output, access control, retention changes, or integration with the customer's systems.

### Requirements

A reader must be able to judge each requirement met or unmet. Three to five functional requirements is usually right. Ten means design decisions got in. The "How it's shown to be met" column is the shape of sign-off, not a test plan. Mark any non-functional target that is proposed but not agreed.

### Constraints

What the solution needs but doesn't control, including what the customer is responsible for. Each is a way to fail that is nobody's bug.

### Architecture Diagram

Redraw it for this reader instead of reusing the design document's diagram. If the solution is too simple for a diagram, say so in one line.

### High-Level Design

- Introduce each concept with an ordinary word and the real term in brackets, such as *a bookmark (cursor)*. Then use only the ordinary word.
- Explain why the mechanism gives the guarantee, not how the algorithm works. "It resumes from an exact recorded position, so no record falls between two pages" is the whole argument. Use one analogy at most.
- In "What changes in practice", name any group for whom nothing changes.
- Each benefit traces to a functional requirement. "Why it matters" is a consequence for someone. "Complete extraction at any volume" is a property. "The limit stops constraining what the customer can ask for" is why anyone cares.

### Concerns

- **Behavior when things go wrong.** Open with the principle in one sentence, usually that the system produces a correct result or stops with a clear reason, never a quietly wrong one. Each row gives the outcome, not the mechanism. Include cases handled invisibly, because leaving them out reads as an omission.
- **Open questions.** A yes/no or a value settles each question. The owner can actually decide, and might be the customer. Mark which questions block sign-off.

### Risks

The impact column says what happens to someone. Every risk needs a mitigation and an owner, or it moves to Open questions. State escalated security and privacy facts plainly.

### Alternatives

Always include the status quo and the cheap option that was rejected, with the specific reason it fails. Give the chosen option's real cost. Nobody believes an option with no drawbacks.

### Data flow

Name kinds of information, such as "alarm history", not fields. If information leaves the customer's site or network, say so plainly.

### Interfaces

Name the owner of each connected system and any change they must make. A change required of another team also goes in Constraints or Open questions.

### Appendix

- **References.** Give each one a descriptive title.
- **Glossary.** Write it fresh for this reader. The design document's glossary brings back the jargon this document avoids.

## Writing standard

Use the `doc-style` skill, then run `unslop` over the finished draft, tables included. Don't let the pass remove numbers, owners, or bad news. Also:

- **Second person.** Address the reader as "you". Name the actor instead of writing "we": "the operations team runs the job".
- **Plain language, not simplified content.** The reader is busy, not incapable.
- **Guarantees, not mechanisms.** State what holds and why. The how is in the design document.
- **Numbers survive the translation.** "5,000 records at a time". Benefits without numbers read as marketing.
- **One name per concept**, matching the Glossary.
- **Every claim traceable** to the design document or the system.

## Reviewing an existing solution document

Check each section against the guidance above, then:

1. Can a non-technical reader finish it without stopping at an undefined term?
2. Would a reader know what they're being asked to decide?
3. Does every benefit trace to a requirement, and every requirement say how it's shown to be met?
4. Has everything the design document understated been escalated into Risks?
5. Has design detail leaked in, especially in Data flow and Interfaces?
6. Have the `doc-style` and `unslop` passes been done?
