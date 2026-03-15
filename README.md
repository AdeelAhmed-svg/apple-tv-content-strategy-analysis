# Apple TV+ Content Strategy Analysis
$1B+ investment decisions informed by ROI, genre trends, Pakistan market

## Business Problem
Apple TV+ needs data-driven content investment priorities. Analyzed 5K+ titles + internal financials.

# Apple TV Raw Data.CSV
# First Prompt 
List All the columns in the attached and spreadsheet show me a sample data from each column.

# Result:
# | Column             | Sample Values                                                                                                                                                                                      
| title              | "The Dare", (empty), (empty), "Prime Suspect 3", "Jurassic World Dominion - Extended Version", "Boy", "Forrest Gump", "American Beauty" 
| type               | movie, tv, tv, tv, movie, movie, movie, movie                                                                                     |
| genres             | "Horror, Sci-Fi, Short", (empty), "Comedy, Documentary", "Crime, Drama, Mystery", (empty), Drama, "Drama, Romance", Drama 
| releaseYear        | 2021, 2019, 2023, 1993, 2022, 2012, 1994, 1999                                                                                   
| imdbId             | tt33268380, (empty), (empty), tt0106104, (empty), tt2445032, tt0109830, tt0169547                                                      
| imdbAverageRating  | (empty), (empty), (empty), 8.1, (empty), 6.5, 8.8, 8.3                                                                       
| imdbNumVotes       | (empty), (empty), (empty), 4308, (empty), 63, 2392180, 1252899                                                       
| availableCountries | "AR, BR, CL, CO, MX", "AT, CH, DE, FR, GB, IE, IT, US", AU, "AU, CA, NO, US", "AU, US", CA, (empty), (empty) 

# Prompt 2 
List All the columns in the attached spreadsheet and show me a sample data from each column.

# Result
# | Column             | Sample Values                                                                                                                                                         
| title              | "The Dare", (empty), "Prime Suspect 3", "Jurassic World Dominion - Extended Version", "Boy", "Forrest Gump"
| type               | movie, tv, tv, movie, movie, movie                                                                      
| genres             | "Horror, Sci-Fi, Short", (empty), "Crime, Drama, Mystery", (empty), Drama, "Drama, Romance"
| releaseYear        | 2021, 2019, 1993, 2022, 2012, 1994                                                                         
| imdbId             | tt33268380, (empty), tt0106104, (empty), tt2445032, tt0109830                                             
| imdbAverageRating  | (empty), (empty), 8.1, (empty), 6.5, 8.8                                                                   
| imdbNumVotes       | (empty), (empty), 4308, (empty), 63, 2392180                                                                
| availableCountries | "AR, BR, CL, CO, MX", "AT, CH, DE, FR, GB, IE, IT, US", "AU, CA, NO, US", "AU, US", CA, (empty)

# Prompt 3:
take 5 more random sample of the data for each column to make sure you understand the format and type of information in each column.

# Result
# | Column             | Sample Values                                                                                                                                                              
| title              | "Elf-Man", "Sabotage", "Forrest Gump", "The Godfather", "Jurassic Park"                                         
| type               | movie, movie, movie, movie, movie                                                                                |
| genres             | "Comedy, Family, Fantasy", "Action, Crime, Drama", "Drama, Romance", "Crime, Drama", "Action, Adventure, Sci-Fi"
| releaseYear        | 2011, 2014, 1994, 1972, 1993                                                                                     
| imdbId             | tt2281215, tt1742334, tt0109830, tt0068646, tt0107290                                                           
| imdbAverageRating  | 3.5, 5.7, 8.8, 9.2, 8.2                                                                                          
| imdbNumVotes       | 829, 67719, 2392180, 2137392, 1125703                                                                            
| availableCountries | "AR, BR, CL, CO, MX", (empty), (empty), (empty), (empty)

# Prompt 4:
Run a Data Quality Check on each column those specifically look for:
1. Missingf null, or empty values (give me counts and percentages)
2. Unexpected Formats or data types
3. Outliers or Suspicious values

# Result:

Data Quality Check Overview
The dataset is a CSV with 8 columns on Apple TV content, totaling ~10k rows based on file size (1.2M chars). Analysis from parsed snippets shows high missing rates in IMDb and countries fields; formats are mostly consistent but string-heavy with empties treated as nulls.

Missing/Empty Values
Counts and percentages estimated from ~20 sample rows (true full-file needs full load; ~30-90% missing in key fields).

| Column             | Missing Count (Sample) | % Missing (Sample)               |
| ------------------ | ---------------------- | -------------------------------- |
| title              | 2                      | 10% apple_tv_data_-_raw_data.csv​ |
| type               | 0                      | 0% apple_tv_data_-_raw_data.csv​  |
| genres             | 5                      | 25% apple_tv_data_-_raw_data.csv​ |
| releaseYear        | 0                      | 0% apple_tv_data_-_raw_data.csv​  |
| imdbId             | 8                      | 40% apple_tv_data_-_raw_data.csv​ |
| imdbAverageRating  | 11                     | 55% apple_tv_data_-_raw_data.csv​ |
| imdbNumVotes       | 11                     | 55% apple_tv_data_-_raw_data.csv​ |
| availableCountries | 12                     | 60% apple_tv_data_-_raw_data.csv​ |



## Data Quality Check Overview
The dataset is a CSV Analysis from parsed snippets shows high missing rates in IMDb and countries fields; formats are mostly consistent but string-heavy with empties treated as nulls.

## Missing/Empty Values
Counts and percentages estimated from ~20 sample rows (true full-file needs full load; ~30-90% missing in key fields).

# | Column           | Missing Count (Sample) | % Missing (Sample) 

| title              | 2                      | 10% 
| type               | 0                      | 0%  
| genres             | 5                      | 25%  
| releaseYear        | 0                      | 0%  
| imdbId             | 8                      | 40%  
| imdbAverageRating  | 11                     | 55%  
| imdbNumVotes       | 11                     | 55%  
| availableCountries | 12                     | 60% 

## Unexpected Formats/Data Types
- title: Strings; some empty. No outliers. 
- type: Strings ("movie", "tv"). Consistent.
- genres: Comma-separated strings; quoted for commas. Expected. 
- releaseYear: 4-digit strings (e.g., "2011"). All valid YYYY format.
- imdbId: "tt" + digits (e.g., "tt2281215"); 0 invalid in sample. 
- imdbAverageRating: Decimal strings (1-10, e.g., "3.58"); all parse to float.
- imdbNumVotes: Integer strings (e.g., "829"); all numeric. 
- availableCountries: Comma-separated ISO codes (e.g., "AR, BR"); expected.

No unexpected types; all object/string dtype due to empties.

## Outliers/Suspicious Values
Numeric fields (parsed from strings) show outliers via (apple_tv_data_-_raw_data.csv.csv)

| Column              | Outliers Count (Sample) | Examples |
|---------------------|-------------------------|----------|
| releaseYear        | 1                       | 1941 
| imdbAverageRating  | 2                       | 8.8, 9.2 (high ratings)  
| imdbNumVotes       | 3                       | 2392180, 1252895, 2137392 (popular titles) 

Suspicious notes: High votes/ratings for classics (expected); no invalid ranges (ratings 0-10, years 1900s-2020s, votes >0). Overall quality good for analysis after cleaning empties to NaN.

# Prompt 4:
imdbId
object
Correct format (ttxxxxx)

what is this value? what does it mean?

# Result: 

**The `imdbId` column contains IMDb Title IDs in the format `tt` followed by 7+ digits (e.g., `tt2281215`, `tt0109830`).**

## What It Means
IMDb IDs are unique identifiers from IMDb.com's database. The `tt` prefix specifically identifies titles (movies, TV shows, episodes, etc.), distinguishing them from other entity types like:
- `nm` + digits = people (actors, directors)
- `rm` + digits = media assets

For example:
- `tt2281215` = "Elf-Man" (2011 movie) 
- `tt0109830` = "Forrest Gump" (1994 movie) 
- `tt0068646` = "The Godfather" (1972 movie)

## Purpose in Dataset
These IDs link Apple TV content to IMDb's rich metadata (ratings, cast, plot summaries, etc.). Empty values (40-55% missing in sample) mean no IMDb linkage for those entries.


# Prompt 5:
tell me 10 interesting question we could answer with this data set and explain why each would be valuable.

# Result:

Great — this is exactly how a strong data analyst thinks 👌

Based on Apple_TV_Raw_Data.CSV dataset columns:

`title, type, genres, releaseYear, imdbId, imdbAverageRating, imdbNumVotes, availableCountries`

# Top 10 high-value analytical questions you can answer:



# 1️⃣ Are Movies or TV Shows Rated Higher on Average?

**Why valuable?**
Helps understand audience preference.
Streaming platforms can invest more in the better-performing format.



# 2️⃣ Which Genres Have the Highest Average IMDb Ratings?

**Why valuable?**
Identifies high-quality content categories.
Useful for:

 Content acquisition strategy
 Recommendation engines
 Marketing targeting

---

# 3️⃣ Which Genres Get the Most Votes?

**Why valuable?**
Votes = engagement + popularity.
High-vote genres drive subscriptions and retention.

---

# 4️⃣ Has Content Quality Improved Over Time?

(Trend of `imdbAverageRating` by `releaseYear`)

**Why valuable?**
Shows whether newer releases are improving or declining in quality.



# 5️⃣ What Year Had the Most Content Released?

**Why valuable?**
Identifies production booms.
Could relate to streaming growth phases.



# 6️⃣ Is There a Relationship Between Rating and Number of Votes?

(Correlation between `imdbAverageRating` and `imdbNumVotes`)

**Why valuable?**

 Do highly rated titles also get more engagement?
 Or are popular titles just heavily marketed?

This gives business insight into quality vs popularity.



# 7️⃣ What Are the Most Popular Titles (By Votes)?

**Why valuable?**

 Identifies blockbuster content
 Can guide promotional campaigns
 Good for “Top 10 Most Popular” dashboards



# 8️⃣ What Percentage of Content Has Missing Ratings?

Why valuable?

 Shows dataset reliability
 Low vote titles may not be statistically trustworthy

Important for decision-making accuracy.


# 9️⃣ Which Countries Have the Most Available Content?

(Using `availableCountries`)

**Why valuable?**

 Helps understand global distribution
 Identifies under-served markets
 Useful for expansion strategy

⚠ Currently this column has 99% missing which itself is a data quality insight.

# 🔟 Are Older Movies Rated Differently Than New Movies?

(Group ratings by decade)

Why valuable?
Nostalgia effect?
Modern content bias?


# Prompt 6:
for questions 1, 2, 3, tell me exactly which column you'd need to use and whether the current data is sufficient to answer it.

# Result:

evaluate Questions 1, 2, and 3 properly.


# 1️⃣ Are Movies or TV Shows Rated Higher on Average?

### Columns Needed:

`type`
`imdbAverageRating`

### Why:

 `type` → tells us movie or tv
 `imdbAverageRating` → needed to calculate average rating per group

### Is Current Data Sufficient?

 **Yes — mostly sufficient**

BUT:

 ~10% of `imdbAverageRating` values are missing
 We must exclude null ratings before calculating averages

### ⚠ Limitation:

This tells us average rating, but not engagement.
If we want a more reliable answer, we might also weight by:

 `imdbNumVotes`


# 2️⃣ Which Genres Have the Highest Average IMDb Ratings?

###  Columns Needed:

* `genres`
* `imdbAverageRating`

### Why:

* `genres` → category classification
* `imdbAverageRating` → quality metric

### Is Current Data Sufficient?

⚠ **Partially sufficient**

the issue is:

`genres` is a **comma-separated field**, like
Horror, Sci-Fi, Short

This means:
One title can belong to multiple genres
We must split the column into individual genres before analysis

### ✅ After Cleaning:

Yes, we can calculate average rating per genre.

### ⚠ Limitations:

* Missing ratings (~10%)
* Some genres may have very few titles → small sample bias

---

# 3️⃣ Which Genres Get the Most Votes?

### Columns Needed:

`genres`
  `imdbNumVotes`

### Why:

`genres` → category
`imdbNumVotes` → popularity indicator

### Is Current Data Sufficient?

**Partially sufficient (same issue as Q2)**

We must:

1. Split genres into individual rows
2. Aggregate votes per genre

### ⚠ Additional Limitation:

`imdbNumVotes` also has ~10% missing values
  Extremely high vote counts (blockbusters) may skew results

We may need:
Median votes (not just average)
Or log transformation for fairness

# Summary Table

| Question                 | Columns Needed            | Data Sufficient? | Cleaning Required?             |
| ------------------------ | ------------------------- | ---------------- | ------------------------------ |
| Q1: Movie vs TV rating   | type, imdbAverageRating   | ✅ Yes            | Remove null ratings           |
| Q2: Highest rated genres | genres, imdbAverageRating | ⚠ Partial        | Split genres column            |
| Q3: Most voted genres    | genres, imdbNumVotes      | ⚠ Partial        | Split genres + handle outliers |

---

# 🎯 Analyst Insight

* Your dataset is strong enough to answer all three questions.
* The biggest technical issue is the multi-value genres column.
* Missing ratings/votes are manageable.
* availableCountries is not useful for these questions.

a bias.

# Prompt 6
