# test linux environment and versions
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

test default package versions

### Problem description

test default package versions, if I don\'t check scoopy reports when
using issue2docker

### Steps to reproduce the issue

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