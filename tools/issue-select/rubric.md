# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Repo-facts block: dates and authors of the last 5 default-branch commits and the maintainer first-response sample. Also inspect the issue opener and comments for `author_association` values `OWNER`, `MEMBER`, or `COLLABORATOR`. | Pass if at least one of these is true: a non-bot commit on the default branch is dated within the last 365 days; a sampled maintainer first response took 90 days or less; or a maintainer filed or commented on this issue. Otherwise fail. Measure dates from the bundle capture date in eval mode and from today in live mode. | required |
| Project is in use | Repo-facts block: archived status, latest release date, and last push to any branch. | Pass only if the repo is not archived and either its latest release is within the last 18 months or its last push to any branch is within the last 180 days. Measure dates from the bundle capture date in eval mode and from today in live mode. | required |
| Newcomer-sized scope | Issue body and comment thread; inspect linked-PR history when it indicates repeated attempts. | Pass if the primary requested outcome is one bounded change with an identifiable result. Judge the shared problem being fixed, not the number of possible causes or optional implementation suggestions; a single concrete bug can pass even when the issue lists alternative causes or approaches. Fail for a tracking/umbrella issue, a pure usage question, work whose design is still actively unsettled, an issue that makes a maintainer-confirmed broad/core-internals change the task, or a product decision with no stated requirements. A feature request also fails when a product-defining input needed to implement it (such as the asset or identity to add) is explicitly TBD. Also fail if an issue has been open for at least 2 years and has at least 2 closed, unmerged linked PR attempts, unless a maintainer later confirms the scope is settled and invites a fresh attempt. Do not fail only because a report is brief, lacks reproduction steps, or lacks a detailed checklist. | required |
| No active claimant | Repo-facts block for assignees and linked PRs; issue comments for claim statements and PRs mentioned in the thread. | Pass only if there is no assignee, no open linked or mentioned PR, and no claim comment (for example, "I'll take this" or "I'm working on it") posted within the last 90 days. A claim older than 90 days is stale unless a later comment confirms work is ongoing. Closed or merged PRs alone are not active claims. Measure comment dates from the bundle capture date in eval mode and from today in live mode. | required |
| Contribution policy allows this workflow | Repo-facts contribution-policy line; in live mode, read `CONTRIBUTING.md` and any linked contributor or AI-policy documents. | Pass if the policy is silent or permits AI-assisted contributions, including conditions such as disclosure, testing, or human review that the student can follow. Fail only for an explicit ban on AI-generated code or documentation. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if every required check passes. Reject if any required check
fails or is unclear. There are no preferred checks; all five checks can
affect the verdict.
