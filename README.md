# Currently Working On This Project. Coming Soon...
# Property-Prices-USA_Data_Analysis
This project analyzes property prices across the US, focusing on regional cost-of-living trends. The dataset was sourced from Kaggle, and the project showcases my skills in SQL, PostgreSQL, and Tableau for data analysis and visualization.

### Outlier Identification and Treatment

During the data exploration phase, one outlier was identified, in the "mortgage_as_percentage_of_income" metric. The outlier was for Santa Barbara, CA, where the mortgage as a percentage of income was 103.7%. 

1. Reviewed Outlier

I found an outlier with the following values:

    Rank: 1
    City: Santa Barbara, CA
    Price to Income Ratio: 13.3
    Gross Rental Yield City Centre: 4.4
    Gross Rental Yield Outside City: 6.2
    Price to Rent Ratio City Centre: 23
    Price to Rent Ratio Outside City: 16.3
    Mortgage as Percentage of Income: 103.7
    Affordability Index: 1

Observations:

    Mortgage as Percentage of Income: 103.7% is unusually high, indicating that mortgage payments exceed the income, which may be an error or an anomaly.
    Price to Income Ratio and other metrics seem reasonable in context but double-check if this value aligns with other cities or looks too extreme.

2. Validate Outlier

Actions:

    Verify Data: Check the source of the data to ensure that 103.7% is not a data entry error.
    Consult External Sources: Compare the values for Santa Barbara with other real estate sources to see if this metric is realistic.
    Business Context: Consult with a domain expert or review historical data for Santa Barbara to understand if this value is plausible.

Based on this, the value was **not removed** or adjusted but marked as a valid outlier in the dataset.

3. Decide on Handling Outliers

Based on validation, decide on the approach:

    If Valid: Keep the outlier if it represents real and important data.
    If Invalid: Correct or remove the outlier if it's a data entry error.

```
-- Check for Outliers
SELECT *
FROM real_estate_metrics
WHERE price_to_income_ratio > 20 -- Possible Outlier
	OR price_to_rent_ratio_city_centre > 100 -- Possible Outlier
	OR mortgage_as_percentage_of_income > 100;

	-- Add a column to flag verified outliers
ALTER TABLE real_estate_metrics
ADD COLUMN outlier_verified BOOLEAN DEFAULT FALSE;

-- Update the flag for Santa Barbara once verified
UPDATE real_estate_metrics
SET outlier_verified = TRUE
WHERE City = 'Santa Barbara, CA' AND "mortgage_as_percentage_of_income" = 103.7;
```
