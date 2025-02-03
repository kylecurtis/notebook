## Zed Resources

https://zed.dev/docs/repl

<br>

---

<br>

## Setup Virtual Environment

```shell
python -m venv venv/
```

```shell
source venv/bin/activate
```

<br>

---

<br>

## Install Packages

```shell
pip install jupyter ipykernel
```

<br>

---

<br>

## Install Kernel

```shell
python -m ipkernel install --user --name env --display-name "Python (env)"
```

<br>

---

<br>

## Testing REPL

test.py

```py
# %%
print("Hello from the REPL!")
```

> NOTE: Run zed command: "repl: run"

<br>

---

<br>

## Remove Kernel

> If you want to remove the kernel installed in previous steps (env):

```shell
jupyter kernelspec uninstall env
```

