# Troubleshooting

Find the symptom, then follow the fix. If it is not here, email [support@hyver.app](mailto:support@hyver.app) with the exact message and the time.

## Account and sign-in

| You see | What to do |
| --- | --- |
| No verification code arrives, or it expired | Choose **Resend code** on the **Confirm account** screen. Check spam. |
| Password rejected when you sign up | It needs at least 10 characters with an uppercase letter, a lowercase letter, a number and a symbol. |
| Cannot reset a password | An account that was never confirmed cannot be reset. Sign up again with the same email, or contact support. |
| Your setup vanished after signing in | A study you began on the public page is kept for 30 minutes in that browser tab. After that you start again. |

## Running a study

| You see | What to do |
| --- | --- |
| The run button is blocked and mentions a limit | You reached the weekly or daily allowance. The message says when the next slot opens. Your settings stay in the form. See [Study Allowance](/account/limits.md). |
| A URL cannot be loaded | Presay must be able to open the page. For a page behind a sign-in, paste the text or upload a screenshot instead. |
| The report says personas judged the page text only | No screenshot could be captured. Paste a screenshot as an image test if layout and design matter. |
| The report says information is "missing" | It may be missing only from the image you gave. Add more images so personas judge them together, or include the details in text. |
| Fewer personas than you asked for in the report | Some responses were not usable. The report says how many were, and every figure uses those. Re-run if the number is too low for your decision. |
| The study seems slow | Larger samples take longer and the form shows an estimate. The study keeps running if you leave the page. |

## Reading a report

| You see | What to do |
| --- | --- |
| A segment is hidden as **insufficient sample** | It has fewer than 5 personas. Run a larger sample, or widen the segment. |
| A segment has no highlight | The difference cannot be told apart from noise at this sample size. |
| Numbers changed when you re-ran the study | Expected: a study is a simulation. To compare versions, run them as one [A/B test](/studies/types.md). |
| A/B warns that the difference is mostly wording | The two versions are nearly the same text. Do not read the gap as a real preference. |
| A shared link says "This shared report is not available" | Sharing was stopped. Create a new link from the study. |
| An export failed | Try again. The report itself is unaffected. |

## Drafts and retesting

| You see | What to do |
| --- | --- |
| **Draft an improved version** is not available | Drafts need a report with reviewed recommendations to apply. One draft can be in progress per study at a time. |
| A draft cannot be scored | The draft or the original has expired. |
| Image drafts are missing | They may not be enabled for your account yet. |
| Draft limit reached | Drafts have their own daily cap, separate from your study allowance. |

## Audiences and imports

| You see | What to do |
| --- | --- |
| An import fails | Check that dimension names are `age`, `gender`, `geography`, `income`, `education` or `area`, and that each dimension's weights add up to 100. The error names the file and the problem. |
| You cannot edit a saved audience | Saved audiences cannot be edited or renamed. **Duplicate** it and change the copy. |

## Assistants and the extension

| You see | What to do |
| --- | --- |
| The assistant cannot sign in | Make sure you have a Presay account, then connect again from the client. **Settings, AI agents** has current steps for each client. |
| Too many wrong passwords | Wait 15 minutes, or reset your password on the website. |
| A burst of studies is queued | Retry in a few seconds. Parallel studies may be queued. |
| The connection stopped working | Sessions end after 90 days. Sign in again from the client. |
| The extension says it is running an older background script | Press **Reload Presay**. If that does not help, remove the extension at `chrome://extensions` and load it again. |
| The extension cannot capture a page | Chrome internal pages cannot be captured. Use an ordinary web page. |
| HubSpot problems | See the table in [Connect Presay in HubSpot](/ai/hubspot.md). |

## Still stuck?

Check the [FAQ](/faq.md), then contact [support@hyver.app](mailto:support@hyver.app).
