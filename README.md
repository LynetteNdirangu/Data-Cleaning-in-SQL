 # World Layoffs Data Cleaning Project (MySQL)

## 📌 Overview
This project focuses on cleaning and standardizing a raw dataset containing global tech layoffs using *MySQL Workbench*. Raw data often contains inconsistencies, duplicate records, and missing values. The primary objective was to transform this raw data into a clean, accurate, and structured format suitable for Exploratory Data Analysis (EDA) and visualization.

---

## 🛠️ Data Cleaning Steps Followed

1. *Creating a Staging Environment*
   * Imported raw data into layoffs.
   * Created a duplicate table layoffs_staging to preserve raw source data and ensure idempotent data cleaning practices.

2. *Removing Duplicate Records*
   * Identified duplicate rows using window functions (ROW_NUMBER() OVER (PARTITION BY ...)).
   * Stored window results in a CTE and subsequently created layoffs_staging2 to safely filter and delete rows where row_num > 1.

3. *Data Standardization*
   * Removed unnecessary whitespace from strings using TRIM().
   * Standardized variation in industry titles (e.g., merging variants like Crypto Currency and Crypto into Crypto).
   * Cleaned trailing punctuation issues in location and country fields (e.g., removing trailing periods like United States.).
   * Converted text-based date fields into valid SQL DATE format using STR_TO_DATE() and updated column schemas using ALTER TABLE.

4. *Handling Null and Blank Values*
   * Converted empty strings ('') to SQL NULL values across columns to enable standardized processing.
   * Utilized self-joins (JOIN) on matching company and location records to populate missing industry data from duplicate company entries.

5. *Removing Unnecessary Data*
   * Filtered out unhelpful records where both total_laid_off and percentage_laid_off were completely null.
   * Dropped temporary operational columns (e.g., row_num) used during duplicate removal.
