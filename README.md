# Messy-data
1. Creating DataFrame
df = pd.DataFrame({...})
This creates a table (like Excel) with:
Missing values (NaN) in age and city
Duplicate row (customer_id = 2)
Categorical data (city, gender)
Numerical data (age, annual_income)
This simulates real-world messy data.

2. Data Cleaning
Fill missing values
df['age'] = df['age'].fillna(df['age'].median())
Replaces missing age values with the median
Median is used because it’s not affected by outliers
df['city'] = df['city'].fillna(df['city'].mode()[0])
Replaces missing city values with the most frequent city (mode)
Remove duplicates
df = df.drop_duplicates()
Removes repeated rows to avoid bias in models

3. Encoding Categorical Data
Machine learning models cannot understand text, so we convert it to numbers.
One-Hot Encoding (for city)
df_encoded = pd.get_dummies(df, columns=['city'])
Converts cities into separate columns:
city_Delhi → 0 or 1
city_Mumbai → 0 or 1
Prevents the model from assuming any order between cities.

Label Encoding (for gender)
le = LabelEncoder()
df_encoded['gender'] = le.fit_transform(df_encoded['gender'])
Converts:
Male → 1
Female → 0
Works well because gender has only two categories.

4. Scaling Numerical Features
Numerical values like:
age (25–40)
income (40,000–120,000)
have very different ranges → this can confuse ML models.

Min-Max Scaling
df_minmax[cols_to_scale] = minmax_scaler.fit_transform(...)
Scales values between 0 and 1

Formula:
(x - min) / (max - min)
Example:
25 → 0
40 → 1
Standardization
df_standard[cols_to_scale] = standard_scaler.fit_transform(...)
Converts data to:
Mean = 0
Standard deviation = 1
Formula:
(x - mean) / std

5. Why We Use Both
Min-Max Scaling
Best for: KNN, Neural Networks
Keeps values in a fixed range
Standardization
Best for: Linear Regression, SVM
Works well with normally distributed data
