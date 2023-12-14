## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем


# Лабораторна робота №1<br>"Базова робота з git"

### КВ-13 Ішмуратов Тимур

## Хід виконання роботи

### 1. Зклонувати будь-який невеликий проєкт open-source з github

Створюю папку для лабораторної роботи:

```
student@virt-linux:~$ mkdir ~/tirpz
student@virt-linux:~$ mkdir ~/tirpz/lab1
student@virt-linux:~$ cd ~/tirpz/lab1
student@virt-linux:~/tirpz/lab1$
```

Повністю клоную обраний репозиторій:

```
student@virt-linux:~/tirpz/lab1$ git clone https://github.com/numpy/numpy
Cloning into 'numpy'...
remote: Enumerating objects: 254138, done.
remote: Counting objects: 100% (1142/1142), done.
remote: Compressing objects: 100% (498/498), done.
remote: Total 254138 (delta 686), reused 968 (delta 629), pack-reused 252996
Receiving objects: 100% (254138/254138), 129.21 MiB | 2.02 MiB/s, done.
Resolving deltas: 100% (200239/200239), done.
```

Частково клоную його:

```
student@virt-linux:~/tirpz/lab1$ git clone https://github.com/numpy/numpy --depth=1 --single-branch --branch=main numpy_shallow
Cloning into 'numpy_shallow'...
remote: Enumerating objects: 2282, done.
remote: Counting objects: 100% (2282/2282), done.
remote: Compressing objects: 100% (2096/2096), done.
remote: Total 2282 (delta 189), reused 880 (delta 144), pack-reused 0
Receiving objects: 100% (2282/2282), 8.93 MiB | 2.17 MiB/s, done.
Resolving deltas: 100% (189/189), done.
```

Порівняння репозиторіїв:

```
student@virt-linux:~/tirpz/lab1$ du -sh ./*/.git
137M	./numpy/.git
9,4M	./numpy_shallow/.git
```

### 2. Зробити не менше трьох локальних комітів

Створюю файл `1.txt` та додаю його командою `git add 1.txt`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add 1.txt 
student@virt-linux:~/tirpz/lab1/numpy$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   1.txt
```

Тепер зроблю коміт із вказанням повідомлення:

```
student@virt-linux:~/tirpz/lab1/numpy$ git commit -m "Adding 1.txt file"
[main 20c99c052] Adding 1.txt file
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```

Створюю додаткові файли `2.txt` та `3.txt` командою `git add .`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add .
student@virt-linux:~/tirpz/lab1/numpy$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   2.txt
	new file:   3.txt
```

Роблю звичайний коміт без параметрів:

```
student@virt-linux:~/tirpz/lab1/numpy$ git commit
```

Введення повідомлення:

```
Adding 2.txt and 3.txt.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch main
# Your branch is ahead of 'origin/main' by 1 commit.
#   (use "git push" to publish your local commits)
#
# Changes to be committed:
#       new file:   2.txt
#       new file:   3.txt
#
```

Вивід у терміналі:

```
student@virt-linux:~/tirpz/lab1/numpy$ git commit
[main 0dd7b69f4] Adding 2.txt and 3.txt.
 2 files changed, 2 insertions(+)
 create mode 100644 2.txt
 create mode 100644 3.txt
```

Змінюю файли і роблю коміт командою `git commit -a`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git commit -am "Modifying files"
[main 0d1570c0c] Modifying files
 3 files changed, 3 insertions(+), 3 deletions(-)
```

### 3. Продемонструвати уміння вносити зміни до останнього коміту за допомогою опції `--amend`

Я створив додатковий файл `4.txt` та модифікував один інший файл. Після цього я роблю коміт:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add .
student@virt-linux:~/tirpz/lab1/numpy$ git commit --amend -m "Modifying files AND adding 4.txt!"
[main 5d783b3bc] Modifying files AND adding 4.txt!
 Date: Thu Oct 26 02:28:48 2023 +0300
 4 files changed, 4 insertions(+), 3 deletions(-)
 create mode 100644 4.txt
```

### 4. Продемонструвати уміння об'єднати кілька останніх комітів в один за допомогою `git reset`

Командою `git reset HEAD~2` я відкочусь назад, а потім використаю команду `git commit`, щоб закомітити збережені зміни:

```
student@virt-linux:~/tirpz/lab1/numpy$ git reset HEAD~2
Unstaged changes after reset:
M	1.txt
student@virt-linux:~/tirpz/lab1/numpy$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	2.txt
	3.txt
	4.txt

no changes added to commit (use "git add" and/or "git commit -a")
student@virt-linux:~/tirpz/lab1/numpy$ git add .
student@virt-linux:~/tirpz/lab1/numpy$ git commit -m "Reset commit"
[main 0a5df9b67] Reset commit
 4 files changed, 4 insertions(+), 1 deletion(-)
 create mode 100644 2.txt
 create mode 100644 3.txt
 create mode 100644 4.txt
```

### 5. Видалити файл(и) одним способом на вибір.

Я створю додатковий файл `dead.txt`, який потім видалю вручну, і закомічу зміни.

Додаю файл:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add .
student@virt-linux:~/tirpz/lab1/numpy$ git commit -m "Adding dead.txt"
[main 05431894c] Adding dead.txt
 1 file changed, 1 insertion(+)
 create mode 100644 dead.txt
```

Видаляю його, додаю цю зміну і роблю коміт:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add dead.txt
student@virt-linux:~/tirpz/lab1/numpy$ git commit -a -m "Deleting the dead"
[main 28d7120d8] Deleting the dead
 1 file changed, 1 deletion(-)
 delete mode 100644 dead.txt
```

### 6. Перемістити файл(и) одним способом на вибір.

Я переміщу файл `4.txt` у теку `abyss`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git add .
student@virt-linux:~/tirpz/lab1/numpy$ git status
On branch main
Your branch is ahead of 'origin/main' by 4 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    4.txt -> abyss/4.txt
	
student@virt-linux:~/tirpz/lab1/numpy$ git commit -m "Move 4.txt to abyss/"
[main a364da314] Move 4.txt to abyss/
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename 4.txt => abyss/4.txt (100%)
```

### 7. Гілкування:

Створюю гілку за допомогою команди `git branch` та переключаємось на неї через `git checkout`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git branch local-branch-1
student@virt-linux:~/tirpz/lab1/numpy$ git checkout local-branch-1
Switched to branch 'local-branch-1'
```

Тепер я зроблю коміт на цій гілці:

```
student@virt-linux:~/tirpz/lab1/numpy$ git commit -am "Modifying 2.txt on local-branch-1"
[local-branch-1 81ff3768b] Modifying 2.txt on local-branch-1
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Тепер створю ще одну гілку, але тепер командою `git checkout -b`:

```student@virt-linux:~/tirpz/lab1/numpy$ git checkout -b local-branch-2
Switched to a new branch 'local-branch-2'
student@virt-linux:~/tirpz/lab1/numpy$ git branch
  local-branch-1
* local-branch-2
  main
student@virt-linux:~/tirpz/lab1/numpy$ git commit -am "Modifying 3.txt on local-branch-2"
[local-branch-2 069164986] Modifying 3.txt on local-branch-2
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Створю останню гілку:

```
student@virt-linux:~/tirpz/lab1/numpy$ git checkout -b local-branch-3
Switched to a new branch 'local-branch-3'
student@virt-linux:~/tirpz/lab1/numpy$ git commit -am "Modifying 1.txt on local-branch-3"
[local-branch-3 21d535131] Modifying 1.txt on local-branch-3
 1 file changed, 1 insertion(+)
```

### 8. Продемонструвати уміння знайти в історії комітів набір комітів, в яких була зміна по конкретному шаблону в конкретному файлі (див. методичні вказівки)

Перегляд останніх 4 комітів:

```
student@virt-linux:~/tirpz/lab1/numpy$ git log -4
commit 21d5351312b2ad18c471326af92295a84e4ede23 (HEAD -> local-branch-3)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 15:39:37 2023 +0300

    Modifying 1.txt on local-branch-3

commit 069164986f61867fc2277836d13fa2b788475bf3 (local-branch-2)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 15:37:50 2023 +0300

    Modifying 3.txt on local-branch-2

commit 81ff3768b386b740905a48d1395de8af35ba2790 (local-branch-1)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 15:35:30 2023 +0300

    Modifying 2.txt on local-branch-1

commit a364da31461295d3f2e6253484cf983dd99c39b0 (main)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 03:53:33 2023 +0300

    Move 4.txt to abyss/
```

Знайдемо зміни у файлі `2.txt` із рядком `Hello` за допомогою команд `git log` та `git diff`:

```
student@virt-linux:~/tirpz/lab1/numpy$ git log -G "Hello" 2.txt
commit 81ff3768b386b740905a48d1395de8af35ba2790 (local-branch-1)
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 15:35:30 2023 +0300

    Modifying 2.txt on local-branch-1

commit 0a5df9b67318ff8b30ad1d5c52ae1755ba0f7d2b
Author: student <ishmuratov.tymur@lll.kpi.ua>
Date:   Thu Oct 26 03:08:58 2023 +0300

    Reset commit
student@virt-linux:~/tirpz/lab1/numpy$ git diff 81ff3768b386b740905a48d1395de8af35ba2790~..81ff3768b386b740905a48d1395de8af35ba2790 2.txt
diff --git a/2.txt b/2.txt
index 7a2aa6710..488b2c3fe 100644
--- a/2.txt
+++ b/2.txt
@@ -1 +1 @@
-Hello!!!
+Hello!!!1!
```