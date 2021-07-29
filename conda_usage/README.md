# Setting up a fresh conda install

Thanks to Kevin Thornton for the tips.

```sh
# Nuke all the things
rm -rf miniconda3/ .conda*
```

Remove these lines from the bottom of `.bashrc`:

```sh
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/condauser/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/condauser/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home/condauser/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/condauser/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

Log out, then log in.

```sh
# Get latest Py 3.8, 64 bit
curl -L https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh > Miniconda3-latest-Linux-x86_64.sh
# Install and say yes to everything
bash Miniconda3-latest-Linux-x86_64.sh
```

Log out, then in again.  Or, `source .bashrc` (that re-inits the user shell).

```sh
# set up channels
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

To create a new environment, we have two options.

```sh
# normal creation of new env
conda create -n new_env python=3.9 -y
```

Or we can proceed by cloning the base environment, which has helped.

```
conda create -n new_env --clone base
```
