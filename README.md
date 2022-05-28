# python_snippet

## Pandas

#### clean names
```
X.columns = X.columns.str.translate("".maketrans({"[":"{", "]":"}","<":"^"}))
```
