## 基础
### 创建新仓库
```bash
git init

# 将这个仓库更新到远端服务器
git remote add origin <server>
```
### 克隆
```bash
# 克隆本地仓库
git clone /path/to/repository

# 克隆远程仓库
git clone username@host:/path/to/repository
```

### 添加和提交
```bash
# 执行完add执行更新到缓存中
git add <filename>  // or git add *

# commit 执行完成后，修改就更新到HEAD中了。
git commit -m "代码提交信息"
```
### 推送改动
```bash
# 更新到远端
git push origin master
```
### 分支
```bash
# 新建分支
git checkout -b feature_new

# 切换分支
git checkout master

# 删除分支
git branch -d feature_new

# 将分支推送远端 
git push origin <branch>
```
### 更新与合并
```bash
# 更新至最新
git pull

# 获取（fetch） 并 合并（merge）
# 在这fetch和merge的情况下，git 都会尝试去自动合并改动。遗憾的是，这可能并非每次都成功，并可能出现冲突（conflicts）。 这时候就需要你修改这些文件来手动合并这些冲突（conflicts）
git merge <branch>

```
### 标签
```bash
# 1b2e1d63ff为commit id
git tag 1.0.0 1b2e1d63ff前10位
```
### 替换本地改动
```bash
# 放弃文件全部修改，回到HEAD中的状态
git checkout -- <filename>

# 放弃本地所有修改，更新为上游最新
git fetch origin
git reset --hard origin/master
```
### 其他
```bash
# 显示历史记录时，每个提交的信息只显示一行：
git config format.pretty oneline
```

## 高级