---
name: user-guide
description: "Write or review a User Guide, the manual a first-time user reads to set up a software product and get real work done with it. Covers what the product does, prerequisites, setup, a tour of the interface, task-by-task instructions, troubleshooting, and a glossary. Use when asked for a 'user guide', 'user manual', 'getting started guide', 'end-user documentation', 'how-to guide', or 'onboarding docs' for an application. The reader is non-technical, so this is not engineer-facing documentation."
---

# User Guide

The reader has never opened this product. They are not an engineer. Someone else chose the software for them, they are short on time, and they will stop reading the moment they feel lost.

Write for that reader. Every rule below follows from it.

## Before you write

Answer these five questions. Look in the source, the running product, and existing docs. Ask the user for anything you cannot find.

1. Who is the reader, and what job are they doing?
2. What do they want to accomplish? List the three to seven real tasks.
3. What must they have first? Account, license, permissions, hardware, network access.
4. What do they see on first launch?
5. What goes wrong most often?

Never invent a screen, menu name, button label, default value, or error message. Check it or ask.

## Structure

Follow `template.md`. Order the sections so the reader can start at the top and work down:

| Section | Purpose |
| --- | --- |
| What this does | One paragraph in plain language, plus who it is for. |
| Before you begin | Everything needed before step one. |
| Set up | Install, sign in, first-run configuration. |
| Find your way around | Names the parts of the screen the tasks refer to. |
| Tasks | One chapter per goal, in the order a new user meets them. |
| When something goes wrong | Symptom, cause, fix. |
| Glossary | Terms the reader will hear from colleagues or see on screen. |
| Get help | Where to go when the guide runs out. |

Name each task chapter after the reader's goal, not the feature. Write "Send a report to your team", not "Export module".

## Writing the steps

- Number the steps of a procedure. Use bullets only for lists of choices.
- One action per step. Split a step that contains "and then".
- Put the location first, then the action: "In the toolbar, click Save."
- Write UI labels exactly as they appear on screen, in bold. Bold nothing else.
- Say what the reader should see after a step when the result is not obvious.
- Put warnings before the step they apply to, never after.
- Start each chapter by saying what the reader will have at the end, and end it by telling them how to confirm it worked.

## Language

- Second person, present tense, active voice. "You click Save", not "The file can then be saved".
- One idea per sentence, around 20 words or fewer.
- Use the plainest word that is accurate. "Use", not "utilize". "Set up", not "provision".
- Define a technical term the first time you use it, or rewrite the sentence to avoid it. Spell out an acronym on first use.
- Cut anything about how the product works internally unless the reader has to act on it.
- Never write "simply", "just", "easy", "obviously", or "of course". The reader who is stuck reads these as an insult.
- Describe what the reader does, not what the system does, unless they are waiting on it.

## Screenshots

Include one when the reader has to find something on screen for the first time, or when a step is hard to describe in words. Crop to the part that matters, mark the target, and caption it with the step it belongs to. Write alt text that names the action, not the pixels.

## Review checklist

Check every one of these before you hand the guide over.

- A reader with no background can go from nothing to a finished task using only this guide.
- Every prerequisite appears before the step that needs it.
- Every label, path, and message in the guide matches the product.
- No undefined jargon and no unexplained acronym.
- Every procedure ends with a way to confirm success.
- The troubleshooting section covers the failures the reader will actually hit, described the way they will see them.

## Related skills

- Use `doc-style` for sentence-level and structural conventions.
- Run `unslop` on the finished draft.
