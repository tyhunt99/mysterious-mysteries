# Importing extra modules

## Background

This was discovered when trying to cleanup imports in a django project to meet pep8 standards. During the cleanup I decided to reduce number of import lines and instead of using a from module import submodule I simply did import module. Then in code I tried to use module.submodule... to use the utility function I wanted.

So I changed from this:

```
import module

from module import submodule

...
mdoule.anothersubmodule.func()
...
submodule.func()

```

To this:
```
import module

...
mdoule.anothersubmodule.func()
...
module.submodule.func()

```

This did not work as expected. Upon inspection the `module` was not importing `submodule` in its `__initi__.py` so it was not being exposed. 

## Quirk

The quirk comes out when I account for this. As expected in an interactive shell running:
```
import module
module.submodule.func()
```
Errors out with `module object has no attribute 'submodule'`

However when I run:
```
import module
from module import submodule

module.submodule.func() . # works
submodule.func() . # works
```
Both work,

And again running:
```
from module import submodule

module.submodule.func() . # does not work
submodule.func()  # works
```

So python will apparently add it to the top level module object if it exists.
