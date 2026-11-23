# Integrations: Salesforce, HubSpot and other apps

Presay's MCP server is at:

```
https://mcp.presay.hyver.app/mcp
```

This page shows how to connect Presay to an app that asks for a client ID and secret, such as Salesforce or HubSpot. For assistants such as Claude, ChatGPT, Cursor or VS Code, which register themselves, use [Connect an Assistant (MCP)](/ai/mcp.md) instead.

> **Status.** Presay's side is live and was checked end to end on production: creating integrations, sign-in with and without PKCE, secrets, refresh, a service account, and revoking. We have **not** yet completed a connection from a real Salesforce org or HubSpot account. The points where those products may differ are marked **Check**. Menu names change between releases, so trust what your org shows over this page.

## 1. Create the integration in Presay

An integration is the client ID (and, for most apps, secret) that the other app uses to sign people in to Presay. You create it yourself, in the web app.

1. Open **Settings, AI agents** and scroll to **Integrations**.
2. Choose the app: **Salesforce**, **HubSpot** or **Other app**. The panel shows the connection steps for that app.
3. Enter a name. Enter the **callback URL** if you have it. You can leave it empty and add it later with **Callback URLs**, because Salesforce shows its callback only after you save the credential there.
4. Choose **Create integration**. Presay shows the **client ID**, the **client secret** (once), and the **server URL**, **identity provider URL** and **scopes** to paste into the other app.

**Copy the secret straight away.** It is shown only once and cannot be recovered. If you lose it, delete the integration and create a new one. Each person can have up to five integrations.

### Three kinds of integration

| Kind | Secret | Who signs in | Use it for |
| --- | --- | --- | --- |
| **Per person** (default) | Yes | Every person, with their own Presay account | Salesforce, and other apps that send people to a sign-in page |
| **No secret** (HubSpot preset, or untick "This app can keep a secret") | No, PKCE only | Every person | Apps that cannot keep a secret, such as HubSpot's MCP component |
| **Service account** | Yes | Nobody: the app acts as **you** | Apps that cannot send people to a sign-in page |

## Many people in one organisation

One integration is enough for a whole organisation. Each person signs in **once**, with their **own** Presay account, when the app first asks. Studies they start use **their** weekly and daily [allowance](/account/limits.md), and each person needs their own [Presay account](/getting-started/account.md). They can remove their connection any time under **Settings, AI agents, Connected assistants**.

A **service account** works differently, on purpose. Everyone using it acts as the person who created it and spends that person's allowance. Use it only when the app offers nothing else. Presay limits it to **read only** unless you choose read and write, issues short-lived tokens (one hour, no refresh token), and lists it under **Connected assistants** as "(service account)", where **Disconnect** ends it at once. Deleting the integration ends it too.

## Salesforce (Agentforce)

Salesforce can register an external MCP server and expose its tools as actions for an Agentforce agent. Sources: Salesforce Help, [Register a Third-Party MCP Server in Agentforce Registry](https://help.salesforce.com/s/articleView?language=en_US&id=ai.agent_mcp_connect_register.htm&type=5) and [Register External MCP Servers in API Catalog](https://help.salesforce.com/s/articleView?language=en_US&id=platform.api_catalog_manage_manual_external_mcp_servers.htm&type=5).

> **Which sign-in does Salesforce offer?** Public sources disagree. A September 2026 write-up says Agentforce supports only **no authentication or OAuth 2.0 client credentials**. Salesforce's own blog describes a **per-user** option. The form asks only for an identity provider URL, client ID, client secret and scopes, which fits client credentials. Presay supports both, so create the kind that matches what your org shows (below).

1. **Create the integration** as above, choosing **Salesforce**.
   - If your org offers a **per-user (authorization code) sign-in**, create it as usual. If it only offers **client credentials**, tick **Service account** and choose the access level.
2. In **Setup**, search for **Agentforce Registry** and add an MCP server. Or open **API Catalog**, **MCP Servers**, **External Servers**, **Add MCP Server**, **Register External MCP Server**. Use the path your org shows.
3. Enter:

   | Field | Value |
   | --- | --- |
   | Name | `Presay` |
   | Server URL | `https://mcp.presay.hyver.app/mcp` |
   | Identity provider URL | `https://mcp.presay.hyver.app` |
   | Scopes (optional) | `presay:read presay:write`, or `presay:read` for read-only |
   | Client ID, client secret | From the integration you created |

4. **Per-user sign-in only:** Salesforce shows a **callback URL** after you save. Copy it and add it in Presay under **Callback URLs**. Presay accepts any plain `https` address. The `.../services/authcallback/...` form is what Salesforce uses for authentication providers, so paste exactly what your org shows.
5. Assign the **permission set** Salesforce created to the people, and to the agent's user, who will use Presay. By default only the person who created the connection has it.
6. In **Agentforce Builder**, open the agent, pick a topic, choose **This Topic's Actions**, **New**, **Add from Asset Library**, and select the Presay tools. Start with the read tools (`list_audiences`, `get_study`, `get_report`, `get_usage`), then add `create_study` and the others. See the [tool list](/ai/mcp.md#what-the-assistant-can-do).
7. Test by asking the agent: "List my Presay audiences". With a per-user sign-in, Salesforce asks each person to sign in to Presay the first time.

**Check.** Salesforce may not send PKCE. Presay allows that for integrations that have a secret, because the secret protects the exchange. We could not confirm from public documentation which callback URL Salesforce shows for MCP servers, or whether your org offers the per-user option. If your org rejects the connection, tell us what the error says.

## HubSpot

**HubSpot does not currently let a customer paste an MCP server URL.** Its Agent Builder connector list is fixed (for example Notion, Atlassian, Gong, Zapier). The documented route is for a developer to package a server as an **MCP server component** inside a HubSpot app (**beta**, private or marketplace distribution). Customers then install the app and the server shows up under **Add tool** in Agent Builder. Sources: HubSpot, [Connect apps to HubSpot's AI agents](https://knowledge.hubspot.com/integrations/customize-breeze-agents-with-hubspot-mcp-client) and [Connect external MCP servers to HubSpot agents (BETA)](https://developers.hubspot.com/docs/apps/developer-platform/add-features/mcp-server).

| HubSpot requires | Presay |
| --- | --- |
| Public HTTPS URL | Yes |
| OAuth 2.1 authorization code with PKCE (S256) | Yes |
| Discovery at `/.well-known/oauth-authorization-server` on the server's domain | Yes |
| Access token **and refresh token** | Yes (refresh tokens last 30 days and rotate) |
| A fixed client ID, no dynamic registration | Yes: create it in Settings |
| Fixed callback `https://oauth-redirect.hubspot.com/callback/mcp_server` | Filled in by the **HubSpot** preset |

To try it you need a HubSpot developer account with access to the **MCP server public beta** and the HubSpot CLI.

1. In Presay, choose the **HubSpot** preset and **Create integration**. It has **no secret**: HubSpot signs in with PKCE only. Copy the client ID.
2. In your HubSpot project, create an app set to **private** distribution with at least the `oauth` scope. The platform version in `hsproject.json` must be the beta one HubSpot names on its page.
3. Add `app/mcp-server/presay-hsmeta.json`:

```json
{
  "uid": "presay_mcp",
  "type": "mcp-server",
  "config": {
    "name": "Presay",
    "description": "Run simulated audience studies and read reports",
    "mcpUrl": "https://mcp.presay.hyver.app/mcp",
    "mcpClientId": "<client ID from Settings, AI agents, Integrations>",
    "requiredScopes": ["presay:read", "presay:write"],
    "enabled": true
  }
}
```

4. Deploy the project, copy the install link from the app's **Distribution** tab and install it in a HubSpot account.
5. In the account, open the project's MCP server component and choose **Test connection**, then **Connect**. Presay's sign-in page opens.
6. In **Agent Hub**, **Agent Builder**, choose **Configure**, **Add tool**, the **MCP Servers** category, and **Connect and add** for Presay.

Field names come from HubSpot's beta page and may change. **Check** that page before you start, and tell us if HubSpot refuses the connection.

## Other apps

For any app that asks for an OAuth client for an MCP server: choose **Other app**, create the integration, and give the app the client ID, the secret if shown, the **server URL** and the **identity provider URL**. Add the callback URL the app shows under **Callback URLs**. Presay supports the authorization-code flow with PKCE (or a secret), refresh tokens, and the client-credentials flow for a service account.

## OAuth or API key?

**OAuth.** Presay has no API key or personal access token, on purpose: every connection is a person (or a revocable service account you created) approved in your account. Neither CRM documents an API-key option for a custom MCP server.

| | Supported by the app | Presay |
| --- | --- | --- |
| **Salesforce** | OAuth 2.0 or none. Per-user authorization code is disputed; client credentials is reported | Both: per person, or a service account |
| **HubSpot** | OAuth 2.1 with PKCE only, for a custom MCP server component | Yes, as an integration with no secret |

## Safety and control

- Only you can create, edit or delete integrations, in the web app. An assistant connected through MCP cannot.
- Secrets are stored only as a hash. Deleting an integration stops its connections from refreshing at once; tokens already issued last up to an hour, except a service account's, which stop immediately.
- Callback URLs must be plain `https` addresses. The sign-in page shows people which app is asking and where it will send them. Only approve apps you recognise.
- A person can remove any connection under **Settings, AI agents, Connected assistants**.

## Until it works in your app

If an app can't connect yet, the study loop still fits your CRM workflow:

- Run the study in the [web app](/getting-started/first-study.md) or through an [assistant](/ai/mcp.md), then paste the [shared report link](/reports/share-export.md) into the Salesforce record or HubSpot note.
- Export the report as PDF, Word or JSON and attach it. See [Share & Export](/reports/share-export.md).

> The respondents are simulated. Whatever an agent in your CRM reports back is a directional signal, not measured demand. See [Limits of Synthetic Research](/limits.md).
