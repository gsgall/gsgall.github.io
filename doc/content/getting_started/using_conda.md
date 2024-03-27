# Using Conda

Every project has different dependencies in order to make life a bit easier and ensure that there are no pontetial conflicts between project dependencies we need a package manager. A great manager is Anaconda. Anaconda allows you to create virtual environments and install, update, and uninstall different packages for different projects. It is reccomended that you create a different Anaconda environment for each project. Not only does this help prevent potential conflicts between projects it also provides an easy to way to install other projects for use in your project if they are available as a Anaconda package. To install Anaconda by following the instructions on the MOOSE website.
- [https://mooseframework.inl.gov/getting_started/installation/conda.html](https://mooseframework.inl.gov/getting_started/installation/conda.html)

This link has complete install instructions for MOOSE but you can stop after you have entered the following command

```bash
  export PATH=$HOME/miniforge/bin:$PATH
```

To create a new conda environment you can use the following command.

```bash
  conda create --name myenv
```

You can enter this environment using the activate command.

```bash
  conda activate myenv
```

To exit the environment you must use the deactivate command.

```bash
  conda deactivate
```

To remove the environement you can use the follow commands.

```bash
  conda activate base
  conda env remove -n myenv
```
