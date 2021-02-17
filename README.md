```bash
git clone https://github.com/Htnek/environment.git
```
```bash
conda env create -f environment.yml
```
```bash
conda activate tf2
```
```bash
python -m ipykernel install --user --name=python3
```
Update environment
```bash
conda activate tf2
```
```bash
conda env update --file environment.yml  --prune
```
