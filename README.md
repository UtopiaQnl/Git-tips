# GIT Commmands

# Features

-   [config](#config)
-   [init](#init)
-   [clone](#clone)
-   [add](#add)
-   [status](#status)
-   [log](#log)
-   [branch](#branch)
-   [checkout](#checkout)
-   [commit](#commit)
-   [push](#push)
-   [remote](#remote)
    -   [fetch](#fetch)
    -   [pull](#pull)
-   [stash](#stash)
-   [tag](#tag)
-   [cherry-pick](#cherry-pick)
-   [rebase](#rebase)
-   [merge](#merge)
    -   [mergetool](#mergetool)
-   [diff](#diff)
    -   [difftool](#difftool)
-   [Стандартный сценарий](#standart-script)
-   [Работа с файлами](#files)
    -   [Удалить файлы](#delete-files)
    -   [Переименовать-файлы](#rename-files)
-   [Работа с удаленным репозиторием](#remote-repos)
-   [Работа с ветками](#branches)
    -   [Работа с ветками (локальными)](#branch-locale)
    -   [Работа с ветками (удаленными)](#branch-remote)
-   [Работа с тегами](#tags)
-   [Редкие случаи](#rare-cases)
    -   [Посмотреть разницу между ветками](#diff-branches)
    -   [Изменить несколько коммитов](#lot-commits)
    -   [Переместить ветку в другое место](#new-branch-pos)

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
git branch [-c | --create] <br_name>  # Создасть ветку br_name
git branch [-d | --delete] <br_name>  # Удалить ветку br_name
git branch -m <old_name> <new_name>  # Переименует ветку
git branch -u <remote>  # Привязать текуюю ветку к удалённой
git branch -f <br_name> <point>  # Заставить указывать ветку на point
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
git init [name]  # Если name не указано, создаст репозиторйи в той папке, где было указано. Иначе создать в папке name
git clone <link> <name>  # Клонировать репозиторйи из link, с папке name
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

<h2 id="branch-remote">
Работа с удалёнными ветками
</h2>



***

<h2 id="rare-cases">
<b>Редкие случаи</b>
</h2>

<h2 id="diff-branches">
Посмотреть разницу между ветками
</h2>

```bash
git log <branch1>..<branch2>
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