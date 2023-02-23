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
-   [Стандартный-сценарий](#standart)
-   [Работа-с-файлами](#files)
    -   [Удалить-файлы](#delete-files)
    -   [Переименовать-файлы](#rename-files)
-   [Работа-с-удаленным-репозиторием](#remote-repos)
-   [Работа-с-ветками](#branches)
    -   [Работа-с-ветками-(локальными)](#work-branch-locale)
    -   [Работа-с-ветками-(удаленными)](#work-branch-remote)
-   [Работа-с-тегами](#tags)
-   [Редкие-случаи](#rare-cases)
    -   [Посмотреть-разницу-между-ветками](#diff-branches)
    -   [Изменить-несколько-коммитов](#lot-commits)

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

>Для настройки данных пользователя (USER):

```bash
git config --global user.name <name>  # Имя коммитера.
git config --global user.email <email>  # Почта коммитера.
```

>Для настройки инициализации репозитория (init):

```bash
git config --global init.defaultBranch <name_branch>  # Имя основной ветки ри инициализации репозитория.
```

>Для настройки вспомогательных инструментов (core):

```bash
git config --global core.editor <name_editor>  # Редактор коммитов по умолчанию.
```

>Для настройки полномочий (credential.helper):

```bash
git config --global credential.helper cache [--timeout <sec>]  # Сохраняет данные в кеше на <sec>. По умолчанию 900.
git config --global credential.helper store [--file <path>]  # Сохраняет данные в файле по пути <path>. По умолчанию в ~/.git-credentials
gti config --global credential.helper <save_data>  # Куда сохранять данные - wincred.  
```

>Для настройки инструментов (***.tool):

```bash
git config merge.tool <path_to_tool>  # Утилита для слияния.
git config dif.tool <path_to_tool>  # Утилита для сравнения.
```

>Для настройки клонирования сторонних репозиториев (clone):

```bash
git config --global clone.defaultRemoteName <name_remote_branch>  # Имя удалённой ветки по-умолчанию.
```

>Для настройки цветов (color):

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
