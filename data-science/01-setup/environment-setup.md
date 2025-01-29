## Python versions

> Note: For Windows only (assuming multiple versions of Python are installed and added to PATH).

<br>

#### List Python Versions

```shell
py --list
```

<br>

#### Using Specific Python Version

> Using 3.13 for example: 

```shell
py -3.13 --version
```

<br>

---

<br>

## Activate Virtual Environment

> Run this command in the root of project directory

```shell
py -3.13 -m venv venv/
```

<br>

> Activate (Windows)

```shell
source venv/Scripts/activate
```

<br>

> Activate (Linux)

```shell
source venv/bin/activate
```

> If these commands do not work, follow the [official guide](https://docs.python.org/3/tutorial/venv.html) for activating.

<br>

---

<br>

## Install Packages

> Current packages I use (Update as needed):

- `numpy`: For numerical operations.
- `scipy`: For scientific computing tasks.
- `pandas`: For data manipulation and analysis.
- `matplotlib`: Core plotting library.

- `jupyter`: Core notebook functionality.
- `jupyterlab`: Enhanced notebook interface.
- `notebook`: Jupyter notebook server.
- `ipython`: Interactive Python shell.
- `ipywidgets`: Interactive widgets for Jupyter notebooks.
- `nbconvert`: Convert notebooks to other formats.

```shell
pip install pandas numpy scipy matplotlib jupyter jupyterlab notebook ipython ipywidgets nbconvert
```