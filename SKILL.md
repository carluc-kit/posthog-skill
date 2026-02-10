---
name: posthog
description: >-
  PostHog analytics via MCP - dashboards, insights, feature flags, experiments, surveys, and error tracking.
  Use when checking PrivaSpeech analytics, viewing dashboards, managing feature flags,
  or investigating error tracking data.
metadata: {"openclaw":{"emoji":"🦔","requires":{"bins":["mcporter"]}}}
---

# PostHog

Analytics, feature flags, experiments, and error tracking via PostHog MCP.

## Setup

PostHog is configured in `config/mcporter.json` with your API key.

## Usage

All commands use mcporter to call PostHog tools:

```bash
mcporter call posthog.<tool> [args]
```

## Quick Reference

### Dashboards

```bash
# List all dashboards
mcporter call posthog.dashboards-get-all

# Get specific dashboard
mcporter call posthog.dashboard-get dashboardId=123

# Create dashboard
mcporter call posthog.dashboard-create --args '{"data":{"name":"My Dashboard","description":"..."}}'

# Delete dashboard
mcporter call posthog.dashboard-delete dashboardId=123

# Add insight to dashboard
mcporter call posthog.add-insight-to-dashboard --args '{"data":{"insightId":"abc","dashboardId":123}}'
```

### Insights & Queries

```bash
# List all insights
mcporter call posthog.insights-get-all

# Get specific insight
mcporter call posthog.insight-get insightId=abc123

# Run a query (trends, funnels, HogQL)
mcporter call posthog.query-run --args '{"query":{...}}'

# Generate HogQL from natural language
mcporter call posthog.query-generate-hogql-from-question question="How many users signed up last week?"

# Create insight from query
mcporter call posthog.insight-create-from-query --args '{"data":{...}}'
```

### Feature Flags

```bash
# List all feature flags
mcporter call posthog.feature-flag-get-all

# Get flag definition
mcporter call posthog.feature-flag-get-definition flagKey=my-flag

# Create feature flag
mcporter call posthog.create-feature-flag name="My Flag" key="my-flag" description="..." filters='{}' active=true

# Update feature flag
mcporter call posthog.update-feature-flag flagKey=my-flag --args '{"data":{...}}'

# Delete feature flag
mcporter call posthog.delete-feature-flag flagKey=my-flag
```

### Experiments (A/B Tests)

```bash
# List experiments
mcporter call posthog.experiment-get-all

# Get experiment details
mcporter call posthog.experiment-get experimentId=123

# Get experiment results
mcporter call posthog.experiment-results-get experimentId=123 refresh=true

# Create experiment
mcporter call posthog.experiment-create name="My Experiment" feature_flag_key="exp-my-test"

# Update experiment
mcporter call posthog.experiment-update experimentId=123 --args '{"data":{...}}'
```

### Surveys

```bash
# List all surveys
mcporter call posthog.surveys-get-all

# Get survey
mcporter call posthog.survey-get surveyId=abc

# Create survey
mcporter call posthog.survey-create name="Feedback Survey" --args '{"questions":["How satisfied are you?"]}'

# Get survey stats
mcporter call posthog.survey-stats survey_id=abc

# Global survey stats
mcporter call posthog.surveys-global-stats
```

### Error Tracking

```bash
# List errors
mcporter call posthog.list-errors orderBy=occurrences

# Get error details
mcporter call posthog.error-details issueId=uuid-here
```

### Events & Properties

```bash
# List event definitions
mcporter call posthog.event-definitions-list

# List properties for an event
mcporter call posthog.properties-list type=event eventName=pageview

# List person properties
mcporter call posthog.properties-list type=person
```

### Logs

```bash
# Query logs
mcporter call posthog.logs-query dateFrom="2026-01-01T00:00:00Z" dateTo="2026-01-12T00:00:00Z"

# List log attributes
mcporter call posthog.logs-list-attributes

# Get attribute values
mcporter call posthog.logs-list-attribute-values key=service.name
```

### Organizations & Projects

```bash
# Get organizations
mcporter call posthog.organizations-get

# Get organization details
mcporter call posthog.organization-details-get

# Get projects
mcporter call posthog.projects-get

# Switch project
mcporter call posthog.switch-project projectId=123
```

### LLM Costs (if using PostHog for AI)

```bash
# Get LLM costs
mcporter call posthog.get-llm-total-costs-for-project projectId=123 days=7
```

### Documentation Search

```bash
# Search PostHog docs
mcporter call posthog.docs-search query="how to track events"
```

## Available Tools (47)

| Category | Tools |
|----------|-------|
| Dashboards | `dashboards-get-all`, `dashboard-get`, `dashboard-create`, `dashboard-update`, `dashboard-delete`, `dashboard-reorder-tiles`, `add-insight-to-dashboard` |
| Insights | `insights-get-all`, `insight-get`, `insight-create-from-query`, `insight-update`, `insight-delete`, `insight-query` |
| Queries | `query-run`, `query-generate-hogql-from-question` |
| Feature Flags | `feature-flag-get-all`, `feature-flag-get-definition`, `create-feature-flag`, `update-feature-flag`, `delete-feature-flag` |
| Experiments | `experiment-get-all`, `experiment-get`, `experiment-create`, `experiment-update`, `experiment-delete`, `experiment-results-get` |
| Surveys | `surveys-get-all`, `survey-get`, `survey-create`, `survey-update`, `survey-delete`, `survey-stats`, `surveys-global-stats` |
| Errors | `list-errors`, `error-details` |
| Events | `event-definitions-list`, `properties-list` |
| Logs | `logs-query`, `logs-list-attributes`, `logs-list-attribute-values` |
| Org/Project | `organizations-get`, `organization-details-get`, `projects-get`, `switch-organization`, `switch-project` |
| Other | `docs-search`, `get-llm-total-costs-for-project` |

## Tips

- Use `--output json` for machine-readable output
- Use `--args '{...}'` for complex JSON parameters
- First run `event-definitions-list` to discover available events before creating queries
- Use `docs-search` for PostHog-specific questions
