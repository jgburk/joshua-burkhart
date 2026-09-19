# AI working conventions

This file is the source of truth for how AI assistants work in this repository. `CLAUDE.md` points here. When a tool-specific file and this file disagree, this file wins.

The repository is the portfolio of Joshua Burkhart, a biomedical informatician working in clinical data science and systems medicine at the University of Hawaii John A. Burns School of Medicine, and an MBA student at the Shidler College of Business. Engagements here draw on health data, biochemical network models, and business analysis.

## Explanation style

Give a full walk-through. Explain the approach before the result, name the alternatives considered and why they were rejected, and show the reasoning behind each non-obvious decision. Show commands and their output rather than summarizing them. Do not shorten explanations to save space.

## What the assistant may draft

- Code, scripts, configuration, and file scaffolding.
- Commit messages and `prompt-log.md` entries.
- Edits to my bio and resume when I supply the source document. The assistant reformats, condenses, and corrects; it does not add facts.
- Critiques of a brief, analysis, or memo I have already drafted: the weakest claim, the alternative I did not consider, the assumption I left unstated.

## What the assistant may not draft

- My briefs, analyses, memos, or reflections, first draft included. These are evidence of my judgment; I write them and the assistant reviews.
- Any biographical, career, or publication fact that is not in a source I provided. If a slot is empty, leave `<!-- TODO -->` and tell me.
- A capability, an engagement, or a data source that does not exist yet.
- Every statistic or figure the assistant gives me is a draft until I verify it against a source.

## What must never be pasted into a model

- Credentials, API keys, tokens, and the contents of any `.env` file.
- Patient records, clinical variables, and sample identifiers from the JABSOM Alzheimer's Disease comorbidity project, or from any other study covered by a UH IRB protocol or HIPAA.
- Controlled-access genomic and clinical data, including dbGaP-governed GTEx and TCGA records and cohort data from the immune checkpoint inhibitor biomarker work.
- Confidential data from an employer, a collaborating institution, or an engagement client, including anything under a data use agreement.
- Unpublished research results, manuscripts under review, and grant applications.
- Personal data about anyone else: names attached to records, contact details, anything identifying a classmate, a colleague, or a study participant.

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

## Naming

- The directory matters most. A file in the wrong folder may not be found at all. If you are not certain which folder a file belongs in, ask me before you write it — do not choose for me.
- Graded files use the exact filename the stage brief gives — lowercase, hyphens, no spaces. Some courses date-stamp (YYYY-MM-DD-lastname-slug.md); the stage page says so when they do.
- Slugs name the engagement, never the week, the course, or the assignment number.
- Never invent a path or a filename. I will give you the exact one.

## Repository rules

- Organize by capability and engagement only. Never name a folder after a course, a term, or a class code.
- Every directory holds at least one file.
- Slugs are lowercase and hyphen-separated, three to six words. Dated files lead with `YYYY-MM-DD-`.
- Briefs are written before the work starts. Decision memos are written after it ends.
- Placeholder files stay placeholders until I fill them.

## Standing rules

- At the end of every session that changed a file, append one entry to prompt-log.md: the date, what I asked, what you produced, what was wrong and how it was caught. Never backfill earlier sessions and never edit a past entry.
- The assistant prints any file that affects publication (`.gitignore`, collaborator settings, visibility) before applying it.
- Commit messages say what changed and why. "Initial commit", "update", and "fix" are not acceptable messages.
- Do the work I asked for. If you notice something worth doing that I did not ask for, tell me instead of doing it.
- When work changes, update the document that describes it in the same commit. A capability's README names the engagements that exercised it; keep that current.

## Mistakes to avoid (append to this list)

Record errors here as they happen, so the same one does not repeat.

- 2026-09-18 — The assistant wrote the prose rules as "short declarative sentences" from a menu of generic options instead of from my writing. Caught when I read the file; corrected by pointing it at my *Patterns* (2023) article. Derive style from a sample of my work, never from a default.
- 2026-09-18 — The assistant recorded in `prompt-log.md` that it had sent the collaborator invitation when I had sent it through the GitHub web UI. Caught on re-reading the log before the final report. Log only actions the assistant performed and verified.
- 2026-09-18 — The assistant offered "first drafts of briefs and decision memos" as a permitted option, contradicting the course rule that briefs, analyses, memos, and reflections are mine from the first draft. Caught when grading the repository against the AI conventions baseline. Check drafting permissions against the course boundary before offering them.
