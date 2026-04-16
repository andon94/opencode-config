---
name: web-design-guidelines
description: Review UI code for Web Interface Guidelines compliance. Use when the user explicitly asks for a UI, UX, accessibility, or design best-practices review. Skip this for routine implementation or debugging tasks that are not framed as a review.
metadata:
  author: vercel
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

# Web Interface Guidelines

Review files for compliance with Web Interface Guidelines when the user is asking for an explicit review or audit.

## How It Works

1. For a full review, fetch the latest guidelines from the source URL below
2. Read the specified files (or prompt user for files/pattern)
3. Check against all rules in the fetched guidelines
4. Output findings in the terse `file:line` format

## Guidelines Source

Fetch fresh guidelines before each substantial review:

```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```

Use WebFetch to retrieve the latest rules. The fetched content contains all the rules and output format instructions.

If the user is asking a narrow implementation or debugging question rather than an explicit review, do not invoke this skill just because UI files are involved.

## Usage

When a user provides a file or pattern argument:
1. Fetch guidelines from the source URL above
2. Read the specified files
3. Apply all rules from the fetched guidelines
4. Output findings using the format specified in the guidelines

If no files specified, ask the user which files to review.
