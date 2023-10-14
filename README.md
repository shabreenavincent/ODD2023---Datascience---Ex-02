# Ex02 Outlier Detection
### AIM:  
You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,
- (1) Remove outliers using IQR
- (2) After removing outliers in step 1, you get a new dataframe.
- (3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result
- (4) for the data set height_weight.csv find the following
  - (i) Using IQR detect weight outliers and print them
  - (ii) Using IQR, detect height outliers and print them
### Explanation:
An Outlier is an observation in a given dataset that lies far from the rest of the observations. That means an outlier is vastly larger or smaller than the remaining values in the set.
An outlier is an observation of a data point that lies an abnormal distance from other values in a given population. (odd man out).
Outliers badly affect mean and standard deviation of the dataset. These may statistically give erroneous results.
### Algorithm:
- Step1: Read the given Data.
- Step2: Get the information about the data.
- Step3: Detect the Outliers using IQR method and Z score.
- Step4: Remove the outliers.
- Step5: Plot the datas using Box Plot.
```
212222230141
shabreena vincent
```
### Code:
##### bhp.csv:
```Python
import pandas as pd
import seaborn as sns
import numpy as np
from scipy import stats
from google.colab import files
uploaded=files.upload()
df=pd.read_csv('bhp.csv')
df.info()
print(df.describe())
df.head()
#BEFORE REMOVING OUTLIER
sns.boxplot(y='price_per_sqft',data=df)

# PERFORMING IQR METHOD
q1=df['price_per_sqft'].quantile(0.25)
q3=df['price_per_sqft'].quantile(0.75)
IQR=q3-q1
low=q1-1.5*IQR
high=q3+1.5*IQR
new=df[((df['price_per_sqft']>=low)&(df['price_per_sqft']<=high))]

#AFTER REMOVING OUTLIER using IQR method
sns.boxplot(y='price_per_sqft',data=new)

# PERFORMING Zscore METHOD
z=np.abs(stats.zscore(df['price_per_sqft']))
new2=df[(z<3)]

#AFTER REMOVING OUTLIER using Zscore method
sns.boxplot(y="price_per_sqft",data=new2)
```
##### height_weight.csv:
```Python
import pandas as pd
import seaborn as sns
from google.colab import files
uploaded=files.upload()
df=pd.read_csv('height_weight.csv')
df.info()
df.describe()
df.head()

#BEFORE REMOVING OUTLIER in HEIGHT
sns.boxplot(y='height',data=df)
#PERFORMING IQR METHOD ON HEIGHTS
height_q1 = df['height'].quantile(0.25)
height_q3 = df['height'].quantile(0.75)
height_IQR = height_q3 - height_q1
height_low = height_q1 - 1.5 * height_IQR
height_high = height_q3 + 1.5 * height_IQR
height_new=df[((df['height']>=height_low)&(df['height']<=height_high))]
#AFTER REMOVING OUTLIER in HEIGHT
sns.boxplot(y='height',data=height_new)

#BEFORE REMOVING OUTLIER in WEIGHT
sns.boxplot(y='weight',data=df)
#PERFORMING IQR METHOD ON HEIGHTS
weight_q1 = df['weight'].quantile(0.25)
weight_q3 = df['weight'].quantile(0.75)
weight_IQR = weight_q3 - weight_q1
weight_low = weight_q1 - 1.5 * weight_IQR
weight_high = weight_q3 + 1.5 * weight_IQR
weight_new=df[((df['weight']>=weight_low)&(df['weight']<=weight_high))]
#AFTER REMOVING OUTLIER in WEIGHT
sns.boxplot(y='weight',data=weight_new)
```
### Output:
##### bhp.csv:
<img height=30% width=70% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/c62482aa-13d3-4e93-84f3-14d77e12ff94">
<img height=20% width=49% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/550161a2-7e49-4873-b9d3-2dee79909859">  <img height=30% width=49% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/77006c4a-5f65-4c46-b43d-62da3adeae72">
<img height=30% width=49% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/6ab44ad1-3d24-49ac-8ed8-0a873ee9094c"><img height=30% width=49% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/699f1ddd-dfb7-4d58-abd5-69614106d9d4">

##### weight_height.csv:
<img height=30% width=60% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/ea846d57-a472-4b28-8d0a-3c405d80f8e0"><img height=30% width=38% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/beead9e7-e4bc-4431-a536-bacdb947e6b6">  

<img height=30% width=48% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/952f228c-8518-4f91-b966-fda9215eb959"><img height=30% width=48% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/35fbb5b8-69b9-4592-9685-d81d4cb0f844">  

<img height=30% width=48% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/3606e325-b846-412f-b0c2-e56d74b16427"><img height=30% width=48% src="https://github.com/ROHITJAIND/Ex-02_Outlier-Detection/assets/118707073/14b3b742-5bfe-47c2-954b-7ee7315c6848">  

### Result:
Hence the given set of data is read and the outliers are removed using the IQR method and Zscore method.
