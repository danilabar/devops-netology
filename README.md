# devops-netology
first modifie

Будут проигнорированы:
- локальные каталоги .terraform
- файлы удовлетворяющие маскам заданных расширений файлов
- log файл журнала сбоев
- файлы переопределения
- файлы конфигурации CLI

## 2.4. Инструменты Git
1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
    - `git log --pretty=oneline -1 aefea` или `git log --pretty=format:"%H %s" -1 aefea` или `git show aefea`\
    `aefead2207ef7e2aa5dc81a34aedf0cad4c32545 Update CHANGELOG.md`
2. Какому тегу соответствует коммит `85024d3`?
    - `git log --pretty=oneline -1 85024d3` или `git log --simplify-by-decoration -1 85024d3`\
    `85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23) v0.12.23`
3. Сколько родителей у коммита `b8d720`? Напишите их хеши.
    - `git log --pretty=%P -n 1 b8d720` или `git show --pretty=%P b8d720`\
    `56cd7859e05c36c06b56d013b55a252d0bb7e158` и `9ea88f22fc6269854151c571162c5bcf958bee2b`
4. Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.
    - `git log --pretty=oneline v0.12.23..v0.12.24`
    ```
     33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24) v0.12.24
     b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
     3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
     6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
     5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
     06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
     d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
     4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
     dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
     225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
    ```
5. Найдите коммит в котором была создана функция `func providerSource`, ее определение в коде выглядит так `func providerSource(...)` (вместо троеточего перечислены аргументы).
    - `git log -G "func providerSource\(.*\)" --oneline --reverse`\
    `8c928e835 main: Consult local directories as potential mirrors of providers` - это первый коммит с данной функцией
6. Найдите все коммиты в которых была изменена функция `globalPluginDirs`.
    - С помощью `git log -G "func globalPluginDirs\(.*\)" --oneline --reverse` узнаем файл в котором находится функция
    - `git log -L :globalPluginDirs:plugins.go`
    ```
    78b12205587fe839f10d946ea3fdc06719decb05
    52dbf94834cb970b510f2fba853a5b49ad9b1a46
    41ab0aef7a0fe030e84018973a64135b11abcd70
    66ebff90cdfaa6938f26f908c7ebad8d547fea17
    8364383c359a6b738a436d1b7745ccdce178df47 - Создана
    ```
7. Кто автор функции `synchronizedWriters`?
    - Узнаем комит где была создана функция synchronizedWriters и в каком файле\
    `git log -G "func synchronizedWriters\(.*\)" --oneline --reverse`\
    `5ac311e2a main: synchronize writes to VT100-faker on Windows`
    - Т.к. файл был удалён переключимся на коммит когда он был создан\
    `git checkout 5ac311e2a`
    - Узнаем автора\
    `git blame -L 15,25 synchronized_writers.go`\
      Martin Atkins