# Setting Up Git
<p style="color: ghost white">This README.md provides step-by-step instructions for setting up Git, creating commits with version control, exploring history and tags, managing branches, handling conflicts and merges, interacting with local and remote repositories, and understanding repository structure—all essential for learning Git basics effectively.</p>

## Installation
- Install Git on your local machine by following the instructions for your operating system on the [official Git website](https://git-scm.com/).

## Configuration
- Configure Git with your username and email address using:
 * git config --global user.name "Your Name"
 * git config --global user.email "your.email@example.com"


## Git Commits

### Commit Initial File
- Create a `hello` subdirectory with `hello.sh`:
```bash
echo "Hello, World" > hello/hello.sh
```

Initialize Git Repository

Initialize Git in the "hello" directory:
   ``` bash
    cd hello
    git init
   
```
### Stage and Commit Changes

* Modify hello.sh to accept an argument:

``` bash

#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```
* Stage and commit the changes:

``` bash

git add hello.sh
git commit -m "Updated hello.sh to accept arguments"
```
* Commit Comments Separately

    Update hello.sh with comments and stage:
```bash

#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

* Make two commits:

``` bash

git add hello.sh
git commit -m "Added comment to hello.sh"
git add hello.sh
git commit -m "Updated default message in hello.sh"
```

## History

* Show full history:

``` bash

git log
```
* Show one-line history:

```bash
git log --oneline
```

* Custom entries:

```bash

git log -n 2
git log --since='5 minutes ago'
```

* Personalized format:

```bash 

git log --pretty=format:"* %h %ad | %s%d [%an]" --graph
```
## Check It Out
### Restore Snapshots

* Revert to initial snapshot:

```bash

git checkout HEAD~2 -- hello/hello.sh
```
* Revert to second recent snapshot:

``` bash

git checkout HEAD~1 -- hello/hello.sh
```

* Return to latest version:

``` bash

    git checkout main -- hello/hello.sh
```
## Tagging

* Tag current version as v1:

``` bash 
git tag v1
```

* Tag previous version as v1-beta:
```bash
git tag v1-beta HEAD^
```

* Navigate between tags:
```bash
git checkout v1
git checkout v1-beta
```
* List all tags:
```bash
    git tag
```
#### Changed Your Mind?

* Revert unwanted comments:

```bash

# Update hello.sh with unwanted comments
git checkout -- hello/hello.sh
```
* Stage and clean:

```bash

# Stage unwanted changes
git add hello/hello.sh
# Clean staging area
git restore --staged hello/hello.sh
```

* Committing and reverting:

``` bash

# Add unwanted changes, stage and commit
git add hello/hello.sh
git commit -m "Added unwanted changes"
# Revert changes
git revert HEAD
```
## Move It

* Move hello.sh to lib/ and commit:

``` bash

git mv hello/hello.sh lib/
git commit -m "Moved hello.sh to lib/"
```

* Create Makefile and commit:

```bash

# Makefile content
TARGET="lib/hello.sh"

run:
  bash ${TARGET}
```
```bash

    git add Makefile
    git commit -m "Added Makefile"
```
## Blobs, Trees and Commits

  *  Explore .git/ directory:

``` bash

cd .git/
ls -l
```

* Latest object hash:

```bash

git log -1 --format="%h %s"
```
* Dump directory tree:
```bash 
git ls-tree HEAD
```

* Dump lib/ directory and hello.sh:

``` bash

    git ls-tree HEAD lib
    git show HEAD:lib/hello.sh
```

## Branching
* Create and switch to greet branch:

```bash

git checkout -b greet
```
* Create greeter.sh in lib/ and commit:

``` bash

# lib/greeter.sh
#!/bin/bash

Greeter() {
  who="$1"
  echo "Hello, $who"
}
```
* Update hello.sh in main branch:

* Show differences between main and greet branches:

``` bash

git diff main greet -- Makefile lib/hello.sh lib/greeter.sh
```

* Generate README.md and commit:

```bash

    echo "This is the Hello World example from the git project." > README.md
    git add README.md
    git commit -m "Added README.md"

```

## Commit Tree Diagram

    Draw commit tree diagram illustrating branch history.

## Conflicts, Merging and Rebasing
#### Merge Main into Greet Branch

```bash

git checkout greet
git merge main
```

#### Merge Main into Greet Branch (Conflict)

```bash

# Conflict occurs
# Resolve conflict manualy i used vim editor to select the changes
git add hello.sh
git commit -m "Resolved conflict in hello.sh"
```

#### Rebasing Greet Branch

``` bash

git rebase main
```

#### Merging Greet into Main

```bash

git checkout main
git merge greet
```

### Understanding Fast-Forwarding and Differences

    Fast-forwarding occurs when no divergent commits exist between branches. Merging combines histories, while rebasing applies commits from one branch onto another's base.

## Local and Remote Repositories
### Clone Repository
 
*  Clone repository to cloned_hello:

``` bash

git clone /path/to/hello cloned_hello
``` 

### Show logs in cloned repository:

``` bash

cd cloned_hello
git log
```

### Display remote repository information:

```bash

git remote show origin
```

### List all branches:

```bash

    git branch -a
```

## Update README.md in Original Repository

#### Commit changes and push to remote:

```bash

git add README.md
git commit -m "Updated README.md"
git push origin main
```

#### Fetch changes from remote and display logs:

```bash

git fetch origin
git log origin/main
```

#### Merge changes from remote main:

```bash

git checkout main
git merge origin/main
```

#### Add local greet branch tracking remote:

```bash

git checkout -b greet origin/greet
```

#### Add new remote and push branches:

``` bash

    git remote add upstream <url>
    git push -u origin main greet
```

  *   Answer: git pull origin main

## Bare Repositories
### Create Bare Repository

 * Define bare repository and its necessity.

#### Create bare repository hello.git:

 ```   bash

git clone --bare /path/to/hello hello.git
```

#### Add bare repository as remote:

```bash

git remote add shared /path/to/hello.git
```

* Update README.md and push to shared repository:

``` bash

git add README.md
git commit -m "Changed README.md"
git push shared main
```

#### Pull changes in cloned_hello from shared repository:

```bash

    git pull shared main
    
```




