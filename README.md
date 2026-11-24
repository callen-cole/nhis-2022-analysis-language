# NHIS 2022: Children's Speech-Language Difficulties and Mental Health Need

An analysis of the 2022 National Health Interview Survey (NHIS) examining the prevalence of parent-reported speech and language difficulties among U.S. children, and how that prevalence varies by family income, health insurance coverage, and race/ethnicity. A secondary section explores children's mental health need by income, region, and urban–rural status.

## Research questions

1. What is the national prevalence of parent-reported speech and language difficulties among children in 2022?
2. How does that prevalence differ across socioeconomic and demographic factors — family income relative to the poverty threshold, health insurance coverage type, and race/ethnicity?
3. How are reported speech difficulties and language difficulties related to one another?
4. How does children's mental health need vary by family income, census region, and urban–rural classification?

## Data

All data come from the CDC National Center for Health Statistics' **2022 National Health Interview Survey**, sample child file. NHIS is a nationally representative household survey using a complex, stratified, multistage sample design.

- **Source:** [CDC/NCHS, NHIS 2022](https://www.cdc.gov/nchs/nhis/index.htm)
- **Unit of analysis:** sample children (one randomly selected child per sampled household)
- **Survey design variables:** `PPSU` (pseudo-PSU), `PSTRAT` (pseudo-stratum), `WTFA_C` (sample child weight)

`NHIS_2022_selected_variables.csv` is a codebook for the variables used in this analysis, including variable descriptions, data types, and code values.

> **Note on the data file:** the raw extract `NHIS_2022_Child_Data.csv` is not included in this repository. Download the 2022 sample child file from the CDC link above and place it in the project root to reproduce the analysis.

## Methods

The analysis accounts for the NHIS complex survey design throughout. A survey design object is constructed once and subset for each outcome:

```r
nhis_design <- svydesign(id = ~PPSU, strata = ~PSTRAT,
                         weights = ~WTFA_C, nest = TRUE,
                         data = NHIS22_recoded)
