# Connect Presay in HubSpot

Run Presay studies and read reports from HubSpot's AI agents (Breeze, Agent Builder). You install Presay's HubSpot app once, then each person signs in with their own Presay account. There is **nothing to copy or configure**: no client ID, no secret, no server URL.

> **Status: private beta.** The app works, but it is not on the HubSpot Marketplace yet, so HubSpot only lets us approve a limited number of accounts. **To get access, email [support@hyver.app](mailto:support@hyver.app) with your HubSpot account ID** and we will send you an install link. You need a HubSpot account that includes **Agent Builder**.

## Connect in four steps

1. **Install the app.** Open the install link, choose your HubSpot account and approve the app. HubSpot then sends you to Presay's **Settings, AI agents** page. That is expected: it only installs the app. **Nothing shows as connected yet**, because nobody has signed in to Presay.
2. **Connect your Presay account.** In **Agent Hub**, **Agent Builder**, open the agent, choose **Configure**, **Add tool**, the **MCP Servers** category, and **Connect and add** for **Presay**.
3. **Sign in.** Presay's sign-in page opens. Type your Presay email and password and choose **Sign in and allow** (pressing Enter does the same). Each person signs in once; studies use their own [allowance](/account/limits.md).
4. **Try it.** Ask the agent: "List my Presay audiences".

## How you know it worked

- In **HubSpot**, the agent's tool list shows **Presay**. Under **Settings, Integrations, Connected Apps** you can choose whether each tool is **Always allow**, **Ask permission** or **Never allow**.
- In **Presay**, **Settings, AI agents** has a **HubSpot** tab with these steps. While it is open it shows **Connected: HubSpot** as soon as you sign in. **Connected assistants** lists **HubSpot** with a **Read and write** badge, the date you connected and the date access ends.
- If there is no HubSpot row in Presay, the sign-in was not completed: nobody is connected, whatever HubSpot's install page said.

## What the sign-in page looks like

- It opens in your browser's language (English, German, Spanish, French, Italian or Portuguese), names **HubSpot** as the app asking, and lists what it can do: see your studies, reports and audiences, and run studies and save audiences. Each study counts toward your own weekly and daily allowance.
- **New to Presay?** Choose **Create a free account** on that page. It opens in a new tab, so the sign-in stays open. Confirm your email, then come back to the first tab and sign in. The page stays valid for 15 minutes. If it has expired, choose **Connect and add** again in HubSpot.
- **Forgot your password?** The link on the same page opens the reset page in a new tab.
- After you sign in, Presay sends you straight back to HubSpot.

## Staying connected

The connection lasts a year and renews itself while the agent is in use. After that, HubSpot asks you to connect again. You can disconnect sooner in HubSpot, or under **Settings, AI agents, Connected assistants** in Presay, where it appears as "HubSpot".

## Troubleshooting

| HubSpot says | What it means | What to do |
| --- | --- | --- |
| "Could not connect account because user denied access. The user declined" | The sign-in page was cancelled, so Presay gave HubSpot no access. Until 23 November 2026 this also happened by mistake when you pressed Enter after typing your password. That is fixed | Choose **Connect and add** again, then **Sign in and allow** |
| The sign-in page says the email and password do not match | A typo or the wrong account. Your email stays filled in so you only retype the password | Retry, or use **Forgot your password?** |
| "This sign-in page expired" | The page was open for more than 15 minutes | Choose **Connect and add** again |
| Nothing under Connected assistants in Presay | The sign-in was not completed | Do steps 2 and 3 again |

If something else goes wrong, email [support@hyver.app](mailto:support@hyver.app) with the exact message and the time. HubSpot's MCP feature is in public beta and may change.

Sources: HubSpot, [Connect apps to HubSpot's AI agents](https://knowledge.hubspot.com/integrations/customize-breeze-agents-with-hubspot-mcp-client) and [Connect external MCP servers to HubSpot agents (BETA)](https://developers.hubspot.com/docs/apps/developer-platform/add-features/mcp-server).

## For developers

HubSpot does not let a customer paste an MCP server URL. A server reaches its agents through an app that the server's owner builds once (an "MCP server component"), and Presay owns that app, so customers create no client. HubSpot sends a fixed client ID, uses PKCE (S256) and does not register clients dynamically. It needs an access token and a refresh token, discovery at `/.well-known/oauth-authorization-server` on the server's domain, and the callback `https://oauth-redirect.hubspot.com/callback/mcp_server`. Presay meets all of these with a Presay-owned public client.
