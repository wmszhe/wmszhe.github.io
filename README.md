### 添加git submodule
```sh
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```


### 更新git submodule
```sh
git submodule update --remote --merge
```
