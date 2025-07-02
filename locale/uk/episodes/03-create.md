---
title: Робота з файлами та каталогами
teaching: 30
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Створити ієрархію каталогів, яка відповідає заданій схемі.
- Створити файли в цій ієрархії за допомогою редактора або шляхом копіювання та перейменування файлів, що вже існують.
- Видалити, скопіювати та перемістити вказані файли та/або каталоги.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу створювати, копіювати та видаляти файли і каталоги?
- Як я можу редагувати файли?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Створення каталогів

Тепер ми знаємо, як досліджувати файли та каталоги, але як їх створювати?

У цьому уроці ми дізнаємося про створення та переміщення файлів і каталогів на прикладі каталогу `exercise-data/writing`.

### Step one: see where we are and what we already have

Ми все ще маємо бути у каталозі `shell-lesson-data` на Робочому столі (англ. Desktop), що ми можемо перевірити за допомогою:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Далі ми перейдемо до каталогу `exercise-data/writing` і подивимося, що у ньому міститься:

```bash
$ cd exercise-data/writing/
$ ls -F
```

```output
haiku.txt LittleWomen.txt
```

### Створення каталогу

Створимо новий каталог з назвою `thesis` за допомогою команди `mkdir thesis` (яка не має виводу):

```bash
$ mkdir thesis
```

Як ви можете здогадатися з її назви, команда `mkdir` означає 'створити каталог' (англ. 'make directory').
Оскільки `thesis` є відносним шляхом
(тобто не має початкової косої риски, як `/what/ever/thesis`),
новий каталог буде створено у поточному робочому каталозі:

```bash
$ ls -F
```

```output
haiku.txt  LittleWomen.txt  thesis/
```

Оскільки ми щойно створили каталог `thesis`, у ньому ще нічого немає:

```bash
$ ls -F thesis
```

Зауважте, що команда `mkdir` не тільки створює окремі каталоги по одному за раз.
Параметр `-p` дозволяє команді `mkdir` створювати каталог із вкладеними підкаталогами за одну операцію:

```bash
$ mkdir -p ../project/data ../project/results
```

Параметр `-R` з командою `ls` покаже усі вкладені підкаталоги у каталозі.
Скористаймось `ls -FR` для рекурсивного зображення нової ієрархії каталогів, яку ми щойно створили у каталозі `project`:

```bash
$ ls -FR ../project
```

```output
../project/:
data/  results/

../project/data:

../project/results:
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Два способи зробити одне й те саме

Використання терміналу для створення каталогу нічим не відрізняється від використання файлового провідника.
Якщо ви зараз відкриєте поточний каталог за допомогою графічного провідника файлів вашої операційної системи, там також з'явиться каталог `thesis`.
Хоча термінал і файловий провідник - це два різні способи взаємодії з файлами, самі файли й каталоги одні й ті ж самі.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Доречні імена для файлів і каталогів

Використання надто складних імен для файлів і каталогів може ускладнити роботу в командному рядку. Ось кілька корисних порад щодо вибору ефективних імен.

1. Не використовуйте пробіли.

Пробіли можуть зробити назву більш змістовною, але оскільки вони використовуються для відокремлення аргументів у командному рядку, краще уникати їх у назвах файлів і каталогів.
Ви можете використовувати `-` або `_` (наприклад, `north-pacific-gyre/` замість `north pacific gyre/`).
Щоб перевірити це, спробуйте набрати `mkdir north pacific gyre` і подивіться, який каталог (або каталоги!)
буде створено, перевірив це за допомогою `ls -F`.

2. Не починайте назву з `-` (тире).

Команди розглядають назви, що починаються з `-`, як опції.

3. Використовуйте літери, цифри, `.` (крапку), `-` (тире) і `_` (підкреслення).

Багато інших символів мають особливе значення у командному рядку.
Деякі з них ми розглянемо у цьому уроці.
Існують спеціальні символи, які можуть спричинити неправильну роботу команди й навіть призвести до втрати даних.

Якщо вам потрібно звернутися до назв файлів або каталогів, які містять пробіли чи інші спеціальні символи, вам слід узяти назву в одинарні [лапки](https://www.gnu.org/software/bash/manual/html_node/Quoting.html) (`''`).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  instructor

Learners can sometimes get trapped within command-line text editors
such as Vim, Emacs, or Nano. Closing the terminal emulator and opening
a new one can be frustrating as learners will have to navigate to the
correct folder again. Для пом'якшення цієї проблеми ми радимо викладачам використовувати той самий текстовий редактор, що й учні під час семінарів (у більшості випадків Nano).

::::::::::::::::::::::::::::::::::::::::::::::::::

### Створення текстового файлу

Перейдімо до каталогу `thesis` за допомогою `cd`, а потім запустимо текстовий редактор Nano та створимо файл з назвою `draft.txt`:

```bash
$ cd thesis
$ nano draft.txt
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Який редактор використовувати?

When we say, '`nano` is a text editor' we really do mean 'text'. It can
only work with plain character data, not tables, images, or any other
human-friendly media. Ми використовуємо його у прикладах, оскільки це один із найпростіших текстових редакторів. Однак, через це він може виявитися недостатньо потужним або гнучким для складніших завдань, які вам потрібно буде виконати після завершення цього семінару. On Unix systems (such as Linux and macOS),
many programmers use [Emacs](https://www.gnu.org/software/emacs/) or
[Vim](https://www.vim.org/) (both of which require more time to learn),
or a graphical editor such as [Gedit](https://projects.gnome.org/gedit/)
or [VScode](https://code.visualstudio.com/). У Windows, можливо, ви захочете скористатися [Notepad++](https://notepad-plus-plus.org/).  Операційна система Windows також має вбудований редактор з назвою `notepad`, який можна запустити з командного рядка так само, як і `nano` для цього семінару.

Незалежно від того, яким редактором ви користуєтеся, вам потрібно знати, де він шукає і зберігає файли. Якщо ви запускаєте його з термінала, він (імовірно) використовуватиме ваш поточний робочий каталог як розташування за замовчуванням. Однак, якщо ви використовуєте меню "Пуск" вашого комп'ютера, файли за замовчуванням можуть зберігатися замість цього на робочому столі або в каталозі "Документи" (Documents). Ви можете змінити це, перейшовши до іншого каталогу під час першого виконання команди "Зберегти як..." ("Save As...").

::::::::::::::::::::::::::::::::::::::::::::::::::

Наберемо кілька рядків тексту.

![](fig/nano-screenshot.png){alt="Скриншот текстового редактора nano в дії з текстом "У минулому це було - публікуй чи зникни, а наразі стало - ділися та процвітай"}

Як тільки ми будемо задоволені нашим текстом, нам треба використати комбінацію <kbd>Ctrl</kbd>\+<kbd>O</kbd> (утримуючи клавішу <kbd>Ctrl</kbd> or <kbd>Control</kbd>, натисніть клавішу <kbd>O</kbd>), щоб зберегти наші дані на диск. Потім нам буде запропоновано вказати ім’я файлу, у якому зберігатиметься наш текст. Натисніть <kbd>Return</kbd>, щоб прийняти запропоновану за замовчуванням назву `draft.txt`.

Як тільки файл було збережено, скористаємось комбінацією клавіш <kbd>Ctrl</kbd>\+<kbd>X</kbd>, щоб вийти з редактора і повернутися до термінала.

:::::::::::::::::::::::::::::::::::::::::  callout

## Клавіша Control, Ctrl або ^

Клавіші Control також називається клавішею 'Ctrl'. There are various ways
in which using the Control key may be described. Наприклад, ви можете побачити вказівку натиснути клавішу <kbd>Control</kbd> і, утримуючи її натиснутою, потім натиснути клавішу <kbd>X</kbd>, описану будь-яким з наступних способів:

- `Control-X`
- `Control+X`
- `Ctrl-X`
- `Ctrl+X`
- `^X`
- `C-x`

У nano, у нижній частині екрана ви побачите `^G Get Help ^O WriteOut`.
Це означає, що ви можете скористатися `Control-G` для отримання довідки й `Control-O` для збереження вашого файлу.

::::::::::::::::::::::::::::::::::::::::::::::::::

Після завершення роботи команда `nano` не залишає жодних даних на екрані, але `ls` тепер показує, що ми створили файл з назвою `draft.txt`:

```bash
$ ls
```

```output
draft.txt
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Створення файлів іншим способом

Ми побачили, як створювати текстові файли за допомогою редактора `nano`.
Тепер спробуйте виконати наступну команду:

```bash
$ touch my_file.txt
```

1. Що зробила команда `touch`?
  When you look at your current directory using the GUI file explorer,
  does the file show up?

2. Use `ls -l` to inspect the files.  How large is `my_file.txt`?

3. When might you want to create a file this way?

:::::::::::::::  solution

## Відповідь

1. The `touch` command generates a new file called `my_file.txt` in
  your current directory.  You
  can observe this newly generated file by typing `ls` at the
  command line prompt.  `my_file.txt` can also be viewed in your
  GUI file explorer.

2. When you inspect the file with `ls -l`, note that the size of
  `my_file.txt` is 0 bytes.  In other words, it contains no data.
  If you open `my_file.txt` using your text editor it is blank.

3. Some programs do not generate output files themselves, but
  instead require that empty files have already been generated.
  When the program is run, it searches for an existing file to
  populate with its output.  The touch command allows you to
  efficiently generate a blank text file to be used by such
  programs.

:::::::::::::::::::::::::

To avoid confusion later on,
we suggest removing the file you've just created before proceeding with the rest
of the episode, otherwise future outputs may vary from those given in the lesson.
Для цього скористайтеся наступною командою:

```bash
$ rm my_file.txt
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## What's In A Name?

You may have noticed that all of Nelle's files are named 'something dot
something', and in this part of the lesson, we always used the extension
`.txt`.  This is just a convention; we can call a file `mythesis` or
almost anything else we want. However, most people use two-part names
most of the time to help them (and their programs) tell different kinds
of files apart. The second part of such a name is called the
**filename extension** and indicates
what type of data the file holds: `.txt` signals a plain text file, `.pdf`
indicates a PDF document, `.cfg` is a configuration file full of parameters
for some program or other, `.png` is a PNG image, and so on.

This is just a convention, albeit an important one. Files merely contain
bytes; it's up to us and our programs to interpret those bytes
according to the rules for plain text files, PDF documents, configuration
files, images, and so on.

Якщо ви назвете зображення кита у форматі PNG як `whale.mp3`, це не перетворить його якимось чарівним чином на запис пісні кита, хоча це _може_ змусити операційну систему спробувати відкрити його за допомогою музичного плеєра. In this case, if someone double-clicked `whale.mp3` in a file
explorer program, the music player will automatically (and erroneously)
attempt to open the `whale.mp3` file.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Moving files and directories

Returning to the `shell-lesson-data/exercise-data/writing` directory,

```bash
$ cd ~/Desktop/shell-lesson-data/exercise-data/writing
```

In our `thesis` directory we have a file `draft.txt`
which isn't a particularly informative name,
so let's change the file's name using `mv`,
which is short for 'move':

```bash
$ mv thesis/draft.txt thesis/quotes.txt
```

The first argument tells `mv` what we're 'moving',
while the second is where it's to go.
In this case,
we're moving `thesis/draft.txt` to `thesis/quotes.txt`,
which has the same effect as renaming the file.
Sure enough,
`ls` shows us that `thesis` now contains one file called `quotes.txt`:

```bash
$ ls thesis
```

```output
quotes.txt
```

One must be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could
lead to data loss. За замовчуванням `mv` не запитуватиме підтвердження перед перезаписом файлів.
Однак додатковий параметр `mv -i` (або `mv --interactive`) змусить `mv` запросити таке підтвердження.

Note that `mv` also works on directories.

Перемістимо `quotes.txt` до поточного робочого каталогу.
Знову скористаємося `mv`, але цього разу ми використаємо лише назву каталогу як другий аргумент щоб повідомити `mv`, що ми хочемо зберегти назву файлу, але перемістити файл у нове місце.
(Ось чому команда називається 'перемістити'.)
У цьому випадку ми використовуємо спеціальну назву `.` поточного каталогу, про яку ми згадували раніше.

```bash
$ mv thesis/quotes.txt .
```

The effect is to move the file from the directory it was in to the current working directory.
`ls` now shows us that `thesis` is empty:

```bash
$ ls thesis
```

```output
$
```

Alternatively, we can confirm the file `quotes.txt` is no longer present in the `thesis` directory
by explicitly trying to list it:

```bash
$ ls thesis/quotes.txt
```

```error
ls: cannot access 'thesis/quotes.txt': No such file or directory
```

`ls` with a filename or directory as an argument only lists the requested file or directory.
If the file given as the argument doesn't exist, the shell returns an error as we saw above.
We can use this to see that `quotes.txt` is now present in our current directory:

```bash
$ ls quotes.txt
```

```output
quotes.txt
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Moving Files to a new folder

Після виконання наступних команд Джеймі зрозуміла, що помістила файли `sucrose.dat` та `maltose.dat` не до того каталогу.
The files should have been placed in the `raw` folder.

```bash
$ ls -F
 analyzed/ raw/
$ ls -F analyzed
fructose.dat glucose.dat maltose.dat sucrose.dat
$ cd analyzed
```

Fill in the blanks to move these files to the `raw/` folder
(i.e. the one she forgot to put them in)

```bash
$ mv sucrose.dat maltose.dat ____/____
```

:::::::::::::::  solution

## Відповідь

```bash
$ mv sucrose.dat maltose.dat ../raw
```

Recall that `..` refers to the parent directory (i.e. one above the current directory)
and that `.` refers to the current directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Copying files and directories

The `cp` command works very much like `mv`,
except it copies a file instead of moving it.
We can check that it did the right thing using `ls`
with two paths as arguments --- like most Unix commands,
`ls` can be given multiple paths at once:

```bash
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

```output
quotes.txt   thesis/quotations.txt
```

We can also copy a directory and all its contents by using the
[recursive](https://en.wikipedia.org/wiki/Recursion) option `-r`,
e.g. to back up a directory:

```bash
$ cp -r thesis thesis_backup
```

We can check the result by listing the contents of both the `thesis` and `thesis_backup` directory:

```bash
$ ls thesis thesis_backup
```

```output
thesis:
quotations.txt

thesis_backup:
quotations.txt
```

It is important to include the `-r` flag. Якщо ви хочете скопіювати каталог і не вкажете цей параметр ви побачите повідомлення про те, що каталог було пропущено, оскільки `-r` не вказано.

```bash
$ cp thesis thesis_backup
cp: -r not specified; omitting directory 'thesis'
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Renaming Files

Припустімо, що ви створили у поточному каталозі простий текстовий файл, який містить список статистичних тестів, які вам знадобляться для аналізу ваших даних, і назвали його `statstics.txt`

Після створення і збереження цього файлу ви зрозуміли, що неправильно написали назву файлу! Ви хочете виправити помилку. Яку з наведених нижче команд ви можете використати для цього?

1. `cp statstics.txt statistics.txt`
2. `mv statstics.txt statistics.txt`
3. `mv statstics.txt .`
4. `cp statstics.txt .`

:::::::::::::::  solution

## Відповідь

1. Ні.  Хоча це створить файл з правильною назвою, неправильно названий файл все одно існуватиме у каталозі, і його потрібно буде видалити.
2. Yes, this would work to rename the file.
3. Ні, крапка (.) indicates where to move the file, but does not provide a new file name;
  identical file names
  cannot be created.
4. Ні, крапка (.) indicates where to copy the file, but does not provide a new file name;
  identical file names cannot be created.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Moving and Copying

What is the output of the closing `ls` command in the sequence shown below?

```bash
$ pwd
```

```output
/Users/jamie/data
```

```bash
$ ls
```

```output
proteins.dat
```

```bash
$ mkdir recombined
$ mv proteins.dat recombined/
$ cp recombined/proteins.dat ../proteins-saved.dat
$ ls
```

1. `proteins-saved.dat recombined`
2. `recombined`
3. `proteins.dat recombined`
4. `proteins-saved.dat`

:::::::::::::::  solution

## Відповідь

Ми розпочинаємо роботу в каталозі `/Users/jamie/data` і створюємо нову папку з назвою `recombined`.
Другий рядок переміщує (`mv`) файл `proteins.dat` до нового каталогу (`recombined`).
Третій рядок робить копію файлу, який ми щойно перемістили.
Складність полягає у тому, куди саме було скопійовано цей файл.
Нагадаємо, що `..` означає "піднятися на рівень вище", тому скопійований файл тепер знаходиться у `/Users/jamie`.
Зверніть увагу, що `..` інтерпретується відносно поточного робочого каталогу, а **не** відносно розташування файлу, який копіюється.
Отже, єдине, що буде показано за допомогою команди `ls` (у каталозі `/Users/jamie/data`) - це каталог `recombined`.

1. Ні, див. пояснення вище.  Каталог `proteins-saved.dat` розташовано у каталозі `/Users/jamie`
2. Так
3. Ні, див. пояснення вище.  Файл `proteins.dat` знаходиться в каталозі `/Users/jamie/data/recombined`
4. Ні, див. пояснення вище.  Файл `proteins-saved.dat` знаходиться в каталозі `/Users/jamie`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Removing files and directories

Повертаючись до каталогу `shell-lesson-data/exercise-data/writing`,
давайте почистимо цей каталог, видаливши створений нами файл `quotes.txt`.
Для цього ми скористаємося командою Unix `rm` (скорочення від англ. `remove` - видаляти):

```bash
$ rm quotes.txt
```

We can confirm the file has gone using `ls`:

```bash
$ ls quotes.txt
```

```error
ls: cannot access 'quotes.txt': No such file or directory
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Deleting Is Forever

The Unix shell doesn't have a trash bin that we can recover deleted
files from (though most graphical interfaces to Unix do).  Instead,
when we delete files, they are unlinked from the file system so that
their storage space on disk can be recycled. Tools for finding and
recovering deleted files do exist, but there's no guarantee they'll
work in any particular situation, since the computer may recycle the
file's disk space right away.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Using `rm` Safely

What happens when we execute `rm -i thesis_backup/quotations.txt`?
Why would we want this protection when using `rm`?

:::::::::::::::  solution

## Відповідь

```output
rm: remove regular file 'thesis_backup/quotations.txt'? y
```

The `-i` option will prompt before (every) removal (use <kbd>Y</kbd> to confirm deletion
or <kbd>N</kbd> to keep the file).
The Unix shell doesn't have a trash bin, so all the files removed will disappear forever.
By using the `-i` option, we have the chance to check that we are deleting only the files
that we want to remove.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

If we try to remove the `thesis` directory using `rm thesis`,
we get an error message:

```bash
$ rm thesis
```

```error
rm: cannot remove `thesis': Is a directory
```

This happens because `rm` by default only works on files, not directories.

`rm` can remove a directory _and all its contents_ if we use the
recursive option `-r`, and it will do so _without any confirmation prompts_:

```bash
$ rm -r thesis
```

Given that there is no way to retrieve files deleted using the shell,
`rm -r` _should be used with great caution_
(you might consider adding the interactive option `rm -r -i`).

## Operations with multiple files and directories

Oftentimes one needs to copy or move several files at once.
This can be done by providing a list of individual filenames,
or specifying a naming pattern using wildcards. Wildcards are
special characters that can be used to represent unknown characters
or sets of characters when navigating the Unix file system.

:::::::::::::::::::::::::::::::::::::::  challenge

## Copy with Multiple Filenames

For this exercise, you can test the commands in the `shell-lesson-data/exercise-data` directory.

In the example below, what does `cp` do when given several filenames and a directory name?

```bash
$ mkdir backup
$ cp creatures/minotaur.dat creatures/unicorn.dat backup/
```

Що робить команда `cp` у наведеному нижче прикладі, коли їй задано три або більше імен файлів?

```bash
$ cd creatures
$ ls -F
```

```output
basilisk.dat  minotaur.dat  unicorn.dat
```

```bash
$ cp minotaur.dat unicorn.dat basilisk.dat
```

:::::::::::::::  solution

## Відповідь

If given more than one file name followed by a directory name
(i.e. the destination directory must be the last argument),
`cp` copies the files to the named directory.

If given three file names, `cp` throws an error such as the one below,
because it is expecting a directory name as the last argument.

```error
cp: target 'basilisk.dat' is not a directory
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Using wildcards for accessing multiple files at once

:::::::::::::::::::::::::::::::::::::::::  callout

## Wildcards

`*` is a **wildcard**, which represents zero or more other characters.
Розглянемо каталог `shell-lesson-data/exercise-data/proteins`: `*.pdb` відповідає `ethane.pdb`, `propane.pdb` і кожному файлу, який закінчується на '.pdb'. On the other hand, `p*.pdb` only represents
`pentane.pdb` and `propane.pdb`, because the 'p' at the front can only
represent filenames that begin with the letter 'p'.

Символ `?` також є символом підстановки, але він відповідає рівно одному будь-якому символу.
Отже, `?ethane.pdb` буде відповідати `methane.pdb`, тоді як `*ethane.pdb` відповідає як `ethane.pdb`, так і `methane.pdb`.

Wildcards can be used in combination with each other. Наприклад, `???ane.pdb` відповідає трьом символам, за якими слідує `ane.pdb`, що дає `cubane.pdb ethane.pdb octane.pdb`.

Коли термінал бачить символ підстановки, він розгортає його для створення списку відповідних імен файлів _до_ запуску команди, яку було введено.
Як виняток, якщо вираз підстановки не відповідає жодному файлу, Bash передасть вираз як аргумент до команди, якою вона є. Наприклад, введення `ls *.pdf` у каталозі `proteins` (який містить лише файли з іменами, що закінчуються на `.pdb`) призведе до повідомлення про те, що не існує файлу з назвою `*.pdf`.
Втім, зазвичай команди на кшталт `wc` і `ls` показують списки імен файлів, які відповідають цим виразам, але не самим символам підстановки. Саме термінал, а не інші програми, виконує розкриття символів підстановки.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## List filenames matching a pattern

При виконанні в каталозі `alkanes`, яка з команд `ls` видасть наступний результат?

`ethane.pdb   methane.pdb`

1. `ls *t*ane.pdb`
2. `ls *t?ne.*`
3. `ls *t??ne.pdb`
4. `ls ethane.*`

:::::::::::::::  solution

## Відповідь

Відповіддю є `3.`

`1.` показує всі файли, назви яких починаюьться з нуля або більше символів (`*`), за якими йде літера `t`, потім нуль або більше символів (`*`) і далі `ane.pdb`.
Це дасть `ethane.pdb methane.pdb octane.pdb pentane.pdb`.

`2.` показує всі файли, назви яких починаються з нуля або більше символів (`*`), за якими йде літера `t`, потім один будь-який символ (`?`), потім `ne.` і далі нуль або більше символів (`*`).
Це дасть нам `octane.pdb` і `pentane.pdb`, але не збігається ні з чим, що закінчується на `thane.pdb`.

`3.` fixes the problems of option 2 by matching two characters (`??`) between `t` and `ne`.
Це і є рішення.

`4.` показує лише файли, що починаються з `ethane.`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## More on Wildcards

Sam has a directory containing calibration data, datasets, and descriptions of
the datasets:

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   └── datasets
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    └── all_november_files
```

Before heading off to another field trip, she wants to back up her data and
send some datasets to her colleague Bob. Саманта використовує наступні команди щоб виконати цю роботу:

```bash
$ cp *dataset* backup/datasets
$ cp ____calibration____ backup/calibration
$ cp 2015-____-____ send_to_bob/all_november_files/
$ cp ____ send_to_bob/all_datasets_created_on_a_23rd/
```

Допоможіть Саманті, заповнивши пропуски.

The resulting directory structure should look like this

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   │   ├── 2015-10-23-calibration.txt
│   │   ├── 2015-10-26-calibration.txt
│   │   └── 2015-11-23-calibration.txt
│   └── datasets
│       ├── 2015-10-23-dataset1.txt
│       ├── 2015-10-23-dataset2.txt
│       ├── 2015-10-23-dataset_overview.txt
│       ├── 2015-10-26-dataset1.txt
│       ├── 2015-10-26-dataset2.txt
│       ├── 2015-10-26-dataset_overview.txt
│       ├── 2015-11-23-dataset1.txt
│       ├── 2015-11-23-dataset2.txt
│       └── 2015-11-23-dataset_overview.txt
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    │   ├── 2015-10-23-dataset1.txt
    │   ├── 2015-10-23-dataset2.txt
    │   ├── 2015-10-23-dataset_overview.txt
    │   ├── 2015-11-23-dataset1.txt
    │   ├── 2015-11-23-dataset2.txt
    │   └── 2015-11-23-dataset_overview.txt
    └── all_november_files
        ├── 2015-11-23-calibration.txt
        ├── 2015-11-23-dataset1.txt
        ├── 2015-11-23-dataset2.txt
        └── 2015-11-23-dataset_overview.txt
```

:::::::::::::::  solution

## Відповідь

```bash
$ cp *calibration.txt backup/calibration
$ cp 2015-11-* send_to_bob/all_november_files/
$ cp *-23-dataset* send_to_bob/all_datasets_created_on_a_23rd/
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Organizing Directories and Files

Jamie is working on a project, and she sees that her files aren't very well
organized:

```bash
$ ls -F
```

```output
analyzed/  fructose.dat    raw/   sucrose.dat
```

The `fructose.dat` and `sucrose.dat` files contain output from her data
analysis. What command(s) covered in this lesson does she need to run
so that the commands below will produce the output shown?

```bash
$ ls -F
```

```output
analyzed/   raw/
```

```bash
$ ls analyzed
```

```output
fructose.dat sucrose.dat
```

:::::::::::::::  solution

## Відповідь

```bash
mv *.dat analyzed
```

Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed` directory.
The shell will expand \*.dat to match all .dat files in the current directory.
The `mv` command then moves the list of .dat files to the 'analyzed' directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reproduce a folder structure

You're starting a new experiment and would like to duplicate the directory
structure from your previous experiment so you can add new data.

Assume that the previous experiment is in a folder called `2016-05-18`,
which contains a `data` folder that in turn contains folders named `raw` and
`processed` that contain data files.  The goal is to copy the folder structure
of the `2016-05-18` folder into a folder called `2016-05-20`
so that your final directory structure looks like this:

```output
2016-05-20/
└── data
   ├── processed
   └── raw
```

Which of the following set of commands would achieve this objective?
What would the other commands do?

```bash
$ mkdir 2016-05-20
$ mkdir 2016-05-20/data
$ mkdir 2016-05-20/data/processed
$ mkdir 2016-05-20/data/raw
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ cd data
$ mkdir raw processed
```

```bash
$ mkdir 2016-05-20/data/raw
$ mkdir 2016-05-20/data/processed
```

```bash
$ mkdir -p 2016-05-20/data/raw
$ mkdir -p 2016-05-20/data/processed
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ mkdir raw processed
```

:::::::::::::::  solution

## Відповідь

The first two sets of commands achieve this objective.
The first set uses relative paths to create the top-level directory before
the subdirectories.

The third set of commands will give an error because the default behavior of `mkdir`
won't create a subdirectory of a non-existent directory:
the intermediate level folders must be created first.

The fourth set of commands achieve this objective. Remember, the `-p` option,
followed by a path of one or more
directories, will cause `mkdir` to create any intermediate subdirectories as required.

The final set of commands generates the 'raw' and 'processed' directories at the same level
as the 'data' directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `cp [old] [new]` copies a file.
- `mkdir [path]` creates a new directory.
- `mv [old] [new]` moves (renames) a file or directory.
- `rm [path]` removes (deletes) a file.
- `*` matches zero or more characters in a filename, so `*.txt` matches all files ending in `.txt`.
- `?` matches any single character in a filename, so `?.txt` matches `a.txt` but not `any.txt`.
- Use of the Control key may be described in many ways, including `Ctrl-X`, `Control-X`, and `^X`.
- The shell does not have a trash bin: once something is deleted, it's really gone.
- Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file.
- Depending on the type of work you do, you may need a more powerful text editor than Nano.

::::::::::::::::::::::::::::::::::::::::::::::::::
