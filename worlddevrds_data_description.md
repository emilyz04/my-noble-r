# worlddevrds Data Description

This document describes the RDS data file named `worlddevrds`, which was inspected in R using `/usr/bin/R` and loaded with `readRDS("worlddevrds")`.

## Overview

The object is an R `data.frame` containing World Bank-style development indicator data arranged in a wide table.

- Class: `data.frame`
- Rows: 396,970
- Columns: 70
- Unique country/region codes: 265
- Unique indicators: 1,498
- Year coverage: 1960 to 2025

This means the dataset is effectively a matrix of country-by-indicator records, with one row for each country-indicator combination and one column for each year.

## Structural layout

The file has 70 columns:

1. `Country Name` — character string with the country or region name
2. `Country Code` — character string with the ISO-style code used by the World Bank
3. `Indicator Name` — character string describing the metric
4. `Indicator Code` — character code identifying the metric
5-70. `1960` through `2025` — numeric annual values for each indicator

The row count is exactly:

- 265 countries × 1,498 indicators = 396,970 rows

This confirms that each row represents a specific combination of:

- a country or region
- an indicator

and the columns for years 1960-2025 hold the observed values for that country and indicator over time.

## Example row

A representative row looks like this:

| Column | Example value |
|---|---|
| Country Name | Africa Eastern and Southern |
| Country Code | AFE |
| Indicator Name | Access to clean fuels and technologies for cooking (% of population) |
| Indicator Code | EG.CFT.ACCS.ZS |
| 2000 | 11.49 |
| 2001 | 11.8 |
| 2002 | 12.2 |
| 2003 | 12.57 |
| ... | ... |

This structure is a wide panel table, not a tidy long table. In other words, each indicator is stored as a row, and each year is a separate column.

## Data types

The columns fall into two main types:

- Character columns:
  - `Country Name`
  - `Country Code`
  - `Indicator Name`
  - `Indicator Code`
- Numeric columns:
  - all year columns from `1960` to `2025`

The numeric columns are mostly missing for earlier years, which is expected in development datasets where many indicators were not available historically.

## Missingness and coverage

The early years contain substantial missing data, for example:

- 1960: 359,744 missing values
- 1961: 354,410 missing values
- 1962: 353,123 missing values

Coverage improves substantially after 2000, when many of the indicators begin to have actual reported values.

## Interpretation

This dataset is suitable for:

- comparing indicators across countries and regions
- studying long-term trends for a given indicator
- creating plots of development outcomes over time
- merging with other country-level or regional metadata

A typical R inspection command is:

```r
x <- readRDS("worlddevrds")
str(x)
summary(x)
```

The object is ready for analysis as a standard `data.frame` in R.

## Summary

In short, `worlddevrds` is a wide, country-by-indicator World Bank development dataset with:

- 396,970 rows
- 70 columns
- 265 countries/regions
- 1,498 indicators
- annual values from 1960 through 2025

The first four columns provide metadata, and the remaining columns are numeric year-by-year measurements for each country-indicator pair.
