# Contributing to Another Project

There may be times when you would like to contribute some of your modifications to anothers github repository. In order to do this in general you should make a fork of their project and maintain an up to date version of their code base in your own remote repo. You should then create your new feature in a branch of your repo. In general you can use instructions similar to these.

!alert note title=We are assuming their default branch is called devel

```bash
  cd ~/<your-local-version>
  git remote add upstream <the-project-your-contributing-to>
```

## Staying up to date

We then need to make sure your main branch is up to date with theirs before creating a new feature branch



```bash
  git checkout devel
  git fetch upstream/devel
```

!alert warning
This command will remove any of your changes and force your branch to be up to date with theirs so make sure you only do this on the devel branch you are keeping up to date with their project.

Now we are doing to force your version of their `devel` branch to be up to date

```bash
  git reset --hard upstream/devel && git submodule update --init
```

## Creating a new feature branch

```bash
  git checkout -b <BRANCH_NAME>
```

You can now push your changes to this new feature branch and then submit a PR to the project that you want to contribute to.

!alert note title=Making the Developers Aware
If there is a feature missing from a github project you are interested in working with it's a good idea to reach out to the developers to ask if this is under development or not. You can do this either by finding their contact information directly, posting on their discussions board (if available), or opening an issue on their github. If you open an issue and they are interested in your work it's good to submit your PR with the #closes issue-number so they know why you are trying to contribute to their project

## Staying up to date

You may find yourself in a situation your feature development is taking some time and the original project has moved on with some new features of their own. If you would like to incorporate these changes into your own work you can either rebase or merge your local repo with your upstream. This will simply allow you to choose which mix of new features from their repo and your work to keep or discard. Merging should be used when your history diverges from theirs. But if you are only adding to their existing code then you can simply rebase your local version with their history. In either case the first step will be to add an upstream

```bash
  git remote add upstream <url-to-the-project>
```

Then fetch their history

```bash
  git fetch upstream
```

Now you can rebase and you should be up to date with their project

```bash
  git rebase upstream/<desired-branch>
```



```bash
  git checkout <feature-branch>
```

To stash any uncommitteed changes you might be working on before you decided to merge

```bash
  git stash
```

Get the latest version of their code

```bash
  git fetch upstream
```

Now you can merge the upstream project into your own

!alert note title=Possible Conflicts
If you are performning this operation you may find yourself in a situation where you have some conflicts between their project and your own. You must resolve these manually before continuing.

```bash
  git merge upstream/devel
```

Now you can get your uncommitted changes back and continue development

```bash
  git stash apply
```
