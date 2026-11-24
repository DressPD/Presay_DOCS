# From Report to Decision

[Reading a Report](/reports/reading.md) explains each part of a report. This page is the routine for turning one into a decision. It takes about ten minutes.

## The routine

### 1. Check the sample first

Open **Methodology & sample** before you read any score. Confirm that:

- enough personas returned a usable response (if fewer than requested did, the report says so)
- the sample matches the audience you asked for, and which dimensions used general-population defaults
- the **Analysed content** is what you meant to test (for a URL, check that the screenshot and text are the page you expected)

If any of these is off, fix the study and re-run before you interpret anything.

### 2. Read the decision and the signal

Start with the call: **Accept: use it as it is** or **Revise: change it first**. Treat it as a recommendation, not a verdict, because it does not know your constraints. The **directional signal** (0 to 100) is for comparing versions, not for judging a single result.

### 3. Look at the four metrics with their intervals

For each of **clarity**, **appeal**, **trust** and **relevance**, look at the mean and its 95% interval, not the mean alone. Two metrics whose intervals overlap heavily are not meaningfully different at this sample size.

| If you see | It usually points to | Look at |
| --- | --- | --- |
| Low **clarity** | People cannot tell what this is or what to do next | The narrative's first statements, then the quoted passages |
| High **appeal**, low **trust** | It grabs attention but does not feel credible enough to act on | Claims without proof, unexplained prices or promises |
| High **trust**, low **appeal** | Credible but easy to ignore | Opening line, headline, visual hook |
| Low **relevance** | It does not speak to this audience's situation | [Segments](/reports/segments.md), and whether the audience matches who you are targeting |
| Everything **moderate** | A mixed, unremarkable read | The segment breakdown for a split hiding behind the average |

These are starting hypotheses drawn from what each metric means (see [Metrics](/reports/metrics.md)). Confirm them in the reactions.

### 4. Trace the narrative to the reactions

Every statement in the narrative cites the reactions it relies on. Select a citation, read the actual persona responses, and decide whether you agree. A citation is the model's judgement, not a statistical test.

### 5. Check segments, if the sample allows

If you ran 100 or more personas, look for groups that react differently. Segments below 5 personas are hidden, and highlighted differences have already been corrected for comparing many segments. If a segment matters to your decision and is hidden, run a larger sample. Read group differences with caution: see [Limits](/limits.md).

### 6. Act on the recommendations

For a **Revise** call, work through the **High** and **Medium** recommendations. Each shows the passage, the evidence, the expected effect and the watch-outs. Then either edit by hand or use [Improve & Retest](/drafts/retest.md), which scores the draft against the original on the same panel.

### 7. Record the decision

Use the report's **decision notes** to write what you decided and what would change your mind. They are for you and your team and are not sent to the study model. To share the report itself, see [Share & Export](/reports/share-export.md).

## What you can conclude, and what you cannot

| Reasonable | Not reasonable |
| --- | --- |
| "Version B reads as clearer and more trustworthy than A to this audience." | "Version B will convert 12% better." |
| "The pricing sentence is the main trust problem." | "This proves the message works." |
| "This is unclear enough to fix before we spend on traffic." | "Real customers will rate this 3.8 out of 5." |
| "This is worth testing with a real panel." | "No need to talk to customers." |

The scores are not calibrated to real-world ratings, and the panel has been checked against real people for group differences and rankings, not for absolute levels. See [Limits of Synthetic Research](/limits.md).

## When to run it again

- **After a real change.** Use [Improve & Retest](/drafts/retest.md) or an [A/B test](/studies/types.md), not a bare re-run.
- **When the sample is too small for your question.** Move from Directional to Indicative or Robust.
- **When the audience was wrong.** Change the mix, not the wording.

Re-running identical content gives slightly different numbers because the study is a simulation. Do not treat a run-to-run wobble as a finding.
