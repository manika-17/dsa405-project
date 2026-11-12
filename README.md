
# Best Picture Winners vs. IMDb Ratings (2015–2024)

**DSA 405: Project Synthesis | Fall 2026**  
**Author:** Manika Jain

## Project Overview

This project investigates whether Academy Award Best Picture winners from 2015 to 2024 receive higher IMDb audience ratings than films nominated for Best Picture that did not win.

The goal is to explore the relationship between critical recognition through the Academy Awards and audience reception as measured by IMDb ratings. By combining Academy Award nomination data from Wikipedia with IMDb movie ratings, this project compares winners and nonwinners to determine whether winning Best Picture is associated with higher audience ratings.

## Research Question

**Do Academy Award Best Picture winners from 2015–2024 have higher IMDb ratings than nominated films that did not win?**

## Key Findings

The analysis found that **Best Picture winners had slightly higher IMDb ratings on average than nonwinning nominees**.

- **Total Best Picture nominees:** 91
- **Successfully matched IMDb records:** 86
- **Unmatched nominees:** 5
- **Average IMDb rating for winners:** 7.778
- **Average IMDb rating for nonwinners:** 7.556
- **Difference in average ratings:** +0.222 points
- **Years in which winners rated higher than nonwinners:** 6 out of 9 comparable years

These results suggest that Best Picture winners tend to receive slightly higher audience ratings than other nominated films. However, the difference is relatively small, and winners did not outperform nonwinners in every year.

**Conclusion:** The results support the original research question at the overall average level. Best Picture winners had higher IMDb ratings than nonwinning nominees among the films successfully matched to IMDb. However, this relationship is descriptive and does not establish that winning an Academy Award causes higher audience ratings.

## Data Sources

### 1. Wikipedia: Academy Award for Best Picture

**Source:** [Academy Award for Best Picture — Wikipedia](https://en.wikipedia.org/wiki/Academy_Award_for_Best_Picture)

Wikipedia provides historical information about Academy Award Best Picture nominees and winners.

The dataset includes:
- Film titles
- Award years
- Best Picture nomination status
- Best Picture winner status

**Data producer:** Wikipedia contributors  
**Access method:** Publicly available Wikipedia tables  
**License:** Generally Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0), subject to Wikimedia terms.

### 2. IMDb Non-Commercial Datasets

**Source:** [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/)

IMDb provides movie metadata and audience ratings.

The project uses two IMDb datasets:

- `title.basics.tsv.gz`: Contains movie titles, release years, title identifiers, and title types.
- `title.ratings.tsv.gz`: Contains IMDb average ratings and numbers of votes.

**Data producer:** IMDb  
**Access method:** Downloadable TSV files  
**Usage terms:** IMDb non-commercial dataset restrictions apply.

IMDb source datasets are not redistributed through this repository.

## Data Cleaning and Preparation

The project combines Wikipedia Academy Award data with IMDb movie information.

The main cleaning steps include:

1. Extracting Best Picture nominees and winners for 2015–2024 from Wikipedia.
2. Loading IMDb title and rating datasets.
3. Filtering IMDb records to relevant movie titles.
4. Standardizing movie titles to improve matching accuracy.
5. Converting titles to lowercase and normalizing Unicode characters.
6. Removing punctuation and unnecessary whitespace.
7. Removing duplicate or ambiguous matching records.
8. Merging Wikipedia and IMDb data using cleaned movie titles and film years.
9. Identifying unmatched nominees.
10. Verifying the accuracy of the final dataset.

### Data Integration

The datasets were merged using the following variables:

- `film_year`
- `title_clean`

A left merge was used to preserve all Academy Award nominees, including those that could not be matched to IMDb.

The project also includes verification checks for duplicate keys, winner identities, row counts, and rating values.

## Missing Data and Limitations

Of the 91 Best Picture nominees, **86 were successfully matched to IMDb**, leaving five unmatched films.

The unmatched films were:

- *Spotlight* (2015)
- *The Father* (2020)
- *Judas and the Black Messiah* (2020)
- *Sound of Metal* (2020)
- *Maestro* (2023)

These unmatched records limit the completeness of the analysis and may affect the comparison between winners and nonwinners.

Additional limitations include:

- IMDb ratings represent users who choose to submit ratings, rather than all movie viewers.
- Audience ratings can change over time.
- The analysis only includes Best Picture nominees, not all movies released during the study period.
- The analysis does not establish a causal relationship between winning Best Picture and receiving higher IMDb ratings.


## Repository Structure

The repository is organized as follows:

```text
DSA405-Project/
|
|-- assignments/
|   |-- labs/
|       |-- DSA405_Lab04_CleaningII_FA26...
|       |-- DSA405_SkillsSelfCheck_FA26.ipynb
|
|-- data/
|   |-- raw/
|       |-- Academy Award for Best Picture...
|       |-- SOURCES.md
|
|-- .gitignore
|-- DSA405_002_FA26_P1_mjain236...
|-- DSA405_002_FA26_P3_mjain23...
|-- DSA405_P2_AuditCleaningLog_FA26...
|-- DSA405_P4_FA26_mjain23.ipynb
|-- README.md
```

### File Descriptions

- **README.md:** Provides the project overview, research question, data sources, findings, and instructions for reproducing the analysis.
- **DSA405_P4_FA26_mjain23.ipynb:** The final project notebook containing data collection, cleaning, integration, verification, and analysis.
- **DSA405_002_FA26_P1_mjain236...:** Initial project milestone documenting the original research question and project planning.
- **DSA405_P2_AuditCleaningLog_FA26...:** Milestone 2 notebook containing data auditing, cleaning, and documentation.
- **DSA405_002_FA26_P3_mjain23...:** Milestone 3 notebook containing data integration and verification.
- **data/raw/:** Contains the original Academy Award data and source documentation.
- **data/raw/SOURCES.md:** Documents the original data sources and provenance.
- **assignments/labs/:** Contains course lab notebooks and skills exercises.
- **.gitignore:** Specifies files and folders excluded from Git tracking.
```

## How to Run the Project

### Step 1: Clone the Repository

Clone the GitHub repository to your computer.

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd DSA405-BestPicture-IMDb
```

Replace `YOUR_GITHUB_REPOSITORY_URL` with the actual URL of this repository.

### Step 2: Install Dependencies

Make sure Python 3.10 or later is installed.

Install the required Python packages:

```bash
python -m pip install -r requirements.txt
```

### Step 3: Open the Jupyter Notebook

Open the following notebook:

`DSA405_P4_FA26_mjain23.ipynb`

Before downloading Wikipedia data, ensure that the `CONTACT` variable contains a valid contact email address or Wikimedia user page.

### Step 4: Run the Notebook

Restart the Jupyter kernel and run all cells from beginning to end.

The notebook performs the following tasks:

1. Downloads or loads the raw datasets.
2. Cleans and standardizes movie information.
3. Merges Academy Award and IMDb records.
4. Verifies the resulting dataset.
5. Calculates average IMDb ratings.
6. Compares winners and nonwinners.
7. Generates visualizations and analysis outputs.

### Step 5: Review the Results

After execution, review the notebook outputs, generated figures, and processed data files.

The notebook includes checks designed to identify potential data integration problems.

**Note:** IMDb datasets are large and may require significant memory and processing time. Downloaded data may also change over time, which could lead to slightly different results in future executions.

## Reproducibility

The project is designed so that another user can reproduce the analysis using the Jupyter notebook and the publicly accessible data sources, subject to IMDb's usage restrictions.

The notebook includes the data preparation, merging, verification, and analysis steps necessary to trace the findings back to the source data.

A successful execution from a restarted kernel should be confirmed before the final submission.

## AI Use and Reflection

AI tools were used to assist with coding, debugging, documentation, and organizing the project findings.

AI-generated suggestions were reviewed against the actual notebook, and project conclusions were based on the analysis results rather than unsupported AI-generated claims.

The written report contains a more detailed AI-use reflection, including challenges encountered and how they were addressed.

## Final Conclusion

**Best Picture winners from 2015–2024 received slightly higher IMDb ratings on average than nonwinning nominees in the successfully matched dataset.**

Winners averaged **7.778**, compared with **7.556** for nonwinners, representing a difference of **0.222 rating points**.

Although this finding supports the original research question, the relatively small difference and variation across years suggest that Academy Award recognition and IMDb audience ratings do not always align.

This project demonstrates how data from multiple sources can be cleaned, integrated, verified, and analyzed to answer a real-world research question.
