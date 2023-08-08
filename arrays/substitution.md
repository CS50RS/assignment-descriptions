# Заміна

Для цієї задачі ви напишете програму, яка реалізує шифр заміни, як описано нижче.

```plaintext
$ ./substitution JTREKYAVOGDXPSNCUIZLFBMWHQ
звичайний текст:  HELLO
шифрований текст: VKXXN
```

## Початок роботи

Відкрийте [VS Code](https://cs50.dev/).

Почніть, клікнувши всередині вікна терміналу, потім виконайте команду `cd`. Ви повинні побачити, що ваш "курсор" виглядає так:

```bash
$
```

Клікніть всередині того вікна терміналу, а потім виконайте

```bash
wget https://cdn.cs50.net/2022/fall/psets/2/substitution.zip
```

після чого натисніть Enter, щоб завантажити ZIP-файл з іменем `substitution.zip` в ваше середовище для кодування. Дбайте, щоб не пропустити пробіл між `wget` і наступним URL, чи будь-яким іншим символом!

Тепер виконайте

```bash
unzip substitution.zip
```

щоб створити папку з іменем `substitution`. Вам більше не потрібний ZIP-файл, тому ви можете виконати

```bash
rm substitution.zip
```

і відповісти "y", а потім натиснути Enter на запитання про видалення завантаженого ZIP-файлу.

Тепер введіть

```bash
cd substitution
```

а потім натисніть Enter, щоб перейти в ту папку (тобто відкрити її). Тепер ваш "курсор" повинен виглядати так:

```bash
substitution/ $
```

Якщо все пройшло успішно, ви можете виконати

```bash
ls
```

і побачити файл з іменем `substitution.c`. Виконання команди `code substitution.c` повинно відкрити файл, де ви будете писати свій код для цієї задачі. Якщо цього не відбулося, пройдіть усі кроки знову та спробуйте з'ясувати, де ви помилилися!

## Опис

У шифрі заміни ми "шифруємо" (тобто приховуємо у зворотно-зворотному способі) повідомлення, замінюючи кожну літеру іншою літерою. Для цього ми використовуємо "ключ": у цьому випадку відображення кожної з літер алфавіту на літеру, на яку вона має перейти, коли ми її шифруємо. Для "дешифрування" повідомлення отримувач повідомлення мусить знати ключ, щоб здійснити зворотний процес: переклад шифрованого тексту (зазвичай називається "шифрований текст") у вихідне повідомлення (зазвичай називається "звичайний текст").

Наприклад, ключ може бути рядок `NQXPOMAFTRHLZGECYJIUWSKDVB`. Цей ключ з 26 символів означає, що `A` (перша літера алфавіту) повинна бути перетворена на `N` (перший символ ключа), `B` (друга літера алфавіту) повинна бути перетворена на `Q` (другий символ ключа) і так далі.

Повідомлення, наприклад, як `HELLO`, буде зашифровано як `FOLLE`, замінюючи кожну з літер відповідно до відображення, визначеного ключем.

Давайте напишемо програму під назвою `substitution`, яка дозволяє вам шифрувати повідомлення за допомогою шифру заміни. Під час виконання користувачем програми вони повинні визначити, надаючи аргумент командного рядка, який буде використовуватися як ключ для введення секретного повідомлення під час виконання.

Ось кілька прикладів того, як може працювати програма. Наприклад, якщо користувач вводить ключ `YTNSHKVEFXRBAUQZCLWDMIPGJO` і звичайний текст `HELLO`:

```plaintext
$ ./substitution YTNSHKVEFXRBAUQZCLWDMIPGJO
plaintext:  HELLO
ciphertext: EHBBQ
```

Отже, якщо користувач надає ключ `VCHPRZGJNTLSKFBDQWAXEUYMOI` та звичайний текст `hello, world`:

```plaintext
$ ./substitution VCHPRZGJNTLSKFBDQWAXEUYMOI
plaintext:  hello, world
ciphertext: jrssb, ybwsp
```

Зверніть увагу, що кімната і кома не були замінені шифром. Замінюються лише букви алфавіту! Також зверніть увагу, що регістр початкового повідомлення зберігається. Великі літери залишаються великими, а малі літери залишаються малими.

Чи має значення те, чи великі літери у ключі чи малі, не має значення. Ключ `VCHPRZGJNTLSKFBDQWAXEUYMOI` функціонально ідентичний ключу `vchprzgjntlskfbdqwaxeuymoi` (і так само, до речі, `VcHpRzGjNtLsKfBdQwAxEuYmOi`).

А що якщо користувач не надасть дійсний ключ? Програма повинна пояснити це за допомогою повідомлення про помилку:

```plaintext
$ ./substitution ABC
Ключ повинен містити 26 символів.
```

Або взагалі не співпрацює, не надаючи аргумент командного рядка взагалі? Програма повинна нагадати користувачу, як використовувати програму:

```plaintext
$ ./substitution
Використання: ./substitution ключ
```

Або навіть, якщо користувач надасть забагато аргументів командного рядка? Програма також повинна нагадати користувачу, як використовувати програму:

```plaintext
$ ./substitution 1 2 3
Використання: ./substitution ключ
```

## Специфікація

Розробіть та реалізуйте програму `substitution`, яка шифрує повідомлення за допомогою шифру заміни.

* Реалізуйте вашу програму в файлі `substitution.c` у папці `substitution`.
* Ваша програма повинна приймати один аргумент командного рядка - ключ для використання при заміні. Сам ключ повинен бути регістронезалежним, тобто те, чи будь-який символ у ключі є великою чи малою літерою, не повинно впливати на роботу програми.
* Якщо вашу програму виконано без аргументів командного рядка або з більш ніж одним аргументом командного рядка, програма повинна вивести повідомлення про помилку на ваш вибір (за допомогою `printf`) і негайно повернутися з `main` зі значенням `1` (яке зазвичай позначає помилку).
* Якщо ключ недійсний (наприклад, не містить 26 символів, містить будь-який символ, який не є літерою алфавіту, або не містить кожну літеру рівно один раз), ваша програма повинна вивести повідомлення про помилку на ваш вибір (за допомогою `printf`) і негайно повернутися з `main` зі значенням `1`.
* Ваша програма повинна вивести `звичайний текст:` (без нового рядка) і потім запитати користувача про `рядок` звичайного тексту (за допомогою `get_string`).
* Ваша програма повинна вивести `шифрований текст:` (без нового рядка), а потім вивести шифрований текст, відповідний звичайному тексту, де кожна буква алфавіту в звичайному тексті замінюється на відповідну букву в шифрованому тексті; не-буквені символи повинні виводитися без змін.
* Ваша програма повинна зберігати регістр: великі букви мають залишитися великими буквами, а маленькі букви - маленькими.
* Після виведення шифрованого тексту, ви повинні вивести новий рядок. Ваша програма повинна вийти, повернувши `0` з `main`.

Вам можуть бути корисні одна або кілька функцій, в

изначених у `ctype.h`, дивіться [manual.cs50.io](https://manual.cs50.io/).

## Як перевірити свій код

Виконайте наступне, щоб оцінити правильність вашого коду за допомогою `check50`. Але не забудьте також скомпілювати та перевірити його самостійно!

```plaintext
check50 cs50/problems/2023/x/substitution
```

Виконайте наступне, щоб оцінити стиль вашого коду за допомогою `style50`.

```plaintext
style50 substitution.c
```

<details><summary>Як використовувати <code>debug50</code></summary><p>Бажаєте запустити <code>debug50</code>? Ви можете зробити це після успішної компіляції свого коду за допомогою <code>make</code>:</p>

```plaintext
debug50 ./substitution KEY
```

де `KEY` - це ключ, який ви вказуєте як аргумент командного рядка для вашої програми. Зверніть увагу, що виконання

```plaintext
debug50 ./substitution
```

(з ідеальним результатом!) повинно призвести до того, що програма завершиться, вимагаючи ввести ключ.</details>