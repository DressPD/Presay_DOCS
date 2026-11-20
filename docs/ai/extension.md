# Browser Extension

The Presay extension lives in the Chrome side panel so you can test a page you are looking at without copying anything.

> The extension is a preview. Ask support for the current install route and whether live study access is enabled for your account.

## Journey

1. **Sign in** with your Presay email and password. No separate window or redirect tab opens.
2. On **Home**, choose **Selected text**, **Visible screen** or **Image**, or use the toolbar button or right-click **Test with Presay** / **Test selected text with Presay**. Only the viewport is captured, not the full page.
3. **Review** the capture: choose the audience and sample size.
4. **Run** the study and read the result in the panel.
5. Optionally **Test a revision**.

## Test a revision

The extension does not edit your page. To test a change:

1. Make the change on the original page.
2. Choose **Capture revision**, or capture the updated selected text from the right-click menu.
3. Review **Revision captured**, then open **Compare versions**.
4. Run the comparison. It is a paired A/B on the same panel.

## Where data lives

Study state and stimulus metadata are stored in your browser. Image stimuli are stored in the extension's local storage. A pending capture is temporary.

## Sign out

**Sign out** in Settings clears local tokens and tries to revoke the session. Other open panels return to the sign-in screen. It does not touch your website cookies.

## After an update

If the panel says it is still running an older background script, press **Reload Presay**. If that does not help, remove the extension at `chrome://extensions` and load it again.

## Tips

- Use ordinary web pages that can be captured. Chrome internal pages cannot be.
- Extension studies count against the same [allowance](/account/limits.md) as the website.
