---
name: move-yaml
description: Move YAML blocks between files without changing their contents. Use for relocations by ID/key, not deduplication or value changes.
---

# YAML block move

Move only the requested blocks. Preserve their exact text and leave everything else unchanged.

## Before moving

- Check repository rules, YAML structure, file-loading behavior, references, and duplicate IDs.
- Identify blocks by ID/key and type where needed. Use YAML structure and indentation to find boundaries, not blank lines alone.
- Include comments belonging to blocks, but leave file headers untouched. Ask if ownership is unclear.
- Check anchors and aliases. Stop if moving would break them.
- Record source, destination, insertion position, and original block order.
- Before editing, record the affected files' current contents, including uncommitted changes. Store any temporary backups outside the repository. Never rely solely on Git history.

## Move

- Copy original text without reformatting or changing values.
- Preserve comments, indentation, line endings, and unrelated content.
- Change only necessary separator blank lines.
- Don't delete files, resolve conflicts automatically, or overwrite newer edits.

## Verify

- Compare moved blocks against originals exactly.
- Confirm every block was removed once and inserted once, with no duplicate IDs.
- Confirm all unrelated content and files remain unchanged.
- Run available YAML parsing and application-loading checks, including references and file discovery.

Use deterministic comparisons, not visual inspection alone. Fix only errors caused by the move. Report failed or unavailable checks.

After successful verification, delete only temporary backups created for this move. Keep them if verification fails.

## Report

Briefly report each move as moved [block ID] from [source file] to [destination file], followed by verification results and anything unverified.
