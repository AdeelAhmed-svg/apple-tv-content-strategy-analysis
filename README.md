# 🎬 Apple TV+ Content Strategy Analysis
**$1B+ investment decisions informed by ROI, genre trends, Pakistan market**

## Business Problem
Apple TV+ needs data-driven content investment priorities. Analyzed 5K+ titles + internal financials.


## Key Findings
| Genre           | ROI (views/$) | Pakistan Share | Recommendation |
| --------------- | ------------- | -------------- | -------------- |
| Sci-Fi/Thriller | 1.2M/$M       | 28% ↑          | ✅ GREENLIGHT   |
| Drama           | 1.0M/$M       | 35%            | ✅ PRIORITIZE   |
| Horror          | 0.3M/$M       | 8%             | ❌ DEPRIORITIZE |


## Methodology
1. Merged catalog metadata + internal viewership/cost data [imdbId key]
2. ROI = totalviewership ÷ totalcost
3. Time-series genre shift analysis (2010s vs 2020s)
4. Pakistan market filtering (availableCountries LIKE '%PK%')

