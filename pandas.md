# Commonly used transformations in the pandas library

## Renaming columns
### Rename using a list to replace all headers
`new_col_names = ['a', 'b', 'c']`
`df.columns = new_col_names`

### Explicitly rename, if misspelled or non-existent, it will be skipped
`df = df.rename(columns={'a': 'A', 'b':'B','c':'C'})`

## Function for finding a column name
```def find_col(df,col): #case sensitive
    cols = df.columns    
    for x in cols:        
    if col in x:            
    print(x)```
