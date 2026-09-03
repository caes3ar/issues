# qt.qpa.plugin: Could not find the Qt platform plugin "wayland" in ""
### Problem description

Attempts to run the \"2D Refraction modelling and inversion\" example

<https://www.pygimli.org/_examples_auto/2_seismics/plot_01_refraction_manager.html#sphx-glr-examples-auto-2-seismics-plot-01-refraction-manager-py>

generate the following output during the \"Model setup\"

    >>> layer1 = mt.createPolygon([[0.0, 137], [117.5, 164], [117.5, 162], [0.0, 135]],
    ...                           isClosed=True, marker=1, area=1)
    >>> layer2 = mt.createPolygon([[0.0, 126], [0.0, 135], [117.5, 162], [117.5, 153]],
    ...                           isClosed=True, marker=2)
    >>> layer3 = mt.createPolygon([[0.0, 110], [0.0, 126], [117.5, 153], [117.5, 110]],
    ...                           isClosed=True, marker=3)
    >>> 
    >>> geom = layer1 + layer2 + layer3
    >>> 
    >>> # If you want no sloping flat earth geometry .. comment out the next 3 lines
    >>> # geom = mt.createWorld(start=[0.0, 110], end=[117.5, 137],
    >>> #                       layers=[137-2, 137-11])
    >>> # slope = 0.0
    >>> 
    >>> pg.show(geom)
    qt.qpa.plugin: Could not find the Qt platform plugin "wayland" in ""
    (<Axes: xlabel='$x$ in m', ylabel='$y$ in m'>, None)
    >>> 
    >>> mesh = mt.createMesh(geom, quality=34.3, area=3, smooth=[1, 10])
    >>> ax, _ = pg.show(mesh)
    >>> 

Prior to getting to that point there were errors from \"import numpy as
np\", specifically

\"libcholmod.so.3: cannot open shared object file: No such file or
directory\"

and

\"libumfpack.so.5: cannot open shared object file: No such file or
directory\"

both of which were resolved by running \"conda install suitesparse=5\"
as mentioned in #721 and #838. Interestingly (to me anyway\...I\'m new
to python, miniconda, and pygimli), I just issued \"quit()\" at the
python prompt at the end of the output I included above and the images
shown in the \"Model setup\" section rendered where they hadn\'t before
I ran \"conda install suitesparse=5\". Before running \"conda install
suitesparse=5\" I tried resolving the \"libcholmod.so.3\" and\
\"libumfpack.so.5\" by creating symbolic links, i.e.

ln -s libcholmod.so.5.3.1 libcholmod.so.3

and

ln -s libumfpack.so.6.3.5 libumfpack.so.5

### Your environment

```code
--------------------------------------------------------------------------------
  Date: Tue Feb 17 20:09:25 2026 UTC

                OS : Linux (Ubuntu 22.04)
            CPU(s) : 4
           Machine : x86_64
      Architecture : 64bit
       Environment : Python

  Python 3.11.9 | packaged by conda-forge | (main, Apr 19 2024, 18:36:13) [GCC
  12.3.0]

           pygimli : 1.5.5
            pgcore : 1.5.0
             numpy : 1.26.4
        matplotlib : 3.10.8
             scipy : 1.14.1
              tqdm : 4.67.3
           pyvista : 0.44.1
--------------------------------------------------------------------------------
```

### Operating System

Linux

### Which Python version are you using?

3.11

### Way of installation

conda create -n pg -c gimli -c conda-forge \"pygimli\>=1.5.0\"

### Which version of PyGIMLI are you using?

1.5.4

### Additional information on the environment

WRT \"Which version of PyGIMLI are you using?\" above, the version
reported by \"print(pygimli.**version**)\" is \"1.5.5\"; note that I ran
\"conda update -c gimli -c conda-forge pygimli\", after running \"conda
install suitesparse=5\".

### Steps to reproduce the issue

*No response*

### Code to reproduce the issue

```code
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