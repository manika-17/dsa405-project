# dsa405-project

# Best Picture and IMDb Audience Ratings

## Project Overview

This project examines whether films that win the Academy Award for Best Picture have higher IMDb audience ratings than non-winning nominees from the same award years. The analysis focuses on film years 2015–2024.

## Research Question

Among films nominated for the Academy Award for Best Picture for film years 2015–2024, do the winners have higher IMDb audience ratings than the non-winning nominees from the same award years?

## Data Sources

The project combines data from two sources:

- **Wikipedia:** [Academy Award for Best Picture](https://en.wikipedia.org/wiki/Academy_Award_for_Best_Picture), which identifies Best Picture nominees and winners.
- **IMDb:** [Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/), which provide audience ratings, vote counts, title information, and release years.

Raw data is preserved in the `data/raw/` folder and is not modified by the project code.

## Project Milestones

### P2: Data Audit and Cleaning

The P2 notebook audits and cleans the Best Picture data from Wikipedia. This includes standardizing film titles, checking for duplicates, validating film years, and documenting cleaning decisions.

### P3: Acquisition and Integration

The P3 notebook retrieves the Wikipedia and IMDb data, integrates the two sources, and verifies the accuracy of the join.

The acquisition process includes:

- Rate-limited requests with an honest coursework User-Agent.
- Caching raw data locally to avoid unnecessary repeated downloads.
- Error handling for failed requests, timeouts, and missing HTML elements.
- Demonstrations showing that the code catches errors rather than silently producing incorrect results.

The datasets are joined using normalized film titles and release years. A **one-to-one left join** is used to preserve all Best Picture nominees, and `validate='one_to_one'` checks that the merge does not create duplicate matches.

### P3 Integration Results

| Metric | Result |
|---|---|
| Best Picture nominees | 91 |
| IMDb matches | 86 |
| Unmatched films | 5 |
| Match rate | 94.5% |
| Best Picture winners verified | 10 of 10 |

Five films remained unmatched because of differences in release years or ambiguous IMDb title matches. These records were preserved rather than forcing potentially incorrect matches.

The notebook includes verification assertions that check:

- Row counts after the join.
- Uniqueness of nominee identifiers.
- Valid IMDb rating ranges.
- Exactly one Best Picture winner per film year.
- Preservation of original nominee records.

## Ethics and Data Use

The project uses publicly accessible data and follows the acquisition plan developed in A8.

- No login, paywall, or personal viewer information is required.
- Wikipedia requests are rate-limited and cached.
- IMDb data is obtained through its official non-commercial downloads rather than scraping IMDb pages.
- No technical protections or access restrictions are bypassed.

Wikipedia content is attributed to Wikipedia contributors under the applicable Creative Commons license.

**IMDb Attribution:** Information courtesy of IMDb (https://www.imdb.com). Used with permission.

## How to Run

1. Open the [P2 Cleaning Notebook](https://colab.research.google.com/drive/1JfLs5wEH0jLQXwqZtiBfSMd-TsmAqpb9?usp=sharing) in Google Colab to review the original cleaning process.
2. Open `DSA405_002_FA26_P3_mjain23.ipynb` from this repository in Google Colab or Jupyter Notebook.
3. Install any missing Python libraries, including `pandas`, `requests`, `beautifulsoup4`, `lxml`, and `numpy`.
4. Ensure the `data/raw/` directory exists and configure the coursework User-Agent contact information.
5. Restart the kernel and run all cells from top to bottom.
6. Review the acquisition results, join diagnostics, and verification assertions.

The P3 notebook uses locally cached raw data when available. If the files are not cached, it retrieves them from the original sources. Because IMDb updates its datasets regularly, results may change between runs.

## Project Limitations

IMDb ratings reflect the opinions of IMDb users and may not represent all moviegoers. Additionally, five Best Picture nominees could not be matched unambiguously to IMDb records, so those films are excluded from analyses requiring audience ratings.

The project examines the relationship between award outcomes and audience ratings but does not establish causation.

## Next Steps

The next milestone will analyze whether Best Picture winners tend to receive higher IMDb audience ratings than non-winning nominees, comparing films within the same award years.

