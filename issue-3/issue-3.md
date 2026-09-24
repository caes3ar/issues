# Show pygimli scoopy report
### Your environment

```code
--------------------------------------------------------------------------------
  Date: Wed Aug 05 13:42:06 2026 UTC

                OS : Linux (Rocky Linux 10.2)
            CPU(s) : 2
           Machine : x86_64
      Architecture : 64bit
       Environment : Python

  Python 3.13.14 | packaged by conda-forge | (main, Jun 12 2026, 09:50:25)
  [GCC 14.3.0]

           pygimli : 1.6.0
            pgcore : 1.6.0
             numpy : 2.2.6
        matplotlib : 3.11.1
             scipy : 1.14.1
              tqdm : 4.70.0
           pyvista : 0.48.4
--------------------------------------------------------------------------------
```

### Operating System

Linux

### Which Python version are you using?

3.13

### Way of installation

pip

### Which version of PyGIMLI are you using?

1.6.0

### Additional information on the environment

*No response*

### Problem description

Hi!

I am testing pygimli 1.6.0 Linux pip install with python 3.13.

### Steps to reproduce the issue

*No response*

### Code to reproduce the issue

```code
# %%
import importlib.metadata

# %%
import sys

# %%
import pygimli
import pygimli as pg

# %%
import pgcore

# %%
import numpy
import scipy

# %%
print(pg.Report())

# %%
print(sys.version)
print(pg.__version__)
print(pg.versionStr())
print(pg.__file__)
print(pgcore.__file__)
print(numpy.__version__)
print(scipy.__version__)

# %%
#### for later test version 20260917 ########
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

Test bot (later add some txt file)

### Expected behavior

### Actual behavior

Test (bot cannot reproduce the image link yet)

### Output of your script

```code
```