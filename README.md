# Image-based Profiling Template

This repository was derived from a [template repository](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/) located at https://github.com/cytomining/profiling-template.
The purpose of the repository is to weld together a versioned data processing pipeline with versioned processed output data for a single image-based profiling experiment.

(Derived from this [template](https://github.com/broadinstitute/pooled-cell-painting-profiling-template))

**AFTER GENERATING A NEW REPO, CHANGE OR DELETE ALL NONSPECIFIC DETAILS**

## Setup

To correctly initialize the repository, we need to perform several manual steps.

### Step 0: Create a new repository **using this repository as a template**

By spinning up a new repo using this repo as a template, you will retain all code, configuration files, computational environments, and directory structure that a standard image-based profiling workflow expects and produces.

### Step 1: Fork the `profiling-recipe` repo

We first want to [fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) the official profiling recipe located at https://github.com/cytomining/profiling-recipe.

* **Result:** The fork creates a copy of a recipe repository.
* **Goals:** 1) Remove the connection to official recipe updates to avoid unintended weld versioning reversal; 2) Enable independent updates to fork code that does not impact official recipe.
* **Execution:** See [forking instructions](https://help.github.com/en/github/getting-started-with-github/fork-a-repo).


### Step 2: Create a submodule inside this repository of the forked recipe

Next, we will create a [submodule](https://gist.github.com/gitaarik/8735255) in this repo.

* **Result:** Adding a submodule initiates the weld.
* **Goals:** 1) Link the processing code (recipe) with the data (current repo); 2) Require a manual step to update the recipe to enable asynchronous development.
* **Execution:** See below

```bash
# In your terminal, clone the repository you just created (THIS REPO)
USER="INSERT-USERNAME-HERE"
REPO="INSERT-NAME-HERE"
git clone git@github.com:$USER/$REPO.git

# Navigate to this directory
cd $REPO

# Add the recipe submodule
git submodule add https://github.com/$USER/profiling-recipe.git profiling-recipe
```

Refer to ["Adding a submodule"](https://gist.github.com/gitaarik/8735255#adding-a-submodule) for more details.

### Step 3: Commit the submodule

Lastly, we will [commit](https://help.github.com/en/desktop/contributing-to-projects/committing-and-reviewing-changes-to-your-project#about-commits) the submodule to github.

* **Result:** Committing this change finalizes the weld.
* **Goals:** 1) Track the submodule (recipe) version with the current repository.
* **Execution:** See below

```bash
# Add, commit, and push the submodule contents
git add profiling-recipe
git add .gitmodules
git commit -m 'finalizing the recipe weld'
git push
```
