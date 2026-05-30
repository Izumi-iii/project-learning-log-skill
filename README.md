# Project Learning Log Skill

`project-learning-log` is a Codex skill for generating structured Markdown learning notes from a programming session. It is designed for learners who use Codex while building small projects and want a reusable record of what changed, why it changed, what concepts were involved, and how the work was verified.

## What It Does

This skill helps Codex create project-specific learning logs by combining:

- The current conversation context
- The project files in the workspace
- Git status and diffs
- Important code snippets
- Validation commands and results
- Follow-up practice ideas

By default, it saves notes inside the project:

```text
docs/learning-notes/YYYY-MM-DD-short-topic.md
```

Example:

```text
docs/learning-notes/2026-05-30-calculator-ui-polish.md
```

## When To Use It

Use this skill when you want Codex to generate or update a study note, project retrospective, coding diary, or learning record.

Example prompts:

```text
Use project-learning-log to generate a learning note for this project.
```

```text
Create a Markdown learning log for today's calculator UI work.
```

```text
Review this coding session and save a study note in docs/learning-notes.
```

```text
Generate a project retrospective that explains the key code changes and what I should review next.
```

## Generated Note Structure

The default Markdown output includes:

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

Sections that are not relevant can be omitted.

## Installation

Clone this repository into your Codex skills directory:

```bash
cd ~/.codex/skills
git clone https://github.com/Izumi-iii/project-learning-log-skill.git project-learning-log
```

Then restart or refresh Codex so the skill can be discovered.

The expected folder structure is:

```text
~/.codex/skills/project-learning-log/
  SKILL.md
  agents/
    openai.yaml
  README.md
```

## Usage

After installation, ask Codex to use the skill while you are inside a project workspace:

```text
Use project-learning-log to create a learning note for the current project.
```

Codex will usually:

1. Inspect the current project root.
2. Check `git status --short`.
3. Review relevant changed files and diffs.
4. Summarize the learning goal and implementation.
5. Save a Markdown note under `docs/learning-notes/`.
6. Read the file back briefly to verify it was created.

## Example Output

```md
# Calculator UI Polish Learning Log

## Session Goal

Improve a simple calculator app visually while understanding how the UI changes work in code.

## What Changed

- Updated the calculator window size.
- Added a modern dark background.
- Styled number, function, operator, and equals buttons.
- Added an expression label to show operations such as `7 + 8`.

## Key Concepts Learned

- How `wantsLayer` enables layer-backed visual styling in AppKit.
- How to set button backgrounds, borders, corner radius, and shadows.
- How to use runtime layout changes while keeping storyboard outlets/actions.

## Validation

Ran:

```bash
xcodebuild -project myCalculator.xcodeproj -scheme myCalculator -configuration Debug build
```
```

## Privacy Notes

The skill is intended to summarize local learning work. Before publishing generated notes, review them for:

- Personal file paths
- Private project names
- Credentials or tokens
- Internal URLs
- Sensitive logs or terminal output

The skill instructions explicitly ask Codex not to include private credentials, tokens, full environment dumps, or unnecessary logs.

## Files

- `SKILL.md` - The actual Codex skill instructions.
- `agents/openai.yaml` - UI metadata used by Codex.
- `README.md` - Human-readable documentation for GitHub.

## License

Add a license if you want others to reuse or modify this skill under clear terms. For small open-source skills, MIT is a common choice.
