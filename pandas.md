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



