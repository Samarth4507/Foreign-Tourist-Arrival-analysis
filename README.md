# Foreign-Tourist-Arrival-analysis
## Overview
This repository contains multiple datasets related to India's tourism statistics from 2001 to 2021. These datasets provide insights into various aspects of tourism, including age groups of tourists, foreign tourist arrivals, quarterly trends, global vs. Indian tourism statistics, regional and reason-based tourism data, and visits to monuments.

## Dataset Descriptions

### 1. **India-Tourism-Statistics-2001-2019-agegroup**
   - **Description:** Data on the age distribution of tourists visiting India between 2001 and 2019.
   - **Possible Use Cases:** Demographic analysis of tourists, age-wise trends in tourism.

### 2. **India-Tourism-Statistics-2001-2020-fta_nri_ita**
   - **Description:** Data on Foreign Tourist Arrivals (FTA), Non-Resident Indians (NRI), and Indian Tourist Arrivals (ITA) from 2001 to 2020.
   - **Possible Use Cases:** Comparison of international and domestic tourism trends, impact analysis of policies affecting tourist arrivals.

### 3. **India-Tourism-Statistics-2001-2019-quarterly**
   - **Description:** Quarterly tourism statistics covering the period 2001-2019.
   - **Possible Use Cases:** Seasonal trends in tourism, identifying peak and off-peak seasons.

### 4. **India-Tourism-Statistics-2001-2019-worldvsindia**
   - **Description:** Comparison of India's tourism statistics with global tourism trends from 2001-2019.
   - **Possible Use Cases:** Benchmarking India's tourism industry against global standards.

### 5. **India-Tourism-Statistics-2019_region-and-reason**
   - **Description:** Regional tourism data and reasons for travel in India for the year 2019.
   - **Possible Use Cases:** Understanding the purpose of visits (business, leisure, medical, etc.), identifying key tourism regions.

### 6. **India-Tourism-Statistics-2021-monuments**
   - **Description:** Data on tourist visits to Indian monuments in 2021.
   - **Possible Use Cases:** Analyzing the impact of COVID-19 on tourism, evaluating monument-wise tourist traffic.

## How to Use the Data
- The datasets can be used for trend analysis, forecasting, and visualization.
- They can be integrated into Power BI, Excel, or Python for further analysis.
- Suitable for academic research, government policy-making, and business insights in the tourism industry.

## Suggested Next Steps
- **Data Cleaning:** Check for missing values and inconsistencies.
- **Integration:** Combine datasets for comprehensive analysis.
- **Visualization:** Use Power BI or other visualization tools to create interactive reports.

## Calculations and Metrics

### State Wise Previous Year Metrics
```DAX
Previous Year %Change = 
VAR SelectedYear = MAX('India-Tourism-Statistics-2001-2019-worldvsindia'[Year])
RETURN 
CALCULATE(
    SUM('India-Tourism-Statistics-2001-2019-worldvsindia'[India - % Change]),
    FILTER(
        ALL('India-Tourism-Statistics-2001-2019-worldvsindia'),
        'India-Tourism-Statistics-2001-2019-worldvsindia'[Year] = SelectedYear - 1
    )
)

Previous Year Rank = 
VAR SelectedYear = MAX('India-Tourism-Statistics-2001-2019-worldvsindia'[Year])
RETURN 
CALCULATE(
    SUM('India-Tourism-Statistics-2001-2019-worldvsindia'[Rank]),
    FILTER(
        ALL('India-Tourism-Statistics-2001-2019-worldvsindia'),
        'India-Tourism-Statistics-2001-2019-worldvsindia'[Year] = SelectedYear - 1
    )
)

Previous Year Share = 
VAR SelectedYear = MAX('India-Tourism-Statistics-2001-2019-worldvsindia'[Year])
RETURN 
CALCULATE(
    SUM('India-Tourism-Statistics-2001-2019-worldvsindia'[Percentage Share of India]),
    FILTER(
        ALL('India-Tourism-Statistics-2001-2019-worldvsindia'),
        'India-Tourism-Statistics-2001-2019-worldvsindia'[Year] = SelectedYear - 1
    )
)
```

### Highest Business Country Calculation
```DAX
HighestBusinessCountry = 
VAR BusinessTable =
    ADDCOLUMNS(
        SUMMARIZE(
            'India-Tourism-Statistics-2019_region-and-reason', 
            'India-Tourism-Statistics-2019_region-and-reason'[Country of Nationality]
        ),
        "TotalBusiness",
        CALCULATE(
            SUMX(
                'India-Tourism-Statistics-2019_region-and-reason',
                'India-Tourism-Statistics-2019_region-and-reason'[Arrivals (in numbers)] * 
                'India-Tourism-Statistics-2019_region-and-reason'[Business and Professional(%)] / 100
            )
        )
    )

VAR TopCountry = 
    TOPN(
        1, 
        BusinessTable, 
        [TotalBusiness], 
        DESC
    )

RETURN 
    SELECTCOLUMNS(TopCountry, "Country", [Country of Nationality])
```

## Contact
For any questions or support regarding these datasets, please reach out via email samarthshetty071@gmail.com

