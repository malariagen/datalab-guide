# Conda environments

Conda environments provide collections of pre-installed software packages. There are two types of conda environments that can be used with MalariaGEN DataLab, described below.

## Shared environments

Shared conda environments are available to all users of MalariaGEN DataLab. Shared conda environments are also accessible from Dask workers and dashboard VMs. Shared conda environments are thus good for:

* When you want to be sure you are using the same collection of software packages and the same versions as someone else you are collaborating with.
* When you are using Dask clusters. 
* When you want to deploy a dashboard.

For example, the "binder-v3.0.0" environment is a shared conda environment that provides a set of useful data science packages.

Shared environments cannot be created or modified by DataLab users. This can only be done by DataLab developers, and requires a redeployment of the service. 

If you would like to create a new shared environment, please start a new discussion in the [datalab-users](https://github.com/orgs/malariagen/teams/datalab-users) forum, describing which software packages and versions you need.

```{warning}
Do not try to use pip install to add new packages into a shared conda environment. This will appear to install the packages, but they will be installed into a separate location in your home directory, and so will not be shared with other users or dask clusters. It can become confusing what versions of packages are available. 

If you need to install packages, create a custom environment, see below.
```

## Custom environments

If you need some packages that are not available in any of the pre-configured shared conda environments, you can create your own custom conda environment, which will be stored in your home directory.

```{note}
Custom environments cannot be shared with other users, and you won't be able to use the environment with dask clusters. It will only be available for running notebooks on your server.
```

To create a new custom environment, open a terminal, and do e.g.:

```
conda create --prefix=/home/jovyan/conda/myenv1 -c conda-forge python=3.7 ipykernel
```

Make sure to include `ipykernel` in the environment, this will make sure the new environment appears in the launcher.

You should see the new environment if you do:

```
conda env list
```

To activate the new environment, use the full environment path, e.g.:

```
conda activate /home/jovyan/conda/myenv1
```

Once activated, you can install any new packages with conda or pip, e.g.:

```
conda install -c conda-forge pandas xarray
pip install malariagen_data
```

You can now exit the terminal. The new environment should appear in the launcher, so you can create a notebook using it.

If you decide you want to get rid of the environment, make sure to shut down any running kernels, then do:

```
conda env remove --prefix=/home/jovyan/conda/myenv1
```

