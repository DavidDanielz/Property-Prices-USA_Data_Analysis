# Property-Prices-USA_Data_Analysis
This project analyzes property prices across the US, focusing on regional cost-of-living trends. The dataset was sourced from Kaggle, and the project showcases my skills in SQL, PostgreSQL, and Tableau for data analysis and visualization.


```
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
