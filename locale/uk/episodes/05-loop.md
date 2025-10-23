---
title: Цикли
teaching: 40
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Написати цикл, який застосовує одну або декілька команд окремо до кожного файлу в наборі файлів.
- Простежити, яких значень набуває змінна циклу під час виконання циклу.
- Пояснити різницю між ім'ям змінної та її значенням.
- Пояснити, чому в іменах файлів не можна використовувати пробіли та деякі розділові знаки.
- Продемонструвати, як побачити, які команди були виконані останнім часом.
- Перезапустити нещодавно виконані команди без повторного введення.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як виконати одні й ті ж дії над різними файлами?

::::::::::::::::::::::::::::::::::::::::::::::::::

**Цикли** - це конструкції програмування, які дозволяють повторити команду або набір команд для кожного елемента у списку.
Таким чином, автоматизація виконання повторюваних дій суттєво підвищує ефективність.
Подібно до шаблонів і автодоповнення, цикли допомагають зменшити кількість вручну набраного тексту (а отже, зменшують кількість помилок).

Припустимо, у нас є кілька сотень файлів даних, які містять інформацію про геноми та мають імена на кшталт `basilisk.dat`, `minotaur.dat` та `unicorn.dat`.
For this example, we'll use the `exercise-data/creatures` directory which only has three
example files,
but the principles can be applied to many many more files at once.

Ці файли мають однакову структуру: перші три рядки містять назву виду, його класифікацію та дату оновлення, а у наступних рядках наведені послідовності ДНК.
Погляньмо, що містять ці файли:

```bash
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```

Для кожного виду ми хотіли б надрукувати його класифікацію, яка наведена у другому рядку відповідного файлу.
Для кожного файлу нам потрібно виконати команду `head -n 2` і передати її результат через канал до команди `tail -n 1`.
Скористаймося циклом, щоб уникнути цю проблему, але спочатку розгляньмо загальну форму циклу, використовуючи наведений нижче псевдокод:

```bash
# Слово "for" вказує на початок команди для виконання циклу "For"
for thing in list_of_things 
# Слово "do" вказує на початок списку завдань для виконання
do 
    # Відступи всередині циклу не є обов'язковими, але сприяють розбірливості
    operation_using/command $thing 
# Слово "done" вказує на кінець циклу
done  
```

У такому разі, ми можемо застосувати це до нашого прикладу наступним чином:

```bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     echo $filename
>     head -n 2 $filename | tail -n 1
> done
```

```output
basilisk.dat
CLASSIFICATION: basiliscus vulgaris
minotaur.dat
CLASSIFICATION: bos hominus
unicorn.dat
CLASSIFICATION: equus monoceros
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Слідкуйте за підказками командного рядка

Під час введення нашого циклу запрошення термінала змінювалося з `$` на `>` та назад. The second prompt, `>`, is different to remind
us that we haven't finished typing a complete command yet. Крапка з комою `;` використовується для розділення двох команд, написаних в одному рядку.

::::::::::::::::::::::::::::::::::::::::::::::::::

Коли термінал бачить ключове слово `for`, він розуміє, що потрібно повторити команду (або групу команд) для кожного елемента зі списку.
Кожного разу, коли цикл виконується (цей процес називається **ітерацією**), елемент списку послідовно присвоюється **змінній** та виконуються команди всередині циклу, після чого цикл переходить до наступного елементу списку.
Усередині циклу ми звертаємося до значення змінної, додаючи `$` перед її іменем.
Символ `$` повідомляє інтерпретатор командного рядка, що далі йде назва змінної, тож слід підставити її значення, а не сприймати запис як текст чи назву команди.

У цьому прикладі список складається з трьох файлів: `basilisk.dat`, `minotaur.dat` та `unicorn.dat`.
Each time the loop iterates, we first use `echo` to print the value that the variable
`$filename` currently holds. Це не обов'язково робити, але допомагає нам слідкувати за виконанням програми.
Далі ми виконаємо команду `head` для файлу, на який зараз посилається `$filename`.
При першому проходженні циклу `$filename` має значення `basilisk.dat`.
Інтерпретатор виконує команду `head` над `basilisk.dat` і передає перші два рядки команді `tail`, яка виводить другий рядок цього файлу.
Для другої ітерації `$filename` стає `minotaur.dat`. Цього разу термінал виконує команду `head` над `minotaur.dat` і передає перші два рядки команді `tail`, яка виводить другий рядок `minotaur.dat`.
На третій ітерації `$filename` стає `unicorn.dat`, тому термінал виконує команду `head` для цього файлу, і `tail` обробляє результат.
Оскільки список містив лише три елементи, оболонка закінчує цикл `for`.

:::::::::::::::::::::::::::::::::::::::::  callout

## Однакові символи, різні значення

Тут ми бачимо, що символ `>` використовується як запрошення командного рядка, але `>` також застосовується для перенаправлення виводу.
Аналогічно, символ `$` діє як запрошення оболонки, але, як ми бачили раніше, його функція теж може полягати в отриманні значення змінної.

Якщо _термінал_ друкує `>` або `$`, то він очікує від вас введення команди й цей символ є підказкою.

Якщо _ви_ вводите ` >` або `$` самостійно, це означає, що ви даєте команду оболонці перенаправити вивід або отримати значення змінної.

::::::::::::::::::::::::::::::::::::::::::::::::::

При використанні змінних також можна брати їхні імена у фігурні дужки, щоб чітко відокремити імена змінних: `$filename` еквівалентно `${filename}`, але відрізняється від `${file}name`. Ви можете побачити таку форму запису в інших програмах.

Ми назвали змінну у цьому циклі `filename` (ім'я файлу), щоб її призначення було зрозуміліше для читачів.
Самій оболонці байдуже, як називається змінна; якби ми написали цей цикл так:

```bash
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
```

або:

```bash
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
```

це спрацювало б точно так само.
_Але не робіть цього._ Програми корисні лише тоді, коли люди можуть їх розуміти, тому беззмістовні (наприклад, `x`) або оманливі (наприклад, `temperature`) назви підвищують ймовірність того, що програма поводитиметься не так, як очікують читачі.

У наведених вище прикладах змінним (`thing`, `filename`, `x` та `temperature`) можна було б призначити будь-які інші імена, аби вони були зрозумілими як автору коду, так і його читачу.

Також майте на увазі, що цикли можна використовувати не лише для імен файлів, а й для списків чисел або підмножини даних.

:::::::::::::::::::::::::::::::::::::::  challenge

## Напишіть свій власний цикл

Як би ви написали цикл, який друкує всі 10 чисел від 0 до 9?

:::::::::::::::  solution

## Відповідь

```bash
$ for loop_variable in 0 1 2 3 4 5 6 7 8 9
> do
>     echo $loop_variable
> done
```

```output
0
1
2
3
4
5
6
7
8
9
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Змінні в циклах

Ця вправа стосується каталогу `shell-lesson-data/exercise-data/alkanes`.
Команда `ls *.pdb` дає такий результат:

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Що виведе наступний код?

```bash
$ for datafile in *.pdb
> do
>     ls *.pdb
> done
```

А цей?

```bash
$ for datafile in *.pdb
> do
>     ls $datafile
> done
```

Чому ці два цикли дають різні результати?

:::::::::::::::  solution

## Відповідь

Перший блок коду дає однаковий результат на кожній ітерації циклу.
Bash розгортає шаблон `*.pdb` в тілі циклу (а також перед початком циклу), щоб знайти всі файли, що закінчуються на `.pdb`, а потім виводить їх список за допомогою `ls`.
Розширений цикл матиме такий вигляд:

```bash
$ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> do
>     ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> done
```

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

The second code block lists a different file on each loop iteration.
The value of the `datafile` variable is evaluated using `$datafile`,
and then listed using `ls`.

```output
cubane.pdb
ethane.pdb
methane.pdb
octane.pdb
pentane.pdb
propane.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Обмеження наборів файлів

Що буде виведено у результаті виконання наступного циклу в каталозі `shell-lesson-data/exercise-data/alkanes`?

```bash
$ for filename in c*
> do
>     ls $filename
> done
```

1. Жодної назви файлу не буде виведено.
2. Будуть перелічені всі файли.
3. Будуть перелічені лише `cubane.pdb`, `octane.pdb` та `pentane.pdb`.
4. Буде виведено лише `cubane.pdb`.

:::::::::::::::  solution

## Відповідь

4 - правильна відповідь. Символ `*` відповідає нулю або більшій кількості символів, тому будь-яке ім'я файлу, що починається з літери 'c', за якою йдуть нуль або більша кількість символів, буде відповідати шаблону `c*`.

:::::::::::::::::::::::::

How would the output differ from using this command instead?

```bash
$ for filename in *c*
> do
>     ls $filename
> done
```

1. Будуть перелічені ті ж самі файли.
2. Цього разу будуть перелічені всі файли.
3. Цього разу не буде виведено жодного файлу.
4. Будуть перелічені файли `cubane.pdb` та `octane.pdb`.
5. Only the file `octane.pdb` will be listed.

:::::::::::::::  solution

## Відповідь

4 - правильна відповідь. Символ `* ` відповідає нулю або більшій кількості символів, тому всі імена файлів з нулем або більшою кількістю символів перед літерою 'c' або після літери 'c' будуть відповідати шаблону `*c*`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Saving to a File in a Loop - Part One

В каталозі `shell-lesson-data/exercise-data/alkanes `, яким буде результат роботи цього циклу?

```bash
for alkanes in *.pdb
do
    echo $alkanes
    cat $alkanes > alkanes.pdb
done
```

1. Буде виведено `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` та `propane.pdb`, а текст з файлу `propane.pdb` буде збережено у файлі з назвою `alkanes.pdb`.
2. Буде виведено `cubane.pdb`, `ethane.pdb` та `methane.pdb`, а текст з усіх трьох файлів буде об'єднано і збережено у файлі з назвою `alkanes.pdb`.
3. Буде виведено `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` та `pentane.pdb`, а текст з файлу `propane.pdb` буде збережено у файлі з назвою `alkanes.pdb`.
4. None of the above.

:::::::::::::::  solution

## Відповідь

1. Текст з кожного файлу по черзі буде записуватися у файл `alkanes.pdb`.
   Однак, файл буде перезаписуватися на кожній ітерації циклу, тому остаточний вміст `alkanes.pdb' буде збігатися з текстом з файлу `propane.pdb\`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Saving to a File in a Loop - Part Two

У тому ж каталозі `shell-lesson-data/exercise-data/alkanes `, що буде виведено у наступному циклі?

```bash
for datafile in *.pdb
do
    cat $datafile >> all.pdb
done
```

1. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` та `pentane.pdb` буде об'єднано і збережено у файлі з назвою `all.pdb`.
2. Текст з файлу `ethane.pdb` буде збережено до файлу з назвою `all.pdb`.
3. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` та `propane.pdb` буде об'єднано та збережено у файл з назвою `all.pdb`.
4. Весь текст з файлів `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` та `propane.pdb` буде виведено на екран і збережено у файлі з назвою `all.pdb`.

:::::::::::::::  solution

## Відповідь

3 - правильна відповідь. `>>` appends to a file, rather than overwriting it with the redirected
output from a command.
Оскільки вивід команди `cat` було перенаправлено, на екран нічого не буде виведено.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Для наступного прикладу перейдемо у каталог `shell-lesson-data/exercise-data/creatures`.
Тут цикл трохи складніший:

```bash
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```

The shell starts by expanding `*.dat` to create the list of files it will process.
The **loop body**
then executes two commands for each of those files.
Перша команда, `echo`, виводить свої аргументи на стандартний вивід (тобто, на standard output).
Наприклад:

```bash
$ echo hello there
```

друкує:

```output
hello there
```

У цьому випадку, оскільки термінал підставить до `$filename` імʼя файлу, `echo $filename` виведе ім'я файлу.
Зауважте, що ми не можемо написати це як:

```bash
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
```

because then the first time through the loop,
when `$filename` expanded to `basilisk.dat`, the shell would try to run `basilisk.dat` as
a program.
Finally,
the `head` and `tail` combination selects lines 81-100
from whatever file is being processed
(assuming the file has at least 100 lines).

:::::::::::::::::::::::::::::::::::::::::  callout

## Пробіли в іменах

Пробіли використовуються для відокремлення елементів списку, які ми будемо перебирати у циклі. Якщо один з цих елементів містить пробіл, нам потрібно взяти його в лапки та зробити те ж саме зі змінною циклу.
Припустимо, що наші файли даних мають імена:

```source
red dragon.dat
purple unicorn.dat
```

Щоб переглянути ці файли у циклі, нам потрібно додати подвійні лапки, ось так:

```bash
$ for filename in "red dragon.dat" "purple unicorn.dat"
> do
>     head -n 100 "$filename" | tail -n 20
> done
```

Простіше уникати використання пробілів (або інших спеціальних символів) у назвах файлів.

The files above don't exist, so if we run the above code, the `head` command will be unable
to find them; however, the error message returned will show the name of the files it is
expecting:

```error
head: cannot open ‘red dragon.dat' for reading: No such file or directory
head: cannot open ‘purple unicorn.dat' for reading: No such file or directory
```

Спробуйте видалити лапки навколо `$filename` у наведеному вище циклі, щоб побачити ефект лапок на назвах з пробілами. Зверніть увагу, що ми отримуємо результат команди циклу для `unicorn.dat` коли ми запускаємо цей код у каталозі `creatures`:

```output
head: cannot open ‘red' for reading: No such file or directory
head: cannot open ‘dragon.dat' for reading: No such file or directory
head: cannot open ‘purple' for reading: No such file or directory
CGGTACCGAA
AAGGGTCGCG
CAAGTGTTCC
...
```

::::::::::::::::::::::::::::::::::::::::::::::::::

We would like to modify each of the files in `shell-lesson-data/exercise-data/creatures`,
but also save a version of the original files. Наприклад, ми хочемо скопіювати оригінальні файли до нових файлів з назвами `original-basilisk.dat` та `original-unicorn.dat`. We can't use:

```bash
$ cp *.dat original-*.dat
```

because that would expand to:

```bash
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

This wouldn't back up our files, instead we get an error:

```error
cp: target `original-*.dat' is not a directory
```

This problem arises when `cp` receives more than two inputs. When this happens, it expects the
last input to be a directory where it can copy all the files it was passed. Since there is
no directory named `original-*.dat` in the `creatures` directory, we get an error.

Замість цього ми можемо використати цикл:

```bash
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

This loop runs the `cp` command once for each filename.
The first time,
when `$filename` expands to `basilisk.dat`,
the shell executes:

```bash
cp basilisk.dat original-basilisk.dat
```

The second time, the command is:

```bash
cp minotaur.dat original-minotaur.dat
```

The third and last time, the command is:

```bash
cp unicorn.dat original-unicorn.dat
```

Since the `cp` command does not normally produce any output, it's hard to check
that the loop is working correctly. However, we learned earlier how to print strings
using `echo`, and we can modify the loop to use `echo` to print our commands without
actually executing them. As such we can check what commands _would be_ run in the
unmodified loop.

The following diagram
shows what happens when the modified loop is executed and demonstrates how the
judicious use of `echo` is a good debugging technique.

![](fig/shell_script_for_loop_flow_chart.svg){alt='The for loop "for filename in .dat; do echo cp $filename original-$filename;done" will successively assign the names of all ".dat" files in your currentdirectory to the variable "$filename" and then execute the command. With thefiles "basilisk.dat", "minotaur.dat" and "unicorn.dat" in the current directorythe loop will successively call the echo command three times and print threelines: "cp basislisk.dat original-basilisk.dat", then "cp minotaur.datoriginal-minotaur.dat" and finally "cp unicorn.datoriginal-unicorn.dat"'}

## Nelle's Pipeline: Processing Files

Nelle is now ready to process her data files using `goostats.sh` ---
a shell script written by her supervisor. This calculates some statistics from a
protein sample file and takes two arguments:

1. an input file (containing the raw data)
2. an output file (to store the calculated statistics)

Since she's still learning how to use the shell,
she decides to build up the required commands in stages.
Her first step is to make sure that she can select the right input files --- remember,
these are ones whose names end in 'A' or 'B', rather than 'Z'.
Переходячи до каталогу `north-pacific-gyre`, Неллі вводить:

```bash
$ cd
$ cd Desktop/shell-lesson-data/north-pacific-gyre
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile
> done
```

```output
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
NENE02043A.txt
NENE02043B.txt
```

Her next step is to decide
what to call the files that the `goostats.sh` analysis program will create.
Prefixing each input file's name with 'stats' seems simple,
so she modifies her loop to do that:

```bash
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile stats-$datafile
> done
```

```output
NENE01729A.txt stats-NENE01729A.txt
NENE01729B.txt stats-NENE01729B.txt
NENE01736A.txt stats-NENE01736A.txt
...
NENE02043A.txt stats-NENE02043A.txt
NENE02043B.txt stats-NENE02043B.txt
```

She hasn't actually run `goostats.sh` yet,
but now she's sure she can select the right files and generate the right output filenames.

Typing in commands over and over again is becoming tedious,
though,
and Nelle is worried about making mistakes,
so instead of re-entering her loop,
she presses <kbd>↑</kbd>.
In response,
the shell redisplays the whole loop on one line
(using semi-colons to separate the pieces):

```bash
$ for datafile in NENE A.txt NENE B.txt; do echo $datafile stats-$datafile; done
```

Using the <kbd>←</kbd>,
Nelle navigates to the `echo` command and changes it to `bash goostats.sh`:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
```

When she presses <kbd>Enter</kbd>,
the shell runs the modified command.
However, nothing appears to happen --- there is no output.
After a moment, Nelle realizes that since her script doesn't print anything to the screen
any longer, she has no idea whether it is running, much less how quickly.
She kills the running command by typing <kbd>Ctrl</kbd>\+<kbd>C</kbd>,
uses <kbd>↑</kbd> to repeat the command,
and edits it to read:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datafile stats-$datafile; done
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Beginning and End

We can move to the beginning of a line in the shell by typing <kbd>Ctrl</kbd>\+<kbd>A</kbd>
and to the end using <kbd>Ctrl</kbd>\+<kbd>E</kbd>.

::::::::::::::::::::::::::::::::::::::::::::::::::

When she runs her program now,
it produces one line of output every five seconds or so:

```output
NENE01729A.txt
NENE01736A.txt
NENE01751A.txt
...
```

1518 times 5 seconds,
divided by 60,
tells her that her script will take about two hours to run.
As a final check,
she opens another terminal window,
goes into `north-pacific-gyre`,
and uses `cat stats-NENE01729B.txt`
to examine one of the output files.
It looks good,
so she decides to get some coffee and catch up on her reading.

:::::::::::::::::::::::::::::::::::::::::  callout

## Those Who Know History Can Choose to Repeat It

Another way to repeat previous work is to use the `history` command to
get a list of the last few hundred commands that have been executed, and
then to use `!123` (where '123' is replaced by the command number) to
repeat one of those commands. Наприклад, якщо Неллі набере наступне:

```bash
$ history | tail -n 5
```

```output
456  for datafile in NENE*A.txt NENE*B.txt; do   echo $datafile stats-$datafile; done
457  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
458  for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
459  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile; bash goostats.sh $datafile
stats-$datafile; done
460  history | tail -n 5
```

then she can re-run `goostats.sh` on the files simply by typing
`!459`.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Other History Commands

There are a number of other shortcut commands for getting at the history.

- <kbd>Ctrl</kbd>\+<kbd>R</kbd> enters a history search mode 'reverse-i-search' and finds the
  most recent command in your history that matches the text you enter next.
  Press <kbd>Ctrl</kbd>\+<kbd>R</kbd> one or more additional times to search for earlier matches.
  You can then use the left and right arrow keys to choose that line and edit
  it then hit <kbd>Return</kbd> to run the command.
- `!!` повертає безпосередньо попередню команду (ви можете знайти це більш зручним, ніж використання <kbd>↑</kbd>)
- `!$` повертає останнє слово останньої команди.
  That's useful more often than you might expect: after
  `bash goostats.sh NENE01729B.txt stats-NENE01729B.txt`, you can type
  `less !$` to look at the file `stats-NENE01729B.txt`, which is
  quicker than doing <kbd>↑</kbd> and editing the command-line.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Doing a Dry Run

A loop is a way to do many things at once --- or to make many mistakes at
once if it does the wrong thing. One way to check what a loop _would_ do
is to `echo` the commands it would run instead of actually running them.

Suppose we want to preview the commands the following loop will execute
without actually running those commands:

```bash
$ for datafile in *.pdb
> do
>     cat $datafile >> all.pdb
> done
```

What is the difference between the two loops below, and which one would we
want to run?

```bash
# Варіант 1
$ for datafile in *.pdb
> do
>     echo cat $datafile >> all.pdb
> done
```

```bash
# Варіант 2
$ for datafile in *.pdb
> do
>     echo "cat $datafile >> all.pdb"
> done
```

:::::::::::::::  solution

## Відповідь

The second version is the one we want to run.
This prints to screen everything enclosed in the quote marks, expanding the
loop variable name because we have prefixed it with a dollar sign.
It also _does not_ modify nor create the file `all.pdb`, as the `>>`
is treated literally as part of a string rather than as a
redirection instruction.

The first version appends the output from the command `echo cat $datafile`
to the file, `all.pdb`. This file will just contain the list;
`cat cubane.pdb`, `cat ethane.pdb`, `cat methane.pdb` etc.

Try both versions for yourself to see the output! Be sure to open the
`all.pdb` file to view its contents.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Nested Loops

Suppose we want to set up a directory structure to organize
some experiments measuring reaction rate constants with different compounds
_and_ different temperatures.  Яким буде результат виконання наступного коду:

```bash
$ for species in cubane ethane methane
> do
>     for temperature in 25 30 37 40
>     do
>         mkdir $species-$temperature
>     done
> done
```

:::::::::::::::  solution

## Відповідь

Ми маємо вкладений цикл, тобто такий, що міститься в іншому циклі, тому для кожного значення змінної `species` у зовнішньому циклі внутрішній цикл (вкладений цикл) перебирає список температур і створює новий каталог для кожної комбінації.

Try running the code for yourself to see which directories are created!

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Цикл `for` повторює команди один раз для кожного елемента списку.
- Every `for` loop needs a variable to refer to the thing it is currently operating on.
- Use `$name` to expand a variable (i.e., get its value). Також можна використовувати `${name}`.
- Do not use spaces, quotes, or wildcard characters such as '\*' or '?' in filenames, as it complicates variable expansion.
- Give files consistent names that are easy to match with wildcard patterns to make it easy to select them for looping.
- Use the up-arrow key to scroll up through previous commands to edit and repeat them.
- Використовуйте <kbd>Ctrl</kbd>\+<kbd>R</kbd> для пошуку попередньо введених команд.
- Use `history` to display recent commands, and `![number]` to repeat a command by number.

::::::::::::::::::::::::::::::::::::::::::::::::::


