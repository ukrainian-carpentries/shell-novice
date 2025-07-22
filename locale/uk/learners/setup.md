---
title: Налаштування
---

## Download files

You need to download some files to follow this lesson.

1. Download [shell-lesson-data.zip][zip-file] and move the file to your Desktop.
2. Розархівуйте файл.
  **Зверніться до інструктора, якщо вам потрібна допомога на цьому етапі**.
  На вашому робочому столі має з'явитися новий каталог з назвою **`shell-lesson-data`**.

## Інсталяція програмного забезпечення

Якщо у вас ще не встановлено програму-термінал, вам потрібно [завантажити та встановити][install_shell] її.

## Відкриття нового терміналу

Після встановлення програмного забезпечення

3. Відкрийте термінал.
  If you're not sure how to open a terminal on your operating system, see the instructions below.
4. У терміналі введіть `cd` і натисніть клавішу <kbd>Return</kbd>.
  This step will make sure you start with your home folder as your working directory.

У цьому уроці ви дізнаєтеся, як отримати доступ до файлів даних у цьому каталозі.

:::::::::::::::::::::::::::::::::::::::::  callout

## Як відкрити новий термінал у вашій операційній системі

The shell is a program that enables us to send commands to the computer and receive output.
Її також називають оболонкою або командним рядком.

На деяких комп'ютерах встановлено програму Unix Shell за замовчуванням.
The steps below describe some methods for identifying and opening
a Unix Shell program if you already have one installed.
There are also options for identifying and downloading a Unix Shell program,
a Linux/UNIX emulator, or a program to access a Unix Shell on a server.

If none of the options below address your circumstances,
try an online search for: Unix shell [your computer model] [your operating system].

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::: solution

### Windows {#windows}

Computers with Windows operating systems do not automatically have a Unix Shell program
installed.
У цьому уроці ми рекомендуємо вам скористатися емулятором, що входить до складу [Git for Windows][install_shell],
який надає доступ як до команд оболонки Bash, так і до Git'у.

Після встановлення ви можете відкрити термінал, запустивши програму Git Bash зі стартового меню Windows.

**Для досвідчених користувачів:**

As an alternative to Git for Windows you may wish to [Install the Windows Subsystem for Linux][wsl]
which gives access to a Bash shell command-line tool in Windows 10 and above.

Зверніть увагу, що команди у підсистемі Windows для Linux (WSL) можуть дещо відрізнятися від тих, що показані в уроці або представлені на семінарі.

::::::::::::

:::::::::::: solution

### MacOS {#macos}

For a Mac computer running macOS Mojave or earlier releases, the default Unix Shell is Bash.
For a Mac computer running macOS Catalina or later releases, the default Unix Shell is Zsh.
Your default shell is available via the Terminal program within your Utilities folder.

Щоб відкрити Термінал, спробуйте один або обидва з наведених нижче способів:

- In Finder, select the Go menu, then select Utilities.
  Locate Terminal in the Utilities folder and open it.
- Скористайтеся функцією пошуку 'Spotlight'.
  Знайдіть `Terminal` і натисніть <kbd>Return</kbd>.

To check if your machine is set up to use something other than Bash,
type `echo $SHELL` in your terminal window.

Якщо ваш комп'ютер налаштований на використання чогось іншого, ніж Bash, ви можете запустити Bash, відкривши термінал і набравши `bash`.

[Як користуватися терміналом на Mac][mac-terminal]

::::::::::::

:::::::::::: solution

### Linux {#linux}

Стандартним терміналом Unix для операційних систем Linux зазвичай є Bash.
On most versions of Linux, it is accessible by running the
[Gnome Terminal][gnome-terminal] or [KDE Konsole][kde-konsole] or [xterm],
which can be found via the applications menu or the search bar.
If your machine is set up to use something other than Bash,
you can run it by opening a terminal and typing `bash`.

::::::::::::

[zip-file]: data/shell-lesson-data.zip
[install_shell]: https://carpentries.github.io/workshop-template/install_instructions/#shell
[wsl]: https://learn.microsoft.com/en-us/windows/wsl/install
[mac-terminal]: https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm



