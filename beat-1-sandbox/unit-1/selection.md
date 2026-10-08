# Issue selection write-up

## Chosen issue

- Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/64
- Title: Relevance scorer "partial overlap" test fixture actually has full query overlap
- Verdict from the skill: accept
- Why it fits: one bounded change (correct the fixture in `test_query_with_partial_overlap`, and drop the strict `xfail` marker with it), a two-line reproduction (`pytest tests/unit/test_relevance_scorer.py -q`), no product ambiguity, and a collaborator-filed issue in an active repo. That matches my fit profile: trace a failing test to a small, testable fix.

## Selection rationale

- **How hard will claiming be?** Hard to get exclusive ownership, and that is expected. Two classmates (djenkins05, Pamzlerinz) already commented on 2026-10-06 and both posted reproductions. Path Review's house rule says shared claims do not block an issue and credit attaches to the PR, so I will claim anyway. I will comment first with my plan, then open a small PR quickly, because the PR is what counts.
- **What did I weigh beyond the verdict?** The skill's accept only says the issue passes the five required checks. I also weighed my fit profile: a narrow code path, concise reproduction steps and little ambiguity. I also checked the one catch the reproductions turned up: the test is now `xfail(strict=True)`, so fixing only the fixture would turn into an unexpected-pass failure unless the marker comes off too. That is still one small change.
- **What could go wrong?** Competing PRs on the same one-line fix. Open PRs 73-79 are all other issues, so none is on #64 yet.

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

## Run history

My rubric was first evaluated with the full harness command:

```bash
python3 /Users/stephen/ai301-unit1-starter/eval/run_eval.py --rubric /Users/stephen/.claude/skills/issue-select/rubric.md --save-run eval-run.txt
```

That full run produced the transcript saved in `eval-run.txt`. The result was 18/20 scored items in agreement, which is exactly at the course bar, with the main disagreements coming from issue-19 and issue-20. I used that output to check which checks were too strict or too permissive, then kept the rubric focused on the four core families the course emphasizes: maintainer health, repo liveness, newcomer-sized scope, and no active claimant, while also keeping the policy check explicit.

## Issue analysis

I used issue-15 (source: zulip/zulip#19589) as the scored item to walk through, because it is the one that drove the rubric's long-open/closed-PR clause. Gold label: reject. My rubric: reject — agreement, but only after the clause was added.

- Gold verdict: reject
- Rubric verdict: reject
- Reasoning: the issue was opened 2021-08-18 and was still open as of the 2026-08-05 capture date, almost five years later. It has two linked PRs, zulip/zulip#20840 and zulip/zulip#23123, both closed without merging. The comment thread shows a long string of contributors claiming the issue via `@zulipbot claim` and then getting auto-unassigned after 14 days of inactivity, going back to 2021. That history is what the "open ≥2 years and ≥2 closed, unmerged linked PRs" clause in the Newcomer-sized scope check is built to catch: a task that reads as a bounded bug but has quietly defeated several attempts already, which makes it a bad bet for a first contribution even though nothing in the issue text itself looks broad.

## Check rationale

The rubric wording that mattered most was the "Newcomer-sized scope" check, quoted verbatim from `skill/rubric.md`:

> "Pass if the primary requested outcome is one bounded change with an identifiable result. Judge the shared problem being fixed, not the number of possible causes or optional implementation suggestions; a single concrete bug can pass even when the issue lists alternative causes or approaches. Fail for a tracking/umbrella issue, a pure usage question, work whose design is still actively unsettled, an issue that makes a maintainer-confirmed broad/core-internals change the task, or a product decision with no stated requirements. A feature request also fails when a product-defining input needed to implement it (such as the asset or identity to add) is explicitly TBD. Also fail if an issue has been open for at least 2 years and has at least 2 closed, unmerged linked PR attempts, unless a maintainer later confirms the scope is settled and invites a fresh attempt. Do not fail only because a report is brief, lacks reproduction steps, or lacks a detailed checklist."

The last added clause (the 2-year/2-closed-PR fail condition) is what turned issue-15 into a correct reject: without it, the check only looks at the issue text, which describes one bounded formatting change and would otherwise pass. Adding the history check let the rubric reject issues that look small on paper but have already consumed multiple contributors' attempts.

## Trade-offs

The 2-year/2-closed-PR clause can misfire on an issue whose old PRs failed for reasons that have nothing to do with the current scope — for example, a PR that was closed because it targeted an abandoned branch, or because the maintainer's requirements changed after the PR was filed, not because the work itself was too hard or ill-defined. In that case the rubric would reject a task that is still genuinely newcomer-sized, purely because of unrelated history.

The accepted miss case is exactly that kind of issue: the rubric trades a few good bounded issues with messy, unrelated PR history for consistently avoiding issues like #19589, where repeat failed attempts are a real signal that something about the task is harder than it looks. The chosen issue, #64, has no PR history at all (no linked PRs, no stale attempts), so the clause does not touch it, and it fits the rubric's other four checks cleanly.
