# python_snippet

## Pandas

#### clean names
```
X.columns = X.columns.str.translate("".maketrans({"[":"{", "]":"}","<":"^"}))
```

#### binning
```
df['Cat Age'] = pd.cut(x=df['Age'], bins=[0, 25, 30, 35, 40, 45, 50, 75])
```
#### check dependencies

```
python -m pip check 
```
