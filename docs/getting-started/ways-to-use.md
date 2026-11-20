# Ways to Use Presay

Presay has three front doors. All three use the **same account**, the same simulated panels and the **same study allowance**, so a study started in one shows up in the others.

| | **Web app** | **AI assistant (MCP)** | **Browser extension** |
| --- | --- | --- | --- |
| **Best for** | Full control: audiences, A/B tests, files, reading and sharing reports | Hands-off work: run, read, improve and retest by asking | Testing the page or text you are looking at, without copying it |
| **Where** | [presay.hyver.app](https://presay.hyver.app/) | Claude, ChatGPT, Cursor, VS Code and other MCP clients | Chrome side panel |
| **Targets** | URL, image, text, document, audio, video | URL, text, image, audio, video; large media through an upload step | Selected text, the visible screen, an image |
| **Audience** | Presets, custom mixes, saved and imported audiences | A saved audience, a built-in template, or a mix the assistant builds from your description | Audience and sample size at review |
| **Reports** | Full interactive report, share link, PDF, Word, JSON | Summary and data the assistant reads back to you | Result in the panel, full report opens on the web |
| **Drafts** | Improve, Apply and retest, Score against original | Yes, through the assistant | Test a revision of a captured page or text |
| **Sign-in** | Email and password | Approve access once, in the browser | Email and password in the panel |

> Studies count against one shared weekly and daily [allowance](/account/limits.md), whichever door you use.

## Which one should I use?

- **Start in the web app** if you are new. It shows every option and is where the full report lives.
- **Use an assistant** when you want to describe the job in words ("test these three headlines on UK adults 25 to 44") and have the assistant run, compare and summarise.
- **Use the extension** when the thing you want to test is already on screen, such as a live landing page, an ad or a paragraph in a draft.

You can mix them. A common loop is: capture a page with the extension, read the full report on the web, then ask an assistant to draft and retest a fix.

## Web app

1. **Sign in** at [presay.hyver.app](https://presay.hyver.app/). See [Create an Account](/getting-started/account.md).
2. Open **Studies**, then **New study**. Choose [A/B test, concept test or messaging test](/studies/types.md).
3. Add the [target](/studies/targets.md): a URL, image, pasted text, document, audio or video.
4. Choose the [audience and sample size](/studies/audience.md): a preset or custom mix, and 1 to 500 personas.
5. **Run study.** It keeps running if you leave the page.
6. Open the report from **Studies** and [read it](/reports/reading.md): decision, metrics, narrative, segments and reactions.
7. Act on it: [share a link or export](/reports/share-export.md), or [Improve & Retest](/drafts/retest.md) a draft.

Manage reusable groups under **Audiences** ([library](/audiences/library.md), [import from a file](/audiences/import.md)). Language, theme and connected assistants live in [Settings](/account/settings.md).

## AI assistant (MCP)

Presay is a remote MCP server. You connect an assistant once and it works inside your own account and allowance.

1. **Connect** with the server URL `https://mcp.presay.hyver.app/mcp`. Step-by-step instructions for each client are in [Connect an Assistant](/ai/mcp.md), and in the web app under **Settings, AI agents**.
2. **Approve access** when the browser opens. You can ask for read-only access.
3. **Ask in plain language.** A study takes a minute or two and the assistant checks until it completes.

Things you can say:

| You say | What happens |
| --- | --- |
| "List my Presay audiences" | Checks the connection and shows your audiences |
| "Run a study of this headline on US adults, 20 respondents" | Creates a study and waits for the result |
| "Show me the report" | Reads the report and summarises scores, segments and the decision |
| "Improve this text from the recommendations and retest it" | Drafts a revision and scores it against the original |
| "Share this study" / "Stop sharing it" | Creates or revokes a read-only link |
| "How many studies do I have left this week?" | Reads your usage |

The assistant relays a simulated, directional result. Ask it to include the interval and the [limits](/limits.md) when you quote a number.

## Browser extension

The extension puts Presay in the Chrome side panel.

1. **Install** the extension and open the panel. Sign in with your Presay email and password. See [Browser Extension](/ai/extension.md).
2. On **Home**, choose what to capture: **Selected text**, **Visible screen** or **Image**. You can also use the toolbar button or right-click **Test with Presay** or **Test selected text with Presay**.
3. In **Review**, choose the audience and sample size, then **Run test**.
4. Read the result in the panel, or choose **View full report on Presay** to open it on the web.
5. To test a change, edit the original, then use **Capture revision** and **Compare versions**.

Studies you run from the extension appear under **Studies** in the panel, and in the web app.

## Same results everywhere

Whichever door you use, the study is the same simulation and the report is the same report. The differences are convenience and control, not accuracy. Read [Limits of Synthetic Research](/limits.md) before you act on any of them.
