# Medha_Task-1
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# 1. [span_1](start_span)Load dataset (Example using House Prices)[span_1](end_span)
# Note: Ensure the dataset file is in your working directory
df = pd.read_csv('house_prices.csv')

# [span_2](start_span)Identify missing values[span_2](end_span)
print("Missing values per column:")
print(df.isnull().sum())

# 2. [span_3](start_span)Visualize missing data patterns[span_3](end_span)
plt.figure(figsize=(10, 6))
df.isnull().sum().plot(kind='bar')
plt.title('Missing Data Count per Column')
plt.ylabel('Number of Missing Values')
plt.show()

# 3. [span_4](start_span)Apply mean/median imputation for numerical columns[span_4](end_span)
# Use Median if there are outliers, Mean if data is normally distributed
numerical_cols = df.select_dtypes(include=[np.number]).columns
for col in numerical_cols:
    df[col] = df[col].fillna(df[col].median())

# 4. [span_5](start_span)Apply mode imputation for categorical columns[span_5](end_span)
categorical_cols = df.select_dtypes(include=['object']).columns
for col in categorical_cols:
    df[col] = df[col].fillna(df[col].mode()[0])

# 5. [span_6](start_span)Remove columns with extremely high missing values[span_6](end_span)
# Threshold: e.g., drop columns with more than 50% missing data
threshold = len(df) * 0.5
df = df.dropna(thresh=threshold, axis=1)

# 6. [span_7](start_span)Validate dataset after cleaning[span_7](end_span)
print("Missing values after cleaning:", df.isnull().sum().sum())

# 7. [span_8](start_span)Compare before vs after dataset quality[span_8](end_span)
print(f"Original shape: {df_original_shape}") # Define this at the start
print(f"Cleaned shape: {df.shape}")

# [span_9](start_span)Save the cleaned dataset for submission[span_9](end_span)
df.to_csv('cleaned_house_prices.csv', index=False)
