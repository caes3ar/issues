# Test pg160 on Linux, full issue version
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
            pgcore : 1.5.4
             numpy : 2.3.5
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

conda create -n pg160 -c gimli -c conda-forge pygimli=1.6.0

### Which version of PyGIMLI are you using?

1.6.0

### Additional information on the environment

*No response*

### Problem description

Version control based on:
<https://github.com/caes3ar/Example_issues/issues/1>

### Steps to reproduce the issue

*No response*

### Code to reproduce the issue

```code
import importlib.metadata
import sys

import pgcore
import pygimli as pg

print(pg.Report())

print("\n=== Python environment ===")
print("Python executable:", sys.executable)

print("\n=== Imported files ===")
print("pygimli file:", pg.__file__)
print("pgcore file:", pgcore.__file__)

print("\n=== Version information ===")
print("pygimli.__version__:", pg.__version__)
print("pg.versionStr():", pg.versionStr())

try:
    print(
        "metadata pygimli:",
        importlib.metadata.version("pygimli"),
    )
except importlib.metadata.PackageNotFoundError:
    print("metadata pygimli: not found")

try:
    print(
        "metadata pgcore:",
        importlib.metadata.version("pgcore"),
    )
except importlib.metadata.PackageNotFoundError:
    print("metadata pgcore: not found")


# %%
import numpy as np
import pygimli as pg
import pygimli.meshtools as mt
import matplotlib.pyplot as plt

mesh_bounds = np.loadtxt(r'./mesh_bounds.txt', delimiter=',')
mesh_bounds = mesh_bounds.tolist()

topo = mt.createPolygon(mesh_bounds, isClosed=True, marker=1, area=1)
mesh = mt.createMesh(topo, quality=32)
ax, _ = pg.show(mesh)
ax.set_aspect(30)
ax, _ = pg.show(mesh)
ax.set_aspect(30)

plt.savefig("mesh.png", dpi=300, bbox_inches="tight")
plt.close()
```

### Additional data to reproduce the issue

[mesh_bounds.txt](https://github.com/user-attachments/files/30746708/mesh_bounds.txt)

### Expected behavior

Just test the pygimli 1.6.0 on Linux, and use the mesh example

### Actual behavior

pgcore 1.5.4 is a typo in scoopy report, because \'conda list\' shows
pgcore is 1.6.0.

But:\
/home/zren/miniforge3/envs/pg160/lib/python3.13/site-packages/pygimli/viewer/showmesh.py:113:
UserWarning: A NumPy version \>=1.23.5 and \<2.3.0 is required for this
version of SciPy (detected version 2.3.5)\
from scipy.sparse import spmatrix

```code
<img width="646" height="252" alt="Image" src="https://github.com/user-attachments/assets/44fb400e-c6e1-4e1d-a0ea-0809b4ad4ea6" />
```
### Output of your script

```code
(pg160) [zren@**** caesar]$ python test.py 

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
            pgcore : 1.5.4
             numpy : 2.3.5
        matplotlib : 3.11.1
             scipy : 1.14.1
              tqdm : 4.70.0
           pyvista : 0.48.4
--------------------------------------------------------------------------------

=== Python environment ===
Python executable: /home/zren/miniforge3/envs/pg160/bin/python

=== Imported files ===
pygimli file: /home/zren/miniforge3/envs/pg160/lib/python3.13/site-packages/pygimli/__init__.py
pgcore file: /home/zren/miniforge3/envs/pg160/lib/python3.13/site-packages/pgcore/__init__.py

=== Version information ===
pygimli.__version__: 1.6.0
pg.versionStr(): libgimli-v1.6.0
metadata pygimli: 1.6.0
metadata pgcore: 1.5.4
/home/zren/miniforge3/envs/pg160/lib/python3.13/site-packages/pygimli/viewer/showmesh.py:113: UserWarning: A NumPy version >=1.23.5 and <2.3.0 is required for this version of SciPy (detected version 2.3.5)
  from scipy.sparse import spmatrix
```