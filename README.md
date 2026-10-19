# 23L-0748 - Cleaned datasets for CS4048 Data Science, Assignment 2

These are the cleaned datasets produced in Assignment 2 (EDA). Assignment 3 loads them from the `v1.0` tag of this repository. Any later change to the cleaning will be published as a new version; v1.0 will not be overwritten.

| File | Rows × cols | Original source |
|---|---|---|
| `23L_0748_A2_netflix_cleaned.csv` | 8,803 × 28 | Netflix Movies and TV Shows, Shivam Bansal, Kaggle: https://www.kaggle.com/datasets/shivamb/netflix-shows (8,807 × 12) |
| `23L_0748_A2_supermarket_cleaned.csv` | 1,000 × 24 | `supermarket_Sales.csv` provided by the course instructor (1,000 × 17) |

The original data belongs to its authors. Credit the sources above and respect their licences.

## Netflix: changes made
- Stripped leading/trailing whitespace in all text columns (88 `date_added` values, 1 title).
- Removed 4 logical duplicates (same title ignoring case, same type, release year and director), keeping the most recent `date_added`.
- Moved 3 durations that had been stored in `rating` (Louis C.K. specials) into `duration`, and set their rating to `Unknown`.
- Merged `UR` into `NR`, filled the 4 missing ratings with `Unknown`, and added `rating_group` (Kids / Older Kids / Teens / Adults / Not Rated / Unknown).
- Filled missing `director`, `cast` and `country` with `Unknown`, and added `director_missing`, `cast_missing` and `country_missing` flags.
- Left `date_added` missing for 10 TV shows.
- Removed empty tokens caused by stray commas in `country` (7 rows).
- Converted `date_added` to ISO date (`YYYY-MM-DD`).
- Added derived columns: `movie_minutes`, `seasons`, `year_added`, `month_added`, `added_gap_years`, `added_before_release`, `n_countries`, `n_genres`, `n_cast`, `primary_country`, `primary_genre`, `is_international`.
- Outliers (very short or long movies, long-running series, old releases) were retained.

## Supermarket Sales: changes made
- No missing values, duplicates or inconsistent labels were found, so no rows were removed or imputed.
- Converted `Date` to ISO format (`YYYY-MM-DD`) and kept `Time` as `HH:MM`.
- Added derived columns: `Datetime`, `Month`, `Weekday`, `Is weekend`, `Hour`, `Day part`, and the flag `Total outlier (IQR)` for 9 high-value invoices, which were retained.
- All original columns were kept, with these documented redundancies:
  - City duplicates Branch.
  - Tax 5%, Cost of goods sold, Gross income and Total are exact functions of Unit price × Quantity.
  - Gross margin percentage is constant.
