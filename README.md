# Переход в ветку main

git checkout main

# Создание каталога branching и файлов merge.sh и rebase.sh с содержимым из задания

# commit "prepare for merge and rebase"

git add branching\merge.sh
git add branching\rebase.sh
commit -m "prepare for merge and rebase"

# Подготовка файла merge.sh

git checkout -b git-merge

# Редактирование файла merge.sh

# commit "@ instead *"

git add branching\merge.sh
git commit -a "merge: @ instead *"

# push repo

git push --set-upstream origin git-merge

# Редактирование файла merge.sh разработчиком

# commit "use shift"

git add branching\merge.sh
git commit -a "merge: use shift"

# Изменение main и содержимого файла rebase.sh

git checkout main
git add branching\rebase.sh
git commit -m "rebase.sh changed"
git push

# Подготовка файла rebase.sh

git checkout fd0f9dd8b95c3a64337eb854054bec1fa2db3d3e
git checkout -b git-rebase

# Редактивароние rebase.sh

git add branching\rebase.sh
git commit -m "git-rebase 1"
git push --set-upstream origin git-rebase

# Редактивароние rebase.sh

git add branching\rebase.sh
git commit -m "git-rebase 2"
git push

# Merge

git checkout main
git merge git-merge
git push

# Rebase

git checkout git-rebase
git rebase -i main

# Решение конфликта и продолжение rebase

git add branching/rebase.sh
git rebase --continue

# Решение второго конфликта и продолжение rebase

git add branching/rebase.sh
git rebase --continue

Successfully rebased and updated refs/heads/git-rebase.

# Push repo

$ git push -u origin git-rebase
To https://github.com/polyakoffalex/devops-netology.git
 ! [rejected]        git-rebase -> git-rebase (non-fast-forward)
error: failed to push some refs to 'https://github.com/polyakoffalex/devops-netology.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

$ git push -u origin git-rebase -f
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/polyakoffalex/devops-netology.git
 + e81f09f...ae40384 git-rebase -> git-rebase (forced update)
Branch 'git-rebase' set up to track remote branch 'git-rebase' from 'origin'.

# Merge ветки git-rebase

git checkout main
git merge git-rebase
