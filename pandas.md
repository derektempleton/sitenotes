# Commonly used transformations in the pandas library

## Importing data into Pandas

### Importing CSV Files
Also see: [https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html](Pandas Documentation)
```python
df = pd.read_csv(path + 'csv_file.csv', encoding = 'utf-8', sep = '\t') # tab delimited
```
### Importing Excel Files
```python
import pandas as pd
df = pd.read_excel(path + 'excel_file.xlsx')
```

### Importing Several CSV Files
```python
import glob
path = '/myfolder'
all_files = glob.glob(path + "/*.csv") #Be careful of temp files in folder that begin with '~$'
frame = pd.DataFrame()
df_list = []
row_cnt = 0

for f in all_files:
    df = pd.read_csv(f, index_col=None, dtype=object, encoding='ISO-8859-1') #imports all fields as object (str)
    row_cnt += df.shape[0]
    print('File: ',f,'Dataframe Shape: ',df.shape,'Row Tally: ', row_cnt)
    df_list.append(df)

df_concated = pd.concat(df_list)
df_concated.shape
```

## Data Quality and Understanding DataFrame
```python
import pandas_profiling
import pydqc
df.describe()
df.info()
df.dtypes
df.hist(bins=50, figsize=(20,15)) #visualize variables in histogram
```

## Renaming columns
### Rename using a list to replace all headers
```python
new_col_names = ['a', 'b', 'c']`
df.columns = new_col_names
```

### Explicitly rename, if misspelled or non-existent, it will be skipped
```python
df = df.rename(columns={'a': 'A', 'b':'B','c':'C'})
```

## Function for finding a column name
```python
def find_col(df,col): #case sensitive
    cols = df.columns    
    for x in cols:        
        if col in x:            
        print(x)
```
## Pivot Tables
Reset the index after to get single header column.
Be careful with NaNs. There is no "Blanks" like in Excel pivot tables, NaN rows will not be included.
```python
df = df.pivot_table(index = 'a',
    columns = 'b',
    values = 'c',
    fill_value = 0,
    aggfunc=np.sum).reset_index()
```

## Output results to json format
```python
df_group.to_json(orient='records')
```

### Groupby
```python
df.groupby(['col_1'])['col_2_be_summed'].sum()
```

## Dates

### Formatting Dates
Filtering a dataframe by start and end dates
Also see all possible strftime formatting options with examples here: http://strftime.org/
```python
month_offset = 3 # 3 months back from today
current_month = pd.Timestamp(pd.Timestamp.now().strftime('%Y-%m'))
start_month = current_month - pd.DateOffset(months=month_offset)
end_month = start_month + pd.DateOffset(months=1) - pd.DateOffset(days=1)
df = df[(df['Paid Date'] >= start_month) & (df['Paid Date'] < end_month)]
print(current_month, start_month, end_month)
```


## Data types and changing between them
df.dtypes
.astype(int) or astype(str)
.to_numeric function
```python
type_conversion = {
'numeric':[
    'int_col_1','int_col_2'
    ],
'date':[
    'date_col_1','date_col_2'
    ]
}
for cat in type_conversion.keys():
    for c in type_conversion[cat]:
        if(cat == 'numeric'):
            df[c] = pd.to_numeric(df[c], errors='coerce')
        elif (cat == 'date'):
            df[c] = pd.to_datetime(df[c], errors='coerce')
```
## Converting Categorical to Numerical Vales

```python
df['category_col'] = df['category_col'].astype('category')
df.dtypes # check conversion
cat_columns = df.select_dtypes(['category']).columns
df[cat_columns] = legal_df[cat_columns].apply(lambda x: x.cat.codes)
```
OR

```python
cat_mapping = {'Highest' : 1,
                'Mid' : 2
                'Lowest' : 3}
cat_column = 'category_col'
legal_df[cat_column] = legal_df[cat_column].map(cat_mapping)
legal_df[cat_column] = legal_df[cat_column].fillna(0)
```

# Filtering / Subsetting dataframes
Dealing with numbers vs strings and multiple combos
iloc vs loc
What is that subsetting warning?
```python
df = df[df['A' == 2]]
```

Subsetting multiple values
subset_list = [1,5,9]
subset_df = df[df.isin(subset_list)]

# Counting values
df['col'].value_counts()
Applying filter and counting values
df[df['col1'] > 10][col2].value_counts()

# Merging dataframes

# Arthemtic between columns
```python
df['calc'] = df['a'] + df['b']
```
### Multiplying conditionally
```python
# Copy the column first (covers if false)
df['AMOUNT_CAD'] = df['AMOUNT']
# Create the condition (covers if true), then multiply the remaining slice
df.loc[df['CURR_CODE'] == 'USD', 'AMOUNT_CAD'] = df['AMOUNT']*1.3
# Other examples applying multiple conditions
df['amount_group'] = '<100'
df.loc[df['amount'] < 100,'amount_group'] = '<100'
df.loc[(df['amount'] > 50) & (df['amount'] < 100), 'amount_group'] = '>50'
df.loc[df['amount'] < 50,'amount_group'] = '<50'
```


# Cleansing data fields
str.zfill(4)
str.replace

# Pandas column to hashkey using hashlib
Better to use hmac module
```python
df['new'] = [hashlib.md5(val.encode('utf-8')).hexdigest() for val in df[1]]
```
# Pandas to JSON

'''python
df.to_json(path, orient='records')
```
