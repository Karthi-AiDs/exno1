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

```import pandas as pd
from google.colab import drive
drive.mount('/content/drive')
df = pd.read_csv('/content/drive/My Drive/SAMPLEIDS.csv')
df
```
![Screenshot 2025-03-10 112301](https://github.com/user-attachments/assets/0f2ed739-0a78-431e-b84c-c9e09987217c)

```df.info()```

![image](https://github.com/user-attachments/assets/619892af-0f9c-4b04-9656-6c0470da0b26)

```df.isnull()```

![image](https://github.com/user-attachments/assets/344a9b6d-8169-43c9-bc7f-ca7ee520cf14)

```df.isnull().sum()```

![image](https://github.com/user-attachments/assets/607e85d1-8645-497d-aa04-44035b41b385)

```df.dropna()```

![image](https://github.com/user-attachments/assets/dfba813a-e2f5-4b7a-81d6-caf3c9a80b3c)

```df.fillna(0)```

![image](https://github.com/user-attachments/assets/d5d8317c-1f1a-44c9-b235-4ddd0614f02a)

```df.fillna(method='ffill')```

![image](https://github.com/user-attachments/assets/572e5fab-d4fc-4619-81c9-3251554098d7)

```df.fillna(method='bfill)```

![image](https://github.com/user-attachments/assets/167f5a42-acbd-4970-98cd-fdce9f2b8c79)

```df['TOTAL'].fillna(value=df['TOTAL'].mean())```

![image](https://github.com/user-attachments/assets/6aa59ce9-e405-430a-8dd2-0ab779a7392b)

```df.dropna()```

![image](https://github.com/user-attachments/assets/617bd83b-7056-4392-b8f1-7064519497b3)

# IQR(Inter Quartile Range)

```
q1 = af.quantile(0.25)
q2 = af.quantile(0.50)
q3 = af.quantile(0.75)
iqr = q3 - q1
iqr
```

![image](https://github.com/user-attachments/assets/4103eafa-774f-4aef-ba81-a88d92bc7ef6)

```
q1 = np.percentile(af,25)
q3 = np.percentile(af,75)
iqr = q3 - q1
iqr
```

![image](https://github.com/user-attachments/assets/679bdfe6-7d7e-4ab5-820f-0b61e33dd50e)

```
lower_bound = q1 - 1.5 *iqr
upper_bound = q3 + 1.5*iqr
print(lower_bound)
print(upper_bound)
```

![image](https://github.com/user-attachments/assets/06518517-d1fa-45b4-ba0c-873baf8b3a8a)

```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
print("Q1: ",q1)
print("Q2: ",q3)
print("IQR: ",iqr)
print("lower_bound: ",lower_bound)
print("upper_bound: ",upper_bound)
print("Outliers: ",outliers)
```

![image](https://github.com/user-attachments/assets/65303b21-e0fb-4dfc-9cf2-f937113ae4e1)

```
af = af[((af >= lower_bound) & (af <= upper_bound))]
af
```

![image](https://github.com/user-attachments/assets/a0311332-1bd1-4cfc-8bbd-1494465f3efc)

```af.dropna()```

![image](https://github.com/user-attachments/assets/1fcf42f5-6739-4665-862c-3a5eeb9b8d1a)

```sns.boxplot(af)```

![image](https://github.com/user-attachments/assets/ca68214f-8a55-48b3-888e-955cf8a1e0c4)

# Z - SCORE

```
mean = np.mean(data)
std = np.std(data)
print("Mean: ",mean)
print("std. deviation: ",std)
```
![image](https://github.com/user-attachments/assets/76904ca9-68a3-40c1-9a98-55d1f9922a8c)

```
threshold = 3
outliers = []
for i in data:
  z = (i-mean)/std
  if z > threshold:
    outliers.append(i)
    print("Outliers: ",outliers)
```

![image](https://github.com/user-attachments/assets/3eaf9b9b-f254-42d9-8d69-68ab9b025179)

```
z = np.abs(stats.zscore(df))
print(df[z ['values']> 3]) # Access the first column by its index instead of a non-existent name
```
![image](https://github.com/user-attachments/assets/9e1af3dc-d46b-444e-9e24-2439fd6c8751)

```
def do(data):
  ts = 3
  m = np.mean(data)
  sd =np.std(data)
  for i in data:
    z = (i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out # Now it returns after processing all elements
op = do(data)
op

```

![image](https://github.com/user-attachments/assets/da19b8d9-0701-42c0-8897-711700aebb88)

```
no_outliers = df[(z < 3).all(axis=1)]
no_outliers
```

![image](https://github.com/user-attachments/assets/e0754347-f809-419c-a528-159282b932ea)

```
sns.boxplot(no_outliers)
```
![image](https://github.com/user-attachments/assets/ab6cb821-eba8-4e94-99c8-cb33222c029e)





# Result
          << Thus the outliers are detected and removed in the given file using IQR and Z-Score Method >>
