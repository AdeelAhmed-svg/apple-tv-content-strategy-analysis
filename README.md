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
