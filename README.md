# Candidate Signal Score

A BrightHire-powered interview-evidence, feedback and fairness layer for a
Greenhouse-based hiring stack. Prepared by Patrick Diamitani for the Gong
Talent Engineer conversation (October 2026). Independent prototype, not a
Gong or vendor product.

**Read the 2-page brief:** [candidate-signal-score.pdf](candidate-signal-score.pdf)

**Full overview site (with the companion Talent Engineer skill):**
https://diamitani.github.io/gong-talent-overview/

## The idea in one line

Apply lead-scoring rigor to interview evidence: a transparent score of how
well-evidenced each candidate's interview loop is, so weak processes get fixed
before they become unfair rejections.

## How it works

1. **Capture.** BrightHire interview events (completed interview, submitted
   scorecard) and Greenhouse stage changes flow into an automation layer
   (n8n) via webhooks and the Greenhouse Harvest API. BrightHire already
   writes scorecards, AI notes and highlight links onto the candidate record,
   so interviewers do zero new data entry.
2. **Store.** Every event lands in a governed store (candidates, stages,
   interviews, scorecards) with role-based access from day one.
3. **Score.** A transparent scoring function computes each candidate's Signal
   Score from four auditable inputs: rubric coverage, evidence depth,
   consistency across candidates for the same role, and scorecard timeliness.
4. **Act.** Three outputs: a debrief packet per candidate, a thin-signal flag
   that pauses a rejection under 60% rubric coverage for re-review, and an
   AI-drafted, human-approved feedback message to every candidate within 48
   hours.

## Guardrails

The score never auto-dispositions anyone. It ranks evidence quality and
prioritizes human attention; humans make every decision. No demographic or
proxy features, ever. Every score shows its inputs.

## Status

This is a workflow design plus a buildable prototype path (Greenhouse webhook
to n8n to Supabase to Slack/email, with recorded-interview transcripts
standing in for BrightHire signals in a sandbox). It has not been run against
any live Greenhouse or BrightHire tenant.
