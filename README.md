[![Build Status](https://travis-ci.org/komissarovrodion21/lab05.svg?branch=master)](https://travis-ci.org/komissarovrodion21/lab05)
## Laboratory work V

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Установить [**Travis CLI**](https://github.com/travis-ci/travis.rb#installation)
- [x] 8. Выполнить инструкцию учебного материала
- [x] 9. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Первоначальные настройки
```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя> #устанавливаем значение переменной GITHUB_USERNAME
$ export GITHUB_TOKEN=<полученный_токен> #устанавливаем значение переменной GITHUB_TOKEN
```
Настройки для соединения с репозиторием пятой лабораторной работы
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 lab05 #клонирование репозитория lab04 в lab05
$ cd lab05 #выбираем директорию lab05
$ git remote remove origin #отключаемся от удаленного репозитория 4 лабораторной
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05 #подключаемся к удаленному репозиторию 5 лабораторной
```
Вносим параметры в конфиг файла для travis-ci - .travis.yml
```ShellSession
$ cat > .travis.yml <<EOF
language: cpp #показываем что язык программирования с++
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF 
#параметр script отвечает за дальнейшую сборку проекта
script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF
#вносим различные пакеты для сборки проекта
addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```ShellSession
$ travis login --github-token ${GITHUB_TOKEN} #авторизуемся своим GITHUB аккаунтом, используя созданный нами токен
```
отображаем предупреждения или ошибки в файле .travis.yml
```ShellSession
$ travis lint
```
вносим изменения в REAMDE.md
```ShellSession
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
```

```ShellSession
$ git add .travis.yml #добавляем .travis.yml в подтвержденные файлы
$ git add README.md #добавляем README.md в подтвержденные файлы
$ git commit -m"added CI" #создаем коммит
$ git push origin master #выгружаем локальную репозиторий в удаленный репозиторий 5 лабораторной
```

```ShellSession
$ travis lint #отображаем предупреждения или ошибки в файле .travis.yml
$ travis accounts #отображаем список аккаунтов
$ travis sync #обновляем информацию о пользователях и репозиториях
$ travis repos #выводим список репозиториев
$ travis enable #с помощью этой команды мы можем активировать репозиторий в Travis
$ travis whatsup #показываем последние изменения в репозиториях
$ travis branches #показываем последние изменения в ветках
$ travis history #отображем всю историю
$ travis show #отображаем информацию о последней сборке проекта
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2017 Братья Вершинины
```
