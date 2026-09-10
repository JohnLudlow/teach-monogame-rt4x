# Agent Configuration Overrides

```yaml
jl_quiz:
  quiz_mode: in_chat
  plan_destination: github_issue
  file_storage_location: docs/plans/

jl_recon:
  decision_gates:
    destination_confirmation: false
    inciting_issue_confirmation: false
    research_afk: false
  uncertainty_tracking:
    pattern: "## Not Yet Specified (Fog of War)"

jl_issue_management:
  plan_destination: github_issue
  file_storage_location: docs/plans/
  decision_gates:
    destination_confirmation: false
    research_afk: false
```

## What Agents MUST NOT do

- Commit or push changes without explicit user permission
- Create or complete pull requests (PRs) without explicit user permission
