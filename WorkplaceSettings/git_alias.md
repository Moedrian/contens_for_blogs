# Set Some Convenient Alias For Git

## User Information First

```git
git config --global user.name "moedrian"

git config --global user.email "xxx.xx@xxx.xx"

git config --global core.editor vim
```

## Simple Commands

```git
git config --global alias.co checkout

git config --global alias.br branch

git config --global alias.ct commit

git config --global alias.st status
```

## A Little Complex

```git
git config --global alias.last "log -1 HEAD"

git config --global alias.unstage "reset HEAD --"

git config --global alias.prog "log --pretty=format:'%h - %an, %ar: %s'"

git config --global alias.trog "log --oneline --decorate --graph"

git config --global alias.alltrog "log --oneline --decorate --graph --all"
```