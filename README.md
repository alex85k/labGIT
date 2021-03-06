Изучаем GIT на практике
=========

Термины:
-------

  - Хранилище, репозиторий, repository = вся история сохранений
     - физически - папка с подпапкой .git
     - может располагаться на удалённом сервере
     - в каждой копии хранилища хранится вся история (по крайней менре, вся исторя нескольких веток): Git - **распределенная** система контроля версий.
  - Коммит, изменение, commit = сохраненное состояние каталога
     - физически хранятся только изменения файлов
     - изменение текстового файла - это информация о том, какие строки добавлены, удалены, изменены
     - у каждого коммита есть автор, дата, осмысленное сообщение об изменениях и уникальный **хэш-код**
     - у каждого коммита имеется коммит-предок (предыдущее состояние, относительно которого сохраняются изменения). У коммитов слияния веток несколько предков.
  - Индекс, буферная зона, index, staging area = место, где хранятся изменения, **подготовленные для сохранения**
     - изменение должно быть помещено в буферную зону командой ``git add файл``, только после этого ``git commit`` сохранит его.
     - предназначена для внесения изменнеий по частям и для исключения случайных сохранений
  - Ветка, ветвь, branch = легковесный подвижный указатель на один из коммитов. 
     - В каждый момент ветка указывает на один из коммитов
     - В данный момент активна одна ветка (сменить - ``git checkout имя ветки``)
     - Когда вы сохраняете состояние, на текущую ветку добавляется один коммит и она сдвигается
  - Тег, метка, tag -  указатель на один заданный коммит (например, выпущенная версия 1.2)
     - В отличие от ветки, после создания не изменяется.
  - Слияние - процедура объединения изменений из нескольких (обычно двух) веток
     - слияние может быть выполнено автоматически, если в сливаемых ветках менялись разные файлы или далеко отстоящие строки одного файла
     - в противном случае могут возникнуть **конфликты** -  программист должен вручную объединить противоречащие друг другу изменения и выполнить ``git add``, ``git commit``.
     - даже если конфликтов не было, программа может перестать работать правильно (противоречия логики работы)

Упражнения:
-----

Рекомендуется использовать FAR Manager с доступным в консоли GIT. (Ctrl-O=показать консоль, Вверх-вниз в консоли = история команд, есть автодополнение)

1.  Создайте рабочую папку (Far-F7). Все команды выполняем в ней.
2.  Создайте текстовый файл ``readme.txt`` (Shift-F4, сохранять - F2)
3.  Создайте пустое хранилище в этой папке:    появится папка ``.git``, в ней вся история и метаданные. Выполните в созданной папке в консоли команду 
   ```bash
   git init
   ```

4.  Посмотрите состояние хранилища
   ```bash
   git status
   ```
   readme.txt - неотслеживаемый файл, его нет в истории.
5. Подготовим ``readme.txt`` для сохранения.
   ```bash
   git add readme.txt
   ```
   
6.  ``git status`` покажет его зеленым цветом.

7.  Представьтесь сиcтеме git, чтобы Ваши коммиты не путались с чужими:
   ```
   git config user.name "Akakiy Akakievich"
   git config user.email "akaka@mail.ru"
   ```
   на своей рабочей машине можно добавить флаг ``--global`` (одни настройки на всех).

8. Первый коммит:
 ```bash
 git commit
 ```
  - Что это такое разноцветное? 
     - Это редактор ``vim`` (можно поменять хоть на блокнот) для набора сообщения.     - ``i`` - режим набора текста, стрелки работают 
     - ``Esc`` - завершить набор
     - заклинание ``:wq`` - сохраниться и выйти
  - введите для истории "добавлен readme.txt"
9. Поменяйте файл ``readme.txt`` (добавьте несколько строк)
10. ``git status`` покажет, что файл изменён. Посмотрите, что поменялось:
   ```bash
   git diff
   ```
   
   (этот текст - **патч**. при необходимости его можно применить в любой момент или кому-то послать в текстовом виде)
11. Сохраним изменения, указав сообщение сразу, без редактора.
   ```bash
    git commit -m "добавил немного в readme.txt"
   ```
   
12. Что забыли??? Подготовить файл.
13. ``git add readme.txt`` и повторяем коммит.
14. Посмотрим историю
   ```bash
   git log
   ```
   
15. Удобный графический инструмент 
  ```bash
  gitk
  ``` 
 
   - что добавилось в первом коммите, во втором?
   - найдите хэш первого коммита
16. Скачайте и поместите рядом с ``.git`` файл ``.gitignore`` для проектов Visual Studio (список файлов, на которые ``git`` не должен обращать внимание).
https://raw.githubusercontent.com/github/gitignore/master/VisualStudio.gitignore
17. Добавьте этот файл и сохраните изменения с помощью графической оболочки 
   ```bash
   git gui
   ```

  - Подготовить файлы Ctrl-T (состояние - подготовить для сохранения) (git add)
  - "Сохранить" с вводом сообщения (git commit)
  - Можно использовать "подготовить все", но осторожно.
  - Всегда следите за списком подготовленных изменений
  - Можно подготавливать изменения построчно (выделить строки, контекстное меню)
  - Убрать изменения из подготовленных или отменить их вообще можно в меню "состояние" (есть горячие клавиши)
  - Обновить состояние без перезапуска git gui - F5
  - **Дальше можно пользоваться git gui для сохранения.**

18. Создайте проект Visual Studio Windows Forms в той же папке хранилища. Сразу добавьте вторую форму (пока пустую).
19. Сохраните изменения, добавив все файлы (проект, ресурсы, код форм) (сообщение типа "создан проект VS").
20. ЗАКРОЕМ Visual Studio и вернёмся на старое состояние:
    ```bash
    git checkout хэш_первого_коммита
    ```

  файлы проекта пропали
21. Вернём всё назад
   ```bash
   git checkout master
   ```
   
   (master - имя ветки по умолчанию)
22. Ещё раз вернёмся в прошлое
   ```bash
   git checkout HEAD~3
   ```
   
   (3 коммита назад от текущей ветки)
   
23. Ответвимся от старого состояния:
   ```bash
   git branch txt
   ```
    и перейдём на созданную ветку:
   ```bash
   git checkout txt
   ```
   
   Можно было сразу сделать 
   ```bash
   git checkout -b txt
   ```
   
24. Поменяем файл readme.txt и сделаем в новой строке какую-нибудь опечатку. Сохраним изменения.
25. Еще раз поменяем файл ``readme.txt``, исправив ошибку. Чтобы коммит с опечаткой не раздувал историю, можно его переделать:

    ```bash
    git add readme.txt
    git commit --amend
    ```
    
    (``:wq`` для подтверждения)

26. Посмотрите историю всех веток:
    ```bash
    gitk --all
    ```
    
27. Теперь осталось соединить обе ветки в одну. При этом в ней окажутся все изменения. Перейдите на ветку ``master`` и влейте в неё ветку ``txt``:
    ```bash
    git checkout master
    git merge txt
    ```
    
28. Есть конфликт в файле readme.txt . Исправим его вручную и сохраним git gui. Посмотрите дерево gitk.


Упражнения с проектом Visual Studio:
-----

1. Откройте проект в хранилище. 
2. Создайте ветку ``menu`` (git checkout -b menu)
3. Добавьте на первую форму меню (MenuStrip)  с несколькими пунктами.
4. Сохраните изменения в веткe menu (git gui)
