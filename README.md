# Pandas

#### clean names
```python
X.columns = X.columns.str.translate("".maketrans({"[":"{", "]":"}","<":"^"}))
```

#### binning
```python
df['Cat Age'] = pd.cut(x=df['Age'], bins=[0, 25, 30, 35, 40, 45, 50, 75])
```
#### check dependencies

```python
python -m pip check 
```
