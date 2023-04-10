在 git 工作目录下：

```zsh
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```
