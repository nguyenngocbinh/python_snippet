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

## create with specify packages
#### Create environment from jupyter notebook

```python
pip install ipykernel
ipython kernel install --user --name=venv
jupyter notebook
```

# conda environment
## create
```python
conda create -n python38 python=3.8.5 pip=20.2.4 ipykernel notebook
conda activate python38
 
conda create -n python36 python=3.6.8 pip=20.2.4 ipykernel notebook
conda activate python36
``
 

## to remove conda environment
```python
conda deactivate
conda env remove -n python36
```

## conda environment list
```python
conda info --env
```
 

## jupyter notebook environment
#### create
```python
conda activate python38
ipython kernel install --user --name=python38

conda activate python36
ipython kernel install --user --name=python36
```
 

#### remove (require run as administrator)

```python
jupyter kernelspec list
jupyter kernelspec uninstall python36 
```
 

#### install pycaret

```python
pip install pycaret --use-feature=2020-resolver
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
