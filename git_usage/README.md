# Setting up a git repository

Note: K Broman's [GitHub
tutorial](https://kbroman.org/github_tutorial/pages/init.html) provides a nice
introduction to getting off the ground with git.

From the directory of the project to be linked to GitHub:

```sh
# cd to directory of project
git init
```

Then add files you want to commit using ``git init``, including
a ``.gitignore``. Then ``git commit -m "first commit"``.

To connect it to GitHub, create a new repository with the project name, then we
need to link it to our local project.

```sh
git remote add origin git@github.com:username/new_repo
git push -u origin main
```

## Adding to the previous commit

If we want to include a change to the previous commit that we already pushed
(say we forgot to add a file or missed something small), we can "amend" the
commit:

```sh
git add xxx
git commit --amend
git push -f origin branch_name
```

The ``-f`` tells git to "force-push", which is needed to overwrite commits on
the remote.

## Adding a remote

Say we have forked another project and want to be able to pull from the
upstream fork. We can add ``upstream`` as a remote:

```sh
git remote add upstream git@github.com:original_user/repo_name
```

Then we can fetch/rebase/etc using the upstream, e.g.:

```sh
git fetch upstream main
git rebase -i upstream/main
git push -f origin branch_name
```

# Setting up the GitHub command line client

## Installation

Via Conda:

```sh
# to install
conda install gh --channel conda-forge
# to upgrade
conda update gh --channel conda-forge
```

Or to install via ``apt``:

```sh
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

And to upgrade:

```sh
sudo apt update
sudo apt install gh
```

Then to authenticate with your GitHub account, run:

```sh
gh auth login
```

It will guide you through some steps to link your CLI client with your GitHub
account.

Nano is the default editor on macOS and Linux, so we might want to switch it to
vim. To do that, use ``gh config set editor vim``.

## Usage

See the [GitHub CLI documentation](https://cli.github.com/manual/) for details.
This is has some notes and highlights.


