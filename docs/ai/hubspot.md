# Connect Presay in HubSpot

Use Presay from HubSpot's AI agents (Breeze, Agent Builder): run studies and read reports by asking the agent. You install Presay's HubSpot app once. Then each person signs in with their own Presay account. **There is nothing to copy or configure.**

**In short:** get the install link, install the app, add Presay as a tool to your agent, sign in.

## Before you start

You need three things:

1. **A Presay account.** It is free. If you do not have one yet, you can create it during step 4.
2. **A HubSpot account with Agent Builder**, and permission to install apps (a Super Admin, or a user with the **HubSpot Marketplace access** permission).
3. **The install link.** Presay's HubSpot app is in a private beta, so we send the link to each account.
   - [Email us to request it](mailto:support@hyver.app?subject=Presay%20for%20HubSpot%3A%20install%20link&body=My%20HubSpot%20account%20ID%3A%20) with your **HubSpot account ID**: the number in HubSpot's web address after `/contacts/` (for example `app.hubspot.com/contacts/`**`1234567`**`/`). You can also see it under your account name at the top right.
   - We reply with a link. It works for your HubSpot account only.

## Connect Presay

1. **Install the app.** Open the install link, choose your HubSpot account and approve the app. HubSpot then opens a Presay **Settings** page. That is normal: this step only installs the app, and **Presay is not connected yet**.
2. **Open your agent.** In HubSpot go to **Agent Hub**, then **Agent Builder**, and open the agent that should use Presay (or create one).
3. **Add Presay as a tool.** Choose **Configure**, then **Add tool**. Open the **MCP Servers** category and choose **Connect and add** next to **Presay**.
4. **Sign in to Presay.** A Presay sign-in window opens. Type your Presay email and password and choose **Sign in and allow** (pressing Enter does the same). HubSpot comes back with Presay connected.
   - **No account yet?** Choose **Create a free account** on that page. It opens in a new tab: confirm your email, then return to the sign-in tab and sign in. The page stays valid for 15 minutes.
5. **Try it.** Ask the agent: **"List my Presay audiences."**

## How to tell it worked

- **In HubSpot:** the agent's tool list shows **Presay**. Under **Settings, Integrations, Connected Apps** you can set each tool to **Always allow**, **Ask permission** or **Never allow**.
- **In Presay:** open **Settings, AI agents**. The guide shows **Connected: HubSpot**, and **Connected assistants** lists **HubSpot** with a **Read and write** badge and the date access ends.

If Presay is not listed under Connected assistants, the sign-in did not finish. Nobody is connected, whatever HubSpot's install page showed. Repeat steps 3 and 4.

## Good to know

- **Each person signs in once**, with their own Presay account. Studies count toward that person's own weekly and daily [allowance](/account/limits.md).
- **The connection lasts a year** and renews itself while the agent is in use. After that, HubSpot asks you to connect again.
- **To disconnect,** remove Presay in HubSpot, or choose **Disconnect** under **Settings, AI agents, Connected assistants** in Presay. Access ends at once.
- **Studies use simulated respondents.** Treat what the agent reports as a directional signal. See [Limits of Synthetic Research](/limits.md).

## Troubleshooting

| You see | What to do |
| --- | --- |
| "Could not connect account because user denied access. The user declined" | The sign-in window was cancelled. Choose **Connect and add** again, then **Sign in and allow**. (Until 23 November 2026, pressing Enter after typing the password cancelled by mistake. That is fixed.) |
| "That email and password do not match" | A typo or another account. Your email stays filled in: retype the password, or choose **Forgot your password?** |
| "This sign-in page expired" | The window was open for more than 15 minutes. Choose **Connect and add** again |
| Presay is not under Connected assistants | The sign-in did not finish. Repeat steps 3 and 4 |
| You cannot see **MCP Servers** under **Add tool** | The app is not installed in this account yet, or your account does not include Agent Builder. Check step 1, or email us |

Still stuck? Email [support@hyver.app](mailto:support@hyver.app) with the exact message and the time.

HubSpot's MCP feature is in public beta and its menus may change. Source: HubSpot, [Connect external MCP servers to HubSpot agents](https://developers.hubspot.com/docs/apps/developer-platform/add-features/mcp-server).

## For developers

HubSpot does not let a customer paste an MCP server URL: a server reaches its agents through an app the server's owner builds once (an "MCP server component"). Presay owns that app, so customers create no client. HubSpot sends a fixed client ID, uses PKCE (S256) and does not register clients dynamically. It needs an access token and a refresh token, discovery at `/.well-known/oauth-authorization-server` on the server's domain, and the callback `https://oauth-redirect.hubspot.com/callback/mcp_server`. Presay meets all of these with a Presay-owned public client.
