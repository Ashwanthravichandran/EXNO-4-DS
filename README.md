# EXNO:4-DS
# AIM:
To read the given data and perform Feature Scaling and Feature Selection process and save the
data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Scaling for the feature in the data set.
STEP 4:Apply Feature Selection for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE SCALING:
1. Standard Scaler: It is also called Z-score normalization. It calculates the z-score of each value and replaces the value with the calculated Z-score. The features are then rescaled with x̄ =0 and σ=1
2. MinMaxScaler: It is also referred to as Normalization. The features are scaled between 0 and 1. Here, the mean value remains same as in Standardization, that is,0.
3. Maximum absolute scaling: Maximum absolute scaling scales the data to its maximum value; that is,it divides every observation by the maximum value of the variable.The result of the preceding transformation is a distribution in which the values vary approximately within the range of -1 to 1.
4. RobustScaler: RobustScaler transforms the feature vector by subtracting the median and then dividing by the interquartile range (75% value — 25% value).

# FEATURE SELECTION:
Feature selection is to find the best set of features that allows one to build useful models. Selecting the best features helps the model to perform well.
The feature selection techniques used are:
1.Filter Method
2.Wrapper Method
3.Embedded Method

# CODING AND OUTPUT:
```
import pandas as pd
from scipy import stats
import numpy as np
df = pd.read_csv("/content/bmi.csv")
df.head()
```

![img-1](https://github.com/user-attachments/assets/c0513064-fa29-4dee-8d86-6ffca1a8739c)

```
df.dropna()
```

![img-2](https://github.com/user-attachments/assets/fa472cdb-aa41-4b9e-8025-5c13255dda20)

```
max_vals=np.max(np.abs(df[['Height']]))
max_vals
```

![img-3](https://github.com/user-attachments/assets/05d3bc49-b1a3-4ffa-97c7-328a09d0f711)

```
max_vals=np.max(np.abs(df[['Weight']]))
max_vals
```

![img-4](https://github.com/user-attachments/assets/a8aaf8de-8fdc-42cb-a8d9-861c66878155)

```
df1 = pd.read_csv("/content/bmi.csv")
from sklearn.preprocessing import StandardScaler
sc=StandardScaler()
df1[['Height','Weight']]=sc.fit_transform(df1[['Height','Weight']])
df1.head(10)
```

![img-5](https://github.com/user-attachments/assets/026e7876-53d9-4856-b466-3db6a1f5b7ce)

```
from sklearn.preprocessing import MinMaxScaler
scaler=MinMaxScaler()
df[['Height','Weight']]=scaler.fit_transform(df[['Height','Weight']])
df.head(10)
```

![img-6](https://github.com/user-attachments/assets/7101284e-25bb-4013-a546-98158986ef6d)

```
df2 = pd.read_csv("/content/bmi.csv")
from sklearn.preprocessing import Normalizer
scaler=Normalizer()
df2[['Height','Weight']]=scaler.fit_transform(df2[['Height','Weight']])
df2
```

![img-7](https://github.com/user-attachments/assets/7d80f53f-5965-487f-8a35-22a6f7115e38)

```
df3 = pd.read_csv("/content/bmi.csv")
from sklearn.preprocessing import MaxAbsScaler
scaler=MaxAbsScaler()
df3[['Height','Weight']]=scaler.fit_transform(df3[['Height','Weight']])
df3
```

![img-8](https://github.com/user-attachments/assets/8e2b7e1d-d9ed-42b1-b97e-688d2d4a2294)

```
df4=pd.read_csv("/content/bmi.csv")
from sklearn.preprocessing import RobustScaler
scaler=RobustScaler()
df4[['Height','Weight']]=scaler.fit_transform(df4[['Height','Weight']])
df4.head()
```

![img-9](https://github.com/user-attachments/assets/f466203a-5d9e-4d1c-a608-1c75a464b4cc)


Feature Selection
```
import pandas as pd
import numpy as np
from scipy.stats import chi2_contingency
import seaborn as sns
tips=sns.load_dataset('tips')
tips.head()
```

![img-10](https://github.com/user-attachments/assets/33904815-0f06-43c9-ad2c-5c80a04f969c)

```
contingency_table=pd.crosstab(tips['sex'],tips['time'])
print(contingency_table)
```

![img-11](https://github.com/user-attachments/assets/2e15e1ce-3492-4974-bb61-d94374aa02e6)

```
chi2, p, _, _ = chi2_contingency(contingency_table)
print(f"Chi-Square Statistic: {chi2}")
print(f"P-value: {p}")
```

![img-12](https://github.com/user-attachments/assets/9cc24f57-2295-4a5c-8883-6dc6262e699a)

```
import pandas as pd
from sklearn.feature_selection import SelectKBest, mutual_info_classif, f_classif
data={
    'Feature1':[1,2,3,4,5],
    'Feature2': ['A','B','C','A','B'],
    'Feature3':[0,1,1,0,1],
    'Target' :[0,1,1,0,1]
}
df=pd.DataFrame(data)
X=df[['Feature1','Feature3']]
y=df['Target']
selector=SelectKBest(score_func=mutual_info_classif, k=1)
X_new = selector.fit_transform (X,y)
selected_feature_indices = selector.get_support(indices=True)
selected_features = X.columns[selected_feature_indices]
print("Selected Features:")
print(selected_features)
```

![img-13](https://github.com/user-attachments/assets/9cde5803-6b3b-4ea8-a7e0-281afe09d6bf)

# RESULT:
      Hence , the Feature Scaling and Feature Selection process of the dataset has been carried out successfully.
