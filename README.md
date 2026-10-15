# prompt-db

A personal prompt database for Claude Code. Save prompts once, run them later. Values you fill in at run time are substituted into `<placeholder>` tokens before the prompt executes.

## Install

Clone this repo into your Claude Code skills directory as a folder named `prompt-db`:

```sh
git clone https://github.com/attentiondotnet/prompt-db ~/.claude/skills/prompt-db
```

On Windows the skills directory is `%USERPROFILE%\.claude\skills`.

## Use

Talk to Claude Code naturally:

- **Save.** "Save this prompt as commit-helper: Write a commit message for `<diff>`."
- **Run.** "Run commit-helper." Claude asks for each placeholder value, substitutes, and executes the prompt.
- **List.** "Show me my saved prompts."
- **Show.** "Show the commit-helper prompt."
- **Delete.** "Delete commit-helper."

## Placeholders

A `<word>` or `<short phrase>` token in a saved prompt becomes a fill-in slot. When you run the prompt, Claude lists the slots and collects values for the ones you did not already provide. Write `\<` in a prompt to keep a literal `<` instead of opening a slot.

## Storage

Prompts live in `~/.claude/prompt-db/` as one markdown file per prompt, named in kebab-case. That folder is yours, is created on first save, and is not part of this repo.
