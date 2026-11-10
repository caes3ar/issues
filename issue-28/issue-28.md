# test pip install pygimli 1.6.1
### Your environment

```code
--------------------------------------------------------------------------------
  Date: Tue Nov 10 10:00:46 2026 UTC

                OS : Windows (11 10.0.26300 SP0 Multiprocessor Free)
            CPU(s) : 14
           Machine : AMD64
      Architecture : 64bit
               RAM : 31.4 GiB
       Environment : Python

  Python 3.13.9 | packaged by Anaconda, Inc. | (main, Oct 21 2025, 19:09:58)
  [MSC v.1929 64 bit (AMD64)]

           pygimli : 1.6.1
            pgcore : 1.6.0
             numpy : 2.5.4
        matplotlib : 3.11.2
             scipy : 1.17.1
              tqdm : 4.70.1
           IPython : 9.18.1
            meshio : 5.3.5
            tetgen : 0.8.4
           pyvista : 0.49.2
--------------------------------------------------------------------------------
```

### Operating System

Windows

### Which Python version are you using?

3.13

### Way of installation

pip

### Other way of installation

*No response*

### Which version of PyGIMLI are you using?

Other version, please specify below

### Additional information on the environment

1.6.1

### Problem description

pygimli.meshtools.grid.appendTetrahedronBoundary problem?

RuntimeError: tetgen binary not found in PATH\
ValueError: pyvista.get_reader does not support\
a file with the .poly extension\
OSError: This file was not able to be\
automatically read by pyvista.

> where.exe tetgen\
> INFO: Could not find files for the given pattern(s).

### Steps to reproduce the issue

Open terminal:

> python -m venv pg161-pip \--prompt=pg161-pip\
> .\\pg161-pip\\Scripts\\Activate.ps1\
> python -m pip install \--upgrade pip\
> python -m pip install \"pygimli\[all\]==1.6.1\"\
> python -c \"import pygimli as pg; pg.test(show=False)\"\
> python \--version\
> python -c \"import pygimli as pg; print(pg.**version**)\"\
> python -c \"import pygimli as pg; print(pg.Report())\"\
> python -c \"import tetgen; print(tetgen.**version**)\"

### Code to reproduce the issue

```code
import pygimli as pg
import tetgen

print(pg.__version__)
print(pg.Report())
pg.test(show=False)
print(tetgen.__version__)
```

### Additional data to reproduce the issue

*No response*

### Expected behavior

*No response*

### Actual behavior

### Output of your script

```code

====================================================== FAILURES =======================================================
_____________________________ [doctest] pygimli.meshtools.grid.appendTetrahedronBoundary ______________________________
563 :py:mod:`pygimli.meshtools.appendBoundary`,
564 :py:mod:`pygimli.meshtools.appendTriangleBoundary`
565
566 Examples
567 --------
568 >>> import pygimli as pg
569 >>> import pygimli.meshtools as mt
570 >>> grid = mt.createGrid(5,5,5)
571 ...
572 >>> mesh = mt.appendBoundary(grid, xbound=5, ybound=5, zbound=5,
UNEXPECTED EXCEPTION: OSError("This file was not able to be automatically read by pyvista.\n  'C:\\\\Users\\\\hitrz\\\\AppData\\\\Local\\\\Temp\\\\tmpvr35_mij.poly'")
Traceback (most recent call last):
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\mesh.py", line 152, in createMesh
    mesh = createMeshTetgen(poly, quality=quality, area=area,
                            verbose=verbose, syscall=syscall,
                            **kwargs)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\mesh.py", line 221, in createMeshTetgen
    raise RuntimeError(f"{tetgenBin} binary not found in PATH")
RuntimeError: tetgen binary not found in PATH
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\fileio.py", line 557, in _read_dispatch
    reader = pv.get_reader(filename, force_ext)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\reader.py", line 186, in get_reader
    raise ValueError(msg)
ValueError: `pyvista.get_reader` does not support a file with the .poly extension
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\fileio.py", line 568, in _read_dispatch
    return read_meshio(filename)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\fileio.py", line 1462, in read_meshio
    mesh = meshio.read(filename, file_format)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\meshio\_helpers.py", line 71, in read
    return _read_file(Path(filename), file_format)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\meshio\_helpers.py", line 96, in _read_file
    possible_file_formats = _filetypes_from_path(path)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\meshio\_helpers.py", line 56, in _filetypes_from_path
    raise ReadError(f"Could not deduce file format from path '{path}'.")
meshio._exceptions.ReadError: Could not deduce file format from path 'C:\Users\hitrz\AppData\Local\Temp\tmpvr35_mij.poly'.
During handling of the above exception, another exception occurred:
Traceback (most recent call last):
  File "C:\Users\hitrz\anaconda3\Lib\doctest.py", line 1398, in __run
    exec(compile(example.source, filename, "single",
    ~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                 compileflags, True), test.globs)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "<doctest pygimli.meshtools.grid.appendTetrahedronBoundary[3]>", line 1, in <module>
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\grid.py", line 191, in appendBoundary
    return appendTetrahedronBoundary(mesh, **kwargs)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\grid.py", line 596, in appendTetrahedronBoundary
    boundMesh = pg.meshtools.createMesh(boundaryBox + meshBoundary)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\mesh.py", line 157, in createMesh
    mesh = createMeshTetgen(poly, quality=quality, area=area,
                            verbose=verbose, syscall=False,
                            **kwargs)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\mesh.py", line 245, in createMeshTetgen
    tet = tg.TetGen(plcFname)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\tetgen\pytetgen.py", line 221, in __init__
    mesh = pv.read(arg0)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\_deprecate_positional_args.py", line 204, in inner_f
    return f(*args, **kwargs)
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\fileio.py", line 442, in read
    result = _read_dispatch(
        filename,
    ...<4 lines>...
        **kwargs,
    )
  File "C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pyvista\core\utilities\fileio.py", line 570, in _read_dispatch
    raise OSError(msg)
OSError: This file was not able to be automatically read by pyvista.
  'C:\\Users\\hitrz\\AppData\\Local\\Temp\\tmpvr35_mij.poly'
C:\Users\hitrz\Desktop\CAESAR\test pygimli version install method\pygimli-pip-161\pg161-pip\Lib\site-packages\pygimli\meshtools\grid.py:572: UnexpectedException
================================================= slowest 5 durations =================================================
5.86s call     pg161-pip/Lib/site-packages/pygimli/testing/test_PhysicsManagers.py::TestManagers::test_ERT
4.77s call     pg161-pip/Lib/site-packages/pygimli/testing/test_Perf.py::TestPerf::test_Performance
3.48s call     pg161-pip/Lib/site-packages/pygimli/testing/test_show.py::TestShow::test_ShowVariants
3.37s call     pg161-pip/Lib/site-packages/pygimli/meshtools/grid.py::pygimli.meshtools.grid.appendTriangleBoundary
2.18s call     pg161-pip/Lib/site-packages/pygimli/testing/test_PhysicsManagers.py::TestManagers::test_VES
=============================================== short test summary info ===============================================
FAILED pg161-pip/Lib/site-packages/pygimli/meshtools/grid.py::pygimli.meshtools.grid.appendTetrahedronBoundary
===================================== 1 failed, 229 passed, 15 skipped in 42.67s ======================================
```