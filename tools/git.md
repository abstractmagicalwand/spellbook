# Git

## Git flow

- [CheatSheet](https://danielkummer.github.io/git-flow-cheatsheet/#)

### Start a new feature

```sh
git flow feature start MYFEATURE
```

### Finish up a feature

```sh
git flow feature finish MYFEATURE
```

## Revert some changes

```sh
git reset --hard
```

## Create a global .gitignore

```sh
git config --global core.excludesfile ~/.gitignore_global
```

## Add some lines from unstaged file

```sh
git add -i
```
