## Basics & Commands
`uv` &rarr; rust based library that make python environment setup easy

`brew install uv` &rarr; installation command

`uv --version` &rarr; gives version

`uv python list` &rarr; installable python version

`uv python install 3.8` &rarr; install this version

`uv python find <version>`

`uv python uninstall <version>`

## Main Commands
`uv init` &rarr; initializes the `.toml` file which is used by uv

`uv run main.py` &rarr; runs the python file with the env

`uv add <package>` &rarr; add packages into env/uv

`uv remove <package>` &rarr; remove packages into env/uv

`uv sync` &rarr; sync the `.toml` file and `.venv` env

`uv lock` &rarr; create the lock file

`uv venv .venv --python 3.12` &rarr; create env with a particular version

`uv run which python` &rarr; shows the route of the python used by uv

## MacOS
> remember that if i install into the env it doesn't automatically update in the `toml` file. it only updates the `toml` changes into the env. also the uv package doesn't have pip

```bash
# only using the uv package to install custom python version
uv venv .venv --python 3.12
uv add pip
pip install <packages>
uv run main.py
```

## Normal Environtment
```python
python -m venv <name> # convention is .venv
source .venv/bin/activate
pip install <package_name>
pip freeze > requirements.txt
pip install -r requirements.txt
```
