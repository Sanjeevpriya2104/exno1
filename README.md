# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output

```
import pandas as pd
from google.colab import files
import io

uploaded = files.upload()

filename = next(iter(uploaded))
df = pd.read_csv(io.BytesIO(uploaded[filename]))


print("Missing values:")
print(df.isnull().sum())

print("\nDuplicate registration numbers:")
print(df[df.duplicated("REGNO", keep=False)])

marks = ["M1", "M2", "M3", "M4"]

df[marks + ["TOTAL"]] = df[marks + ["TOTAL"]].apply(
    pd.to_numeric, errors="coerce"
)

calculated_total = df[marks].sum(axis=1, min_count=4)

print("\nInconsistent total marks:")
print(df[df["TOTAL"] != calculated_total])


df = df.drop_duplicates()

output_file = "SAMPLEIDS_cleaned.csv"
df.to_csv(output_file, index=False)

print("\nCleaning completed!")

files.download(output_file)

```
## output

<img width="1036" height="808" alt="image" src="https://github.com/user-attachments/assets/38635f25-bba3-4a9b-9406-718b6bed8163" />

```

import pandas as pd
from google.colab import files
import io

uploaded = files.upload()
df = pd.read_csv(io.BytesIO(uploaded["heights.csv"]))

Q1 = df["height"].quantile(0.25)
Q3 = df["height"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[(df["height"] < lower) | (df["height"] > upper)]

print("Unusual height measurements:")
print(outliers)
```
## output
<img width="728" height="170" alt="image" src="https://github.com/user-attachments/assets/10991d4a-a256-431a-86c5-339e7513f4ed" />


# Result
Thus the given data successfully performed data cleaning and saved the cleaned data to a file.
