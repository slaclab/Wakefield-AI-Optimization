# HOW TO SETUP WARPX JUPYTER DEV ENVIRONMENT

## WARPX
All physics simulation code is pulled from the [WarpX](https://github.com/ECP-WarpX/WarpX) repository.

## JUPYTER ACCOUNT + SSH SETUP
Before setting up the development environment, create a jupyter account and [connect](https://docs.nersc.gov/connect/) to perlmutter via nersc.

## WARPX INSTALLATION
First, clone the WarpX repository - 

```
git clone git@github.com:ECP-WarpX/WarpX.git
```

OR

```
git clone https://github.com/ECP-WarpX/WarpX.git
```

Build and compile using cmake -

```
cmake .

cmake -S . -B build

cmake --build build -j 4
```

Setup python on perlmutter - 

```
module load python/3.9

python3 -m pip wheel -v .
```

To set up as a python module -

```
export PYTHONUSERBASE=/YOUR_PATH/WarpXPython

python setup.py install --user
```

## CONDA ENVIRONMENT SETUP
Load python version 3.9 as a module -

```
module load python/3.9
```

Create a warpx conda environment -

```
conda create -n warpx -c conda-forge warpx
```

Activate the environment - 

```
conda activate warpx
```

Configure your environment according to WarpX documentation - 

```
conda config --set solver libmamba

mamba install --yes -c conda-forge python ipykernel ipympl matplotlib numpy pandas yt openpmd-viewer openpmd-api h5py fast-histogram dask dask-jobqueue pyarrow

python -m ipykernel install --user --name warpx --display-name warpx

echo -e '#!/bin/bash\nmodule load python\nsource activate warpx\nexec "$@"' > $HOME/.local/share/jupyter/kernels/warpx/kernel-helper.sh

chmod a+rx $HOME/.local/share/jupyter/kernels/warpx/kernel-helper.sh

KERNEL_STR=$(jq '.argv |= ["{resource_dir}/kernel-helper.sh"] + .' $HOME/.local/share/jupyter/kernels/warpx/kernel.json | jq '.argv[1] = "python"')

echo ${KERNEL_STR} | jq > $HOME/.local/share/jupyter/kernels/warpx/kernel.json

conda install --channel conda-forge yt

conda update -y -n base conda
```
