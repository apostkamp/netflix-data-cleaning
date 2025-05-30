# Netflix Dataset Cleaning Project

## 1. Introduction

This project focuses on cleaning and preprocessing a Netflix dataset (`netflix.csv`). The primary goal was to transform the raw data into a more structured and usable format for potential analysis or visualization. The tools that we utilized were `Python`, `Pandas` for data manipulation and analysis & `Jupyter Notebook` for interactive coding and documentation.

## 2. Dataset

* **Original Dataset:** [Netflix Data: Cleaning, Analysis and Visualization](https://www.kaggle.com/datasets/ariyoomotade/netflix-data-cleaning-analysis-and-visualization) (`netflix.csv`)
    * This dataset contains information about TV shows and movies available on Netflix, including details like `show_id`, `type`, `title`, `director`, `country`, `date_added`, `release_year`, `rating`, `duration` and `genre`.
* **Cleaned Dataset:** `Cleaned_Dataset_CSV.csv`
    * This is the output of the cleaning process, ready for further use.

## 3. Data Cleaning Steps

The following steps were taken to clean and prepare the dataset:

1.  **Loading Data and Initial Setup:**
    * Imported the `pandas` library.
    * Loaded the `netflix.csv` dataset into a pandas DataFrame.

2.  **Initial Data Exploration:**
    * Used `data.head()` to view the first few rows and get an overview of the data structure.
    * Used `data.info()` to understand data types, column names, and non-null value counts for each column.

3.  **Removing Redundant Columns:**
    * The `rating` column was identified as redundant or not needed for this specific cleaning pass and was dropped from the DataFrame using `data.drop(columns="rating", inplace=True)`.

4.  **Renaming Columns:**
    * Column names were standardized by capitalizing the first letter of each word (e.g., `show_id` became `Show_id`) using `data.columns = data.columns.str.capitalize()`.

5.  **Handling Duplicates:**
    * Checked for duplicate rows using `data.duplicated().sum()`. No complete duplicate rows were found in this instance.
    * The code includes a step `data.drop_duplicates(inplace=True)` which would remove duplicates if any were present.

6.  **Handling Missing Values (NaN):**
    * Checked for missing values using `data.isna().sum()`. The initial check after loading indicated no missing values recognized by default as NaN.
    * Despite this, `data.dropna(inplace=True)` was used to remove any rows that might contain NaN values, ensuring data integrity. (Note: Some columns like 'Director' might have string placeholders like "Not Given" which are not treated as NaN by default but were not specifically handled in this cleaning script beyond the general `dropna`).

7.  **Column-Specific Cleaning and Transformations:**

    * **`Show_id` Column:**
        * Removed the prefix 's' from all entries (e.g., 's1' became '1') using `data["Show_id"] = data["Show_id"].str.replace("s", "")`.
        * Converted the data type of the `Show_id` column from object (string) to integer using `data["Show_id"] = data["Show_id"].astype(int)`.

    * **`Date_added` Column:**
        * Standardized the date format by replacing '/' with '-' (e.g., '9/25/2021' became '9-25-2021') using `data["Date_added"] = data["Date_added"].str.replace("/", "-")`.
        *(Note: For more advanced date-based analysis, this column would typically be converted to a datetime object, which was not part of this specific cleaning script.)*

8.  **Saving the Cleaned Data:**
    * The cleaned DataFrame was saved to a new CSV file named `Cleaned_Dataset_CSV.csv` without the DataFrame index using `data.to_csv('Cleaned_Dataset_CSV.csv', index=False)`.

## 4. How to Use / Reproduce

1.  Ensure you have Python and the necessary libraries installed. You can install the required packages using the `requirements.txt` file:
    ```bash
    pip install -r requirements.txt
    ```
2.  Place the original `netflix.csv` dataset in the same directory as the Jupyter Notebook.
3.  Run the `notebook.ipynb` file in a Jupyter environment.
4.  The cleaned dataset will be saved as `Cleaned_Dataset_CSV.csv`.
---
