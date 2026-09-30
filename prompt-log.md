# Prompt log

A running record of AI sessions that mattered. An entry is logged when a session changes a deliverable, a decision, a convention, or the shape of the repository; routine questions are not logged. Each entry states what I asked for, what the assistant built, and what I had to correct. The assistant appends the entry at the end of the session it describes. Entries are never backfilled, so a missing entry means the session was not logged.

## 2026-09-18 — Stage 0 repository setup

**What I asked for.** Stand up this portfolio repository to the fixed Stage 0 standard: directory skeleton with stub READMEs, grouped `.gitignore`, the five root files, two descriptive commits, a public push, and a collaborator invite for the instructor.

**What the assistant built.** The folder layout (`.claude/skills`, `capabilities`, `docs/briefs`, `docs/decisions`, `data`, `analysis`, `analysis/figures`) with a one-sentence README in each; the `.gitignore`, printed for review before commit; `README.md` with the bio placeholder and an empty engagement index; `RESUME.md` converted from my Word resume; `AGENTS.md` written from my answers to four questions on explanation style, drafting limits, what never goes into a model, and house style; the one-line `CLAUDE.md`; and this log. It made the two commits and pushed to `jgburk/joshua-burkhart`; I sent the collaborator invite to `adamwstauffer` myself through the GitHub web UI.

**What I had to correct.**

- The repository already existed on GitHub with a web-generated first commit, so the assistant asked whether to recreate it; I told it to keep the existing repository and skip `gh repo create`. The two new commits sit on top of that first commit.
- The GitHub CLI was not installed. The assistant installed it with Homebrew and I ran `gh auth login` myself.
- The instructions called for `RESUME.md` to hold section headers and `<!-- TODO -->` markers only. I supplied `JGB_CORPORATE_RESUME.docx` and told the assistant to use it instead, so the resume is real content rather than a placeholder.
- I dropped the Word resume into the repository folder; the assistant moved it and `instructions.txt` out of the working tree so neither is committed and the final grep check runs clean.
- After the first two commits I asked the assistant to review the course pages against the repository. It found two open checklist items: the instructor invitation had not been sent (the `gh` invite call needs the owner's login) and the bio was still a placeholder. I added `adamwstauffer` through the GitHub web UI; the assistant confirmed the pending invitation with `gh api` once I logged in as the owner.
- The assistant drafted one bio from `RESUME.md`. I rewrote it: I cut the narrative framing and the closing sentence about the portfolio, replaced the industry description with named sectors and product types, and shortened the credentials.
- The first `AGENTS.md` prescribed short declarative sentences. I pointed the assistant at my *Patterns* (2023) article to learn my actual voice; it rewrote the prose rules to call for declarative headings that state the finding, claims that carry their number and comparison, choices that carry their reason, calibrated hedging, a limitations section, and cutting rather than adding when editing my prose.
- `RESUME.md` now lists both GitHub accounts (`joshuaburkhart` and the `jgburk` portfolio) and both career documents carry the one-line AI disclosure the course asks for.

## 2026-09-18 — Grade the repository against the course standard and fix AGENTS.md

**What I asked.** Review the Stage 0 pages and grade the submission, then apply the fixes.

**What the assistant produced.** A grade of A− against the nine-item checklist (all met) with five deductions, all in `AGENTS.md`, taken from the portfolio-repo standard and the AI-conventions baseline the stage page delegates to. It then edited `AGENTS.md`: the assistant may no longer draft briefs, analyses, memos, or reflections, first draft included; the baseline Naming section is included word for word; the standing prompt-log rule is the exact sentence the setup prompt requires; the never-paste list names my own records (JABSOM Alzheimer's project data, dbGaP-governed GTEx and TCGA, ICI biomarker cohort data, manuscripts under review, grant applications); the file names my field; and a Mistakes to avoid section records the three errors from this session.

**What was wrong and how it was caught.** The first `AGENTS.md` permitted first drafts of briefs and memos because the assistant offered that as an option and I chose it; the course forbids it. Caught by reading the AI-conventions baseline rather than the stage page alone. The verbatim Naming section contains the word "week," which the setup grep flags; kept verbatim because the standard requires it and the rule targets folder names.

## 2026-09-29 — Stage 0 path fixes and AGENTS.md notes

**What I asked.** Follow my Stage 1 plan: close the two canonical paths the Stage 0 feedback flagged, explain in `AGENTS.md` why the verbatim Naming section keeps the word "week," and prepare the repository for a brief I write myself.

**What the assistant produced.** A read-only orientation report confirming that no spec, workbook, analysis, or decision memo exists; `docs/README.md`; `capabilities/marginal-analysis/README.md` with an empty engagements list; reworded naming lines in `docs/briefs/README.md` and `docs/decisions/README.md`; and two `AGENTS.md` additions, a subsection after Naming explaining why that section keeps "week" and a rule under "What the assistant may not draft" forbidding any computation or modeling for an engagement before its brief is committed.

**What was wrong and how it was caught.** The `docs/briefs/` and `docs/decisions/` READMEs prescribed `YYYY-MM-DD-engagement-slug.md`, which contradicts the undated `perfect-competition-brief.md` the stage page gives; the assistant caught it during orientation and I chose to align both READMEs with the stage-given filenames. My plan listed the Stage 0 drafting-permission error as a possible addition to "Mistakes to avoid"; the assistant found it already recorded, and I left the list unchanged. My plan also called for a commit after each phase; I overrode that and held all changes uncommitted, then chose two commits when the brief was ready: these supporting changes first, then the brief alone under the message the stage page prescribes. The assistant's mechanical lint of my first brief draft failed four checks (status value, no bed counts, empty assumptions section, no falsifying outcome); I revised the brief myself and the second lint passed, with length flagged as borderline at 221 words.
