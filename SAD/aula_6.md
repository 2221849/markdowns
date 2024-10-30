# Decision Support Systems

## Lesson 6

This lesson covers the importance of **data quality** to ensure that data analysis is reliable and supports accurate decision-making. Here's a breakdown of each aspect mentioned and the role of the tables described:

### Data Quality Aspects

To ensure reliable analysis, the following aspects of data quality need to be addressed:

- **Correction**: Values comply with official rules.
- **Clarity**: Each data item has only one meaning.
- **Consistency**: A unified view is maintained, with a single version of the data.
- **Completeness**: All necessary values are present, and the total number of rows is as expected.

### Table Types

- **`T_CLEAN_*`**: Tables with cleaned and ready-to-use data.
- **`T_TEL_*`**: Tables for the Transformation Error Logger, tracking data transformation errors.
- **`T_LOOKUP_*`**: Tables containing preference data used for reference or mapping.
- **`SCREEN_*`**: Tables used for quality testing and data validation.
- **`TRANSFORM_*`**: Tables that transform raw data into a more usable format.

These structures and practices ensure that data quality is maintained throughout the decision support process.
