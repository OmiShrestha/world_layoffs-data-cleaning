# Data Cleaning of `world_layoffs` Excel File

## Project Overview
This project involves the data cleaning of a `world_layoffs` Excel file to ensure the data is accurate, consistent, and ready for analysis. The cleaning process utilizes SQL queries executed through MySQL Workbench to efficiently manipulate and transform the data.

## Goals
The main objectives of this project are:

1. **Remove Duplicates**: Identify and eliminate any duplicate records in the dataset to ensure each entry is unique.
  
2. **Standardize the Data**: Ensure consistency across the dataset, including uniform formatting of text, dates, and numerical values. This may involve converting text to lowercase, standardizing date formats, and ensuring numerical values are stored in a consistent format.
  
3. **Handle Null or Blank Values**: Identify and address any null or blank values within the dataset. This could involve replacing null values with appropriate defaults, removing records with missing critical information, or filling in gaps using data imputation techniques.
  
4. **Remove Unnecessary Columns**: Eliminate any columns that do not contribute to the analysis or are irrelevant to the dataset, reducing clutter and improving data usability.

## Tools Used
- **MySQL Workbench**: A powerful tool for database design, development, and management that allows users to execute SQL queries and visualize data structures.
  
- **SQL Queries**: Structured Query Language (SQL) is used to perform data manipulation operations, including selecting, inserting, updating, and deleting records.

## Steps for Data Cleaning

1. **Load the Data into MySQL**:
   - Import the `world_layoffs` Excel file into a MySQL database.
   - Create a table that accurately reflects the structure of the data.

2. **Remove Duplicates**:
   - Use SQL queries to identify duplicates based on key columns (e.g., company name, location, date of layoffs).
   - Implement a `DELETE` statement using a Common Table Expression (CTE) or other methods to remove duplicate records.

   ```sql
   WITH duplicate_cte AS (
       SELECT *,
       ROW_NUMBER() OVER (PARTITION BY company, location, date ORDER BY id) AS row_num
       FROM world_layoffs
   )
   DELETE FROM world_layoffs
   WHERE id IN (SELECT id FROM duplicate_cte WHERE row_num > 1);
