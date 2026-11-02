---
name: commit
description: Write commit messages when creating or amending commits, or when asked to suggest a commit message.
---

# Commit messages

- Follow the repository's documented commit conventions first.
- Check recent commit messages with `git log -10 --format=%s` and match the established style. If there is no clear style, use Conventional Commits: `type(scope): summary` (scope optional).
- Review the staged diff and describe only what is being committed.
- Keep the subject concise, imperative, and specific. Add a body only when useful to explain why.
- Do not create, amend, or push a commit unless asked.
