# Salesforce

**Presay cannot be connected to Salesforce (Agentforce) yet.** We have not been able to confirm that it works with Salesforce, so we do not publish setup steps that might fail.

## Why

- Salesforce has each customer's admin register an MCP server by hand, with credentials they enter themselves. There is no install link like [HubSpot's](/ai/hubspot.md).
- Salesforce limits what an MCP server may expose, for example the characters allowed in tool names and the length of descriptions. Presay's tools need changes to fit, and we will not ship those until we can test them in a real Salesforce org.

## What you can do now

- **Run studies from anywhere else and bring the result into Salesforce.** Run a study in the [web app](/getting-started/first-study.md) or through an [assistant](/ai/mcp.md), then paste the [shared report link](/reports/share-export.md) into the Salesforce record.
- **Attach the report.** Export it as PDF, Word or JSON. See [Share & Export](/reports/share-export.md).

## Tell us you need it

If your team uses Salesforce and wants Presay in Agentforce, email [support@hyver.app](mailto:support@hyver.app) with your Salesforce edition and whether you use Agentforce Service or Agentforce Employee agents. It tells us how much to prioritise it.

> Studies use simulated respondents. Treat results as a directional signal, not measured demand. See [Limits of Synthetic Research](/limits.md).
