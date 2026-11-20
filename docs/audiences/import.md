# Import from a File

Create saved presets from spreadsheets instead of entering weights by hand. Each file becomes one preset, named after the file.

On **New study**, under demographics, open **Import from file** and choose your files.

**Accepted:** `.csv`, `.tsv`, `.xlsx` or `.json`, up to the size and file count shown on the screen.

## Option 1: summary table (recommended)

One row per segment.

| dimension | value | weight |
| --- | --- | --- |
| gender | female | 52 |
| gender | male | 48 |
| geography | DE | 100 |
| age | 18-34 | 40 |
| age | 35-54 | 35 |
| age | 55-74 | 25 |

- `dimension` is one of `age`, `gender`, `geography`, `income`, `education` or `area`.
- `weight` is the share of the audience in percent. Each dimension should add up to 100.
- Age rows can use `min` and `max` columns instead of a label such as `25-34`.
- Age, gender and geography are required.

## Option 2: one row per person

Columns named `age`, `gender`, `country`, `income`, `education` or `area`. Presay counts the rows and works out the percentages. Other columns are ignored.

**Nothing from the file is stored except the resulting mix.** The rows themselves are not kept.

## Templates

**What should my file look like?** offers downloadable templates for both options in the formats above. Start from one to avoid column-name mistakes.

## If an import fails

Check the dimension names and that each dimension's weights add to 100. Error messages name the file and the problem. Fix the file and import it again.
