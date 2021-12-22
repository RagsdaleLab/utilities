# .bashrc

These go in your `~/.bashrc`

## Color support of `ls` and some handy aliases

```sh
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
```

## Bash prompt

We can do a lot of fancy things with our bash prompt, including nice coloring,
showing working directory, the current git branch, and/or current virtual
environment.

For example, the `.bash_prompt` in this directory has
```sh
# The various escape codes that we can use to color our prompt.
        RED="\[\033[0;31m\]"
     YELLOW="\[\033[1;33m\]"
      GREEN="\[\033[1;32m\]"
       BLUE="\[\033[1;34m\]"
     PURPLE="\[\033[1;35m\]"
  LIGHT_RED="\[\033[1;31m\]"
LIGHT_GREEN="\[\033[1;32m\]"
      WHITE="\[\033[1;37m\]"
 LIGHT_GRAY="\[\033[0;37m\]"
 COLOR_NONE="\[\e[0m\]"

# determine git branch name
function parse_git_branch(){
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# determine mercurial branch name
function parse_hg_branch(){
  hg branch 2> /dev/null | awk '{print " (" $1 ")"}'
}

# Determine the branch/state information for this git repository.
function set_git_branch() {
  # Get the name of the branch.
  branch=$(parse_git_branch)
  # if not git then maybe mercurial
  if [ "$branch" == "" ]
  then
    branch=$(parse_hg_branch)
  fi

  # Set the final branch string.
  BRANCH="${LIGHT_GRAY}${branch}${COLOR_NONE} "
}

# Return the prompt symbol to use, colorized based on the return value of the
# previous command.
function set_prompt_symbol () {
  if test $1 -eq 0 ; then
      PROMPT_SYMBOL="\$"
  else
      PROMPT_SYMBOL="${LIGHT_RED}\$${COLOR_NONE}"
  fi
}

# Determine active Python virtualenv details.
function set_conda_env () {
  if test -z "$CONDA_DEFAULT_ENV" ; then
      CONDA_ENV=""
  else
      CONDA_ENV="${PURPLE}[`basename \"$CONDA_DEFAULT_ENV\"`]${COLOR_NONE} "
  fi
}

# Set the full bash prompt.
function set_bash_prompt () {
  # Set the PROMPT_SYMBOL variable. We do this first so we don't lose the
  # return value of the last command.
  set_prompt_symbol $?

  # Set the PYTHON_VIRTUALENV variable.
  set_conda_env

  # Set the BRANCH variable.
  set_git_branch

  # Set the bash prompt variable.
  PS1="${CONDA_ENV}${GREEN}\u@\h${COLOR_NONE}:${BLUE}\w${COLOR_NONE}${BRANCH}${PROMPT_SYMBOL} "
}

# Tell bash to execute this function just before displaying its prompt.
PROMPT_COMMAND=set_bash_prompt
```

And at the end of your `.bashrc` or `.bash_profile`, place:
```sh
. ~/.bash_prompt
```

# .vimrc

See the `.vimrc` file here.

This requires installing some packages, such as `vundle`:

```sh
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
