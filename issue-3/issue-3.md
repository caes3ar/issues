# Issue with mesh generation for gravimetric inversion
### Your environment

```code
```

### Operating System

Mac

### Which Python version are you using?

3.12

### Way of installation

*No response*

### Which version of PyGIMLI are you using?

1.5.4

### Additional information on the environment

*No response*

### Problem description

Hi!

I am trying to use pygimly to perform a gravimetric inversion. The
gravimetric profile i want to invert has a length of about 35
kilometers, but I only need the mesh to be a few hundred meters deep,
and this has brought me issues generating an adequate mesh. Here you can
see my code, I also attach file with the boundaries of the mesh, and an
image showing the mesh I have been able to generate so far. I would
really appreciate if someone has any recomendation on how I can improve
this.

### Steps to reproduce the issue

*No response*

### Code to reproduce the issue

```code
import numpy as np
import pygimli as pg
import pygimli.meshtools as mt

mesh_bounds = np.loadtxt(r'./mesh_bounds.txt', delimiter=',')
mesh_bounds = mesh_bounds.tolist()

topo = mt.createPolygon(mesh_bounds, isClosed=True, marker=1, area=1)
mesh = mt.createMesh(topo, quality=32)
ax, _ = pg.show(mesh)
ax.set_aspect(30)
```

### Additional data to reproduce the issue

[mesh_bounds.txt](https://github.com/user-attachments/files/30504382/mesh_bounds.txt)

### Expected behavior

A mesh that is only a few meters deep.

### Actual behavior

```code
<img width="646" height="252" alt="Image" src="https://github.com/user-attachments/assets/8f086ee1-bd98-454e-b617-7f3774df43b9" />
```
### Output of your script

```code
```