# Audience & Sample Size

## Demographics

Under **Demographics**, choose a **Preset** (a prebuilt general-population audience) or **Custom**. A custom audience is a weighted mix across:

- **Age** (ranges with weights)
- **Gender**
- **Geography** (countries)
- **Income**
- **Education**
- **Area** (urban, suburban, rural and similar)

Each dimension's weights should add up to 100%. Age, gender and geography are required. If you leave income, education or area unspecified, Presay fills them with general-population defaults for the region and says which ones in the report.

### Saved presets

Save a custom mix to reuse it in later studies: name it under **Save preset**, then pick it from **Saved presets**. You can also [import presets from a file](/audiences/import.md).

## Audience attributes

Optional settings describe the panel's relationship to your brand:

| Attribute | Meaning |
| --- | --- |
| **Relationship to the brand** | **Lead**: already in contact with the brand. **Prospect**: not yet. |
| **Brand awareness** | Whether they know the brand. A lead always does. |

Presay checks that the shares are consistent, for example there cannot be more leads than people who know the brand. If your content names a brand, Presay shows the one it detected.

Saved audiences hold demographics only. These attributes are study settings you choose on **New study**.

## Sample size

Set **Sample size (n)** from 1 to 500. More personas make the result more precise but take longer to run. In an A/B test it is the number per variant.

Before you run, the form shows the worst-case margin of error at 95% confidence and a confidence tier:

| Tier | n | What it means |
| --- | --- | --- |
| **Directional** | 1 to 29 | A quick read of which way opinion leans. A signal, not a precise result to plan spending around. |
| **Indicative** | 30 to 99 | Enough to trust the overall direction, still wide on individual segments. |
| **Robust** | 100 and up | Tight enough to quote as a finding, and to cut by segment and keep meaning. |

As a rule of thumb the worst-case margin is about ±20 points at n = 25, ±10 at n = 100 and ±5 at n = 400.

Segments with fewer than 5 personas are suppressed in the report. If you plan to cut by segment, size the panel so each segment you care about has enough personas.

> The margin of error describes spread across simulated personas. It is not uncertainty about a real population. See [Limits](/limits.md).
