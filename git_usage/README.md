# Setting up a git repository

Note: much is learned from K Broman's github tutorial
(https://kbroman.org/github_tutorial/pages/init.html).

From the directory of the project to be linked to GitHub:

```sh
# cd to directory of project
git init
```

Then add files you want to commit using ``git init``, including
a ``.gitignore``. Then ``git commit -m "first commit"``.

To connect it to GitHub, create a new repository with the project name, then we need to link it to our local project.

```sh
git remote add origin git@github.com:username/new_repo
git push -u origin main
```

