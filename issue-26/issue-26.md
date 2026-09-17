# pygimli 1.6.0-python 3.12-Windows-conda install-no scoopy specified (Install failed) (python 3.13 also failed)
### Your environment

```code
Install failed
```

### Operating System

Windows

### Which Python version are you using?

3.12

### Way of installation

conda

### Which version of PyGIMLI are you using?

1.60

### Additional information on the environment

*No response*

### Problem description

Just test, since pygimli 1.6.0 has some issues with conda install.\
<https://github.com/gimli-org/pyGIMLi/issues/969>\
<https://github.com/gimli-org/pyGIMLi/issues/973>

### Steps to reproduce the issue

conda create -n pg160-conda-312 python=3.12\
conda activate pg160-conda-312\
conda install -c gimli -c conda-forge pygimli=1.6.0

### Code to reproduce the issue

```code
import pygimli as pg
import pgcore
import importlib.metadata

print(pg.__version__)
print(pgcore.__version__)

print(importlib.metadata.version("pygimli"))

# %%
import json
import platform
import sys
from importlib.metadata import distribution
from pathlib import Path

import pgcore
import pygimli as pg


def get_installation_info(package):
    conda_meta = Path(sys.prefix) / "conda-meta"
    conda_records = list(conda_meta.glob(f"{package}-*.json")) if conda_meta.exists() else []

    if conda_records:
        record = json.loads(conda_records[0].read_text())
        return {
            "method": "conda",
            "version": record.get("version", "unknown"),
            "build": record.get("build", "unknown"),
            "channel": record.get("channel", "unknown"),
        }

    dist = distribution(package)
    installer = dist.read_text("INSTALLER")

    return {
        "method": installer.strip() if installer else "unknown",
        "version": dist.version,
        "build": "-",
        "channel": "-",
    }


print("=== System ===")
print("OS:", platform.platform())
print("Python:", sys.version.split()[0])

print("\n=== Installation ===")

for package in ["pygimli", "pgcore"]:
    info = get_installation_info(package)
    print(
        f"{package}: version={info['version']}, "
        f"method={info['method']}, "
        f"build={info['build']}, "
        f"channel={info['channel']}"
    )

print("\n=== pyGIMLi Scooby Report ===")
print(pg.Report())

print("\n=== SuiteSparse-related libraries ===")

search_dirs = [
    Path(pgcore.__file__).parent,
    Path(pgcore.__file__).parent.parent,
    Path(sys.prefix) / "lib",
    Path(sys.prefix) / "Library" / "bin",
]

keywords = ["suitesparse", "umfpack", "cholmod"]
found = set()

for directory in search_dirs:
    if directory.exists():
        for file in directory.rglob("*"):
            if file.is_file() and any(name in file.name.lower() for name in keywords):
                if file not in found:
                    print(file)
                    found.add(file)

if not found:
    print("No SuiteSparse/UMFPACK/CHOLMOD library files found.")
```

### Additional data to reproduce the issue

*No response*

### Expected behavior

*No response*

### Actual behavior

*No response*

### Output of your script

```code
```