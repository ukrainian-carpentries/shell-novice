---
title: Обговорення
---

## Таємничі назви команд

Якщо команда, що дає змогу дізнатися, хто ми є, називається `whoami`, то команда, яка показує, де ми є, мала б називатися `whereami` — то чому ж тоді вона зветься `pwd`? На початку 1970-х кожне натискання клавіші мало значення, адже тодішні пристрої були повільними. Виправляти помилки та зворотні видалення на телетайпі було так важко, що менше клавіш означало менше помилок — і це було зручніше. Реальність полягає у тому, що команди додавалися до Unix одна за одною, без жодного загального плану, людьми, які були занурені в його жаргон. Результат настільки ж непослідовний, як би ми писали 'roolz uv Inglish speling' англійською (rules of English spelling) — і з цим доведеться змиритися.

## Спеціальні комбінації клавіш

Термінал приймає кілька спеціальних команд, які дозволяють користувачам взаємодіяти з процесами чи програмами, що вже запущені. You can enter each of these
"control codes" by holding down the `Ctrl` key and then pressing one
of the control characters. In other tutorials, you may see the term
`Control` or the `^` used to represent the `Ctrl` key (e.g. the
following are all equivalent `Ctrl-C`, `Ctrl+C`, `Control-C`, `Control+C`, `^C`).

- `Ctrl-C`:
  перериває і скасовує запущену програму.
  Це корисно, якщо ви хочете скасувати команду, яка виконується занадто довго.

- `Ctrl-D`:
  вказує на кінець файлу або потоку символів, які ви вводите у командному рядку.
  For example, we saw earlier that the `wc` command counts lines, words, and characters in a file.
  If we just type `wc` and hit the Enter key without providing a file name,
  then `wc` will assume we want it to analyze all the stuff we type next.
  After typing our magnum opus directly into the shell prompt,
  we can then type Ctrl-D to tell `wc` that we're done
  and we'd like to see the results of the word count.

- `Ctrl-Z`:
  Призупиняє процес, але не завершує його.
  Потім ви можете скористатися командою `fg`, щоб перезапустити процес у активному режимі.

For new shell users, these control codes can all appear to have
the same effect: they make things "go away." Але корисно
розуміти відмінності. Загалом, якщо щось пішло не так
і ви просто хочете повернути запит командного рядка, краще скористатися комбінацією
`Ctrl-C`.

## Інші термінали

До того, як Bash став популярним наприкінці дев'яностих, вчені широко використовували (а дехто й досі використовує) інший термінал: C-shell , або Csh. Bash and Csh
have similar feature sets, but their syntax rules are different and
this makes them incompatible with each other. A few other shells have
appeared since, including ksh, zsh, and a number of others; they are
mostly compatible with Bash, and Bash is the default shell on most
modern implementations of Unix (including most packages that provide
Unix-like tools for Windows) but if you get strange errors in shell
scripts written by colleagues, check to see which shell they were
written for.

## Конфігурації Bash

Want to customize paths, environment variables, aliases,
and other behaviors of your shell?
This excellent blog post "[Bash Configurations Demystified][bash-demystified]"
from Dalton Hubble
covers tips, tricks, and how to avoid dangers.

[bash-demystified]: https://blog.dghubble.io/posts/.bashprofile-.profile-and-.bashrc-conventions/



