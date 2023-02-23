# GIT Commmands

# Features

-   [config](#config)
-   [init](#init)
-   [clone](#clone)
-   [add](#add)
-   [status](#status)
-   [log](#log)
-   [branch](#branch)
-   [switch](#switch)
-   [checkout](#checkout)
-   [commit](#commit)
-   [push](#push)
-   [remote](#remote)
    -   [fetch](#fetch)
    -   [pull](#pull)
-   [stash](#stash)
-   [tag](#tag)
-   [cherry-pick](#cherry-pick)
-   [diff](#diff)
-   [Стандартный сценарий](#standart-script)
-   [Работа с файлами](#files)
    -   [Удалить файлы](#delete-files)
    -   [Переименовать файлы](#rename-files)
    -   [Восстановить файлы](#restore-files)
    -   [Просмотреть изменения файла](#changed-history)
-   [Работа с удаленным репозиторием](#remote-repos)
-   [Работа с ветками](#branches)
    -   [Работа с ветками (локальными)](#branch-locale)
    -   [Работа с ветками (удаленными)](#branch-remote)
-   [Работа с тегами](#tags)
-   [Работа со стешем](#stashes)
-   [Редкие случаи](#rare-cases)
    -   [Посмотреть разницу между ветками](#diff-branches)
    -   [Изменить несколько коммитов](#lot-commits)
    -   [Переместить ветку в другое место](#new-branch-pos)
    -   [Удалить последний коммит](#remove-last-commit)

***

## **config**

>Утилита для настройки конфига для работы в гитом. Флаги для настройки системного, глобального и локального конфига:

```bash
git config --system
git config --global
git config --local
```

>Для просмотра всех принятых настроек:

```bash
git config --list
```

>Для просмотра всех изменённых настроек:

```bash
git config --list --show-origin
```

>Для настройки данных пользователя (**user**):

```bash
git config --global user.name <name>  # Имя коммитера.
git config --global user.email <email>  # Почта коммитера.
```

>Для настройки инициализации репозитория (**init**):

```bash
git config --global init.defaultBranch <name_branch>  # Имя основной ветки ри инициализации репозитория.
```

>Для настройки вспомогательных инструментов (**core**):

```bash
git config --global core.editor <name_editor>  # Редактор коммитов по умолчанию.
```

>Для настройки полномочий (**credential.helper**):

```bash
git config --global credential.helper cache [--timeout <sec>]  # Сохраняет данные в кеше на <sec>. По умолчанию 900.
git config --global credential.helper store [--file <path>]  # Сохраняет данные в файле по пути <path>. По умолчанию в ~/.git-credentials
gti config --global credential.helper <save_data>  # Куда сохранять данные - wincred.  
```

>Для настройки инструментов (***.**tool**):

```bash
git config merge.tool <path_to_tool>  # Утилита для слияния.
git config dif.tool <path_to_tool>  # Утилита для сравнения.
```

>Для настройки клонирования сторонних репозиториев (**clone**):

```bash
git config --global clone.defaultRemoteName <name_remote_branch>  # Имя удалённой ветки по-умолчанию.
```

>Для настройки цветов (**color**):

```bash
git config --global color.ui [false | true | auto]  # Включить выделение информации цветом.
git config --global color.[status | branch | diff] auto  # Переназначить цвета выделения.
git config --global color "branch" \  # Настрйока отображения веток*
    -current = <color>
    -local = <color>
    -remote = <color>
git config --global color "status" \  # Настрйока отображения статуса.
    -added = <color>  # Для файлов, которые добавили.
    -changed = <color>  # Для файлов, которые изменили. 
    -untracked = <color>  # Для файлов, которые убрали из слежения*
```

***

## **init**

> Инициализирует репозиторий в <path>. Без <path> инициализирует на месте.
```bash
git init <path>  # Создает репозпиторий с именем path или путём к path.
```
### Остальное:
```bash
git init --bare  # Создать *голый репозиторий (для серверов).
git init [-b <br_name> | --initial-branch=<br_name>]  # Создает репозиторий с основной. веткой <br_name>
```

***

## **clone**

>Инициализирует удалённый репозиторий, который находится по адресу <link>.
```bash
git clone <link> <path>  # Создает реопзиторий на месте, иначе в <path>.
git clone <link> [-o <name> | --origin <name>]  # Имя вместо origin.
```

***


## **add**

> Делает файлы отслеживаемые (tracked).
```bash
git add .  # Добавить все файлы, которых нет в .gitignore
git add [-f | --force]  # Для добавления вообще всех файлов в обход .gitignore
```
***

## **status**

> Показывает состояние репозитория на момент вызова.
```bash
git status  # Показывает состояние файлов.
git status [-s | --short]  # Показывает состояние в компактном виде.
```

***

## **log**

> Покажет хронологическую историю <branch> или <file>. Иначе всего репозиторя.
```bash
git log <branch> <file>
```

> Полезные флаги:
```bash
git log -n  # Покажет последние n коммитов.
git log -p  # Покажет что именно добавлялось в коммиты.
git log -S <string>  # Покажет где изменялась строка <string>.
```

> Комплексные опции:
```bash
git log --stat  # Краткая статистика изменений, того что было.
git log --oneline  # Выведет коммиты в одну строку.
git log --graph  # Покажет в виде древа ASCII.
```

> Опция --pretty=<presset\>:
* oneline - Выводит каждый коммит на отдельно строке.
* short - Выводит в коротком виде.
* medium - Выводит в среднем виде.
* full - Выводит в полном виде.
* fuller - Выводит всю информацию.
* email - Выводит информацию о почтах коммита.


> Формат для --pretty:<format\>:
* %H, %h = Полный и которокий хеш коммита.
* %an, %ae = Имя и почта автора.
* %cn, %ce = Имя и почта коммитера.
* %ad = Дата коммита.
* %s = Содержание коммита.
* %Cred, %Cgrean, %Cblue, %Creset, %C(...) = Цвета, сброс цвета, свой.

***

## **branch**

>Утилита для работы с ветками. По-умолчанию просматривает все доступные ветки.
```bash
git branch [--list]  # Покажет список всех веток
git branch [-c | --create] <br_name>  # Создасть ветку br_name.
git branch [-d | --delete] <br_name>  # Удалить ветку br_name.
git branch -m <old_name> <new_name>  # Переименует ветку.
git branch -u <remote>  # Привязать текуюю ветку к удалённой.
git branch -f <br_name> <point>  # Заставить указывать ветку на point.
git branch --merged  # Покажет ветки, которые слиты (можно удалять).
git branch --no-merged  # Покажет ветки, которые ещё не слиты.
```

***

## **switch**

> Переключает ветки
```bash
git switch <name_branch>  # Переключает на name_branch.
git switch [-c | --create] <name_branch>  # Создает и переключает на ветку name_branch.
git switch -  # Переключает на предыдущую ветку.
```

***

## **checkout**

> Переключает на <point\>
```bash
git checkout <point>  # Может быть ветка, тег, хеш коммита и т.д.
git checkout -b <name_branch>  # Создаст и переключится на ветку name_branch.
```

***

## **commit**

> Фиксация изменений иднекса в коммит
```bash
git commit  # Сделать коммит без сообщения.
git commit -m <text>  # Создаст коммит с сообщением <text>.
git commit -a  # Сделает git add . и только потом git commit.
git commit -am <text>  # Тое что и git commit -a -m <text>.
git commit --amend  # Заменить последний коммит новым, с изменениями.
git commit -v  # Добавит в сообщенеи коммита инфу о том, что было изменено (в комментах).
```

***

## **push**

> Утилита для отправки коммитов на удалённый репозиторий
```bash
git push <remote> <local_branch>  # Отправить ветку в удалённый репозиторий или просто отправить изменения этой ветки в удалённую.
git push <remote> --delete <local_branch>  # Удалит удалённую ветку <local_branch> в <remote>.
git push <remote> --all  # Публикация всех локальных веток в <remote>.
git push <remote> --tags  # Публикация всех локальных тегов в <remote>.
git push [-u | --set-upstream]  # Привяжет ветку <branch> к <remote>/<branch>
```

***

## **remote**

> Утилита для работы с удалёнными репозиториями
```bash
git remote  # Вывод удалённых репозиторий (имена).
git remote -v  # Подробный вывод удалённых репозиторией.
git remote add <remote> <url>  # Добавить удалённый репозиторий <url> как <remote>.
git remote rm <remote>  # Удалить удалённый репозиторий <remote>.
git remote rename <remote> <new_remote>  # Переименовать <remote> в <new_remote>.
git remote show <remote>  # Для получение инфы о <remote>.
git remote get-url <remote>  # Для получения урла от <remote>.
git remote prune <remote>  # Для удаление старых веток слежения.
```

## fetch

> Извлекает все нововведения из удалённого репозитория, но не сливает их с локальным репозиторием
```bash
git fetch <remote>  # Извлечет все изменения с удалённого репозитория.
git fetch <remote> <branch>  # Извлечет изменения с репозитория и отведет для них ветку.
git fetch --all  # Извлечет все зарегистрированные репозитории и их ветки.
```

## pull

> Забирает все нововведения из удалённого репозитория и сливает их с текущей веткой
```bash
git pull [-u | --set-upstream]  # Привяжет текущую ветку к <remote>
```

***

## **stash**

> Позволяет спрятать изменения, которые были не зафиксированны
```bash
git stash  # Прячем все untracked измения в stash.
git stash list  # Показвает список всех спрятанных стешей.
git stash apply  # Восстановит последний стеш, но не удалит его из списка.
git stash apply stash@{ID} # Восстановит стеш c ID, но не удалит его из списка.
git stash drop stash@{ID}  # Удалить стеш с ID из списка.
git stash pop  # Восстановит последний стеш из спика и сразу же удалит его из списка.
git stash branch <branch_name>  # Создаст отдельную ветку и применит туда стеш.
git stash --keep-index  # Сделает слепок изменений, но не сотрёт рабочую директорию.
git stash --path  # Откроет интерактивный режим, и спросит отдельно для каждого файла, что сохранять, а что нет.
git stash [-u | --include-untracked]  # Позволит сохранить не только индекс и изменнёный файлы, но и не отслеживаемые.
git stash [-a | --all]  # Сохранит вообще все файлы, даже которые в .gitignore
```

***

## **tag**

> Создает отметки (теги) на коммите, которые могут содержать информацию
```bash
git tag <tag_name>  # Создаст тег на текущем коммите.
git tag <tag_name> <hash_cmt>  # Создаст тег на другом коммите.
git tag [-l | --list]  # Покажет список всех тегов в репозитории.
git tag <tag_name> -d  # Удалит тег.
git tag -a  # Создаст аннотированный тег (как коммит).
```

***

## **cherry-pick**

> Выберет определёный коммит и перемести его на указатель текущей ветки
```bash
git cherry-pick <cmt1> ... <cmtN>  # Будет так <currnt_cmt> <cmt1> ... <cmtN>
```

***

## **diff**

> Показывает разницу изменений для файлов
```bash
git diff  # Покажет разницу между последним коммитом и untracked файлами.
git diff --staged  # Покажет разницу между последним коммитом и tracked файлами.
git dfff HEAD  # Покажет разницу между последним коммитом и рабочим окружением.
```

***

<h2 id="standart-script">
Стандартный сценарий
</h2>

### Если только не был установлен гит:
```bash
git config --global user.name "<name>"
git config --global user.email <email>
```
### Установка редактора по-умолчанию:
```bash
git config --global core.editor <name_editor>
```

### Имя ветки по-умолчанию:
```bash
git config --global init.defaultBranch <name_branch>
```

### Клонировать или создать репозиторий
```bash
git init [name]  # Если name не указано, создаст репозиторйи в той папке, где было указано. Иначе создать в папке name.
git clone <link> <name>  # Клонировать репозиторйи из link, с папке name.
```

***

<h2 id="files">
<b>Работа с файлами</b>
</h2>

<h2 id="delete-files">
Удалить файлы
</h2>

```bash
git rm <file_name>  # Удалить файлы везде, с диска и из индекса
git rm -f <file_name>  # Удалить принудительно файл с диска и из индекса.
git rm --cached <file_name>  # Удаляет файл из индекса, но не с диска.
git restore --staged <file_name>  # Удалить файл из индекса, но не с диска 2. 
```

<br>


<h2 id="rename-files">
Переименовать файлы
</h2>

```bash
git mv <old_file_name> <new_file_name>
```

<br>


<h2 id="restore-files">
Восстановить файлы
</h2>

```bash
git restore <file_name>  # Убрать все изменения и вернуть состояние файла с прерыдущего коммита.
```

<br>


<h2 id="changed-history">
Просмотреть изменения файла
</h2>

```bash
git log --full-history -- <path_file>  # Покажет историю файла, даже если он был удалён.
```

<br>

***

<h2 id="remote-repos">
Работа с удалённым репозиторием
</h2>

### Просмотреть удалённые репозитории
```bash
git remote -v
```

### Добавить удалённый репозиторий
```bash
git remote add <remote_name> <url>
```

### Удалить удалённый репозиторий
```bash
git remote rm <remote_name>
```

### Переименовать удалённый репозиторий
```bash
git remote rename <old_remote_name> <new_remote_name>
```

### Отправить ветку в удалённый репозитрий
```bash
git push <remote_name> <local_branch>
```

### Удалить удалённую ветку в удалённом репозитории
```bash
git push <remote_name> --delete <branch_name>
```

***

<h2 id="branches">
<b>Работа с ветками</b>
</h2>

<h2 id="branch-locale">
Работа с локальными ветками
</h2>

### Создать новую ветку
```bash
git branch <name_branch>
```

### Переключиться на ветку
```bash
git switch <name_branch>
```

### Создать и переключиться на ветку
```bash
git switch -c <name_branch>
```

### Переименовать ветку
```bash
git branch -m <old_branch> <new_branch>
```

### Переместить указатель ветки на другой коммит
```bash
git branch -f <name_branch> <point>
```

### Удалить ветку
```bash
git branch [-d | -D (-f -d)] <name_branch>
```

<br>

<h2 id="branch-remote">
Работа с удалёнными ветками
</h2>

### Для получений обновлений из remote, но не сливая их
```bash
git fetch <remote>
```

### Для получений обновления из remote, посредством слияния / перебазирования в <name_branch>
```bash
git merge | rebase <remote>/<name_branch>
```

***

<h2 id="tags">
Работа с тегами
</h2>

### Для создание тега
```bash
git tag <tag_name>  # Создаст обычный тег на текущем месте.
git tag <tag_name> <hash_cmt>  # Созаст тег на коммите hash_cmt.
```

### Для удаления тега
```bash
git tag -d <tag_name>
```

### Для просмотра тега
```bash
git show <tag_name>
```

### Для перехода на тег
```bash
git checkout <tag_name>
```

### Для отправки тегов в удалённый репозиторий
```bash
git push <remote> <teg_name>  # Для отправки одно обычного тега.
git push <remote> --tags  # Для отправки всех обычных тегов.
git push <remote> --follow-tags  # Для отправки всех аннотированных тегов.
```

### Для удаления тегов с удалённого репозитория
```bash
git push <remote> --delete <tag_name>
```

***

<h2 id="stashes">
Работа со стешем
</h2>

### Спрятать не зафиксированные наработки
```bash
git stash
```

### Увидить список закладок*
```bash
git stash list
```

### Восстановить последний стеш из списка
```bash
git stash apply  # Не удалит его из списка.
```

### Восстановить последний стеш из списка и удалить его
```bash
git stash pop
```

### Восстановить определенный стеш из списка
```bash
git stash apply stash@{ID}  # Удалить стеш с ID из списка.
```

### Восстановить последний стеш из списка в определённую ветку
```bash
git stash branch <branch_name>  # Создаст отдельную ветку и применит туда стеш.
```

### Удалить определённый стеш из списка
```bash
git stash drop stash@{ID}
```


***

<h2 id="rare-cases">
<b>Редкие случаи</b>
</h2>

<h2 id="diff-branches">
Посмотреть разницу между ветками
</h2>

```bash
git log <branch1>..<branch2>
git log <local_branch>..<remote>/<remote_branch>  # Для просмотра разницы между локальной и удаленной веткой.
```
За место log можно использовать любой другой формат вывода разницы

<br>


<h2 id="lot-commits">
Изменить несколько коммитов
</h2>

```bash
git rebase -i HEAD~n  # Начать редактирование последних n коммитов.
git rebase --amend  # Во время редактирования изменить имя коммита.
git rebase --continue  # Во время редактирования пропустить коммит.
```

<br>


<h2 id="new-branch-pos">
Переместить ветку в другое место
</h2>

```bash
git branch -f <name_branch> <point>
```
Point может быть другая ветка, коммит или HEAD~n, где n кол-во коммитов от текущего положения HEAD

<br>

<h2 id="remove-last-commit">
Удалить последний коммит (Откатиться назад на один коммит)
</h2>

```bash
git reset --hard HEAD^
```
<br>
