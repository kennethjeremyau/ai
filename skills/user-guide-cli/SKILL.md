---
name: user-guide-cli
description: "Write or review a User Guide for a command-line tool, the manual a first-time user reads to install it and get real work done with it. Covers what the tool does, prerequisites, installation, a command-by-command reference with an example for each, troubleshooting, and a glossary. Use when asked for a 'user guide', 'user manual', 'getting started guide', 'end-user documentation', 'how-to guide', or 'onboarding docs' for a CLI, command-line tool, or terminal application. The reader runs commands but is not an expert, so this is not engineer-facing documentation. For an application with a graphical interface, this skill does not apply."
---

# User Guide (CLI)

The reader has never run this tool. They are comfortable enough in a terminal to type what you give them, but they are not an engineer and they do not know this tool. Someone else chose it for them, they are short on time, and they will stop reading the moment they feel lost.

Write for that reader. Every rule below follows from it.

## Before you write

Answer these five questions. Look in the source, the running product, and existing docs. Ask the user for anything you cannot find.

1. Who is the reader, and what job are they doing?
2. What do they want to accomplish? List the three to seven real tasks.
3. What must they have first? Account, license, permissions, hardware, network access.
4. What is the base command, and what does it print with no arguments or with `--help`?
5. What goes wrong most often?

Never invent a command, subcommand, flag, default value, output, or error message. Run the tool or read the source. Check it or ask.

## Structure

Follow `template.md`. Order the sections so the reader can start at the top and work down:

| Section | Purpose |
| --- | --- |
| Summary | One paragraph in plain language, plus who it is for. |
| Prerequisites | Everything needed before step one. |
| Installation | Install and configure, up to the point the command runs. |
| Operation | One subsection per command, in the order a new user meets them. |
| Troubleshooting | One heading per problem, then the cause and the fix. |
| Glossary | Terms the reader will hear from colleagues or see in the output. |

Name each Operation subsection after the command it covers. Give every command a description saying what it does and when the reader would run it, and an example the reader can copy and run. Lead the description with the reader's goal, not the internals: "Sends a report to your team", not "Invokes the export module".

Operation carries two levels of table. Open the section with one row per command, so a reader who knows what they want can find it without reading the rest. Then give each command's subsection a table with one row per parameter: the name, whether it is required, what it does, and the default when the reader leaves it out. List every parameter the command accepts. Never close a table with "and others".

## Writing the steps

- Number the steps of a procedure. Use bullets only for lists of choices.
- One action per step. Split a step that contains "and then".
- Say where the reader runs a command before giving it, when it matters: "From the project directory, run:".
- Write commands, subcommands, flags, paths, and filenames exactly as the tool spells them, in backticks. Put a command the reader types on its own line in a code block.
- Show a real example, not a placeholder, and show the output the reader should expect.
- Say what the reader should see after a step when the result is not obvious.
- Put warnings before the step they apply to, never after.
- Start each section by saying what the reader will have at the end, and end it by telling them how to confirm it worked.

## Language

- Second person, present tense, active voice. "Run `export`", not "The report can then be exported".
- One idea per sentence, around 20 words or fewer.
- Use the plainest word that is accurate. "Use", not "utilize". "Set up", not "provision".
- Define a technical term the first time you use it, or rewrite the sentence to avoid it. Spell out an acronym on first use.
- Cut anything about how the product works internally unless the reader has to act on it.
- Never write "simply", "just", "easy", "obviously", or "of course". The reader who is stuck reads these as an insult.
- Describe what the reader does, not what the system does, unless they are waiting on it.

## Examples

Every command gets at least one. Use values the reader could plausibly type, and mark the ones they must replace. Keep the example to the options the command actually needs; move the rest into the prose. Show the output too when the reader has to read it to know the command worked, and trim it to the lines that matter.

## Review checklist

Check every one of these before you hand the guide over.

- A reader with no background can go from nothing to a finished task using only this guide.
- Every prerequisite appears before the step that needs it.
- Every command, flag, path, and message in the guide matches the tool, and every example runs as written.
- No undefined jargon and no unexplained acronym.
- Every procedure ends with a way to confirm success.
- The troubleshooting section covers the failures the reader will actually hit, described the way they will see them.

## Related skills

- Use `doc-style` for sentence-level and structural conventions.
- Run `unslop` on the finished draft.
