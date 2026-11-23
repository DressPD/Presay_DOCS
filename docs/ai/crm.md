# Salesforce and HubSpot

Presay's MCP server is at:

```
https://mcp.presay.hyver.app/mcp
```

This page shows where a CRM asks for an MCP server and what to enter. For assistants such as Claude, ChatGPT, Cursor or VS Code, use [Connect an Assistant (MCP)](/ai/mcp.md) instead.

> **Status: not yet tested end to end.** The CRM steps below come from Salesforce's and HubSpot's own published documentation. We have not yet completed a connection from either product. The points where Presay may not fit are marked **Check**. Menu names change between releases, so trust what your org shows over this page.

## What Presay offers a CRM

| | |
| --- | --- |
| **Transport** | Streamable HTTP |
| **Sign-in** | OAuth 2.1 with PKCE (S256). Each person signs in with their own Presay email and password and approves access |
| **Scopes** | `presay:read` (see studies, reports, audiences), `presay:write` (run studies, change things) |
| **Client registration** | Dynamic Client Registration (`POST /oauth/register`) or a client ID metadata document (the `client_id` is an HTTPS URL). **Public clients only: there is no client secret** |
| **Discovery** | `https://mcp.presay.hyver.app/.well-known/oauth-authorization-server` |
| **Allowance** | Studies started from a CRM use that person's own weekly and daily [allowance](/account/limits.md) |

Each person who uses Presay from a CRM needs their own [Presay account](/getting-started/account.md).

## OAuth or API key?

**OAuth.** Presay has no API key or personal access token, on purpose: every connection is a person signing in and approving access, which you can revoke under **Settings, AI agents**. A CRM must therefore support OAuth to connect.

What each CRM documents (checked November 2026):

| | OAuth | API key or bearer token |
| --- | --- | --- |
| **Salesforce** | Yes. External MCP servers use OAuth 2.0 (or no authentication). Salesforce describes both a per-user flow and a client-credentials service account. One third-party write-up says only client credentials work, so check what your org offers. | Not documented for external MCP servers |
| **HubSpot** | Yes, and only OAuth 2.1 with PKCE for a custom MCP server component | Not documented. The only token-in-URL case is a fixed connector (Zapier), not a custom server |

Presay supports the authorization-code flow with PKCE, which is what both CRMs' per-user paths use. It does **not** support client credentials, so a Salesforce service-account setup will not work.

## Salesforce (Agentforce)

Salesforce can register an external MCP server and expose its tools as actions for an Agentforce agent. Salesforce documents two Setup paths, depending on release. Use the one your org shows.

Sources: Salesforce Help, [Register a Third-Party MCP Server in Agentforce Registry](https://help.salesforce.com/s/articleView?language=en_US&id=ai.agent_mcp_connect_register.htm&type=5) and [Register External MCP Servers in API Catalog](https://help.salesforce.com/s/articleView?language=en_US&id=platform.api_catalog_manage_manual_external_mcp_servers.htm&type=5).

### 1. Register the server

You need a Salesforce admin with access to Setup and an Agentforce-enabled org.

**Path A: Agentforce Registry.** In **Setup**, search for **Agentforce Registry** and add an MCP server.

**Path B: API Catalog.** In **Setup**, search for **API Catalog**, open **MCP Servers**, select the **External Servers** tab, choose **Add MCP Server**, then **Register External MCP Server**.

Enter:

| Field | Value for Presay |
| --- | --- |
| Name | `Presay` |
| Description | Simulated audience research: run studies and read reports |
| Server URL | `https://mcp.presay.hyver.app/mcp` |
| Identity provider URL | `https://mcp.presay.hyver.app` |
| Scopes (optional) | `presay:read presay:write`, or `presay:read` for read-only |
| Client ID, client secret | See the check below |

Salesforce then validates the server with a ping and creates a **named credential**, an **external credential** and a **permission set**.

> **Check: client ID and secret.** Salesforce asks for both. Presay registers public clients that use PKCE and have no secret, and it does not issue a pre-registered client ID with a secret. Whether Salesforce accepts a connection without a secret, or can register itself through Dynamic Client Registration, is not confirmed. If the form requires a secret, it will not connect today.

### 2. Choose per-user sign-in

Add a principal with the **per-user** identity type. Each Salesforce user then goes through Presay's sign-in once, and Salesforce keeps a separate token for each. That keeps the study allowance per person, and every person needs a Presay account.

A shared service account (client credentials) is **not** available: Presay only supports the authorization-code flow with a signed-in person.

### 3. Give people access

In **Setup**, **Permission Sets**, open the permission set Salesforce created and assign it to the users, and to the agent's user, who will use Presay. Under **External Credential Principal Access**, make sure it is enabled. By default the permission set is assigned only to the person who created the connection.

### 4. Add the tools to an agent

1. Open **Agentforce Builder** and open the agent.
2. Pick a topic, then **This Topic's Actions**.
3. Choose **New**, then **Add from Asset Library**, and select the Presay tools.

Start with the read tools (`list_audiences`, `get_study`, `get_report`, `get_usage`). Add `create_study` and the others once the read path works. See the [tool list](/ai/mcp.md#what-the-assistant-can-do).

### 5. Test

In the agent, ask: "List my Presay audiences". Salesforce asks you to sign in to Presay the first time. Then try "Run a study of this headline on US adults, 20 respondents".

## HubSpot

**HubSpot does not currently let a customer paste an MCP server URL.** The Agent Builder connector list is fixed (for example Notion, Atlassian, Gong, Zapier), and none of the pages we read describes a "custom server" option for customers.

The only documented route is for a developer to package a server as an **MCP server component** inside a HubSpot app (**beta**, private or marketplace distribution). Customers then install the app and the server shows up under **Add tool** in Agent Builder.

Sources: HubSpot, [Connect apps to HubSpot's AI agents](https://knowledge.hubspot.com/integrations/customize-breeze-agents-with-hubspot-mcp-client) and [Connect external MCP servers to HubSpot agents (BETA)](https://developers.hubspot.com/docs/apps/developer-platform/add-features/mcp-server).

### What HubSpot requires from the server

| HubSpot requirement | Presay |
| --- | --- |
| Public HTTPS URL | Yes |
| OAuth 2.1 authorization code with PKCE (S256) | Yes |
| Discovery at `/.well-known/oauth-authorization-server` on the server's domain | Yes |
| Access token **and refresh token**, with the `refresh_token` grant | Yes (refresh tokens last 30 days and rotate) |
| Dynamic Client Registration | HubSpot does **not** support it. You must supply a fixed client ID |
| Fixed redirect URI `https://oauth-redirect.hubspot.com/callback/mcp_server` | **Check:** it must be accepted for the client ID you supply |

> **Check: the client ID.** HubSpot sends the `mcpClientId` you configure as `client_id`. Presay can take an HTTPS **client ID metadata document** URL as a client ID, if that document lists HubSpot's redirect URI. That is the most likely fit, but we have not tried it, and HubSpot may not accept a URL as a client ID.

### If you want to try it

You need a HubSpot developer account with access to the **MCP server public beta**, and the HubSpot CLI.

1. Create a project and an app set to **private** distribution. The app needs the `oauth` scope at least. The platform version in `hsproject.json` must be the beta one HubSpot names on its page.
2. Add `app/mcp-server/presay-hsmeta.json`:

```json
{
  "uid": "presay_mcp",
  "type": "mcp-server",
  "config": {
    "name": "Presay",
    "description": "Run simulated audience studies and read reports",
    "mcpUrl": "https://mcp.presay.hyver.app/mcp",
    "mcpClientId": "<client ID, see the check above>",
    "requiredScopes": ["presay:read", "presay:write"],
    "enabled": true
  }
}
```

3. Deploy the project, copy the install link from the app's **Distribution** tab and install it in a HubSpot account.
4. In the account, open the project's MCP server component and choose **Test connection**, then **Connect**. Presay's sign-in page opens.
5. In **Agent Hub**, **Agent Builder**, choose **Configure**, **Add tool**, then the **MCP Servers** category, and **Connect and add** for Presay.

Field names are copied from HubSpot's beta page and may change. Check that page before you start.

## Until it works natively

If your CRM can't connect yet, the study loop still fits a CRM workflow:

- Run the study in the [web app](/getting-started/first-study.md) or through an [assistant](/ai/mcp.md), then paste the [shared report link](/reports/share-export.md) into the Salesforce record or HubSpot note.
- Export the report as PDF, Word or JSON and attach it. See [Share & Export](/reports/share-export.md).

## Disconnect

Remove the connection in the CRM, and under **Settings, AI agents** in the Presay web app. Access ends at the next call.

> The respondents are simulated. Whatever a CRM agent reports back is a directional signal, not measured demand. See [Limits of Synthetic Research](/limits.md).
