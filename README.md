## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING:
  ```
   import pandas as pd

# Creating the dataframe based on the source data [1]
data = {
    'id': [1,2,3,4,5,6,7,8,9,10],
    'bin_1': ['F', 'F', 'F', 'F', 'T', 'T', 'F', 'T', 'F', 'F'],
    'bin_2': ['N', 'Y', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'Y'],
    'nom_0': ['Red', 'Blue', 'Blue', 'Green', 'Red', 'Green', 'Red', 'Red', 'Blue', 'Red'],
    'ord_2': ['Hot', 'Warm', 'Cold', 'Warm', 'Cold', 'Hot', 'Cold', 'Cold', 'Warm', 'Hot']
}
df = pd.DataFrame(data)

# 1. Binary Encoding
# Map 'F'/'N' to 0 and 'T'/'Y' to 1 [1]
df['bin_1'] = df['bin_1'].map({'F': 0, 'T': 1})
df['bin_2'] = df['bin_2'].map({'N': 0, 'Y': 1})

# 2. Ordinal Encoding
# Manually map 'ord_2' to preserve the logical order of temperature [1]
# Note: This specific ordering logic is not in the sources and follows standard data conventions.
ord_map = {'Cold': 0, 'Warm': 1, 'Hot': 2}
df['ord_2'] = df['ord_2'].map(ord_map)

# 3. One-Hot Encoding
# Use get_dummies for the nominal feature 'nom_0' which has no inherent order [1]
df = pd.get_dummies(df, columns=['nom_0'])

print(df)
import pandas as pd
from sklearn.preprocessing import LabelEncoder

# Recreating the data structure from the sources [1]
data = {
    'id': [1,2,3,4,5,6,7,8,9,10],
    'ord_2': ['Hot', 'Warm', 'Cold', 'Warm', 'Cold', 'Hot', 'Cold', 'Cold', 'Warm', 'Hot']
}
df = pd.DataFrame(data)

# Initialize the LabelEncoder
le = LabelEncoder()

# Fit and transform the ord_2 column [1]
df['ord_2_encoded'] = le.fit_transform(df['ord_2'])

print(df[['ord_2', 'ord_2_encoded']])
# Note: This requires the category_encoders library
from category_encoders import TargetEncoder

# Adding nominal data from the sources and a dummy target [1]
df['nom_0'] = ['Red', 'Blue', 'Blue', 'Green', 'Red', 'Green', 'Red', 'Red', 'Blue', 'Red']
df['target'] = [1,0,1,0,1,0,1,0,1,0]

# Initialize TargetEncoder for the nom_0 column [1]
te = TargetEncoder(cols=['nom_0'])

# Fit and transform based on the dummy target
df['nom_0_encoded'] = te.fit_transform(df['nom_0'], df['target'])

print(df[['nom_0', 'target', 'nom_0_encoded']])
```
## OUTPUT:


# RESULT:
      Thus,for the given dataset feature encoding and transformation are done successfully.

       
