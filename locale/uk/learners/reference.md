---
title: 'Короткий опис основних команд'
---

## Короткий опис основних команд

| Дія                                                            | Для файлів | Для каталогів |
| -------------------------------------------------------------- | ---------- | ------------- |
| Оглянути                                                       | ls         | ls            |
| Проглянути вміст                                               | cat        | ls            |
| Перейти до ... |            | cd            |
| Перемістити                                                    | mv         | mv            |
| Копіювати                                                      | cp         | cp -r         |
| Створити                                                       | nano       | mkdir         |
| Видалити                                                       | rm         | rmdir, rm -r  |

## Ієрархія файлової системи

Нижче наведено огляд стандартної файлової системи Unix.
Її точна ієрархія може відрізнятися залежно від платформи. Ваша структура файлів/каталогів може дещо відрізнятися:

![](fig/standard-filesystem-hierarchy.svg){alt='Ієрархія файлової системи Linux'}

## Глосарій

[абсолютний шлях]{#absolute-path}
:   [Шлях](#path), який посилається на певне місце у файловій системі.
Абсолютні шляхи зазвичай записуються відносно [кореневого каталогу](#root-directory) файлової системи та починаються з символів "/" (у Unix) або "\\" (у Microsoft Windows).
Див. також: [відносний шлях](#relative-path).

[аргумент]{#argument}
:    Значення, яке передається до функції або програми під час її запуску.
Цей термін часто (та непослідовно) замінюється на [параметр](#parameter).

[командна оболонка]{#command-shell}
:   Дивись [термінал](#shell)

[інтерфейс командного рядка]{#command-line-interface}
:   Інтерфейс користувача, заснований на введенні команд,
зазвичай у циклі [REPL](#read-evaluate-print-loop).
Див. також: [графічний інтерфейс користувача](#graphical-user-interface).

[коментар]{#comment}
:   Зауваження в програмі, яке пояснює код людині-читачеві, але ігнорується комп'ютером.
Comments in Python, R, and the Unix shell start with a `#` character
and run to the end of the line;
comments in SQL start with `--`,
and other languages have other conventions.

[поточний робочий каталог]{#current-working-directory}
:   Каталог, з якого визначаються [відносні шляхи](#relative-path); тобто місце, де відбувається пошук файлів, вказаних лише за назвою.
Кожен [процес](#process) має власний поточний робочий каталог.
На поточний робочий каталог зазвичай посилаються за допомогою скорочення `.` (тобто "крапка").

[файлова система]{#file-system}
:   Набір файлів, каталогів та пристроїв вводу/виводу (таких як клавіатури та екрани).
Файлова система може бути розподіленою на кількох фізичних пристроях одразу, або декілька файлових систем можуть зберігатися на одному пристрої; доступом керує [операційна система](#operating-system).

[розширення файлу]{#filename-extension}
:   Частина імені файлу, яка йде після останнього символу ".".
За домовленістю це визначає тип файлу: `.txt` означає "текстовий файл (від англ. "TeXT"), `.png` означає "файл портативної мережевої графіки" (від англ. "Portable Network Graphics file"), і так далі. Більшість операційних систем не наполягають на дотриманні цих домовленостей: цілком можливо (але призведе до плутанини!) назвати звуковий MP3 файл `homepage.html`.
Since many applications use filename extensions to identify the
[MIME type](#mime-type) of the file,
misnaming files may cause those applications to fail.

[фільтр]{#filter}
:   Програма, яка перетворює потік даних.
Багато інструментів командного рядка Unix написано у вигляді фільтрів: вони зчитують дані зі [стандартного вводу](#standard-input), обробляють їх і записують результат у [стандартний вивід](#standard-output).

[for loop]{#for-loop}
:   A loop that is executed once for each value in some kind of set, list, or range.
See also: [while loop](#while-loop).

[graphical user interface]{#graphical-user-interface}
:   A user interface based on selecting items and actions from a graphical display,
usually controlled by using a mouse.
Дивись також: [інтерфейс командного рядка](#command-line-interface).

[home directory]{#home-directory}
:   The default directory associated with an account on a computer system.
By convention, all of a user's files are stored in or below her home directory.

[loop]{#loop}
:   A set of instructions to be executed multiple times.
Consists of a [loop body](#loop-body) and (usually) a
condition for exiting the loop. See also [for loop](#for-loop) and [while loop](#while-loop).

[loop body]{#loop-body}
:   The set of statements or commands that are repeated inside a [for loop](#for-loop)
or [while loop](#while-loop).

[MIME type]{#mime-type}
:   MIME (Multi-Purpose Internet Mail Extensions) types describe different file types for exchange
on the Internet, for example, images, audio, and documents.

[operating system]{#operating-system}
:   Software that manages interactions between users, hardware, and software [processes](#process).
Common examples are Linux, macOS, and Windows.

[option]{#option}
:   A way to specify an argument or setting to a command-line program.
By convention Unix applications use a dash followed by a single letter,
such as `-v`, or two dashes followed by a word, such as `--verbose`,
while DOS applications use a slash, such as `/V`.
Depending on the application, an option may be followed by a single argument,
as in `-o /tmp/output.txt`.

[parameter]{#parameter}
:   A variable named in a function's declaration that is used to hold a value passed into the call.
The term is often used interchangeably (and inconsistently) with [argument](#argument).

[батьківський каталог]{#parent-directory}
:   Каталог, який "містить" каталог, про який йде мова.
Every directory in a file system except the [root directory](#root-directory) has a parent.
A directory's parent is usually referred to using the shorthand notation `..`
(pronounced "dot dot").

[path]{#path}
:   A description that specifies the location of a file or directory within a
[file system](#file-system).
See also: [absolute path](#absolute-path), [relative path](#relative-path).

[pipe]{#pipe}
:   A connection from the output of one program to the input of another.
When two or more programs are connected in this way, they are called a "pipeline".

[process]{#process}
:   A running instance of a program, containing code, variable values,
open files and network connections, and so on.
Processes are the "actors" that the [operating system](#operating-system) manages;
it typically runs each process for a few milliseconds at a time
to give the impression that they are executing simultaneously.

[prompt]{#prompt}
:   A character or characters display by a [REPL](#read-evaluate-print-loop) to show that
it is waiting for its next command.

[quoting]{#quoting}
:   (in the shell):
Using quotation marks of various kinds to prevent the shell from interpreting special
characters.
For example, to pass the string `*.txt` to a program,
it is usually necessary to write it as `'*.txt'` (with single quotes)
so that the shell will not try to expand the `*` wildcard.

[read-evaluate-print loop]{#read-evaluate-print-loop}
:   (REPL): A [command-line interface](#command-line-interface) that reads a command from the user,
executes it, prints the result, and waits for another command.

[redirect]{#redirect}
:   To send a command's output to a file rather than to the screen or another command,
or equivalently to read a command's input from a file.

[регулярний вираз]{#regular-expression}
:   Шаблон, який визначає набір рядків символів.
REs are most often used to find sequences of characters in strings.

[relative path]{#relative-path}
:   A [path](#path) that specifies the location of a file or directory
with respect to the [current working directory](#current-working-directory).
Any path that does not begin with a separator character ("/" or "\\") is a relative path.
See also: [absolute path](#absolute-path).

[root directory]{#root-directory}
:   The top-most directory in a [file system](#file-system).
Its name is "/" on Unix (including Linux and macOS) and "\\" on Microsoft Windows.

[shell]{#shell}
:   A [command-line interface](#command-line-interface) such as Bash (the Bourne-Again Shell)
or the Microsoft Windows DOS shell
that allows a user to interact with the [operating system](#operating-system).

[shell script]{#shell-script}
:   A set of [shell](#shell) commands stored in a file for re-use.
A shell script is a program executed by the shell;
the name "script" is used for historical reasons.

[standard input]{#standard-input}
:   A process's default input stream.
In interactive command-line applications,
it is typically connected to the keyboard;
in a [pipe](#pipe),
it receives data from the [standard output](#standard-output) of the preceding process.

[standard output]{#standard-output}
:   A process's default output stream.
In interactive command-line applications,
data sent to standard output is displayed on the screen;
in a [pipe](#pipe),
it is passed to the [standard input](#standard-input) of the next process.

[підкаталог]{#sub-directory}
:   Каталог, що міститься у іншому каталозі.

[tab completion]{#tab-completion}
:   A feature provided by many interactive systems in which
pressing the Tab key triggers automatic completion of the current word or command.

[variable]{#variable}
:   A name in a program that is associated with a value or a collection of values.

[while loop]{#while-loop}
:   A loop that keeps executing as long as some condition is true.
See also: [for loop](#for-loop).

[wildcard]{#wildcard}
:   A character used in pattern matching.
In the Unix shell,
the wildcard `*` matches zero or more characters,
so that `*.txt` matches all files whose names end in `.txt`.

## External references

### Opening a terminal

- [How to Use Terminal on a Mac](https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)
- [Git for Windows](https://git-for-windows.github.io/)
- [How to Install Bash shell command-line tool on Windows 10](https://www.windowscentral.com/how-install-bash-shell-command-line-windows-10)
- [Install and Use the Linux Bash Shell on Windows 10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)
- [Using the Windows 10 Bash Shell](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/)
- [Using a UNIX/Linux emulator (Cygwin) or Secure Shell (SSH) client (Putty)](https://faculty.smu.edu/reynolds/unixtut/windows.html)

### Manuals

- [GNU manuals](https://www.gnu.org/manual/manual.html)
- [Core GNU utilities](https://www.gnu.org/software/coreutils/manual/coreutils.html)

### Miscellaneous

- [North Pacific Gyre](https://en.wikipedia.org/wiki/North_Pacific_Gyre)
- [Great Pacific Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch)
- ['Ensuring the longevity of digital information' by Jeff Rothenberg](https://www.clir.org/pubs/archives/ensuring.pdf)
- [Computer error haikus](https://wiki.c2.com/?ComputerErrorHaiku)
- [How to name files nicely, by Jenny Bryan](https://speakerdeck.com/jennybc/how-to-name-files)


