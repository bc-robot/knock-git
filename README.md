Git基本的工作流程：
  --Git使用40个16进制字符的SHA-1 Hash来唯一标识对象
  1、blob
  2、tree
  3、commit
  4、tag

Git初始化
  git init git_non_bare_repo
  git init --bare git_bare_repo (裸仓库，不带工作区)
  mkdir git_init_repo&&cd git_init_repo&& git init
  git clone git_bare_repo/ git_clone_repo

git用例
  #git init git_basics
  #cd git_basics
  #touch a b
  #git add a b
  #git commit -m "Initial commit"
  #vim a   (append "test")
  #git add a && git commit -m "modify a"
  #git rm a (删除工作区和暂存区)
  #git rm --cached a (只删除暂存区的文件)
  #git mv a c (deleted a, 在暂存区中删除原有的并添加新的)
  #git add -A
  #vim .gitignore
  (*.[oa]  *~ *.pyc 不忽略文件：!test.pyc 感叹号开头：\!test.py 文件夹：foo/ 匹配1个或多个文件夹：**/res)

Git暂存区




Git本地分支与合并
    git init git_checkout_merge
    vim master.txt&& git add . && git commit -m "Initial commit on master"
    vim master.txt&& git add . && git commit -m "Initial commit on master"

    git branch test
    git checkout test

    vim master.txt
    touch test.txt
    git add .
    git commit -m "Initial commit on test"

    git checkout master

    git log --oneline --decorate --graph --all
    git tag "v0" a1aba30(hash前七位)
    git tag -a "INITIAL_COMMIT" a1aba30
    git tag
    git log --oneline --decorate --graph --all

    git config --global alias.lol "log --oneline --decorate --graph --all"
    git show INITIAL_COMMIT
    git checkout -b fix_v0 (checkout&&branch)

    git stash save -a "stash1" (保存暂存区)
    git checkout master  (切换到主分支工作)
    git checkout fix_v0  (切回来)
    git stash list
    git stash pop --index stash@{0} (stash返还到工作和缓存区,pop清除stash历史)

    git stash list
    git stash save -a "stash1"

    git stash list
    git stash apply --index stash@{0}
    git stash drop stash@{0}  (清除stash，不加第几个默认清除最上面的，清除所有git stash clear)

    git checkout master
    git checkout -b test_merge
    vim master.txt
    git add .
    git commit -m "Initial commit on test_merge"

    git check master
    git merge test_merge

    git merge --abort (放弃合并)

    git log --oneline --decorate --graph --all

    git show HEAD
    git show a32f886
    git show master^2 (数字代表第几次)
    git show --stat master^2

    git show 67f180

    git log -p (输出每个差异信息)

    git log --oneline --stat -p (stat差异统计)
    git log --oneline --decorate --graph --all

    git diff (默认输出工作区和暂存区的差异)
    git diff --cached (暂存区与历史差异)
    git diff HEAD~2 --master.txt (指定文件)

    git diff --word-dif

Git撤销修改
    git checkout INITIAL_COMMIT -- master.txt
    git checkout HEAD -- master.txt

    git reset INITIAL_COMMIT -- master.txt

    git clean -n (查看将要清理内容)
    git clean -f

    git clean -n -X (只删除.gitignore里面的)
    git clean -n -x (删除)


Git重写历史记录
    git checkout HEAD~ -- .gitignore
    git commit --amend

    git checkout -b test_rebase HEAD~
    vim master.txt
    git rebase

    git add master.txt
    git rebase --continue

    git lol
    git reflog
    git reset --hard HEAD@{5}

    （git reset 重写暂存区，git checkout覆盖工作区)
