# P1: Framing a Data Problem

**DSA 405 · Fall 2026 · Project Milestone 1**

| | |
|---|---|
| **Introduced** | Week 1 (Aug 21). Prep: post three project ideas to the Week 2 forum. |
| **Due** | **Thursday, Sep 3, 11:59 PM** |
| **Weight** | 5% of course grade · scored on the P1 rubric, 4 criteria |
| **Submit** | Notebook to Moodle. Filename `DSA405_002_FA26_P1_[yourUnityID].ipynb` |
| **Time** | 2–3 hours across two weeks, most of it looking at candidate sources |

---

## Purpose

P1 is the project plan: the question, the sources, and the declared difficulty, written
precisely enough that a reader could judge whether the plan will work.

Four components: a question, two named sources with evidence that each is reachable,
evidence that collection is permitted, and a tier declaration.

**The core requirement:** answer a question using **at least two data
sources that must be combined**, where **at least one comes off the web** by scrape or
API. A pre-packaged Kaggle download does not satisfy the web-source requirement.

---

## Deliverables

Four sections, one notebook. Prose cells for the writing, code cells for the evidence.

### 1. The question

One sentence, answerable with data that can be named, plus a short paragraph on why it
matters to someone besides the grader and what an answer would change.

The test is topic versus question. "Restaurant inspections in Wake County" is a topic.
"Do chain restaurants in Wake County hold more stable inspection scores than
independents?" is a question: the table that would answer it can be described.

The question usually changes once the data is in hand; P4 asks for a description of that
shift. P1 grades whether a real question exists at all.

### Answer

Among films nominated for the Academy Award for Best Picture for film years 2015–2024, do the winners have higher IMDb audience ratings than the non-winning nominees from the same award years?

This question tests whether the Academy's top choice tends to align with the preferences of IMDb viewers. The answer would matter to moviegoers deciding whether an Oscar winner is also likely to be broadly enjoyed and to film marketers deciding how strongly a Best Picture win signals audience appeal. I would create a nominee-level table with film year, title, winner status, IMDb average rating, and IMDb vote count. The main comparison would pair each year's winner with that year's non-winners, rather than combining unrelated eras. I would also repeat the comparison after requiring at least 10,000 IMDb votes because ratings based on very few votes are less stable. This is an association question; it will not claim that winning the award causes a higher rating.

### 2. Sources & access evidence

**Two or more sources, at least one off the web.** For each one:

| | |
|---|---|
| Publisher | who produces and hosts it |
| URL | the actual page, not the site's front door |
| Coverage & time span | what it includes, over what period |
| Approximate size | rows, records, or pages, as a number |
| Access method | download / `read_html` / scrape / API |

Then **paste in evidence that each source is reachable**: a row count from `read_csv`
or `read_html` (the Week 2 Lab covers both), a status code, or a screenshot of the data
on screen. A screenshot requires no code, so no source is exempt.

Finish with one sentence naming the **likeliest failure point**: the least trusted
source, and the fallback if it falls through.

### Source 1: Best Picture winners and nominees
| Field | Description |
|---|---|
| Publisher | Wikipedia contributors; hosted by the Wikimedia Foundation |
| URL | https://en.wikipedia.org/wiki/Academy_Award_for_Best_Picture |
| Coverage & time span | Best Picture winners and nominees from the award's beginning through film year 2025; this project will use film years 2015–2024 |
| Approximate size | 91 nominee records across the 10 selected film years |
| Access method | One rate-limited HTML request followed by `pandas.read_html`; the relevant decade tables are combined and filtered |
<img width="552" height="400" alt="image" src="https://github.com/user-attachments/assets/9004e59f-3a85-41dc-af33-5b85bb9b7bcc" />

### Source 2
| Field | Description |
|---|---|
| Publisher | IMDb.com, Inc. |
| URL | Documentation: https://developer.imdb.com/non-commercial-datasets/ ; files: https://datasets.imdbws.com/title.basics.tsv.gz and https://datasets.imdbws.com/title.ratings.tsv.gz |
| Coverage & time span | `title.basics` identifies titles, release years, and title types; `title.ratings` supplies current weighted average user ratings and vote counts. Files are refreshed daily. |
| Approximate size | 12,760,017 title records and 1,712,588 rating records when checked September 2, 2026 |
| Access method | Direct download of IMDb's official gzipped TSV files with `pandas.read_csv` |
<img width="572" height="194" alt="image" src="https://github.com/user-attachments/assets/cc1cea8c-ac9e-4c1d-b0d9-e7d84dde67be" />

The sources must be combined because Wikipedia identifies which films were nominated and which nominee won, while IMDb supplies audience ratings and vote counts. Neither source alone can answer the question. The planned relationship is one nominee to one IMDb title.

**Likeliest failure point:** title punctuation, subtitles, or release-year conventions may prevent an exact title-year match; if that occurs, I will create and report a manually validated crosswalk for only the unmatched nominees using their individual Wikipedia and IMDb pages, and if reliable one-to-one resolution is not possible I will exclude and list those films rather than force a match.

### 3. Constraints & guardrails

For each source, find and **quote** the constraint that applies to it:

- **Anything scraped:** the site's `robots.txt` (it lives at `site.com/robots.txt`; open
  it in a browser) and its terms of service. Week 8 covers reading these in detail; for
  P1, find them, quote the relevant line, and flag anything uncertain.
- **Downloads and APIs:** the license or terms of use, and any attribution they require.

Then certify the plan against the **course guardrails**, which are the following:

- Scrape only purpose-built sandboxes, sites with a documented API or open-data license,
  or sites whose robots.txt and terms of service permit it
- Never data behind a login or paywall
- Never personal or identifiable information about individuals
- Always rate-limit, identify the scraper honestly, and cache

If a site says no, that is the answer. A source ruled out with the terms quoted is good
P1 material, not a failure. When in doubt, ask the instructor before writing the
request.

### Wikipedia HTML table

**robots.txt:** Wikipedia's wildcard block states `User-agent: *` and disallows `/w/`, `/api/`, `/trap/`, and several `/wiki/Special:` paths. The planned page is the ordinary article path `/wiki/Academy_Award_for_Best_Picture`, which is not among those disallowed paths. Source: https://en.wikipedia.org/robots.txt.

Relevant excerpt:

> `User-agent: *`  
> `Disallow: /w/`  
> `Disallow: /api/`  
> `Disallow: /trap/`  
> `Disallow: /wiki/Special:`

**License/terms:** Wikipedia's page footer states: "Text is available under the Creative Commons Attribution-ShareAlike License 4.0; additional terms may apply." Source: https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use and the article footer. I will attribute Wikipedia and link the source page. If I publish adapted Wikipedia material, I will use the same or a compatible license as required.

### IMDb downloads

IMDb's official dataset documentation states: "Subsets of IMDb data are available for access to customers for personal and non-commercial use. You can hold local copies of this data, and it is subject to our terms and conditions." Source: https://developer.imdb.com/non-commercial-datasets/.

IMDb's non-commercial licensing page further states: "The data must be taken only from the datasets made available ... You may not use data mining, robots, screen scraping, or similar online data gathering and extraction tools on our website." It also requires this attribution:

> Information courtesy of IMDb (https://www.imdb.com). Used with permission.

Source: https://help.imdb.com/article/imdb/general-information/can-i-use-imdb-data-in-my-software/G5JTRESSHJBBHTGX. This educational project is non-commercial, will use only the sanctioned dataset files, will not scrape IMDb pages, and will include the required attribution. If manual match validation becomes necessary, I will inspect the relevant pages in a browser rather than scrape them.

### Certification against every course guardrail

- **Permitted source only:** Wikipedia's ordinary article is not disallowed by its robots.txt and is CC BY-SA 4.0 licensed; IMDb data will come only from its official non-commercial downloads.
- **No login or paywall:** Both planned sources are public and require no account, login, subscription, or paywall access.
- **No personal or identifiable information:** The analysis uses film titles, award status, aggregate audience ratings, and aggregate vote counts. It collects no viewer identities or individual-level records. Producer names present in the Wikipedia table are unnecessary and will be dropped immediately.
- **Rate-limit, identify, and cache:** The Wikipedia page will be requested once with an honest course-project User-Agent containing my contact email, followed by a pause if another request is ever necessary. The HTML response and IMDb downloads will be cached locally and reused. I will not repeatedly request either source.
- **Attribution:** The final work will link and credit Wikipedia under CC BY-SA 4.0 and include IMDb's exact required attribution statement.

### 4. Tier declaration

Declare a tier, with one sentence on why it fits the student and these sources.

| Tier | What it takes |
|---|---|
| **1 — Solid** | Two sources; one via `read_html` or a documented API. A one-to-one or one-to-many join. |
| **2 — Ambitious** | Two or more sources; one requiring a multi-page scrape with pagination, session handling, and rate limiting. |
| **3 — Stretch** | Tier 2, plus either structured extraction from unstructured text or PDF with a validated schema, or a third source requiring a many-to-many resolution. |

Tiers may be raised any time up to P3 and may not be lowered after P3. Tier affects
exactly one rubric row in the entire course: P4 Criterion 5, Technical Ambition. 

**Tier 1 — Solid.** This fits my current experience with Python and pandas because it combines one permitted `read_html` web source with one official downloadable dataset through a validated one-to-one title match; it is technically meaningful without requiring pagination, sessions, or unstructured extraction.

---

## How this is graded

| Criterion | Wt | The short version |
|---|---|---|
| Question & motivation | ×1 | A real question, answerable with the stated data, that matters to someone |
| Sources & access evidence | ×2 | Named precisely, one off the web, reachability shown not asserted |
| Applicable constraints & guardrails | ×2 | The constraint that applies to each source, quoted; every guardrail certified |
| Tier declaration & fit | ×1 | A tier that matches the project described |

Full descriptors in *DSA 405 Project Rubrics*.

**Submit a self-scored copy of the rubric.** It is ungraded and catches omissions before grading does.

## Self-scored P1 rubric

Scored on the apparent 0–3 course scale; I would revise these numbers if the rubric copy supplied in Moodle uses different labels.

| Criterion | Weight | Self-score | Evidence |
|---|---:|---:|---|
| Question & motivation | ×1 | 3/3 | One answerable comparative question, a defined population and time span, named variables, stakeholders, and a clear interpretation limit |
| Sources & access evidence | ×2 | 3/3 | Two precisely named sources; Wikipedia is collected from the web with `read_html`; executed outputs show HTTP 200, 91 selected rows, and both IMDb row counts |
| Applicable constraints & guardrails | ×2 | 3/3 | Source-specific robots/license terms are quoted, required IMDb attribution is included, and every named guardrail is certified |
| Tier declaration & fit | ×1 | 3/3 | Tier 1 matches a two-source, one-to-one join and my current Python/pandas skills |
| **Weighted total** | **×6** | **18/18** | Ready for instructor review; the remaining risk is documented title matching |

---

## Common failure modes

**A topic instead of a question.** A Section 1 with no verb is a topic. Identify the
table or chart that would settle the question; if none can be described, keep
sharpening.

**Access asserted, not evidenced.** "The data is available on the county website" scores
2. A pasted row count scores 3. The difference is twenty minutes of work now versus a
dead project in October.

**The generic constraints paragraph.** "I will follow all applicable terms of service"
cites nothing and scores 2. Quote the line from the source's own robots.txt or license
that permits the planned collection.

---

## P1 Checklist

- [ ] One sentence stating the question, answerable with the named data
- [ ] Two or more sources, each with publisher, URL, coverage, and size
- [ ] At least one source comes off the web (scrape or API)
- [ ] Evidence each source is reachable, pasted in
- [ ] The constraint that applies to each source, quoted
- [ ] Every course guardrail addressed by name
- [ ] Tier declared, with one sentence on why
- [ ] Self-scored rubric attached
