# Git指令

git branch 查看本地所有分支

git branch -d nudun 删除本地分支

git checkout nudun 切换分支，如果本地没有，会自动拉取线上

git checkout -b nudun 根据当前分支的代码创建新的本地分支

git log 查看所有提交

git add . 选中需要提交的改动，.表示当前文件夹，..表示上层文件夹，会选中指定目录树下所有改动

git commit -m "add some code" 提交

git push 将本地的所有提交同步到线上（远端），可以理解成保存进度

git push --force 强制将本地的所有提交同步到线上（远端）

git pull 拉取线上的提交，会和本地的代码合并，可理解成拉取进度

git stash 将所有提交加到暂存区

git stash pop 将暂存区的代码复原回来

git reset 1c8b533c7a1a01d5f8f633f09a261151f601711a 将当前版本回退至指定提交

git reset 1c8b533c7a1a01d5f8f633f09a261151f601711a --hard 将当前版本回退至指定提交，丢弃所有改动

git merge master 将指定分支的代码合并到当前分支上，合并前最好先在指定分支上pull一下
