# Connect Presay in Microsoft Copilot Studio

Use Presay from a **Microsoft Copilot Studio** agent, including agents that work with **Dynamics 365** (Sales and others): run studies and read reports by asking the agent. Each person signs in with their own Presay account. Presay reads no Microsoft 365, Dynamics 365 or Dataverse data: the server receives only what the agent sends in a tool call, for example the text of a headline to test.

**In short:** open your agent → add the Presay MCP server → sign in to Presay → ask the agent to list your audiences.

> **Status:** Presay is preparing Microsoft's MCP certification and is **not yet in the Copilot Studio catalog**. Until it is, add it by its address as described below. Once it is listed you will find **Presay** in the catalog and can skip the address.

## Before you start

1. **A Copilot Studio agent** you can edit, in an environment where your admin allows MCP servers.
2. **A Presay account.** It is free: create one at [presay.hyver.app/signup](https://presay.hyver.app/signup).

## Connect Presay

1. **Open your agent** in Copilot Studio and go to **Tools**, then **Add a tool**.
2. **Add the server.** Choose **New tool**, then **Model Context Protocol**. If Presay is in the catalog, pick it there and go to step 4.
3. **Fill in the form.** Name: **Presay**. Description: *Run simulated audience studies and read the reports*. Server URL: `https://mcp.presay.hyver.app/mcp`. Authentication: **OAuth 2.0**, with **Dynamic discovery** (or **Dynamic**) if Copilot Studio offers it. Presay registers the client by itself.
4. **Create the connection.** A Presay sign-in window opens. Type your Presay email and password and choose **Sign in and allow**.
5. **Add the tools to the agent** and publish it if your setup needs that.
6. **Try it.** Ask the agent: **"List my Presay audiences."**

> Microsoft changes its menus often. If a name above does not match your screen, look for **Add a tool** on your agent and the **Model Context Protocol** option.

## How to tell it worked

In Presay open **Settings, AI agents**. **Connected assistants** lists the connection with a **Read and write** badge and the date access ends. If it is not listed, the sign-in did not finish: nobody is connected. Repeat steps 4 and 5.

## Good to know

- **It is free.** Presay costs nothing to use within the weekly and daily study [allowance](/account/limits.md) (currently 30 a week and 10 a day per account). Microsoft's own licensing for Copilot Studio is separate. See the [Terms of Service](https://presay.hyver.app/terms-of-service.html) and the [Privacy Notice](https://presay.hyver.app/privacy-policy.html).
- **Each person signs in once**, with their own Presay account. Studies count toward that person's own allowance, not the organisation's.
- **To disconnect,** remove Presay from the agent, or choose **Disconnect** under **Settings, AI agents, Connected assistants** in Presay. Access ends at once.
- **Studies use simulated respondents.** Treat what the agent reports as a directional signal. See [Limits of Synthetic Research](/limits.md).

## Troubleshooting

| You see | What to do |
| --- | --- |
| "That email and password do not match" | A typo or another account. Your email stays filled in: retype the password, or choose **Forgot your password?** |
| "This sign-in page expired" | The window was open for more than 15 minutes. Create the connection again |
| Presay is not under Connected assistants | The sign-in did not finish. Create the connection again |
| Copilot Studio cannot add the server | Your admin may block MCP servers or external connections in that environment. Ask them to allow `mcp.presay.hyver.app` |
| Presay asks for a client ID and secret | Choose the dynamic option for authentication. If your tenant only offers manual entry, [email us](mailto:support@hyver.app?subject=Presay%20for%20Copilot%20Studio%3A%20client) and we will send you one |

Still stuck? Email [support@hyver.app](mailto:support@hyver.app) with the exact message and the time.

## For developers

The server is a remote MCP server (Streamable HTTP) at `https://mcp.presay.hyver.app/mcp`, and its own OAuth 2.1 authorization server (discovery at `/.well-known/oauth-authorization-server`, dynamic client registration, PKCE S256). Microsoft's certified-server flow stores a client ID and secret in the publisher's Azure Key Vault and does not use PKCE, so the certified listing uses a Presay confidential client with a secret, which the server accepts without PKCE.
