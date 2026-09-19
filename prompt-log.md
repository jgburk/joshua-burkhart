# Prompt log

A running record of AI sessions that mattered. An entry is logged when a session changes a deliverable, a decision, a convention, or the shape of the repository; routine questions are not logged. Each entry states what I asked for, what the assistant built, and what I had to correct. The assistant appends the entry at the end of the session it describes. Entries are never backfilled, so a missing entry means the session was not logged.

## 2026-09-18 — Stage 0 repository setup

**What I asked for.** Stand up this portfolio repository to the fixed Stage 0 standard: directory skeleton with stub READMEs, grouped `.gitignore`, the five root files, two descriptive commits, a public push, and a collaborator invite for the instructor.

**What the assistant built.** The folder layout (`.claude/skills`, `capabilities`, `docs/briefs`, `docs/decisions`, `data`, `analysis`, `analysis/figures`) with a one-sentence README in each; the `.gitignore`, printed for review before commit; `README.md` with the bio placeholder and an empty engagement index; `RESUME.md` converted from my Word resume; `AGENTS.md` written from my answers to four questions on explanation style, drafting limits, what never goes into a model, and house style; the one-line `CLAUDE.md`; and this log. It made the two commits, pushed to `jgburk/joshua-burkhart`, and sent the collaborator invite to `adamwstauffer`.

**What I had to correct.**

- The repository already existed on GitHub with a web-generated first commit, so the assistant asked whether to recreate it; I told it to keep the existing repository and skip `gh repo create`. The two new commits sit on top of that first commit.
- The GitHub CLI was not installed. The assistant installed it with Homebrew and I ran `gh auth login` myself.
- The instructions called for `RESUME.md` to hold section headers and `<!-- TODO -->` markers only. I supplied `JGB_CORPORATE_RESUME.docx` and told the assistant to use it instead, so the resume is real content rather than a placeholder.
- I dropped the Word resume into the repository folder; the assistant moved it and `instructions.txt` out of the working tree so neither is committed and the final grep check runs clean.
- After the first two commits I asked the assistant to review the course pages against the repository. It found two open checklist items: the instructor invitation had not been sent (the `gh` invite call needs the owner's login) and the bio was still a placeholder. I added `adamwstauffer` through the GitHub web UI; the assistant confirmed the pending invitation with `gh api` once I logged in as the owner.
- The assistant drafted one bio from `RESUME.md`. I rewrote it: I cut the narrative framing and the closing sentence about the portfolio, replaced the industry description with named sectors and product types, and shortened the credentials.
- The first `AGENTS.md` prescribed short declarative sentences. I pointed the assistant at my *Patterns* (2023) article to learn my actual voice; it rewrote the prose rules to call for declarative headings that state the finding, claims that carry their number and comparison, choices that carry their reason, calibrated hedging, a limitations section, and cutting rather than adding when editing my prose.
- `RESUME.md` now lists both GitHub accounts (`joshuaburkhart` and the `jgburk` portfolio) and both career documents carry the one-line AI disclosure the course asks for.
