# lab2_titanic_Gerbise

1. Load and Inspect the Data

import pandas as pd
df = pd.read_csv("train.csv")
df.head()
  
  Loads the raw Titanic dataset (train.csv) into a DataFrame.
  df.head() previews the first 5 rows to understand the structure and contents.

df.info()
df.describe()
df.columns

  info() shows data types and null values.
  describe() gives statistical summaries for numerical columns.
  columns lists the column names in the dataset.
  
2. Handle Missing Values

df.isnull().sum()
df['Age'] = df['Age'].fillna(df['Age'].median())

  isnull().sum() shows the total number of missing values in each column.
  Missing values in the Age column are filled using the median age — a common strategy to avoid skewing the data.

3. Drop Irrelevant Columns

df = df.drop(columns=["Cabin"])

  The Cabin column is removed since it contains too many missing values to be useful in basic analysis.

4. Remove Duplicate Rows

df.duplicated().sum()
df.drop_duplicates(inplace=True)

  Checks for and removes duplicate entries from the dataset to ensure data integrity.

5. Convert Data Types

df["Survived"] = df["Survived"].astype("category")
df["Pclass"] = df["Pclass"].astype("category")

  Converts Survived and Pclass columns to categorical types, improving memory efficiency and clarifying their qualitative nature.

6. Standardize Column Names

df.columns = df.columns.str.lower()

  Converts all column names to lowercase for consistency and ease of use in later analysis.

7. Save the Cleaned Dataset

df.to_csv("titanic_cleaned.csv", index=False)

  Exports the cleaned dataset as a new CSV file (titanic_cleaned.csv) for future analysis or modeling.

Basic Visualization

1. Bar chart showing how many passengers survived vs. did not survive.

df["survived"].value_counts().plot(kind="bar")
plt.title("Survival Count")
plt.xlabel("Survived")
plt.ylabel("Number of Passengers")
plt.show()

2. Histogram visualizing the age distribution of passengers.

df["age"].plot(kind="hist", bins=20, edgecolor="black")
plt.title("Age Distribution")
plt.xlabel("Age")
plt.show()

3. Survival Rate by Gender

df.groupby("sex")["survived"].mean().plot(kind="bar")
plt.title("Survival Rate by Gender")
plt.ylabel("Survival Rate")
plt.show()

  Bar chart showing the average survival rate for each gender.
  Helps reveal that women had a higher chance of survival.



4. Survival Rate by Passenger Class

df.groupby("pclass")["survived"].mean().plot(kind="bar")
plt.title("Survival Rate by Class")
plt.ylabel("Survival Rate")
plt.show()

  Highlights how survival rates varied by ticket class (1st, 2nd, 3rd).

5. Replot Age Distribution

df["age"].plot(kind="hist", bins=20, edgecolor="black")
plt.title("Age Distribution")
plt.xlabel("Age")
plt.show()

  Confirms the cleaned age distribution.
