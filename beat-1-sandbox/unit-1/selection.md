# Issue selection write-up

## Chosen issue

- Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/64
- Verdict from the skill: accept
- Why it fits: this is a focused test-fixture correction with an exact failing test command and a clear expected result. It matches my interest in Python, reading tests, and making small, verifiable changes. The live run also accepted issue #62, but ranked #64 higher for my fit profile. It rejected #61 because an open PR already addresses it.

## Run history

1. **October 1 — initial full run.** I ran the full 20-issue harness with the original rubric and saved its transcript. It agreed on 18/20, met the category floor, and passed the bar. It rejected issue-19 (gold: accept) on newcomer-sized scope and accepted issue-20 (gold: reject). This showed that my scope language was too strict about a bug report listing possible causes, and not explicit enough about an unresolved product-defining requirement.
2. **October 3 — targeted re-check.** I clarified that the scope check should judge the shared outcome rather than optional implementation suggestions, and that a feature request fails when a product-defining input is explicitly TBD. I ran `--only issue-19,issue-20`; both then matched their gold labels.
3. **October 3 — revised full run.** The full run agreed on 19/20. It now matched issue-19 and issue-20, but accepted issue-15 (gold: reject). The issue had been open for years and had two closed, unmerged linked PR attempts; I had not made that evidence a clear pass/fail rule.
4. **October 3 — targeted re-check and final full run.** I added a specific scope threshold for issues open at least two years with at least two closed, unmerged linked PR attempts, unless a maintainer later confirms the scope is settled and invites a fresh attempt. `--only issue-15` matched gold. I then ran the complete harness again with `--save-run` to create the submitted `eval-run.txt`. The final result was **20/20**, with a match in every category. No partial run was used as the submitted transcript.

5. **October 9 — independent final verification.** I ran the full 20-issue Sonnet harness against `tools/issue-select/rubric.md` and `tools/issue-select/SKILL.md`. It again agreed on **20/20** and met every category floor. The harness-generated transcript is the current `eval-run.txt`; its fingerprints match the submitted files.

## Issue analysis

I am analyzing **issue-15** (`zulip/zulip#19589`), a scored issue from the final run.

- **My rubric's verdict:** reject
- **Gold verdict:** reject
- **Why:** the requested change is described as separating the command and message fields in an outgoing webhook, but the snapshot also shows the issue had been open since 2021 and had two closed, unmerged linked PRs. The earlier rubric did not clearly treat repeated failed attempts as a scope warning, so the first revised full run accepted it based on the issue's concise description. I added an explicit threshold for long-open issues with repeated closed, unmerged attempts; the final rubric then rejected it for newcomer-sized scope. This is evidence about the history of the task, not simply its “good first issue” label.

## Check rationale

The current “Newcomer-sized scope” check in the uploaded rubric says:

> Pass if the primary requested outcome is one bounded change with an identifiable result. Judge the shared problem being fixed, not the number of possible causes or optional implementation suggestions; a single concrete bug can pass even when the issue lists alternative causes or approaches. Fail for a tracking/umbrella issue, a pure usage question, work whose design is still actively unsettled, an issue that makes a maintainer-confirmed broad/core-internals change the task, or a product decision with no stated requirements. A feature request also fails when a product-defining input needed to implement it (such as the asset or identity to add) is explicitly TBD. Also fail if an issue has been open for at least 2 years and has at least 2 closed, unmerged linked PR attempts, unless a maintainer later confirms the scope is settled and invites a fresh attempt. Do not fail only because a report is brief, lacks reproduction steps, or lacks a detailed checklist.

This check addresses the three scope disagreements I saw: issue-19's possible causes do not change its single reported freeze, issue-20's logo asset is explicitly TBD, and issue-15's repeated closed attempts indicate that its short issue description understates the difficulty.

## Trade-offs

The scope check deliberately balances clear outcomes against evidence of hidden difficulty. The two-year/two-PR threshold is concrete and caught issue-15, but it could reject an issue whose old attempts were unrelated or whose scope was later clarified; the maintainer-confirmation exception helps avoid that. The rubric also remains conservative about an explicitly unresolved product choice such as issue-20's unspecified logo asset. The final 20/20 is a strong result on these snapshots, not a guarantee that every live issue is equally straightforward.

## Verdict output


Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/64

Live-mode run of `issue-select` (2026-10-08, evidence from the GitHub API). Scope: repo is `codepath/pathreview-ai301-fa26-howard`, so it is in scope. House rule applied: classmates' claim comments are ignored.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/64",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass", "evidence": "Opener Aburke225 is author_association COLLABORATOR; last default-branch commit 2026-09-16 by Andrew Burke (22 days before 2026-10-08)"},
    {"name": "Project is in use", "grade": "pass", "evidence": "archived=false; last push 2026-09-16, within 180 days (no releases, so the push date decides)"},
    {"name": "Newcomer-sized scope", "grade": "pass", "evidence": "One bounded change: fix the test_query_with_partial_overlap fixture so overlap is partial, and remove the strict xfail marker; reproduction is a single pytest command"},
    {"name": "No active claimant", "grade": "pass", "evidence": "No assignee, no linked or open PR mentioning #64 (open PRs 73-79 target other issues); 2026-10-06 claim comments are classmates', ignored per the Path Review house rule"},
    {"name": "Contribution policy allows this workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branch names, Conventional Commits and the PR process; it has no ban on AI-assisted contributions"}
  ],
  "verdict": "accept"
}
```

