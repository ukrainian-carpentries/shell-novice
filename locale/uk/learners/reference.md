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
Коментарі у мовах Python, R та в терміналі Unix починаються з символу `#` та тривають до кінця відповідного рядка; коментарі в SQL починаються з `--`, а в інших мовах існують інші домовленості.

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
Оскільки багато програм використовують розширення назв файлів для ідентифікації [MIME типу](#mime-type) файлу, неправильні назви файлів можуть призвести до збоїв у роботі відповідних застосунків.

[фільтр]{#filter}
:   Програма, яка перетворює потік даних.
Багато інструментів командного рядка Unix написано у вигляді фільтрів: вони зчитують дані зі [стандартного вводу](#standard-input), обробляють їх і записують результат у [стандартний вивід](#standard-output).

[цикл for]{#for-loop}
:   Цикл, який виконується один раз для кожного значення в деякому наборі, списку або діапазоні.
Дивись також: [цикл while](#while-loop).

[графічний інтерфейс користувача]{#graphical-user-interface}
:   Інтерфейс користувача, у якому елементи й дії обираються на графічному екрані, зазвичай за допомогою миші.
Дивись також: [інтерфейс командного рядка](#command-line-interface).

[домашній каталог]{#home-directory}
:   Каталог за замовчуванням, пов'язаний з обліковим записом у комп'ютерній системі.
Зазвичай усі файли користувача зберігаються у домашньому каталозі або його підкаталогах.

[цикл]{#loop}
:   Набір інструкцій, що виконується декілька разів.
Складається з [тіла циклу](#loop-body) та (зазвичай) умови для виходу з нього. Дивись також: [цикл for](#for-loop) та [цикл while](#while-loop).

[тіло циклу]{#loop-body}
:   Набір операторів або команд, які повторюються всередині [циклу for]((#for-loop) чи [циклу while](#while-loop).

[тип MIME]{#mime-type}
:   Типи MIME (багатоцільові розширення інтернет-пошти, з англ. Multi-Purpose Internet Mail Extensions) описують різні типи файлів для обміну в Інтернеті через Інтернет, наприклад: зображення, аудіо та документи.

[операційна система]{#operating-system}
:   Програмне забезпечення, що забезпечує взаємодію між користувачами, обладнанням і програмними [процесами](#process).
Поширеними прикладами є Linux, macOS та Windows.

[опція]{#option}
:   Спосіб вказати аргумент або параметр у програмі, що викликається з командного рядка.
Зазвичай програми для Unix використовують тире, за яким слідує одна літера (наприклад, `-v`) або два тире за якими слідує слово (наприклад, `--verbose`). Застосунки DOS натомість використовують скісну риску (наприклад `/V`).
Залежно від програми, опція може супроводжуватися одним аргументом, наприклад `-o /tmp/output.txt`.

[параметр]{#parameter}
:   Змінна в оголошенні функції, яка отримує значення при виклику функції.
Цей термін часто (та непослідовно) замінюється на [аргумент](#аргумент).

[батьківський каталог]{#parent-directory}
:   Каталог, який "містить" каталог, про який йде мова.
Кожен каталог у файловій системі, окрім [кореневого каталогу](#root-directory), має батьківський каталог.
На батьківський каталог зазвичай посилаються за допомогою скороченого позначення `..` ("крапка крапка").

[шлях]{#path}
:   Нотація, яка вказує розташування файлу або каталогу у [файловій системі](#file-system).
Див. також: [абсолютний шлях](#absolute-path), [відносний шлях](#relative-path).

[канал]{#pipe}
:   З'єднання виходу однієї програми зі входом іншої.
Коли дві або більше програм з'єднані таким чином, вони називаються "конвеєром" (pipeline).

[процес]{#process}
:   Виконуваний екземпляр програми, який містить код, значення змінних, відкриті файли, мережеві з'єднання тощо.
Процеси - це "актори", якими керує [операційна система](#operating-system); зазвичай вона виконує кожен процес по кілька мілісекунд за раз щоб створити враження, що вони виконуються одночасно.

[запит на введення]{#prompt}
:   Символ або символи, які виводяться циклом [REPL](#read-evaluate-print-loop), щоб показати, що він чекає на наступну команду.

[взяття в лапки]{#quoting}
:   (в терміналі):
Використання лапок різного типу із метою запобігання інтерпретації командним рядком спеціальних символів.
Наприклад, щоб передати програмі рядок `*.txt`, зазвичай потрібно записати його як `'*.txt'` (з одинарними лапками), щоб термінал не намагався розгорнути символ підстановки `*`.

[цикл REPL]{#read-evaluate-print-loop}
:   (REPL): [Інтерфейс командного рядка](#command-line-interface), який читає команду від користувача, виконує її, виводить результат і чекає на наступну команду.

[перенаправлення]{#redirect}
:   Надсилання виводу команди до файлу замість екрана чи іншої команди або читання її вхідних даних із файлу.

[регулярний вираз]{#regular-expression}
:   Шаблон, який визначає набір рядків символів.
Регулярні вирази найчастіше використовуються для пошуку послідовностей символів у рядках.

[відносний шлях]{#relative-path}
:   [Шлях](#path), який вказує розташування файлу або каталогу відносно [поточного робочого каталогу](#current-working-directory).
Будь-який шлях, який не починається з символу-розділювача ("/" або "\\"), є відносним шляхом.
Див. також: [абсолютний шлях](#absolute-path).

[кореневий каталог]{#root-directory}
:   Найвищий каталог у [файловій системі](#file-system), від якого відгалужуються всі інші каталоги.
Він позначається "/" в Unix (включаючи Linux і macOS) та "\\" в Microsoft Windows.

[термінал]{#shell}
:   (оболонка):
[Інтерфейс командного рядка](#command-line-interface), наприклад, Bash (Bourne-Again Shell) або DOS термінал у Microsoft Windows, що дозволяють користувачеві взаємодіяти з [операційною системою](#operating-system).

[скрипт терміналу]{#shell-script}
:   (скрипт оболонки):
Набір команд [терміналу](#shell), збережений у файлі для повторного використання.
Скрипт терміналу - це програма, яку виконує термінал; назва "скрипт" використовується з історичних причин.

[стандартний ввід]{#standard-input}
:   Потік вхідних даних, який процес використовує за замовчуванням.
In interactive command-line applications,
it is typically connected to the keyboard;
in a [pipe](#pipe),
it receives data from the [standard output](#standard-output) of the preceding process.

[стандартний вивід]{#standard-output}
:   Вихідний потік процесу за замовчуванням.
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


