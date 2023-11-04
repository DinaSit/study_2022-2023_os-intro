---
## Front matter
title: "Шаблон отчёта по лабораторной работе"
subtitle: "Простейший вариант"
author: "Дмитрий Сергеевич Кулябов"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить идеологию и применение средств контроля версий.  
Освоить умения по работе с git.

# Задание

* Создать базовую конфигурацию для работы с git.
* Создать ключ SSH.
* Создать ключ PGP.
* Настроить подписи git.
* Зарегистрироваться на Github.
* Создать локальный каталог для выполнения заданий по предмету.

# Выполнение лабораторной работы

## Установка программного обеспечения
Установим git при помощи команды:  
dnf install git

Установим gh при помощи команды:  
dnf install gh

## Базовая настройка git
* Зададим имя и email владельца репозитория при помощи следующих команд:  
  git config --global user.name "Name Surname"  
  git config --global user.email "work@mail"

* Настроим utf-8 в выводе сообщений git командой:  
  git config --global core.quotepath false

* Зададим имя начальной ветки (будем называть её master):  
  git config --global init.defaultBranch master

* Параметр autocrlf:  
  git config --global core.autocrlf input

* Параметр safecrlf:  
  git config --global core.safecrlf warn

## Созданиче ключа ssh
* по алгоритму rsa с ключём размером 4096 бит:  
  ssh-keygen -t rsa -b 4096

* по алгоритму ed25519:  
  ssh-keygen -t ed25519
  
## Создание ключа pgp
* Генерируем ключ при помощи команды:  
  gpg --full-generate-key

* Из предложенных опций выбираем:
  * тип RSA and RSA;
  * размер 4096;
  * выберите срок действия; значение по умолчанию — 0 (срок действия не истекает никогда).
* GPG запросит личную информацию, которая сохранится в ключе:
  * Имя (не менее 5 символов).
  * Адрес электронной почты.
    * При вводе email убедитесь, что он соответствует адресу, используемому на GitHub.
  * Комментарий. Можно ввести что угодно или нажать клавишу ввода, чтобы оставить это поле пустым.

## Настройка github
Создайте учётную запись на https://github.com.  
Заполните основные данные на https://github.com.

## Добавление PGP ключа в GitHub
* Выводим список ключей и копируем отпечаток приватного ключа:
  gpg --list-secret-keys --keyid-format LONG

* Отпечаток ключа — это последовательность байтов, используемая для идентификации более длинного, по сравнению с самим отпечатком ключа.
* Формат строки:  
  sec   Алгоритм/Отпечаток_ключа Дата_создания [Флаги] [Годен_до]
      ID_ключа
* Cкопируйте ваш сгенерированный PGP ключ в буфер обмена:  
  gpg --armor --export <PGP Fingerprint> | xclip -sel clip
* Перейдите в настройки GitHub (https://github.com/settings/keys), нажмите на кнопку New GPG key и вставьте полученный ключ в поле ввода.

## Настройка автоматических подписей коммитов git
* Используя введёный email, укажите Git применять его при подписи коммитов:  
  git config --global user.signingkey <PGP Fingerprint>  
  git config --global commit.gpgsign true  
  git config --global gpg.program $(which gpg2)

## Настройка gh
* Для начала необходимо авторизоваться  
  gh auth login
* Утилита задаст несколько наводящих вопросов.
* Авторизоваться можно через броузер.

## Сознание репозитория курса на основе шаблона
* Необходимо создать шаблон рабочего пространства (см. Рабочее пространство для лабораторной работы).
* Например, для 2022–2023 учебного года и предмета «Операционные системы» (код предмета os-intro) создание репозитория примет следующий вид:  
  mkdir -p ~/work/study/2022-2023/"Операционные системы"  
  cd ~/work/study/2022-2023/"Операционные системы" 
  gh repo create study_2022-2023_os-intro --template=yamadharma/course-directory-student-template --public  
  git clone --recursive git@github.com:<owner>/study_2022-2023_os-intro.git os-intro  

## Настройка каталога курса
* Перейдите в каталог курса:  
  cd ~/work/study/2022-2023/"Операционные системы"/os-intro
* Удалите лишние файлы:  
  rm package.json
* Создайте необходимые каталоги:  
  echo os-intro > COURSE  
  make
* Отправьте файлы на сервер:  
  git add .  
  git commit -am 'feat(main): make course structure'  
  git push

Описываются проведённые действия, в качестве иллюстрации даётся ссылка на иллюстрацию (рис. @fig:001).
![Название рисунка](image/placeimg_800_600_tech.jpg){#fig:001 width=70%}

# Выводы

В ходе выполнения лабораторной работы я изучила идеологию и применение средств контроля версий, а также освоила умения по работе с git.

# Контрольные вопросы

1. Что такое системы контроля версий (VCS) и для решения каких задач они предназначаются?
   
3. Объясните следующие понятия VCS и их отношения: хранилище, commit, история, рабочая копия.
   
5. Что представляют собой и чем отличаются централизованные и децентрализованные VCS? Приведите примеры VCS каждого вида.
   
7. Опишите действия с VCS при единоличной работе с хранилищем.
   
9. Опишите порядок работы с общим хранилищем VCS.
    
11. Каковы основные задачи, решаемые инструментальным средством git?
    
13. Назовите и дайте краткую характеристику командам git.
    
15. Приведите примеры использования при работе с локальным и удалённым репозиториями.
    
17. Что такое и зачем могут быть нужны ветви (branches)?
    
19. Как и зачем можно игнорировать некоторые файлы при commit?
    
