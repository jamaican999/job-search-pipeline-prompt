# Job Search Pipeline Prompt

An operating prompt that turns an AI coding assistant (Claude Code, or any agent that can read and write files) into a careful job-application assistant. For each job posting, it verifies the posting on the employer's own site, researches the company, scores your fit, writes a tailored résumé and cover letter as editable Word files, and hands everything back to you to review and submit yourself.

The full prompt is [`job-search-pipeline-prompt.md`](job-search-pipeline-prompt.md).

## Quick start
1. Create an empty folder for your job search.
2. Save `job-search-pipeline-prompt.md` at its root as your assistant's instructions file (`CLAUDE.md` for Claude Code, `AGENTS.md` for many other agents).
3. Fill in the Candidate Profile (§3): location rules, pay target, tracks, display preferences, and the standing lines you want in every cover letter.
4. Start a session and say "set up the pipeline." The assistant walks you through building a master résumé, base résumés, and a voice guide.
5. Paste a job posting or link. You get a résumé, a cover letter, and a fitness report.

## Principles
- **Truth is fixed.** Every claim comes from your master résumé. Gaps are named, never papered over.
- **You decide.** The assistant drafts and recommends; you approve, edit, and submit.
- **Ask first.** By default the assistant asks before every action, and some actions (submitting applications, sending messages, deleting files) are never allowed.

## What you get per job
- A tailored **résumé** and **cover letter** (.docx), built from your own facts and written in your voice.
- A **fitness report**: a full hiring-readiness evaluation of the final résumé against the posting, with interview questions, objection handling, a LinkedIn message, and a follow-up email.
- In batch mode, one folder per job and a summary table sorted by overall score.

## Scoring
Each job gets three independent scores and one overall score. Keeping them separate shows tradeoffs at a glance, such as a strong fit with a bad commute.

| Score | Question it answers | How it works |
|---|---|---|
| **Fit** (0–100) | Can I win this job? | A seven-lens hiring readiness evaluation (ATS, recruiter, hiring manager, HR, candidate, team, trajectory) with fixed weights: must-have coverage 30%, functional depth 30%, role and seniority 20%, achievement quality 20%. Threshold 75. |
| **Practicality** (0–100) | Do I want it on these terms? | Commute 40%, pay 35%, level 25%. Remote scores 100 on commute; hybrid and on-site roles use real driving miles from home × office days, with extra weight on long drives. Pay compares the posted midpoint with your target range. Level compares the role with your last level. |
| **Language penalty** (0 to −10) | What does the posting's wording signal? | Points for warning signs (scope far beyond the level or pay, overwork culture phrases, stale or evergreen postings, title and body mismatches, two roles blended into one, requirement stacking, friction between teams, sibling postings), offset by credit for candor (explicit success measures, honest constraints). Every signal must quote its evidence. |
| **Overall** | Where should I spend my time first? | round(√(fit × practicality)) − penalty. The geometric mean rewards jobs that are good on both fit and terms; a strong score on one can't hide a weak score on the other. |

Batch summaries list every subscore (overall, fit, practicality, commute, pay, level, penalty) and sort by overall, high to low. Folder names carry fit and practicality, for example `Acme - Sales Operations Manager - 82-75`.

## Batch mode
Send a list of postings (company links or LinkedIn links). The assistant builds every package without stopping, verifies each posting on the employer's own careers system, skips job-board-only listings (a common scam pattern), and records any roadblock in the summary instead of pausing.

## Attribution
The hiring readiness evaluation inside the prompt (Appendix A) is the "Hiring Readiness Report" prompt by Chander Shankar, Luminary AI, https://www.luminaryai.com.au/hiring-readiness, published under the terms "Free to use. Change it, share it." It is reproduced unchanged; the pipeline's adaptations are described in the prompt.
