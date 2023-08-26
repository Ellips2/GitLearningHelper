# Git Learning Helper
Это проект для помощи в изучении систем контроля версий.

**СКВ** (система контроля версий) / VCS (version control system) / SCM (Source control management).

_Популярные VCS:_ Git, Mercurial, Subversion.

**Версия / ревизия** – одно изменение или группа изменений. Кто, что и когда внес + комментарии.

# Команды
pwd (print working directory)

Операнды для использования с командами:
1. Символ «~» – домашняя директория
2. Отдельный символ «/» - корневая директория
3. Чтобы перейти выше используют «..», при этом чтобы перейти на 2 папки выше можно указать «../..» на 3 «../../..».
4. Чтобы обратиться к текущей папке используют «.».
cd (change directory). Если в названии папки есть пробелы, то используют кавычки. 

ls (list directory content). ls -a – покажет все содержимое включая скрытые файлы и папки.

touch – создать файл. Указываем как путь от текущей директории, можно сразу несколько файлов создать, указав их через пробел.

mkdir – создать папку. Чтобы создать сразу цепочку вложенных папок используют аргумент «-p» перед цепочкой.

cp (copy) – через пробел сначала указываем что копируем (можно несколько подряд), потом куда копируем.

mv (move) – через пробел указываем что переместить (можно несколько), потом куда переместить.

cat (concatenate and print) – чтение.

echo “Какой-то текст” > filename.txt – добавить текст в файл с полной заменой содержимого.

echo “Какой-то текст” >> filename.txt – добавить к содержимому файла текст.

rm (remove) – удалить файл

rmdir (remove directory) – удалить директорию, если она пустая.

rm -r (ключ -r от англ. recursive) – удалить файл или папку вместе с содержимым.

rm -rf (ключ f от англ. Force - заставить) – такая вариация избавит вас от вопросов системы типа «Вы точно хотите удалить этот файл? А этот? И этот тоже?».

notepad.exe filePath fileName.fileExtension – открыть файл через блокнот. Можно не указывать  путь, если ты уже в папке с файлом.

# Советы и приемы
«&&» - операнд для выполнения нескольких команд сразу в одной строке

Двойной «Tab» – автозаполнение команд и названий файлов и папок.

Тройной «Tab» – вывод команд/папок/файлов начинающихся одинаково

# Работа с git
git config --global user.name (user.email) – задание основных параметров.

cat ~/.gitconfig – вывод основных настроек.

git config –list – вывод всех настроек.

git init – сделать текущую папку репозиторием.

rm -rf .git – отменить у текущей папки функцию репозитория, удалив служебную папку «.git», в которой хранится вся история изменений. И тогда вся история будет удалена и сохранится только последняя версия файлов.

git status – проверить состояние репозитория.

git add –all или «.» – добавить все файлы в текущей папки или соответственно всю папку целиком в трек отслеживания изменений. Эта команда запоминает состояние файлов, но не сохраняет их в репозиторий.

git commit – сделать коммит (от англ. «совершить» / «фиксировать»), т.е. сохранить данные в репозиторий.

	-m (от англ. message) – добавляет к коммиту сообщение.

	root-commit – ремарка у коммита, который был сделан самым первым. У остальных такой заметки нет.

	mode 100644 – маркер обычного файла.

	mode 100755 – маркер исполняемых файлов (exe).

	mode 120000 – маркер файлов-ссылок в Linux.

git log – просмотр истории коммитов.

git log –oneline – сокращенный лог. Если выход из просмотра логов не произошёл автоматически, нажмите клавишу Q (от англ. Quit — «выйти»). Хэши при этом тоже будут сокращенные, но ровно настолько, чтобы они были уникальными в текущем списке.

# Работа с GitHub
SSH-ключи (от англ. Secure Shell — «безопасная оболочка») – протокол обмена данными, который предусматривает шифрование с помощью публичного и приватного ключа (первый для шифрования кем угодно чего угодно, второй для расшифровки, он должен быть только у вас). Используется для доступа к удаленным серверам или репозиториям.

Обычно SSH-ключи лежат в домашней директории.

## Генерация SSH ключа:
ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"

или

ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"

ls -la .ssh/ – вывод списка созданных ключей с доп. инфой (владелец, дата и др.).

ls -a ~/.ssh – вывод списка созданных ключей.


В итоге получится два ключа: один без расширения (приватный), второй с расширением .pub (публичный).

clip < путь к файлу.расширение – копирование файла в буфер обмена. В качестве альтернативы можно использовать команду cat, чтобы распечатать содержимое и скопировать вручную.

ssh -T git@github.com – проверка корректности SSH-ключа.

Если это первое подключение, то будет выведен публичный ключ сервера, он должен совпадать с одним из тех ключей, которые официально опубликованы гитом (GitHub's SSH key fingerprints): https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints

## Cоединение локального репозитория с удаленным необходимо
Необходимые шаги:
1. Перейти в папку локального репозитория через cd
2. Выполнить команду: git remote add “название удаленного репозитория (обычно это origin)” “адрес со страницы github репозитория, сгенерированный по кнопке HTTPS”. 
3. Проверка, что репозитории связанны: git remote или git remote -v (v от англ. Verbose – подробный).


## Синхронизация локального и удаленного репозиториев:
git push -u «имя удал. репозитория» «имя ветки удал. репозитория» – отправить изменения на удаленный репозиторий. Флаг -u связывает локальную ветку с используется только при первой синхронизации. Обычно имя репозитория origin, а имя ветки master или main.


## Файл Readme

Правила составления readme:
1. Название проекта
2. Краткое описание
a. Кем создан
b. Зачем
c. Какие решает задачи
d. Какие закрывает проблемы
3. Технологии, которые использовались. 
4. В чем отличие проекта от аналогичных.
5. Документация проекта – инструкции установки и пользования программой. 
6. Планы проекта если они есть.


Форматирование с помощью «маркдаун» (markdown) разметки:
1. Заголовки

• # H1 — заголовок первого уровня, самый большой

• ## H2 — заголовок второго уровня, поменьше

• ### H3

• #### H4

• ##### H5

• ###### H6 — заголовок шестого уровня, самый маленький

2. Черта, разделяющая текст «---»
3. Разрыв строки – два пробела или <br>
4. Новый параграф – два переноса (два раза enter).
5. Текст курсивом – *текст* или _текст_
6. Текст полужирным **текст**
7. Зачеркнутый текст – ~~текст~~
8. Ненумерованные списки оформляются звездочкой с пробелом «* пункт 1, * пункт 2, …» или дефисом с пробелом «- пункт 1, пункт 2, …».
9. Текст как ссылка – [Яндекс](https://www.yandex.ru)
10. Title. Подсказка при наведении на ссылку – [Яндекс](https://www.yandex.ru "Я Yandex!")
11. Текст как код – текст заключается в грависы (тройные косые кавычки ```). После открывающего грависа указывается язык программирования. Второй гравис всегда располагается с новой строки. Пример:
```bash 
ls - la
```
Или:
```html
<h1>А я просто текст</h1>
```
https://www.markdownguide.org/cheat-sheet/
https://gist.github.com/fomvasss/8dd8cd7f88c67a4e3727f9d39224a84c

# Навигация по коммитам. Статусы файлов
Для каждого коммита существует свой хэш, который служит идентификатором.

Git ведет таблицу соответствия хэшей и информации о коммите (автор, дата, комментарий, содержимое коммита) в служебных файлах в скрытой папке «.git».

Для хэширования Git использует алгоритм SHA-1.

Head – фай в скрытой папке «.git», хранящий хэш последнего коммита. Также этот коммит отмечается словом «HEAD» при выводе лога всех коммитов (git log).
cat head – узнать, где находится head.

Если нужно передать в аргумент команды хэш последнего коммита, достаточно написать слово «head».

# Статусы файлов

1. Untracked – не отслеживаемый. Это новый файл, о котором Git знает, но не хранит историю его изменений.
2. Staged / indexed / cached – подготовленный. Файл в списке staging area (синонимы: index - каталог, cache - кэш) – список тех, кто войдет в коммит. Добавляется с помощью команды «git add». Чтобы убрать файл из списка на коммит есть команда «git restore <file>».
3. Modified – измененный. Файл, чья текущая версия отличается от последней сохраненной.
4. Tracked – отслеживаемый. Файл, историю изменения которого хранит Git. К таким файлам относятся и закоммиченные файлы и подготовленные, и измененные.

Файлы, которые ранее уже попадали в список на коммит, но в последствии были изменены и снова добавлены в этот список не будут иметь приставки new при выводе от команды «git status»

Файлы, которые были закоммичены и в последствии не менялись, в выводе git status отображаться не будут, чтобы не засорять экран излишним количеством информации.

### Жизненный цикл файлов в Git:

```mermaid
graph TD;
    untracked -- git add --> staged;
    modified -- git add --> staged;
    staged -- git commit --> tracked;
    tracked -- Изменения --> modified;
    staged -- Изменения --> modified;
```

# Правила оформления коммитов
1. Сообщение не длиннее 72 символов. Это пошло от того, что команда git log --oneline может вывести максимум 72 символа.
2. Информативность. Что и где изменено.
3. В разных компаниях могут быть свои правила оформления, их надо уточнять.

Стили оформления:
1. Корпоративный. В начале указывают ID задачи, а потом текст. Пример: "LGS-239: дополнить список пасхалок новыми числами". Как правило так делают в компаниях, которые используют СКВ «Jira», чтобы связывать задачи проекта и коммиты.
2. Conventional Commits (англ. «соглашение о коммитах»). Подходит для репозиториев с исходным кодом программ. Шаблон: <тип изменения>: <сообщение>. 
Типы:
* fix – исправление.
* feat – новая фича.
* [Остальные типы](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#спецификация)

3.	GitHub-стиль. В Github можно вести список задач (issue) с id. Если коммит закрывает задачу, то её id указывается в произвольном месте сообщения. Пример: «Исправить #334, добавить график температуры».
