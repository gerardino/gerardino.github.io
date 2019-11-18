# Work git branch name in terminal

```bash
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# export PS1="\h:\W \u\$"
export PS1="\[\033[94m\]cs\[\033[0m\](\t):\W\[\033[32m\]\$(parse_git_branch)\[\033[00m\]\$ "
```
[`.bash_profile`](https://gist.github.com/gerardino/281c37bd4b54d2e6c949197b7d09f2e4)

`parse_git_branch()` from [https://gist.github.com/joseluisq/1e96c54fa4e1e5647940](https://gist.github.com/joseluisq/1e96c54fa4e1e5647940)

And here are some escape values for the prompt:

```
 \d – Current date
 \t – Current time
 \h – Host name
 \# – Command number
 \u – User name
 \W – Current working directory (ie: Desktop/)
 \w – Current working directory with full path (ie: /Users/Admin/Desktop/)
```
