---
title: Примітки для інструктора
---

- Навіщо ми вчимося користуватися терміналом?
  - Дозволяє користувачам автоматизувати повторювані завдання
  - Та зберігає маленькі кроки роботи з даними, які зазвичай не записують — щоб дослідження можна було повторити
- Проблема
  - Запускати той самий процес для кількох зразків — це зайва робота
  - Ручна маніпуляція з файлами даних:
    - часто не відображається в документації
    - важка для відтворення
    - важко усунути несправності, переглянути або вдосконалити
- Термінал
  - Робочі процеси можна автоматизувати за допомогою скриптів терміналу
  - Вбудовані команди дозволяють легко маніпулювати даними (наприклад, sort, grep тощо.)
  - Кожен крок може бути зафіксований у скрипті терміналу, що забезпечує відтворюваність та легке усунення несправностей

## Підсумок

Багато хто ставить під сумнів, чи варто нам продовжувати навчати людей працювати з терміналом.
Адже перейменувати тисячі файлів можна в Python, а серйозний аналіз даних можна зробити у IPython Notebook або R Studio.
Тож навіщо навчатися роботі в терміналі?

Перша відповідь така:
"Тому що багато інших речей залежать від цього."
Встановлення програмного забезпечення,
налаштування редактора за замовчуванням
та керування віддаленими комп'ютерами часто вимагають базового знайомства з командним терміналом
та пов'язаними з ним поняттями, такими як стандартний ввід та вивід.
Багато інструментів також використовують його термінологію
(наприклад, магічні команди `%ls` та `%cd` в IPython).

Друга відповідь така:
"Тому що це простий спосіб показати деякі фундаментальні ідеї про те, як користуватися комп'ютером."
Коли ми вчимо людей користуватися терміналом Unix,
ми вчимо їх, що вони повинні змусити комп'ютер повторювати дії
(за допомогою завершення клавішею табуляції,
знаком `!`, за яким йде номер команди,
та циклів "for")
замість того, щоб повторювати щось самому.
Ми також вчимо їх брати речі, які, як виявилося, вони роблять часто,
і зберігати їх для подальшого використання
(за допомогою скриптів терміналу),
давати речам розумні назви
і писати невелику документацію
(наприклад, коментар у верхній частині скрипта терміналу)
щоб покращити життя свого майбутнього "Я".

Третя відповідь така:
"Тому що це дозволяє використовувати багато вузькоспеціалізованих інструментів та обчислювальних ресурсів,
до яких дослідники не можуть отримати доступ інакше."
Знання терміналу дуже стає у пригоді — для віддаленого доступу до комп'ютерів,
роботи з потужними обчислювальними системами
та використання нових спеціалізованих інструментів у багатьох дисциплінах.
Ми не навчаємо навичкам роботи з високопродуктивними обчислювальними системами або роботі в конкретних галузях,
але закладаємо основу для подальшого розвитку цих навичок.
Зокрема,
розуміння синтаксису команд, їх опцій та довідкових систем допомагає використовувати спеціалізовані інструменти.
А розуміння файлової системи (та способів навігації по ній) корисне для віддаленого доступу.

І нарешті, мабуть, найважливіше: навчання людей роботі з терміналом, ми вчимо їх думати про програмування з точки зору композиції функцій.
У терміналі замість вкладених функцій використовуються конвеєри, але ідея та сама: "маленькі частини, нещільно з'єднані між собою".

Цей матеріал можна викласти за три години — якщо в учнів на Windows не виникне таких проблем, як:

- труднощі з визначенням розташування домашнього каталогу (особливо якщо вони використовують Cygwin);
- невміння запустити звичайний текстовий редактор;
  та
- відмова терміналу виконувати скрипти, які містять закінчення рядків DOS.

## Підготовка до викладання

- Використовуйте каталог `data` для вправ на семінарах та для прикладів кодування в реальному часі.
  Ви можете клонувати репозиторій shell-novice або скористатися кнопкою \* Download ZIP\* праворуч, щоб отримати весь [репозиторій](https://github.com/swcarpentry/shell-novice). Також тепер ми надаємо
  zip-файл каталогу `data`
  на [Сторінці налаштування](../learners/setup.md).

- Вебсайт: до цього використовувалися різні практики.

  - Option 1: Can give links to learners before the lesson so they can follow along,
    catch up,
    and see exercises (particularly if you're following the lesson content without many changes).
  - Варіант 2: Не показуйте вебсайт під час уроку — він відволікає. Учні будуть читати замість того, щоб слухати, а зайве вікно заважає зосередитися.
  - У будь-якому випадку, обов'язково вкажіть на вебсайт як на довідковий ресурс після семінару.

- Зміст:
  Якщо ви не маєте багато часу (4+ години), швидше за все, ви не встигнете пройти ВЕСЬ матеріал за одне заняття тривалістю пів дня.
  Заздалегідь вирішіть, що можна пропустити, а на чому варто зробити акцент тощо.

- Вправи:
  Заздалегідь продумайте, як ви будете організовувати виконання вправ під час уроку.
  Як слухачі будуть бачити завдання (вебсайт, слайд, супровідні матеріали)?
  Чи хочете ви, щоб усі спробували виконати вправу, а потім ви покажете розв'язок?
  Або запропонуєте одному з учасників продемонструвати розв'язок?
  Have groups each do a different exercise and present their solutions?

- На ваш вибір, [сторінку довідки](../learners/reference.md) можна надрукувати та роздати студентам для ознайомлення.

- Подальша підготовка:
  Ви можете додавати власні приклади чи коментарі,
  але знайте, що це не обов'язково: усі поняття та команди можна викладати так, як зазначено на сторінках уроку.
  Якщо ви вважаєте, що в уроці чогось не вистачає, не соромтеся повідомити про проблему або створити запит на зміну матеріалу.

## Нотатки для викладача

- Чудовий онлайн-ресурс!
  [http://explainshell.com/](https://explainshell.com/) аналізує будь-яку команду терміналу та показує пояснення до кожної її частини.
  Additional nice manual tool could be [http://tldr.sh/](https://tldr.sh/)
  with short very descriptive manuals for shell commands,
  useful especially on Windows while using Git BASH where `man` could not work.

- Another super cool online resource is [http://www.shellcheck.net](https://www.shellcheck.net),
  which will check shell scripts (both uploaded and typed in) for common errors.

- Resources for "splitting" your shell so that recent commands
  remain in view: [https://github.com/rgaiacs/swc-shell-split-window](https://github.com/rgaiacs/swc-shell-split-window).

- Tab completion sounds like a small thing: it isn't.
  Re-running old commands using `!123` or `!wc`
  isn't a small thing either,
  and neither are wildcard expansion and `for` loops.
  Each one is an opportunity to repeat one of the big ideas of Software Carpentry:
  if the computer _can_ repeat it,
  some programmer somewhere will almost certainly have built
  some way for the computer _to_ repeat it.

- Building up a pipeline with four or five stages,
  then putting it in a shell script for re-use
  and calling that script inside a `for` loop,
  is a great opportunity to show how
  "seven plus or minus two"
  connects to programming.
  Once we have figured out how to do something moderately complicated,
  we make it re-usable and give it a name
  so that it only takes up one slot in working memory
  rather than several.
  It is also a good opportunity to talk about exploratory programming:
  rather than designing a program up front,
  we can do a few useful things
  and then retroactively decide which are worth encapsulating
  for future re-use.

- If everything is going well, you can drive home the point that file
  extensions are essentially there to help computers (and human
  readers) understand file content and are not a requirement of files
  (covered briefly in
  [Navigating Files and Directories](../episodes/02-filedir.md)).
  This can be done in the
  [Pipes and Filters](../episodes/04-pipefilter.md) section by showing
  that you can redirect standard output to a file without the .txt extension
  (e.g., lengths), and that the resulting file is still a perfectly usable text file.
  Make the point that if double-clicked in the GUI, the computer will
  probably ask you what you want to do.

- We have to leave out many important things because of time constraints,
  including file permissions, job control, and SSH.
  If learners already understand the basic material,
  this can be covered instead using the online lessons as guidelines.
  These limitations also have follow-on consequences:

- Важко обговорювати `#!` (шебанг), не обговоривши попередньо дозволів, чого ми не робимо.  `#!` is also [pretty
  complicated][shebang], so even if we did discuss permissions, we
  probably still wouldn't want to discuss `#!`.

- Installing Bash and a reasonable set of Unix commands on Windows
  always involves some fiddling and frustration.
  Please see the latest set of installation guidelines for advice,
  and try it out yourself _before_ teaching a class.

- By default, you may have a long string of information attached to
  your command prompt in Git Bash. To reduce the "noise" and proceed
  with a tidier prompt, enter the command:

  ```bash
  PS1='$ '
  ```

- On Windows machines
  if `nano` hasn't been properly installed with the
  [Software Carpentry Windows Installer][windows-installer]
  it is possible to use `notepad` as an alternative.  There will be a GUI
  interface and line endings are treated differently, but otherwise, for
  the purposes of this lesson, `notepad` and `nano` can be used almost interchangeably.

- On Windows, it appears that:

  ```bash
  $ cd
  $ cd Desktop
  ```

  will always put someone on their desktop
  (unless their machine is backed up using enterprise OneDrive, see next point).
  Have them create the example directory for the shell exercises there
  so that they can find it easily
  and watch it evolve.

- If a Windows machine is backed up with enterprise OneDrive, their GUI desktop may
  be rendered from a folder within OneDrive, which will not match the contents of `~/Desktop`.
  The OneDrive desktop should be accessible using one of the following commands
  (if the name of the enterprise isn't clear, look through the output of `ls` to find
  the right folder):

  ```bash
  $ cd "~/OneDrive - Name Of Enterprise/Desktop"
  $ cd "C:/Users/Username/OneDrive - Name Of Enterprise/Desktop"
  ```

  One way to spot if the computer is using this kind of configuration is to look at files,
  folders or links on the desktop. Usually the icon contains a shortcut/arrow symbol if it
  is a link, or just the plain icon if the file is just saved in the `Desktop` folder.
  Files synced with OneDrive contain an additional symbol indicating the sync status
  (typically blue arrows for 'sync pending' or a green tick for 'synced').

- Stay within POSIX-compliant commands, as all the teaching materials do.
  Your particular shell may have extensions beyond POSIX that are not available
  on other machines, especially the default macOS bash and Windows bash emulators.
  For example, POSIX `ls` does not have an `--ignore=` or `-I` option, and POSIX
  `head` takes `-n 10` or `-10`, but not the long form of `--lines=10`.

## Windows

Installing Bash and a reasonable set of Unix commands on Windows
always involves some fiddling and frustration.
Please see the latest set of installation guidelines for advice,
and try it out yourself _before_ teaching a class.
Options we have explored include:

1. [msysGit](https://msysgit.github.io/) (also called "Git Bash"),
2. [Cygwin](https://www.cygwin.com/),
3. using a desktop virtual machine, and
4. having learners connect to a remote Unix machine (typically a VM in the cloud).

Cygwin was the preferred option until mid-2013,
but once we started teaching Git,
msysGit proved to work better.
Desktop virtual machines and cloud-based VMs work well for technically sophisticated learners,
and can reduce installation and configuration at the start of the workshop,
but:

1. they don't work well on underpowered machines,
2. they're confusing for novices (because simple things like copy and paste work differently),
3. learners leave the workshop without a working environment on their operating system of choice,
   and
4. learners may show up without having downloaded the VM or the wireless will go down
   (or become congested) during the lesson.

Whatever you use,
please _test it yourself_ on a Windows machine _before_ your workshop:
things may always have changed behind your back since your last workshop.
And please also make use of our
[Software Carpentry Windows Installer][windows-installer].

[shebang]: https://www.in-ulm.de/~mascheck/various/shebang/
[windows-installer]: https://github.com/swcarpentry/windows-installer



