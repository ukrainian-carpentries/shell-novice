---
title: Скрипти командної оболонки
teaching: 30
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Написати скрипт командної оболонки, який виконує одну або декілька команд для заздалегідь визначеного набору файлів.
- Запустити скрипт командної оболонки з термінала.
- Написати скрипт командної оболонки, який обробляє файли, вказані користувачем у командному рядку.
- Створити конвеєри, що використовують скрипти оболонки, створені вами та іншими користувачами.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу зберігати та повторно використовувати команди?

::::::::::::::::::::::::::::::::::::::::::::::::::

Нарешті ми готові дізнатися, чому оболонка є таким потужним середовищем програмування.
Ми збираємося зібрати та зберегти у файлах часто використовувані команди, щоб пізніше можна було виконати всі ці дії одночасно, набравши лише одну команду.
For historical reasons,
a bunch of commands saved in a file is usually called a **shell script**,
but make no mistake --- these are actually small programs.

Написання командних скриптів не тільки прискорить вашу роботу, а й дозволить уникнути постійного повторного введення тих самих команд. Крім того, це підвищить якість вашої роботи (зменшить ризик друкарських помилок) і полегшить її відтворення. Якщо ви повернетеся до своєї роботи пізніше (або якщо хтось знайде вашу роботу і захоче її використати), відтворити ті ж результати можна буде просто запустивши скрипт, без потреби пригадувати та повторно вводити довгий перелік команд.

Спершу повернемося до каталогу `alkanes/` і створимо новий файл `middle.sh`, який стане нашим скриптом терміналу:

```bash
$ cd alkanes
$ nano middle.sh
```

Команда `nano middle.sh` відкриває файл `middle.sh` у текстовому редакторі 'nano' (який запускається у терміналі).
Якщо файл не існує, його буде створено.
Ми можемо скористатися текстовим редактором для безпосереднього редагування файлу, додавши до нього наступний рядок:

```source
head -n 15 octane.pdb | tail -n 5
```

Це варіант каналу, який ми побудували раніше: він вибирає рядки 11-15 файлу `octane.pdb`. Пам'ятайте, ми поки _не запускаємо_ його як команду: ми лише записуємо команди у файл.

Потім ми зберігаємо файл (`Ctrl-O` у nano) і виходимо з текстового редактора (`Ctrl-X` у nano).
Переконайтеся, що в каталозі `alkanes` тепер міститься файл з назвою `middle.sh`.

Після того, як ми зберегли файл, ми можемо дати оболонці команду виконати його вміст.
Оскільки термінал називається `bash`, ми виконаємо наступну команду:

```bash
$ bash middle.sh
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

Дійсно, результат роботи скрипту збігається з тим, що ми отримали б, запустивши конвеєр напряму у терміналі.

:::::::::::::::::::::::::::::::::::::::::  callout

## Текст або будь-що інше?

We usually call programs like Microsoft Word or LibreOffice Writer "text
editors", but we need to be a bit more careful when it comes to
programming. By default, Microsoft Word uses `.docx` files to store not
only text, but also formatting information about fonts, headings, and so
on. This extra information isn't stored as characters and doesn't mean
anything to tools like `head`, which expects input files to contain
nothing but the letters, digits, and punctuation on a standard computer
keyboard. When editing programs, therefore, you must either use a plain
text editor or be careful to save files as plain text.

::::::::::::::::::::::::::::::::::::::::::::::::::

What if we want to select lines from an arbitrary file?
We could edit `middle.sh` each time to change the filename,
but that would probably take longer than typing the command out again
in the shell and executing it with a new file name.
Instead, let's edit `middle.sh` and make it more versatile:

```bash
$ nano middle.sh
```

Тепер у "nano" замініть текст `octane.pdb` на спеціальну змінну з назвою `$1`:

```source
head -n 15 "$1" | tail -n 5
```

Inside a shell script,
`$1` means 'the first filename (or other argument) on the command line'.
Тепер ми можемо запустити наш скрипт наступним чином для того ж самого файлу:

```bash
$ bash middle.sh octane.pdb
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

or on a different file like this:

```bash
$ bash middle.sh pentane.pdb
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Double-Quotes Around Arguments

For the same reason that we put the loop variable inside double-quotes,
in case the filename happens to contain any spaces,
we surround `$1` with double-quotes.

::::::::::::::::::::::::::::::::::::::::::::::::::

Currently, we need to edit `middle.sh` each time we want to adjust the range of
lines that is returned.
Let's fix that by configuring our script to instead use three command-line arguments.
After the first command-line argument (`$1`), each additional argument that we
provide will be accessible via the special variables `$1`, `$2`, `$3`,
which refer to the first, second, third command-line arguments, respectively.

Knowing this, we can use additional arguments to define the range of lines to
be passed to `head` and `tail` respectively:

```bash
$ nano middle.sh
```

```source
head -n "$2" "$1" | tail -n "$3"
```

We can now run:

```bash
$ bash middle.sh pentane.pdb 15 5
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

By changing the arguments to our command, we can change our script's
behaviour:

```bash
$ bash middle.sh pentane.pdb 20 5
```

```output
ATOM     14  H           1      -1.259   1.420   0.112  1.00  0.00
ATOM     15  H           1      -2.608  -0.407   1.130  1.00  0.00
ATOM     16  H           1      -2.540  -1.303  -0.404  1.00  0.00
ATOM     17  H           1      -3.393   0.254  -0.321  1.00  0.00
TER      18              1
```

This works,
but it may take the next person who reads `middle.sh` a moment to figure out what it does.
We can improve our script by adding some **comments** at the top:

```bash
$ nano middle.sh
```

```source
# Виділення рядків з середини файлу.
# Використання: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
```

A comment starts with a `#` character and runs to the end of the line.
The computer ignores comments,
but they're invaluable for helping people (including your future self) understand and use scripts.
Єдине застереження полягає у тому, що кожного разу, коли ви змінюєте скрипт, ви повинні перевіряти, що коментар все ще правильний. Пояснення, яке спрямовує читача в неправильному напрямку, гірше, ніж його відсутність.

What if we want to process many files in a single pipeline?
For example, if we want to sort our `.pdb` files by length, we would type:

```bash
$ wc -l *.pdb | sort -n
```

because `wc -l` lists the number of lines in the files
(recall that `wc` stands for 'word count', adding the `-l` option means 'count lines' instead)
and `sort -n` sorts things numerically.
We could put this in a file,
but then it would only ever sort a list of `.pdb` files in the current directory.
If we want to be able to get a sorted list of other kinds of files,
we need a way to get all those names into the script.
We can't use `$1`, `$2`, and so on
because we don't know how many files there are.
Instead, we use the special variable `$@`,
which means,
'All of the command-line arguments to the shell script'.
We also should put `$@` inside double-quotes
to handle the case of arguments containing spaces
(`"$@"` is special syntax and is equivalent to `"$1"` `"$2"` ...).

Here's an example:

```bash
$ nano sorted.sh
```

```source
# Сортування файлів за їх розміром.
# Використання: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

```bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

```output
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
163 ../creatures/basilisk.dat
163 ../creatures/minotaur.dat
163 ../creatures/unicorn.dat
596 total
```

:::::::::::::::::::::::::::::::::::::::  challenge

## List Unique Species

Лія має кілька сотень файлів даних, кожен з яких відформатований наступним чином:

```source
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
2013-11-06,deer,2
2013-11-06,fox,1
2013-11-07,rabbit,18
2013-11-07,bear,1
```

An example of this type of file is given in
`shell-lesson-data/exercise-data/animal-counts/animals.csv`.

We can use the command `cut -d , -f 2 animals.csv | sort | uniq` to produce
the unique species in `animals.csv`.
In order to avoid having to type out this series of commands every time,
a scientist may choose to write a shell script instead.

Write a shell script called `species.sh` that takes any number of
filenames as command-line arguments and uses a variation of the above command
to print a list of the unique species appearing in each of those files separately.

:::::::::::::::  solution

## Відповідь

```bash
# Script to find unique species in csv files where species is the second data field
# This script accepts any number of file names as command line arguments

# Loop over all files
for file in $@
do
    echo "Unique species in $file:"
    # Extract species names
    cut -d , -f 2 $file | sort | uniq
done
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Suppose we have just run a series of commands that did something useful --- for example,
creating a graph we'd like to use in a paper.
We'd like to be able to re-create the graph later if we need to,
so we want to save the commands in a file.
Instead of typing them in again
(and potentially getting them wrong)
we can do this:

```bash
$ history | tail -n 5 > redo-figure-3.sh
```

The file `redo-figure-3.sh` now contains:

```source
297 bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
298 bash goodiff.sh stats-NENE01729B.txt /data/validated/01729.txt > 01729-differences.txt
299 cut -d ',' -f 2-3 01729-differences.txt > 01729-time-series.txt
300 ygraph --format scatter --color bw --borders none 01729-time-series.txt figure-3.png
301 history | tail -n 5 > redo-figure-3.sh
```

After a moment's work in an editor to remove the serial numbers on the commands,
and to remove the final line where we called the `history` command,
we have a completely accurate record of how we created that figure.

:::::::::::::::::::::::::::::::::::::::  challenge

## Why Record Commands in the History Before Running Them?

Якщо виконати команду:

```bash
$ history | tail -n 5 > recent.sh
```

останньою командою у файлі є сама команда `history`, тобто, термінал додав `history` до журналу команд перед тим, як фактично її виконав. In fact, the shell _always_ adds commands to the log
before running them. Why do you think it does this?

:::::::::::::::  solution

## Відповідь

If a command causes something to crash or hang, it might be useful
to know what that command was, in order to investigate the problem.
Were the command only be recorded after running it, we would not
have a record of the last command run in the event of a crash.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

In practice, most people develop shell scripts by running commands
at the shell prompt a few times
to make sure they're doing the right thing,
then saving them in a file for re-use.
This style of work allows people to recycle
what they discover about their data and their workflow with one call to `history`
and a bit of editing to clean up the output
and save it as a shell script.

## Nelle's Pipeline: Creating a Script

Nelle's supervisor insisted that all her analytics must be reproducible.
The easiest way to capture all the steps is in a script.

First we return to Nelle's project directory:

```bash
$ cd ../../north-pacific-gyre/
```

She creates a file using `nano` ...

```bash
$ nano do-stats.sh
```

...which contains the following:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

She saves this in a file called `do-stats.sh`
so that she can now re-do the first stage of her analysis by typing:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt
```

She can also do this:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt | wc -l
```

so that the output is just the number of files processed
rather than the names of the files that were processed.

One thing to note about Nelle's script is that
it lets the person running it decide what files to process.
She could have written it as:

```bash
# Calculate stats for Site A and Site B data files.
for datafile in NENE*A.txt NENE*B.txt
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

The advantage is that this always selects the right files:
she doesn't have to remember to exclude the 'Z' files.
The disadvantage is that it _always_ selects just those files --- she can't run it on all files
(including the 'Z' files),
or on the 'G' or 'H' files her colleagues in Antarctica are producing,
without editing the script.
If she wanted to be more adventurous,
she could modify her script to check for command-line arguments,
and use `NENE*A.txt NENE*B.txt` if none were provided.
Of course, this introduces another tradeoff between flexibility and complexity.

:::::::::::::::::::::::::::::::::::::::  challenge

## Variables in Shell Scripts

Уявіть, що у каталозі `alkanes` у вас є скрипт з назвою `script.sh`, який містить наступні команди:

```bash
head -n $2 $1
tail -n $3 $1
```

Перебуваючи у каталозі `alkanes`, ви вводите наступну команду:

```bash
$ bash script.sh '*.pdb' 1 1
```

Які з наведених нижче результатів ви очікуєте побачити?

1. Усі рядки між першим та останнім рядками кожного файлу, що закінчується на `.pdb` у каталозі `alkanes`
2. Перший та останній рядок кожного файлу, що закінчується на `.pdb` у каталозі `alkanes`
3. Перший та останній рядок кожного файлу в каталозі `alkanes`
4. Помилку через лапки навколо `*.pdb`

:::::::::::::::  solution

## Відповідь

The correct answer is 2.

The special variables `$1`, `$2` and `$3` represent the command line arguments given to the
script, such that the commands run are:

```bash
$ head -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
$ tail -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
```

The shell does not expand `'*.pdb'` because it is enclosed by quote marks.
Таким чином, першим аргументом скрипту є `'*.pdb'`, який буде розгорнуто у скрипті за допомогою `head` і `tail`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Find the Longest File With a Given Extension

Напишіть сценарій терміналу з назвою `longest.sh`, який отримує в якості аргументів ім'я каталогу і розширення імені файлу як аргументи, і виводить назву файлу з найбільшою кількістю рядків у цьому каталозі з цим розширенням. For example:

```bash
$ bash longest.sh shell-lesson-data/exercise-data/alkanes pdb
```

виведе назву файлу `.pdb` у каталозі `shell-lesson-data/exercise-data/proteins`, який має найбільшу кількість рядків.

Feel free to test your script on another directory e.g.

```bash
$ bash longest.sh shell-lesson-data/exercise-data/writing txt
```

:::::::::::::::  solution

## Відповідь

```bash
# Shell script which takes two arguments:
#    1. a directory name
#    2. a file extension
# and prints the name of the file in that directory
# with the most lines which matches the file extension.

wc -l $1/*.$2 | sort -n | tail -n 2 | head -n 1
```

The first part of the pipeline, `wc -l $1/*.$2 | sort -n`, counts
the lines in each file and sorts them numerically (largest last). When
there's more than one file, `wc` also outputs a final summary line,
giving the total number of lines across _all_ files.  Ми використовуємо `tail -n 2 | head -n 1`, щоб відкинути цей останній рядок.

With `wc -l $1/*.$2 | sort -n | tail -n 1` we'll see the final summary
line: we can build our pipeline up in pieces to be sure we understand
the output.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Script Reading Comprehension

For this question, consider the `shell-lesson-data/exercise-data/alkanes` directory once again.
This contains a number of `.pdb` files in addition to any other files you
may have created.
Explain what each of the following three scripts would do when run as
`bash script1.sh *.pdb`, `bash script2.sh *.pdb`, and `bash script3.sh *.pdb` respectively.

```bash
# Скрипт 1
echo *.*
```

```bash
# Скрипт 2
for filename in $1 $2 $3
do
    cat $filename
done
```

```bash
# Скрипт 3
echo $@.pdb
```

:::::::::::::::  solution

## Відповідь

In each case, the shell expands the wildcard in `*.pdb` before passing the resulting
list of file names as arguments to the script.

Script 1 would print out a list of all files containing a dot in their name.
The arguments passed to the script are not actually used anywhere in the script.

Script 2 would print the contents of the first 3 files with a `.pdb` file extension.
`$1`, `$2`, and `$3` refer to the first, second, and third argument respectively.

Script 3 would print all the arguments to the script (i.e. all the `.pdb` files),
followed by `.pdb`.
`$@` refers to _all_ the arguments given to a shell script.

```output
cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Debugging Scripts

Suppose you have saved the following script in a file called `do-errors.sh`
in Nelle's `north-pacific-gyre` directory:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datfile
    bash goostats.sh $datafile stats-$datafile
done
```

Якщо ви запускаєте його з каталогу `north-pacific-gyre`:

```bash
$ bash do-errors.sh NENE*A.txt NENE*B.txt
```

програма нічого не виводить.
Щоб з'ясувати причину, перезапустіть скрипт з опцією `-x`:

```bash
$ bash -x do-errors.sh NENE*A.txt NENE*B.txt
```

Що показує вивід?
Which line is responsible for the error?

:::::::::::::::  solution

## Відповідь

The `-x` option causes `bash` to run in debug mode.
This prints out each command as it is run, which will help you to locate errors.
In this example, we can see that `echo` isn't printing anything. We have made a typo
in the loop variable name, and the variable `datfile` doesn't exist, hence returning
an empty string.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Save commands in files (usually called shell scripts) for re-use.
- `bash [ім'я файлу]` виконує команди, збережені у відповідному файлі.
- `$@` refers to all of a shell script's command-line arguments.
- `$1`, `$2`, etc., refer to the first command-line argument, the second command-line argument, etc.
- Place variables in quotes if the values might have spaces in them.
- Letting users decide what files to process is more flexible and more consistent with built-in Unix commands.

::::::::::::::::::::::::::::::::::::::::::::::::::


