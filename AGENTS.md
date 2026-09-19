# AI working conventions

This file is the source of truth for how AI assistants work in this repository. `CLAUDE.md` points here. When a tool-specific file and this file disagree, this file wins.

## Explanation style

Give a full walk-through. Explain the approach before the result, name the alternatives considered and why they were rejected, and show the reasoning behind each non-obvious decision. Show commands and their output rather than summarizing them. Do not shorten explanations to save space.

## What the assistant may draft

- Code, scripts, configuration, and file scaffolding.
- Commit messages and `prompt-log.md` entries.
- First drafts of engagement briefs and decision memos. The hypothesis in a brief and the recommendation in a memo come from me; the assistant drafts structure and prose around them, and I rewrite before anything is final.
- Edits to my bio and resume when I supply the source document. The assistant reformats, condenses, and corrects; it does not add facts.

## What the assistant may not draft

- Any biographical, career, or publication fact that is not in a source I provided. If a slot is empty, leave `<!-- TODO -->` and tell me.
- A capability, an engagement, or a data source that does not exist yet.
- The hypothesis of a brief or the recommendation of a memo.

## What must never be pasted into a model

- Credentials, API keys, tokens, and the contents of any `.env` file.
- Confidential data from an employer or an engagement client.
- Protected health information, identifiable human-subjects data, or anything covered by an IRB protocol or HIPAA.
- Unpublished research results and manuscripts.

If a task appears to need any of these, stop and ask me for a redacted or synthetic substitute.

## House style

### Prose

Voice reference: Burkhart et al., "Biology-inspired graph neural network encodes reactome and reveals biochemical reactions of disease," *Patterns* (2023), <https://pmc.ncbi.nlm.nih.gov/articles/PMC10382942/>, and the bio in `README.md`. Match them.

- Headings are declarative sentences that state the finding, not the topic. "Our GNN differs from and extends existing models," not "Comparison with prior work."
- Every claim carries its number and its comparison in the same sentence. State the metric, the control it is measured against, and the margin.
- Every choice carries its reason in the same sentence. "PCA was selected due to concerns for both performance and simplicity." A choice without a stated reason is unfinished.
- Hedge in proportion to the evidence. *Plausibly*, *may*, *we contend*, and *suggesting* each mean something different; use the one the evidence supports and no stronger.
- Limitations and compromises get their own section, stated plainly, each with the reason the compromise was made and what would remove it.
- Formal register. Sentences may be long and subordinate when the qualification belongs in the sentence; connectives such as *thus*, *furthermore*, and *however* are welcome. No marketing voice, no superlatives, no closing flourish.
- Prefer concrete categories and named things to narrative. "Enterprise IT, automotive, and defense industries," not "a varied career in industry." Name functions, identifiers, datasets, and versions exactly: `prcomp()`, `GraphConv()`, Reactome:R-HSA-381750.
- Abbreviations are acceptable where the reader will recognize them: U. Hawaii, HI, GNN, ARI.
- First person. Singular for this repository's own documents, plural in co-authored work.
- Numbers carry units and a source. Cite inline.
- When editing my prose, cut rather than add. Do not append summary sentences or transitions I did not write.

### Code

- Python only unless I say otherwise.
- Formatted with `black` and linted with `ruff`; the formatter decides, not taste.
- `snake_case` for functions and variables, `PascalCase` for classes, `UPPER_CASE` for constants.
- Type hints on every function signature. Docstrings on public functions.
- Comments explain why, not what. No commented-out code.

## Repository rules

- Organize by capability and engagement only. Never name a folder after a course, a term, or a class code.
- Every directory holds at least one file.
- Slugs are lowercase and hyphen-separated, three to six words. Dated files lead with `YYYY-MM-DD-`.
- Briefs are written before the work starts. Decision memos are written after it ends.
- Placeholder files stay placeholders until I fill them.

## Standing rules

- At the end of every session the assistant appends an entry to `prompt-log.md` stating what was asked, what was built, and what I had to correct. Entries are written at the time of the session and are never backfilled.
- The assistant prints any file that affects publication (`.gitignore`, collaborator settings, visibility) before applying it.
- Commit messages say what changed. "Initial commit", "update", and "fix" are not acceptable messages.
