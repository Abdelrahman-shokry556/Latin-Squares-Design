# Latin-Squares-Design
# Latin Square Experimental Design Data

## Overview
This repository contains data from a 6×6 Latin Square experimental design with 6 treatments (A, B, C, D, E, F).

## Data Structure

### Raw Data Table
The following table shows the experimental layout where each cell contains the treatment letter and its corresponding measured value in parentheses:

| Row | Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 |
|-----|-------|-------|-------|-------|-------|-------|
| 1   | A(12.5) | B(14.2) | C(13.8) | D(15.1) | E(13.9) | F(12.3) |
| 2   | B(13.7) | C(15.1) | D(14.6) | E(13.2) | F(12.8) | A(11.9) |
| 3   | C(14.9) | D(13.8) | E(12.7) | F(13.4) | A(12.1) | B(14.5) |
| 4   | D(15.3) | E(14.1) | F(13.2) | A(12.8) | B(13.6) | C(14.7) |
| 5   | E(13.4) | F(12.9) | A(11.8) | B(13.9) | C(15.2) | D(14.8) |
| 6   | F(12.6) | A(12.3) | B(14.3) | C(15.4) | D(14.5) | E(13.1) |

### Treatment Values Summary

| Treatment | Values | Mean | Count |
|-----------|--------|------|-------|
| A | 12.5, 11.9, 12.1, 12.8, 11.8, 12.3 | 12.23 | 6 |
| B | 14.2, 13.7, 14.5, 13.6, 13.9, 14.3 | 14.03 | 6 |
| C | 13.8, 15.1, 14.9, 14.7, 15.2, 15.4 | 14.85 | 6 |
| D | 15.1, 14.6, 13.8, 15.3, 14.8, 14.5 | 14.68 | 6 |
| E | 13.9, 13.2, 12.7, 14.1, 13.4, 13.1 | 13.40 | 6 |
| F | 12.3, 12.8, 13.4, 13.2, 12.9, 12.6 | 12.87 | 6 |

## Data Files

### CSV Format
```csv
Row,Col,Treatment,Value
1,1,A,12.5
1,2,B,14.2
1,3,C,13.8
1,4,D,15.1
1,5,E,13.9
1,6,F,12.3
2,1,B,13.7
2,2,C,15.1
2,3,D,14.6
2,4,E,13.2
2,5,F,12.8
2,6,A,11.9
3,1,C,14.9
3,2,D,13.8
3,3,E,12.7
3,4,F,13.4
3,5,A,12.1
3,6,B,14.5
4,1,D,15.3
4,2,E,14.1
4,3,F,13.2
4,4,A,12.8
4,5,B,13.6
4,6,C,14.7
5,1,E,13.4
5,2,F,12.9
5,3,A,11.8
5,4,B,13.9
5,5,C,15.2
5,6,D,14.8
6,1,F,12.6
6,2,A,12.3
6,3,B,14.3
6,4,C,15.4
6,5,D,14.5
6,6,E,13.1
```

## Statistical Analysis

### ANOVA Model
The Latin Square design allows for the analysis of:
- **Treatment effects** (A, B, C, D, E, F)
- **Row effects** (blocking factor 1)
- **Column effects** (blocking factor 2)

### Model Equation
Y_ijk = μ + α_i + β_j + τ_k + ε_ijk

Where:
- Y_ijk = observed response
- μ = overall mean
- α_i = row effect (i = 1,2,3,4,5,6)
- β_j = column effect (j = 1,2,3,4,5,6)
- τ_k = treatment effect (k = A,B,C,D,E,F)
- ε_ijk = random error

## Usage

### R Code Example
```r
# Load data
data <- read.csv("latin_square_data.csv")

# Perform ANOVA
model <- aov(Value ~ Treatment + factor(Row) + factor(Col), data = data)
summary(model)

# Post-hoc analysis
TukeyHSD(model, "Treatment")
```

### Python Code Example
```python
import pandas as pd
import scipy.stats as stats
from statsmodels.stats.anova import anova_lm
from statsmodels.formula.api import ols

# Load data
df = pd.read_csv("latin_square_data.csv")

# Perform ANOVA
model = ols('Value ~ C(Treatment) + C(Row) + C(Col)', data=df).fit()
anova_results = anova_lm(model, typ=2)
print(anova_results)
```

## Files in Repository
- `README.md` - This file
- `latin_square_data.csv` - Raw data in CSV format
- `analysis.R` - R script for statistical analysis
- `analysis.py` - Python script for statistical analysis

## License
This data is provided for educational and research purposes.

## Contact
For questions about this dataset, please open an issue in this repository.
