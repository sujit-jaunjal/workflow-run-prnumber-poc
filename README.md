# workflow_run PR_NUMBER reproduction

Minimal reproduction of a GitHub Actions pattern for an authorized bug-bounty report.

A `workflow_run` workflow derives a PR number from
`github.event.workflow_run.pull_requests[0].number`. That array is empty for pull requests from
forks, so the expression renders as an empty string and a `[[ -z "$PR_NUMBER" ]]` test selects the
"not a pull request" branch — publishing fork-controlled build output to the deploy ROOT instead of
an isolated per-PR path.

The deploy step here is a **stub**: it logs the command that the real workflow would run and
executes nothing against any cloud provider. No credentials are configured.
