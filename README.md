# 1. Setup environment
## 1.1. Using **conda**

### 1.1.1. Create conda environment

```python
conda create -n python38 python=3.8.5 pip=20.2.4 ipykernel notebook
conda activate python38
 
conda create -n python36 python=3.6.8 pip=20.2.4 ipykernel notebook
conda activate python36
```

### 1.1.2. Conda environment list
```python
conda info --env
```

### 1.1.3. Remove conda environment

```python
conda deactivate
conda env remove -n python36
```

### 1.1.4. Activate conda environment

```python
conda activate python38
```


## 1.2. Create environment for jupyter notebook

### 1.2.1. create

```python
conda activate python38
ipython kernel install --user --name=python38

conda activate python36
ipython kernel install --user --name=python36
```
 

### 1.2.2. Remove jupyter notebook environment (require run as administrator)

```python
jupyter kernelspec list
jupyter kernelspec uninstall python36 
```

# 2. Install packages

## 2.1. Install OFFLINE packages using requirements.txt 

- Step 1: Input to `requirements.txt` file in current directory.  Eg. content `"jupyter-contrib-nbextensions==0.5.1"`

- Step 2: Create folder `wheel` (Eg. D:\wheel)

- Step 3: Run following command to download dependencies packages to folder `wheel`

```python
pip download -r requirements.txt -d wheel
```

- Step 4: Run following command to install


```
pip install -r requirements.txt --find-links=D:\wheel --no-index
```

## 2.2. Install OFFLINE Linux package

Activate same version python (i.e 3.7.0) and type command following

```
pip download --platform manylinux1_x86_64 --only-binary=:all: --no-binary=:none: pandas
```


# 3. Install Extension for jupyter notebook

- nbextension

```
pip install jupyter_contrib_nbextensions
pip install jupyter_nbextensions_configurator
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```

# 4. Other ultilities command

#### check dependencies

```
python -m pip check 
pip freeze > requirements.txt
```

#### install pycaret

```
pip install pycaret --use-feature=2020-resolver
```

#### Themes

```
jt -t onedork -fs 13 -altp -tfs 14 -nfs 14 -cellw 88% -T
```


# 5. Pandas

- clean names

```python
X.columns = X.columns.str.translate("".maketrans({"[":"{", "]":"}","<":"^"}))
```

- rename

```python
df.columns = df.columns.str.lower()
```

- binning

```python
df['Cat Age'] = pd.cut(x=df['Age'], bins=[0, 25, 30, 35, 40, 45, 50, 75])
```

- groupby stratify

```python
df.groupby('target', group_keys=False).apply(lambda x: x.sample(frac=0.8))  
```

- read data

```python
appended_data = []
for infile in glob.glob("*.xlsx"):
    data = pandas.read_excel(infile)
    # store DataFrame in list
    appended_data.append(data)

# Use pd.concat to merge a list of DataFrame into a single big DataFrame.
appended_data = pd.concat(appended_data)
appended_data = [df.set_index('ID') for df in appended_data]
appended_data = pd.concat(appended_data)
```

- filter

```python
df[~df['name'].isin(list1)]
df[df['name'].isna()]
df[df['name'].notna()]
```

- convert

```python
# pd.to_numeric
# pd.factorize
# df['STRING'].astype(str)
# pd.to_datetime(df['DATE'], format='%d%m%Y')
```

- Excel date

```python
import functools as ft
fn_convert_date = ft.partial(xlrd.xldate_as_datetime, datemode=0)
df['DATE'].apply(fn_convert_date).dt.year
```
- aggregate

```python
df = df.groupby('ID').agg('first')
```

# 6. Join

#### reduce merge

- `pandas.concat`

```python
dfs = [df0, df1, df2, ..., dfN]
dfs = [df.set_index('name') for df in dfs]
# cant not run if index not unique 
dfs = pd.concat(dfs, join='outer', axis = 1) 
```


- `functools.reduce`

```python
# still run with index not unique 
import functools as ft
df_final = ft.reduce(lambda left, right: pd.merge(left, right, on='name', how = 'outer'), dfs)
```
- `join`

```python
# cant not run if index not unique 
dfs = [df.set_index('name') for df in dfs]
dfs[0].join(dfs[1:], how = 'outer')
```
# 7. Files and folder

```python
list_files = glob.glob(".data/*.xlsx")
```

# 99. Equivalent R

- `functools` ~ `purrr`



 





