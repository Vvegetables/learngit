### 1. Fork目标仓库（它会clone一份源代码在你自己的git仓库中）

### 2. 克隆仓库到本地 
1. 复制你自己仓库中的目标仓库的SSH路径
2. 
```
git clone git@github.com:Vvegetables/learngit.git
```
### 3. 建立与目标仓库的链接
使用git remote -v 命令查看克隆下来的本地仓库与哪些远程仓库建立了链接，你会发现，只与复制到自己git仓库的远程克隆仓库建立了链接，很显然没有与目标远程仓库建立链接，所以目标仓库的更新不会反应到我们clone到本地的本地仓库，为此我们建立一下与目标远程仓库的链接。
```
git remote add upstream https://github.com/JiaYingZhang/CTUtil.git
```
### 4. 添加自己的修改
保留master分支代码不动，建立新的修改分支

1. 
```
git checkout -b dev-branch
```
2. 进行修改
3. 进行 git add, git commit, git push等操作

### 5. 发起Pull Request
到你自己克隆的远程仓库上，点击Pull Request，再点击New Pull Request按钮，
填写一些描述信息之后，就可以点击Create Pull Request按钮提交了。

### 6. Merge操作
这个是交由目标仓库的拥有者操作的。