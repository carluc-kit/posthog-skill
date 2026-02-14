# 🦔 PostHog Skill for OpenClaw

An [OpenClaw](https://github.com/openclaw/openclaw) skill that gives your AI agent full access to [PostHog](https://posthog.com) analytics — dashboards, insights, feature flags, experiments, surveys, error tracking, and more.

## Prerequisites

- [OpenClaw](https://github.com/openclaw/openclaw) installed and running
- [mcporter](https://github.com/anthropics/mcporter) CLI installed
- A PostHog account with an API key

## Installation

```bash
# Install the skill
openclaw skill add carluc-kit/posthog-skill
```

## Configuration

Add your PostHog MCP server to `config/mcporter.json`:

```json
{
  "mcpServers": {
    "posthog": {
      "command": "npx",
      "args": ["-y", "@nicholasoxford/posthog-mcp"],
      "env": {
        "POSTHOG_API_KEY": "phx_your_api_key_here",
        "POSTHOG_PROJECT_ID": "your_project_id"
      }
    }
  }
}
```

You can find your API key in PostHog under **Project Settings → Personal API Keys**.

## What Can It Do?

| Feature | Examples |
|---------|---------|
| **Dashboards** | List, create, update, delete dashboards; add insights to them |
| **Insights** | Query trends, funnels, retention; create saved insights |
| **Feature Flags** | Create, toggle, update flags and rollout conditions |
| **Experiments** | Set up A/B tests, check results, manage variants |
| **Surveys** | Create in-app surveys, view responses and stats |
| **Error Tracking** | List errors by frequency, get stack traces and details |
| **HogQL** | Run raw queries or generate them from natural language |
| **Logs** | Query and filter application logs |
| **LLM Costs** | Track AI/LLM spending per project |

## Usage Examples

Once installed, just ask your agent naturally:

- *"How many signups did we get this week?"*
- *"Show me the top errors by occurrence"*
- *"Create a feature flag called dark-mode for 10% rollout"*
- *"What's our conversion funnel look like?"*
- *"Set up an A/B test for the new pricing page"*

The agent uses `mcporter` under the hood to call PostHog's MCP tools. See [SKILL.md](SKILL.md) for the full command reference.

## 47 Available Tools

Covers the full PostHog API surface: dashboards, insights, queries, feature flags, experiments, surveys, error tracking, events, properties, logs, organizations, projects, docs search, and LLM cost tracking.

## License

MIT
