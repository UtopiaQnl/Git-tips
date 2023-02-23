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
gti config --global credential.helper <save_data>  # Куда сохранять данные - wincred    
```

>Для настройки инструментов (***.tool):

```bash
git config merge.tool <path_to_tool>  # Утилита для слияния.
git config dif.tool <path_to_tool>  # Утилита для сравнения.
```

>Для настройки клонирования сторонних репозиториев (clone):

```bash
git config --global clone.defaultRemoteName <name_remote_branch>  # Имя удалённой ветки по-умолчанию. Origin
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