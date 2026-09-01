---
name: reference-documents
description: Create quick-reference documents from instructional source material and the user's notes. Use when the user wants a reference note, cheat sheet, glossary, runbook, or Obsidian note for later lookup.
---

# Reference Documents

Create a **companion note**: a clean, searchable rendering of the user's notes,
not a substitute for the instructional source. Preserve what the user chose to
capture; link outward for depth.

## 1. Establish the source set

Collect the user's notes, instructional source, raw-note files, and desired
output location or format. Infer these from context when possible. If the user's
notes or source are unavailable, ask for them rather than reconstructing them
from parametric knowledge.

The user's notes control scope, emphasis, order, and level of detail. The
instructional source controls factual corrections and supplies only context
needed to make a captured point understandable. Surface discrepancies instead
of silently choosing a side.

This step is complete when every supplied item is accessible and classified as
user notes, instructional source, or raw attachment.

## 2. Transcribe the notes

Inventory only what the user recorded: headings, concepts, procedures,
relationships, examples, warnings, and personal observations. Preserve the
notes' sequence and hierarchy unless a small reorganization materially improves
lookup.

Translate handwriting or rough notes into concise Markdown. Retain the user's
wording where clear; normalize spelling, terminology, and formatting. Use a
table, checklist, diagram, code block, or callout only when it directly reflects
the notes' structure.

Consult the instructional source when a note is ambiguous, incomplete enough to
mislead, or appears inaccurate. Add the smallest clarification needed and avoid
importing uncaptured sections, examples, edge cases, or comprehensive detail.

This step is complete when every legible note is represented or explicitly
marked unreadable, and every addition from the source is necessary to understand
or correct it.

## 3. Write the companion note

When creating or editing an Obsidian note, invoke the `obsidian-markdown` skill
and follow its workflow for properties, internal links, embeds, and callouts.

Write concise Obsidian-flavored Markdown unless the user requests another
format. Follow the handwritten notes closely in content and detail. Favor short
headings and bullets over orientation prose, exhaustive explanations, expanded
checklists, or newly invented structure.

End with:

- a direct link to each instructional source
- links or embeds for the imported raw notes

Add wikilinks only for notes known to exist. The note may depend on its linked
source for fuller teaching; it needs only enough context to retrieve what the
user recorded quickly.

## 4. Verify and save

Compare the draft line by line with the user's notes. Remove source-derived
material that is not required for clarification or correction. Check links and
raw-note embeds, preserve unresolved ambiguity, and save to the requested
location. If none was given, propose a filename and return the complete note.

The work is complete when the document faithfully mirrors the user's notes,
necessary source clarifications are minimal, and all source and raw-note links
resolve.
