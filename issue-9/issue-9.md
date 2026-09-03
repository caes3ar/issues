# @pg.cache decorator hides docstring of original function
### Problem description

\@pg.cache decorator hides docstring of original function

### Operating System

Windows

### Optionally add details on your operating system

*No response*

### Which Python version are you using?

3.14

### Python version if not in the list

*No response*

### Which version of PyGIMLI are you using?

1.5.4

### Code to reproduce

```code
import pygimli

help(pygimli.physics.ert.createGeometricFactors)
```

### Expected behavior

Show docstring.

### Actual behavior

    Help on function wrapper in module pygimli.utils.cache:

    wrapper(*args, **kwargs)

test