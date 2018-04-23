# Local Outlier Factor

Using Local Outlier Factor (LOF) is handy when you are looking for an unsupervised approach to identifying outliers in a 2D matrix. Tukey fences 
are great for identifying outliers in 1D space, when data is normally distributed and the outlier is an extreme value on the distribution. 
However, many real-life business problems are more complex. In credit card fraud or call center examples, we do not have the
classification of whether a transaction is actually fraudulent or a specific call center representative is under-performing relative 
to his or her peers. This is where LOF comes in.  

### Step 1: Standardize Variables
When each variable is scaled differently, it's not possible to identify true clusters or outliers. First we'll bring the values 
closer to the same center (mean, median, trimean, etc) and spread (standard deviation) using standardization.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler

df_arr = df.values
scaler = StandardScaler() #Std Dev won't match due to degrees of freedom (sample vs population)
print(scaler)
features_std = scaler.fit_transform(cc_arr)
print(scaler.scale_)
```

### Challenges
- Variables that are not continuous (ie. categorical or binary)

Data source
www.wiley.com/go/datasmart

References: John w. Foreman, Data Smart: Using Data Science to Transform Information into Insight
