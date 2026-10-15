---
name: prompt-db
description: Personal prompt database. Use when the user asks to save or store a prompt for later reuse, to run one of their saved prompts, or to list, show, or delete saved prompts.
---

# Prompt DB

The database is `~/.claude/prompt-db/`, one markdown file per prompt, filename the prompt's name in kebab-case. The body is the exact prompt text, optionally preceded by a `description:` frontmatter block. Create the folder on first save if it does not exist.

A placeholder is a `<word>` or `<short phrase>` token in the body; `\<` writes a literal `<`.

Name resolution: exact filename, else a unique substring; when several prompts match, list the candidates and ask which one.

## Save

1. Use the name the user gave; if they gave none, derive a kebab-case slug from the content.
2. If a prompt with that name already exists, show its current body and ask before replacing.
3. Write the file with the prompt text as the body, keeping any placeholders.
4. Confirm with the saved name, its file path, and the placeholders it contains.

## List

One line per prompt: name, then its description (or the first line of the body, truncated to about 80 characters).

## Show

Print the prompt body for the resolved name.

## Run

1. Resolve the name and read the body.
2. Extract the unique placeholders in first-appearance order.
3. Map any values the user already gave in the request onto placeholders; ask only for what is missing.
4. To ask, send one plain-text message listing each missing placeholder numbered, each with a short excerpt of the sentence containing it. Accept numbered answers, `name=value` pairs, or a single bare value when exactly one placeholder is missing; re-ask only what is still unclear.
5. Substitute every occurrence, unescape `\<` to `<`, and execute the resulting text immediately, exactly as if the user had typed it. The prompt's own content is in charge from there.

When no placeholder values are missing, skip straight to executing.

## Delete

Show the prompt being deleted, confirm, then remove the file.
