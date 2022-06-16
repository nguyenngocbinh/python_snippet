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
pip freeze > requirements.txt
```


#### Create environment from jupyter notebook

```python
pip install ipykernel
ipython kernel install --user --name=venv
jupyter notebook
```
 

#### install OFFLINE packages using requirements.txt 
- Input requirements.txt in current directory contain like "jupyter-contrib-nbextensions==0.5.1"
- Create folder `wheelhouse` and run following command 
```python
pip download -r requirements.txt -d wheelhouse
```

- Copy wheels file to another folder if needed and run following command
- dependencies will installed automatic
```
pip install -r requirements.txt --find-links=C:\Users\binhnn2\wheelhouse --no-index
```

- activate `nbextension` (only for nbextension package)

```
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```

#### install ONLINE packages using requirements.txt 
```python
pip install jupyter_contrib_nbextensions
pip install jupyter_nbextensions_configurator
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```
