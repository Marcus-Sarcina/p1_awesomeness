The presentation corresponding to this project can be found [in Google Docs](https://docs.google.com/presentation/d/1NwpHAuz2lmeUtYniD-MF0iTmUpPHJJw5jBckDqBocs0/edit#slide=id.g25f889760f8_0_74).

# A Thirst for Death
#### *Exploring the potential of simple, space-filling datasets to illuminate common subjects of social and economic data science.*

## Concept:

We wanted to demonstrate the potential of well-organized space-filling datasets to illuminate or correct trends in apparently unrelated data domains. The idea was to capture a small number of dimensions from a comprehensive dataset into a form where they could be rapidly collated and compared to unrelated datsets.

We chose to work with drought data because of it's availability and comprehensiveness along with the possibility that drought (long-duration event with drastic effects on the natural world) might be reveled to have subtle impacts on any number of natural and social systems.

## Method:

We acquired two initial datasets. 

For our space-filling dataset, we retrieved drought categorizations from the [USDA Drought monitor API](https://droughtmonitor.unl.edu). This service provides drought category data for all locations in the US for all weeks from Jan 1, 2000 until the present, making it possible to insert drought-related dimensions into any dataset which specifies date and a location, with proper formatting.

For our target dataset, we used the Murder Accountability Project's [Homicide Reports, 1980-2014](https://www.kaggle.com/datasets/murderaccountability/homicide-reports), which we retrieved from Kaggle.

We restricted both datasets to a select four cities which we believed would represent a range of drought activity during the time period where the datasets overlapped (2000 - 2014) and formatted the data to index on a combination of City, Year, and Month.

## Initial Results

We were able to recognize a number of well-known trends in the data, including the general decline in violent crime between 1995 and 2018 and the drastic reduction in crime in New Orleans following Hurricane Katrina.

We found no corelation between drought state and murder rate in our sample and so abandoned further comparative analysis of these initial datasets.

## Follow-On Application

In order to test the core concept of rapid data recombination, we pulled a second comparison dataset of Real Estate market reports from [Redfin](https://www.redfin.com/news/data-center/).

This data was in the form of an automated report from Tableu which presented a significant data cleaning challenge due to interspersed CSV rows with differing column types and multiple delimiters and system-assigned column names. Nonetheless, after a couple hours of data cleaning, the effort to combine this new dataset with our drought dataset was trivial.

Analysis of the real estate data revealed a mild positive corelation (~0.25) between drought and several measures of RE sales, prices, and construction industry health (% of sales aren new construction and low new construction inventory). This corelation increased in strength when all drought states were considered and increased even more when our synthetic severity-weighted measure of drought severity was considered.

## Object-level Conclusions

1. Droughts are a powerful natural process which may have subtle and unexpected effects on natural and social systems.
1. Intuition is a poor guide for predicting which such effects may surface in any particular domain. The intuitive hypothesis in each comparison was that drought, as a stress-inducing condition would lead to worse social outcomes, but it turned out that drought had a no effect (or a slightly positive effect) on murder rates and appears to have a significantly positive effect on the real estate market within our samples.
1. Considering (1) and (2), we urge social scientists and data analysts to consider and correct for often-overlooked systemic conditions such as drought when examining social data.

## Methodological Conclusions

1. We believe this general approach - that of creating space-filling mappings of common factors for use in analyzing and correcting ad-hoc datasets is highly promising.

## Suggested Follow-On Work

To operationalize the practice we explored in this project, it might be useful to create a series of such space-filling maps with standardized semantics and deploy APIs for accessing such maps.

I envision a standard library which would automate access to these standard maps such that an arbitrary dataset with the proper indices could be fortified with matching values like so:

```
import standard_candles as sc

my_data['drought_state', 'inflation', 'local_language', 'at_war_?', 'mean_temp'] = sc.time_location(my_data.year, my_data.month, my_data.postal_code)
```
