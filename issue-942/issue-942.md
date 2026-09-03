# Error message in LCInversion
### Problem description

I\'m having a problem with the lcinversion function while following the
API reference, but I don\'t understand what\'s causing this error.

### Your environment

```code
pygimli : 1.5.1
            pgcore : 1.5.0
             numpy : 1.24.0
        matplotlib : 3.7.3
             scipy : 1.13.1
              tqdm : 4.66.4
           IPython : 8.15.0
           pyvista : 0.43.8
```

### Operating System

Windows

### Which Python version are you using?

3.9

### Way of installation

*No response*

### Which version of PyGIMLI are you using?

1.5.1

### Additional information on the environment

I\'m using empymod as the EM forward modelling framework in 1D

### Steps to reproduce the issue

*No response*

### Code to reproduce the issue

```code
import matplotlib.pyplot as plt
import pygimli as pg
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.colors as clr
import empymod

rx = np.arange(50., 501., 50)
ry = np.zeros(rx.size)
#rx = np.array([50.])
#ry = np.array([0.]))

txLen = 400
inpdat = {'src': [0, 0, txLen/2, -txLen/2., 0.1, 0.1], 'strength': 1,  # ground
           'mrec': True, 'rec': [rx, ry, -20, 0, 90],  # Hz air
           # 'mrec': False, 'rec': [rx, ry, 0.1, 90, 0],  # Ey ground
          'srcpts': 11, 'htarg': {'pts_per_dec': -1}, 'verb': 1}
freqs = [10., 20, 50, 100, 200, 500, 1000, 2000., 5000.]

def fwd(res, dep):
    """Call empymods function bipole with the above arguments."""
    assert len(res) == len(dep)

depth = [0, 100, 200]  
res = [100, 10, 100]
A0 = fwd(res, depth)
A1 = A0.T
data = np.abs(A1)
relative_error = np.ones_like(data) * 0.01  
data *= (np.random.randn(*data.shape) * relative_error + 1.0)  
    OUT = np.zeros((len(freqs), len(rx)), dtype=complex)
    for i, f in enumerate(freqs):
        OUT[i, :] = empymod.bipole(res=np.concatenate(([2e14], res)),
                                   depth=dep, freqtime=f, **inpdat)
    return OUT

class myFwd(pg.Modelling):
    def __init__(self, depth=None, **kwargs):
        """Initialize the model."""
        if depth is None:
            depth = np.linspace(0., 300., 21)
        self.dep = depth
        self.mesh1d = pg.meshtools.createMesh1D(len(self.dep))
        super().__init__()
        self.setMesh(self.mesh1d)
    def response(self, model):
        """Forward response."""
        A = fwd(model, self.dep)#
        Avec = A.T
        return np.abs(Avec)

depth_fixed = np.linspace(0., 300., 21)
fop = myFwd(depth_fixed)

S1D = pg.frameworks.LCModelling(fop=myFwd) 
inv = pg.frameworks.LCInversion(fop=myFwd, verbose=True)
model = inv.run(data, relative_error, nLayers=4)
```

### Additional data to reproduce the issue

*No response*

### Expected behavior

*No response*

### Actual behavior

When running the final line model = inv.run(data, relative_error,
nLayers=4), an error message pops up.

### Output of your script

```code
---------------------------------------------------------------------------
ArgumentError                             Traceback (most recent call last)
Cell In[78], line 3
      1 S1D = pg.frameworks.LCModelling(fop=myFwd) 
      2 inv = pg.frameworks.LCInversion(fop=myFwd, verbose=True)
----> 3 model = inv.run(data, relative_error, nLayers=4)

File D:\anaconda\envs\adam\lib\site-packages\pygimli\frameworks\inversion.py:1133, in LCInversion.run(self, dataVals, errorVals, nLayers, **kwargs)
   1131 print(kwargs)
   1132 print('#'*50)
-> 1133 return super(LCInversion, self).run(dataVec, errVec, lam=lam, **kwargs)

File D:\anaconda\envs\adam\lib\site-packages\pygimli\frameworks\inversion.py:621, in Inversion.run(self, dataVals, errorVals, **kwargs)
    618         self.setRegularization(**di)
    620 # Triggers update of fop properties, any property to be set before.
--> 621 self.inv.setTransModel(self.fop.modelTrans)  # why from fop??
    622 self.dataVals = dataVals
    623 self.errorVals = errorVals

File D:\anaconda\envs\adam\lib\site-packages\pygimli\frameworks\modelling.py:158, in Modelling.modelTrans(self)
    155 @property
    156 def modelTrans(self):
    157     """Return model transformation."""
--> 158     self._applyRegionProperties()
    159     if self.regionManager().haveLocalTrans():
    160         return self.regionManager().transModel()

File D:\anaconda\envs\adam\lib\site-packages\pygimli\frameworks\modelling.py:362, in Modelling._applyRegionProperties(self)
    360     if rMgr.region(rID).constraintType() != vals['cType']:
    361         self.clearConstraints()
--> 362         rMgr.region(rID).setConstraintType(vals['cType'])
    364 if vals['zWeight'] is not None:
    365     rMgr.region(rID).setZWeight(vals['zWeight'])

ArgumentError: Python argument types in
    None.setConstraintType(Region, list)
did not match C++ signature:
    setConstraintType(GIMLI::Region {lvalue}, unsigned long long type)
```