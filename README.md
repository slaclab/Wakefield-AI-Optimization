# HOW TO SETUP WARPX JUPYTER DEV ENVIRONMENT

## WARPX
All physics simulation code is pulled from the [WarpX](https://github.com/ECP-WarpX/WarpX) repository.


## CONDA
Follow the conda installation instructions from [this link.](https://warpx.readthedocs.io/en/latest/install/dependencies.html#conda-linux-macos-windows)

## PYTHON WARPX INSTALLATION

Go to the Python subdirectory and run 

```
python setup.py install
```

This installs the Python scripts as a package (named pywarpx) in your standard Python installation (i.e. in your site-packages directory). If you do not have write permission to the default Python installation (e.g. typical on computer clusters), there are two options. The recommended option is to use a virtual environment, which provides the most flexibility and robustness.

Alternatively, add the --user install option to have WarpX installed elsewhere.

```
python setup.py install --user
```

With --user, the default location will be in your home directory, ~/.local, or the location defined by the environment variable PYTHONUSERBASE
