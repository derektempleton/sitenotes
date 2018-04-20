# Commonly used transformations in the pandas library

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
```python
df = df.pivot_table(index = 'a',
    columns = 'b',
    values = 'c',
    fill_value = 0,
    aggfunc=np.sum).reset_index()
```

# Data types and changing between them
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

# Filtering / Subsetting dataframes
Dealing with numbers vs strings and multiple combos
iloc vs loc
What is that subsetting warning?

# Merging dataframes

# Arthemtic between columns
```python
df['calc'] = df['a'] + df['b']
```

# Cleansing data fields
str.zfill(4)
str.replace

# Pandas column to hashkey using hashlib
Better to use hmac module
```python
df['new'] = [hashlib.md5(val.encode('utf-8')).hexdigest() for val in df[1]]
```
