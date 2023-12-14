## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №1<br>"Базова робота з git"

### КВ-13 Ішмуратов Тимур

## Хід виконання роботи

### 1. Зклонувати репозиторій для ЛР2 використавши локальний репозиторій від ЛР1 в якості <br>"віддаленого".

Для початку створимо папку для роботи над ЛР2. Після цього склонуємо репозиторій з першої ЛР як віддалений:

```
student@virt-linux:~/tirpz/lab2$ git clone file:///home/student/tirpz/lab1/numpy
Cloning into 'numpy'...
remote: Enumerating objects: 253369, done.
remote: Counting objects: 100% (253369/253369), done.
remote: Compressing objects: 100% (51317/51317), done.
remote: Total 253369 (delta 199666), reused 253337 (delta 199659)
Receiving objects: 100% (253369/253369), 128.77 MiB | 49.85 MiB/s, done.
Resolving deltas: 100% (199666/199666), done.
```

### 2. Робота з ремоутами.

Перевіримо гілки які в нас є зараз:

```
student@virt-linux:~/tirpz/lab2/numpy$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/local-branch-1
  remotes/origin/local-branch-2
  remotes/origin/local-branch-3
  remotes/origin/main
```

Тепер зробимо ремоут на цей же репозиторій, але використовуючи інтернет-джерело:

```
student@virt-linux:~/tirpz/lab2/numpy$ git remote add upstream https://github.com/numpy/numpy
student@virt-linux:~/tirpz/lab2/numpy$ git remote -v
origin	file:///home/student/tirpz/lab1/numpy (fetch)
origin	file:///home/student/tirpz/lab1/numpy (push)
upstream	https://github.com/numpy/numpy (fetch)
upstream	https://github.com/numpy/numpy (push)
```

Тепер створимо нову гілку `lab2-branch`:

```
student@virt-linux:~/tirpz/lab2/numpy$ git checkout -b lab2-branch
Switched to a new branch 'lab2-branch'
student@virt-linux:~/tirpz/lab2/numpy$ git branch
* lab2-branch
  main
```

Зробимо кілька комітів:

```
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add rem1.txt"
[lab2-branch 48ece0af7] Add rem1.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 rem1.txt
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add rem2.txt"
[lab2-branch 04e6c6939] Add rem2.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 rem2.txt
```

Тепер запушимо цю гілку на ремоут:

```
student@virt-linux:~/tirpz/lab2/numpy$ git push origin lab2-branch 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 2 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 455 bytes | 455.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
To file:///home/student/tirpz/lab1/numpy
 * [new branch]          lab2-branch -> lab2-branch
```

Зробимо ще один коміт на гілку, а потім знову зробимо push, але тепер із зв'язанням гілки:

```
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add rem3.txt"
[lab2-branch 9d337b0ee] Add rem3.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 rem3.txt
student@virt-linux:~/tirpz/lab2/numpy$ git push -u origin lab2-branch 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 241 bytes | 241.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0)
To file:///home/student/tirpz/lab1/numpy
   04e6c6939..9d337b0ee  lab2-branch -> lab2-branch
Branch 'lab2-branch' set up to track remote branch 'lab2-branch' from 'origin'.
```

Робимо останній коміт для цього завдання і пушимо просто командою `git push`, адже ми вже зробили зв'язання:

```
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add rem4.txt"
[lab2-branch ccce6ec3e] Add rem4.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 rem4.txt
student@virt-linux:~/tirpz/lab2/numpy$ git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 241 bytes | 241.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0)
To file:///home/student/tirpz/lab1/numpy
   9d337b0ee..ccce6ec3e  lab2-branch -> lab2-branch
```

Тепер можна перевірити гілки у репозиторії ЛР1, щоб подивитись, чи є там якісь зміни:

```
student@virt-linux:~/tirpz/lab1/numpy$ git branch -a
  lab2-branch
  local-branch-1
  local-branch-2
  local-branch-3
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/origin/maintenance/1.0.3.x
  remotes/origin/maintenance/1.1.x
  remotes/origin/maintenance/1.10.x
```

Як ми бачимо, гілка яку ми створили у репозиторії ЛР2 з'явилась і тут.

### 3. Змерджити гілку, що була створена при виконанні ЛР1, в поточну гілку lab2-branch.

Зробимо merge віддаленої гілки з попередньої ЛР та подивимось на логи у вигляді графа:

```
student@virt-linux:~/tirpz/lab2/numpy$ git merge origin/local-branch-1
Merge made by the 'recursive' strategy.
 2.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
student@virt-linux:~/tirpz/lab2/numpy$ git log --pretty=oneline -n 4 --graph
*   dc1aa9228610c03cb34a2d968a34806fe6ef7c99 (HEAD -> lab2-branch) Merge remote-tracking branch 'origin/local-branch-1' into lab2-branch
|\  
| * 81ff3768b386b740905a48d1395de8af35ba2790 (origin/local-branch-1) Modifying 2.txt on local-branch-1
* | ccce6ec3e34609e0f7adead54d22fe2545d4f0b5 (origin/lab2-branch) Add rem4.txt
* | 9d337b0ee214152eb11fb9e8fc32f816a2c06513 Add rem3.txt
```

### 4. Перенесення комітів.

Перейдемо на гілку `main`, створимо нову гілку і зробимо в ній 3 коміти:

```
student@virt-linux:~/tirpz/lab2/numpy$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
student@virt-linux:~/tirpz/lab2/numpy$ git checkout -b lab2-branch-2
Switched to a new branch 'lab2-branch-2'
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add mov1.txt"
[lab2-branch-2 0b20ff964] Add mov1.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 mov1.txt
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add mov2.txt"
[lab2-branch-2 60ba8138e] Add mov2.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 mov2.txt
student@virt-linux:~/tirpz/lab2/numpy$ git add .
student@virt-linux:~/tirpz/lab2/numpy$ git commit -m "Add mov3.txt"
[lab2-branch-2 9b40dae4c] Add mov3.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 mov3.txt
```

Користуючись командою `git log` знайдемо хеш другого коміту:

```
student@virt-linux:~/tirpz/lab2/numpy$ git log -n 3
commit 9b40dae4ccd8c97231ccef8f886f52809249959b (HEAD -> lab2-branch-2)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Dec 14 04:08:06 2023 +0200

    Add mov3.txt

commit 60ba8138e47e7bf110f6e848c0ecf2f74c589949
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Dec 14 04:07:37 2023 +0200

    Add mov2.txt

commit 0b20ff96480aec8438c37078fe5f9bd8e6396a06
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Dec 14 04:07:20 2023 +0200

    Add mov1.txt
```

Це `60ba8138e47e7bf110f6e848c0ecf2f74c589949`. Тепер можна переключитись на гілку `lab2-branch` і перенести в неї цей коміт:

```
student@virt-linux:~/tirpz/lab2/numpy$ git checkout lab2-branch
Switched to branch 'lab2-branch'
Your branch is ahead of 'origin/lab2-branch' by 2 commits.
  (use "git push" to publish your local commits)
student@virt-linux:~/tirpz/lab2/numpy$ git cherry-pick 60ba8138e47e7bf110f6e848c0ecf2f74c589949
[lab2-branch 264b1d83c] Add mov2.txt
 Date: Thu Dec 14 04:07:37 2023 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 mov2.txt
student@virt-linux:~/tirpz/lab2/numpy$ git log --pretty=oneline --graph -n 3
* 264b1d83ccc0abd8d1fd0ae53ab111fb2a40c1a9 (HEAD -> lab2-branch) Add mov2.txt
*   dc1aa9228610c03cb34a2d968a34806fe6ef7c99 Merge remote-tracking branch 'origin/local-branch-1' into lab2-branch
|\  
| * 81ff3768b386b740905a48d1395de8af35ba2790 (origin/local-branch-1) Modifying 2.txt on local-branch-1
```

### 5. Визначити останнього спільного предка між двома будь-якими гілками.

Командою `git merge-base` можна визначити хеш коміта на якому дві гілки розійшлися. Зробимо це для гілок `lab2-branch` та `lab2-branch-2`:

```
student@virt-linux:~/tirpz/lab2/numpy$ git merge-base lab2-branch lab2-branch-2
a364da31461295d3f2e6253484cf983dd99c39b0
student@virt-linux:~/tirpz/lab2/numpy$ git show a364da31461295d3f2e6253484cf983dd99c39b0
commit a364da31461295d3f2e6253484cf983dd99c39b0 (origin/main, origin/HEAD, main)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 03:53:33 2023 +0300

    Move 4.txt to abyss/

diff --git a/4.txt b/abyss/4.txt
similarity index 100%
rename from 4.txt
rename to abyss/4.txt
```

### 6. Робота з ничкою.

Зробимо зміни у робочому дереві, але не будемо їх комітити, а створимо ничку. Зробимо це 2 рази:

```
student@virt-linux:~/tirpz/lab2/numpy$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   rem1.txt

no changes added to commit (use "git add" and/or "git commit -a")
student@virt-linux:~/tirpz/lab2/numpy$ git stash
Saved working directory and index state WIP on lab2-branch: 264b1d83c Add mov2.txt
student@virt-linux:~/tirpz/lab2/numpy$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   rem2.txt

no changes added to commit (use "git add" and/or "git commit -a")
student@virt-linux:~/tirpz/lab2/numpy$ git stash
Saved working directory and index state WIP on lab2-branch: 264b1d83c Add mov2.txt
student@virt-linux:~/tirpz/lab2/numpy$ git stash list
stash@{0}: WIP on lab2-branch: 264b1d83c Add mov2.txt
stash@{1}: WIP on lab2-branch: 264b1d83c Add mov2.txt
```

Тепер ми маємо дві нички. Використаємо вміст першої нички і подивимось на статус:

```
student@virt-linux:~/tirpz/lab2/numpy$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
student@virt-linux:~/tirpz/lab2/numpy$ git stash apply stash@{1}
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   rem1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### 7. Робота з файлом `.gitignore`.

Для виконанная цього завдання створимо файли з розширенням `.txt` та якимось незнайомим, наприклад, `.kvfpm`. Потім подивимось на статус гіта:

```
student@virt-linux:~/tirpz/lab2/numpy$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   rem1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gignr1.txt
	gignr2.kvfpm
	gignr3.kvfpm

no changes added to commit (use "git add" and/or "git commit -a")
```

У проєкті з яким я працюю у цій ЛР вже є файл `.gitignore`, тому я просто додам у нього рядок `*.kvfpm`. Цей рядок -- шаблон, який буде використовуватись гітом для фільтрування файлів, які не треба відображати у статусі. Після цього подивимось на сам статус:

```
student@virt-linux:~/tirpz/lab2/numpy$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore
	modified:   rem1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gignr1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Як бачимо, файли з цим розширенням зникли. Але ці файли все одно можна відобразити додавши аргумент `--ignored`:

```
student@virt-linux:~/tirpz/lab2/numpy$ git status --ignored
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   .gitignore
	modified:   rem1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	gignr1.txt

Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
	gignr2.kvfpm
	gignr3.kvfpm

no changes added to commit (use "git add" and/or "git commit -a")
```

Всі, навіть ігноровані файли відображаються. Виконаємо очистку від untracked файлів:

```
student@virt-linux:~/tirpz/lab2/numpy$ git clean -fdx
Removing gignr1.txt
Removing gignr2.kvfpm
Removing gignr3.kvfpm
```

### 8.  Робота з `reflog`.

Подивимось на лог:

```
student@virt-linux:~/tirpz/lab2/numpy$ git log -n 4 --pretty=oneline --graph
* 684d6232406a5960de7061b961add7212f61b7ce (HEAD -> lab2-branch) Mod rem1.txt
* 264b1d83ccc0abd8d1fd0ae53ab111fb2a40c1a9 Add mov2.txt
*   dc1aa9228610c03cb34a2d968a34806fe6ef7c99 Merge remote-tracking branch 'origin/local-branch-1' into lab2-branch
|\  
| * 81ff3768b386b740905a48d1395de8af35ba2790 (origin/local-branch-1) Modifying 2.txt on local-branch-1
```

Тепер видалимо гілку `lab2-branch` та переглянемо reflog командою `git reflog`:

```
student@virt-linux:~/tirpz/lab2/numpy$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
student@virt-linux:~/tirpz/lab2/numpy$ git branch -D lab2-branch
Deleted branch lab2-branch (was 684d62324).
student@virt-linux:~/tirpz/lab2/numpy$ git reflog
a364da314 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: checkout: moving from lab2-branch to main
684d62324 HEAD@{1}: commit: Mod rem1.txt
264b1d83c HEAD@{2}: reset: moving to HEAD
264b1d83c HEAD@{3}: reset: moving to HEAD
```

Тепер створимо нову гілку `lab2-ressurected` через хеш `684d62324`, переключимося на неї та подивимося лог:

```
student@virt-linux:~/tirpz/lab2/numpy$ git checkout -b lab2-ressurected 684d62324
Switched to a new branch 'lab2-ressurected'
student@virt-linux:~/tirpz/lab2/numpy$ git log -n 5 --pretty=oneline --graph
* 684d6232406a5960de7061b961add7212f61b7ce (HEAD -> lab2-ressurected) Mod rem1.txt
* 264b1d83ccc0abd8d1fd0ae53ab111fb2a40c1a9 Add mov2.txt
*   dc1aa9228610c03cb34a2d968a34806fe6ef7c99 Merge remote-tracking branch 'origin/local-branch-1' into lab2-branch
|\  
| * 81ff3768b386b740905a48d1395de8af35ba2790 (origin/local-branch-1) Modifying 2.txt on local-branch-1
* | ccce6ec3e34609e0f7adead54d22fe2545d4f0b5 (origin/lab2-branch) Add rem4.txt
```