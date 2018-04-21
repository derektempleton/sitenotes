# Local Outlier Factor

Using Local Outlier Factor (LOF) is handy when you are looking for an unsupervised approach to identifying outliers in a 2D matrix. One-class SVM or Tukey fences 
are great for identifying outliers in 1D space, when data is normally distributed and the outlier is an extreme value on the distribution. 
However, many real-life business problems are more complex. In credit card fraud or call center examples, we do not have the
classification of whether a transaction is actually fraudulent or a specific call center representative is under-performing relative 
to his or her peers. This is where LOF comes in.  

### Step 1: Standardize Variables
When each variable is scaled differently, it's not possible to identify true clusters or outliers. First we'll bring the values 
closer to the same center (mean, median, trimean, etc) and spread (standard deviation) using standardization.

```python
df_arr = df.values
# 
```

### Challenges
- Variables that are not continuous (ie. categorical or binary)

Data source
www.wiley.com/go/datasmart

References: John w. Foreman, Data Smart: Using Data Science to Transform Information into Insight
