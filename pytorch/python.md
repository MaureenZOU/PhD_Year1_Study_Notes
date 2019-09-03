# Python

### Modules and Import
（糊涂了这么长时间，还是要认真看一波哎）

```Python
# Package: A regular package is typically implemented as a directory containing an __init__.py file.
# the following file system layout defines a top level parent package with three subpackages
parent/
    __init__.py
    one/
        __init__.py
    two/
        __init__.py
    three/
        __init__.py
# Importing parent.one will implicitly execute parent/__init__.py and parent/one/__init__.py. Subsequent imports of parent.two or parent.three will execute parent/two/__init__.py and parent/three/__init__.py respectively.

# python root path is where we execute python command, and all the module we import should count from that directory
```
