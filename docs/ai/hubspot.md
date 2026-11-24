# Connect Presay in HubSpot

Use Presay from HubSpot's AI agents in **Breeze**: run studies and read reports by asking the agent. You install Presay's HubSpot app once, finish a short setup on a Presay page, then add Presay to your agent. Each person signs in with their own Presay account. **There is nothing to copy or configure.**

**In short:** get the install link → install the app → finish on the Presay page → add Presay to your Breeze agent → sign in.

## Before you start

1. **A HubSpot account** with Breeze and permission to install apps (a Super Admin, or a user with the **HubSpot Marketplace access** permission).
2. **The install link.** Presay's HubSpot app is in a private beta, so we send the link to each account.
   - [Email us to request it](mailto:support@hyver.app?subject=Presay%20for%20HubSpot%3A%20install%20link&body=My%20HubSpot%20account%20ID%3A%20) with your **HubSpot account ID**: the number in HubSpot's web address after `/contacts/` (for example `app.hubspot.com/contacts/`**`1234567`**`/`).
   - We reply with the link.
3. **A Presay account** is free. You can create it on the page you reach after installing.

## Connect Presay

1. **Install the app.** Open the install link, choose your HubSpot account and approve the app.
2. **Finish on the Presay page.** HubSpot sends you to a Presay page titled **"Presay is installed in HubSpot"**. It lists the steps below. If you do not have a Presay account yet, choose **Create a free account** there. Installing the app does **not** connect your account: that happens in step 4.
3. **Open your agent in Breeze.** In HubSpot open **Breeze**, then **Breeze Studio**, and open an agent you can edit. HubSpot's default agents have to be cloned first (**Clone**, then open your copy).
4. **Add Presay as a tool.** Choose **Configure agent**, then **Add tool**. In the panel, open the **MCP Servers** tab (some accounts call it **Connectors**) and choose **Connect and add** next to **Presay**.
5. **Sign in to Presay.** A Presay sign-in window opens. Type your Presay email and password and choose **Sign in and allow** (pressing Enter does the same). HubSpot comes back with Presay connected.
6. **Try it.** Ask the agent: **"List my Presay audiences."**

> HubSpot changes its menus often and its own pages name them differently (Breeze Studio, Agent Builder, Connectors, MCP Servers). If a name above does not match your account, look for **Add tool** on your agent and the **MCP Servers** or **Connectors** list. HubSpot does not document connecting a custom server to the Breeze Assistant chat itself, so use an agent.

## How to tell it worked

- **In HubSpot:** the agent's tool list shows **Presay**. In HubSpot's **Settings, Integrations, Connected Apps** you can set each tool to **Always allow**, **Ask permission** or **Never allow**.
- **In Presay:** open **Settings, AI agents**. The guide's **HubSpot** tab shows **Connected: HubSpot**, and **Connected assistants** lists **HubSpot** with a **Read and write** badge and the date access ends.

If Presay is not listed under Connected assistants, the sign-in did not finish: nobody is connected, whatever HubSpot's install page showed. Repeat steps 4 and 5.

## Good to know

- **It is free.** Presay costs nothing to use within the weekly and daily study [allowance](/account/limits.md) (currently 30 a week and 10 a day per account). HubSpot's own pricing is separate: running an agent can use HubSpot credits, depending on your HubSpot plan. See the [Terms of Service](https://presay.hyver.app/terms-of-service.html) and the [Privacy Notice](https://presay.hyver.app/privacy-policy.html).
- **Each person signs in once**, with their own Presay account. Studies count toward that person's own weekly and daily allowance.
- **The sign-in page** opens in your browser's language (English, German, Spanish, French, Italian or Portuguese). Choose **Create a free account** or **Forgot your password?** on it: both open in a new tab, so the sign-in stays open. The page stays valid for 15 minutes.
- **The connection lasts a year** and renews itself while the agent is in use. After that, HubSpot asks you to connect again.
- **To disconnect,** remove Presay in HubSpot, or choose **Disconnect** under **Settings, AI agents, Connected assistants** in Presay. Access ends at once.
- **Studies use simulated respondents.** Treat what the agent reports as a directional signal. See [Limits of Synthetic Research](/limits.md).

## Troubleshooting

| You see | What to do |
| --- | --- |
| "Could not connect account because user denied access. The user declined" | The sign-in window was cancelled. Choose **Connect and add** again, then **Sign in and allow**. (Until 23 November 2026, pressing Enter after typing the password cancelled by mistake. That is fixed.) |
| "That email and password do not match" | A typo or another account. Your email stays filled in: retype the password, or choose **Forgot your password?** |
| "This sign-in page expired" | The window was open for more than 15 minutes. Choose **Connect and add** again |
| Presay is not under Connected assistants | The sign-in did not finish. Repeat steps 4 and 5 |
| No **MCP Servers** or **Connectors** tab under **Add tool** | The app is not installed in this account yet (step 1), or your HubSpot plan does not include Breeze agents. Email us |
| The install link does not work | It is private to the account we approved. Email us your HubSpot account ID |

Still stuck? Email [support@hyver.app](mailto:support@hyver.app) with the exact message and the time.

HubSpot's MCP feature is in public beta and may change. Source: HubSpot, [Connect external MCP servers to HubSpot agents](https://developers.hubspot.com/docs/apps/developer-platform/add-features/mcp-server).

## For developers

HubSpot does not let a customer paste an MCP server URL: a server reaches its agents through an app the server's owner builds once (an "MCP server component"). Presay owns that app, so customers create no client. HubSpot sends a fixed client ID, uses PKCE (S256) and does not register clients dynamically. It needs an access token and a refresh token, discovery at `/.well-known/oauth-authorization-server` on the server's domain, and the callback `https://oauth-redirect.hubspot.com/callback/mcp_server`. Presay meets all of these with a Presay-owned public client.
