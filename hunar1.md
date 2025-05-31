import pandas as pd

# Load your dataset (replace 'data.csv' with your actual file)
df = pd.read_csv("C:/Users/Devi Mahitha/Downloads/food_coded.csv")

# Display initial data info
print("Initial Data Info:")
print(df.info())

# 1. Handling missing values
# Fill missing values in numerical columns with mean, median, and mode
for column in df.columns:
    if df[column].isnull().sum() > 0:
        if df[column].dtype in ['float64', 'int64']:
            # Fill with mean
            df[column + '_mean'] = df[column].fillna(df[column].mean())
            # Fill with median
            df[column + '_median'] = df[column].fillna(df[column].median())
            # Fill with mode
            mode_val = df[column].mode()[0]
            df[column + '_mode'] = df[column].fillna(mode_val)
        else:
            # For categorical data, use mode
            mode_val = df[column].mode()[0]
            df[column] = df[column].fillna(mode_val)

# 2. Remove duplicate rows
df = df.drop_duplicates()

# 3. Remove duplicate columns
# Transpose the DataFrame, drop duplicates, then transpose back
df = df.T.drop_duplicates().T

# Display cleaned data info
print("\nCleaned Data Info:")
print(df.info())
