---
name: project-learning-log
description: Generate a Markdown learning record from the current conversation and project state, using the user's language by default. Use when the user asks to create, save, summarize, review, or update study notes, learning logs, project retrospectives, lesson notes, coding diaries, or `.md` documentation that explains what was built, which files changed, key code concepts, validation commands, mistakes fixed, and follow-up exercises for a learning-focused programming project.
---

# Project Learning Log

Create concise, practical Markdown notes that help the user review what they learned from a coding session. Prefer project-specific evidence over generic explanations.

## Workflow

1. Confirm the target project root from the current working directory or the user's path.
2. Inspect the project lightly:
   - Run `git status --short`.
   - Use `git diff --stat` and focused `git diff -- <file>` when there are local changes.
   - Use `rg --files` and read only files relevant to the learning topic.
3. Reconstruct the learning arc from the conversation:
   - Initial goal.
   - Important decisions.
   - Mistakes or confusing points.
   - Final implementation and verification.
4. Write one Markdown file under the target project directory unless the user requests only a draft response.
5. Verify the file exists and briefly inspect the rendered content by reading it back.

## Default Location And Naming

Use this default path inside the target project root unless the user specifies another destination:

```text
docs/learning-notes/YYYY-MM-DD-short-topic.md
```

Use the current date from the environment. Keep the slug lowercase with hyphens, for example:

```text
docs/learning-notes/2026-05-30-calculator-ui-polish.md
```

Create parent directories when needed.

Never save the learning note inside the skill directory unless that directory is itself the project being documented.

## Language

Write the learning note in the user's language by default:

- If the user asks in Chinese, write the note in Chinese.
- If the user asks in English, write the note in English.
- If the user explicitly requests a language, follow that request.

Keep code identifiers, file paths, command names, API names, and code snippets in their original language.

## Note Structure

Use this structure by default. Omit sections that would be empty.

```md
# <Project Topic> Learning Log

## Session Goal

## Project Context

## What Changed

## Key Concepts Learned

## Code Walkthrough

## Problems And Fixes

## Validation

## Review Checklist

## Follow-Up Practice
```

## Writing Guidelines

- Write for a learner who will reread the note later, not for a code reviewer.
- Use concrete file references and line references when useful.
- Prefer short explanations followed by small code snippets.
- Explain why the code exists, not just what it does.
- Include commands that were actually run, especially build/test commands.
- Mark any unverified claims clearly.
- Do not include private credentials, tokens, full environment dumps, or unnecessary logs.
- Keep the note focused. A typical note should be 80-180 lines.

## Content Requirements

For each meaningful code change, include:

- File path.
- Purpose of the change.
- The main API, language feature, or design idea involved.
- One short snippet when it helps learning.

For UI/frontend work, also include:

- Layout strategy.
- Color/type/spacing decisions.
- Interaction states and feedback.
- How visual behavior was verified.

For debugging work, also include:

- Symptom.
- Root cause.
- Fix.
- How the fix was validated.

## Output Behavior

If the user asks to save the note, edit the filesystem directly. Use `apply_patch` for manual file creation or edits. If the user asks only for a draft, return the Markdown in the final answer and do not write a file.

End the final response with the saved file path and a one-sentence summary of what the note covers.
