# Agent skills

A collection of workflows I'm building to make AI coding agents more reliable and less tedious to work with.

## Skill: move-yaml

Move YAML blocks between files by ID/key while preserving their original content, comments, and unrelated code. The skill includes checks for missing or duplicated blocks, file discovery, and application loading.

**The problem**

While contributing to a large open-source game codebase, I needed to relocate over 50 YAML blocks across six files into more appropriate locations.

As someone new to Codex, I spent considerable time experimenting with the migration, manually exploring the codebase, and asking Codex to find similar existing definitions.

There were several decisions and concerns to keep track of:
- Where should the blocks go? I needed to examine existing files and follow the repository's conventions.
- Which blocks belong together? Related definitions needed to be grouped into appropriate destinations.
- What about existing comments? Some blocks contained comments about unfinished work that needed to survive the move.
- Can I trust the result? After each migration, I had to consider:
  - Did Codex identify the correct blocks?
  - Were they removed from their original locations?
  - Was every block copied completely, without losing or changing anything?
  - Was the destination file's structure and indentation preserved?
  - Did the verification actually check what I expected it to check?

**Current solution**

Not every part of a refactor can be standardized. Choosing where definitions belong still requires understanding the codebase and making decisions. But the actual relocation process involves many repetitive instructions.

This skill provides a reusable workflow for identifying YAML blocks, moving them without changing their contents, and checking the results against the originals.

My goal is to spend less time repeating conditions and verification requirements in every prompt, and more time planning changes and reviewing unexpected cases.

Since YAML is a major part of the codebase I contribute to, even a modest improvement to this workflow could be useful.

**Future possibilities**

If this approach proves useful through testing, similar workflows could be developed for other structured file formats.

### Install (Codex)

From your project's terminal (requires Node.js and npm):

```sh
npx skills add alekszejg/agent-skills --skill move-yaml -a codex
```

(unverified) For Claude Code, replace `-a codex` with `-a claude-code`.

### Use

Once installed, Codex can automatically select the skill when your request matches its description. No special command syntax is required.

E.g: "Move Block1 and Block2 from file1.yml to file2.yml, ordered alphabetically by ID."

Automatic selection isn't guaranteed. To explicitly invoke the skill in Codex, use $move-yaml in your prompt.

## Q&A
I've discussed developing Codex skills with several people and encountered quite a bit of skepticism and speculation. Here are some questions I've actually been asked.

#### What's the problem you're trying to solve?
One source of friction in AI-assisted development is writing and repeatedly refining prompts. Skills are one possible way to reduce that repetition.

Voice input has already made prompting significantly faster for me, but I still find myself repeating the same requirements, precautions, and verification steps just to be sure.

Ideally, I'd like to move closer to short, task-focused prompts such as "Move these definitions into that file," while keeping the established workflow consistent.

#### Won't better prompt understanding make skills redundant? Isn't this overengineering?
Possibly, for some tasks. But understanding a request and consistently following a particular workflow are different problems.

Skills let developers reuse instructions for recurring tasks instead of reconstructing them each time. You can install them globally or use them only in projects where they're relevant. If someone has already developed and tested a useful workflow, reusing it may be easier than recreating it yourself.

That doesn't mean every task needs a skill. A one-off instruction may be perfectly sufficient.

#### AI agents already let users do whatever they want. Why introduce skills?
Freedom to instruct an agent doesn't eliminate the effort required to formulate those instructions.

Sometimes a task involves a methodology you've already worked out, or one that somebody else has spent time developing. A skill packages that methodology so it can be reused.

It doesn't replace the user's prompt or decision-making. It provides additional instructions for how the task should be carried out.

## Status

Early draft. Real-world testing and cross-agent compatibility checks are still pending.

Licensed under MIT.
