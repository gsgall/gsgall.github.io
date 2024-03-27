# Dependency on MOOSE

Since this system relies on the MOOSE documentation system you will need MOOSE installed to build and host the documentation site locally. We expect you to have MOOSE installed  at `~/projects/moose` if you would like to do this. MOOSE can be downloaded from [here](https://mooseframework.inl.gov/getting_started/installation/index.html).

# Building an Interavtive View

The MOOSEDocs system is designed to have an interactive view so when you modify the content of a file your site will reflect those changes if you are serving the site locally. However, you will have to re-serve your site if you have added a new page or tab to the site. To serve the site locally you can use these instructions.

!alert warning title=Project Specific Commands
The commands on this site are specific to the code standards website and you will need to adjust the first line of the following commands for your project.

```bash
cd ~/projects/code-standards/doc
MOOSE_DIR=~/projects/moose ROOT_DIR=./ ./moosedocs.py build --serve
```

# Manual Update

The changes you push to the code standards site will not automatically be reflected on the website. If you would like to udpate the site you will need to push some changes to the `gh-pages` branch of the site. To do you can use the following commands. Assuming you have the documentation downloaded in `~/projects`

```bash
  mkdir -p ~/projects/temp
  cd ~/projects/code-standards/doc
  MOOSE_DIR=~/projects/moose ROOT_DIR=./ ./moosedocs.py build --destination site
  rm -rf ~/projects/temp/site
  mv site ~/projects/temp
  cd ../
  git checkout -f gh-pages
  cp -r ~/projects/temp/site/* ./
  rm -rf adaptivity aux_kernels auxkernels executioner framework geomsearch markers mesh meshgenerators partitioner porous_flow problems sqa time_integrators transfers userobjects variables vectorpostprocessors
  git add .
  git commit -m "Manual site update"
  git push
  git checkout -f main
```
