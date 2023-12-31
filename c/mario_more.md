# Маріо (складніше)

Відкрийте [VS Code](https://cs50.dev/).

Почніть, клікнувши в термінальному вікні, а потім виконайте `cd` без параметрів. Ви повинні побачити, що ваш "курсор" виглядає так:

```bash
$
```

Клікніть всередині цього термінального вікна, а потім виконайте

```bash
wget https://cdn.cs50.net/2022/fall/psets/1/mario-more.zip
```

і натисніть Enter, щоб завантажити ZIP-файл з назвою `mario-more.zip` у ваш кодспейс. Пам'ятайте, щоб не пропустити пробіл між `wget` і наступною URL-адресою чи будь-яким іншим символом!

Тепер виконайте

```bash
unzip mario-more.zip
```

щоб створити папку з назвою `mario-more`. Вам більше не потрібний ZIP-файл, тому можете виконати

```bash
rm mario-more.zip
```

і відповісти "y", а потім Enter на підтвердження видалення завантаженого ZIP-файлу.

Тепер введіть

```bash
cd mario-more
```

і натисніть Enter, щоб перейти (відкрити) до цієї папки. Ваш "курсор" тепер має вигляд:

```bash
mario-more/ $
```

Якщо все пройшло успішно, ви можете виконати

```bash
ls
```

і побачити файл з назвою `mario.c`. Виконання `code mario.c` відкриє файл, де ви будете вводити свій код для цього набору завдань. Якщо ні, повторіть свої кроки і перевірте, де ви помилились!

## World 1-1

Приблизно в кінці світу 1-1 у гри Super Mario Brothers від Nintendo, Маріо повинен перестрибнути через прилеглі піраміди з блоків, як на зображенні нижче:

![знімок екрану Маріо, який стрибає через прилеглі піраміди](https://cs50.harvard.edu/x/2023/psets/1/mario/more/pyramids.png)

Давайте перетворимо ці піраміди на мові С, хоча в текстовому варіанті, використовуючи хеш-символи (#) для блоків, як показано нижче. Кожен хеш має трохи більше висоти, ніж ширини, тому піраміди будуть вищими.

```bash
   #  #
  ##  ##
 ###  ###
####  ####
```

Програму, яку ми напишемо, називатимемо `mario`. І дозволимо користувачеві визначити, наскільки високими повинні бути піраміди, запитавши спочатку додатнє ціле число від 1 до 8, включно.

Ось як програма може працювати, якщо користувач вводить `8` при запиті:

```bash
$ ./mario
Height: 8
       #  #
      ##  ##
     ###  ###
    ####  ####
   #####  #####
  ######  ######
 #######  #######
########  ########
```

Ось як програма може працювати, якщо користувач вводить `4` при запиті:

```bash
$ ./mario
Height: 4
   #  #
  ##  ##
 ###  ###
####  ####
```

Ось як програма може працювати, якщо користувач вводить `2` при запиті:

```bash
$ ./mario
Height: 2
 #  #
##  ##
```

І ось як програма може працювати, якщо користувач вводить `1` при запиті:

```bash
$ ./mario
Height: 1
#  #
```

Якщо користувач не вводить додатнє ціле число від 1 до 8, включно, коли його запитують, програма повинна знову пропонувати ввести число:

```bash
$ ./mario
Height: -1
Height: 0
Height: 42
Height: 50
Height: 4
   #  #
  ##  ##
 ###  ###
####  ####
```

Зверніть увагу, що ширина "прогалини" між прилеглими пірамідами дорівнює ширині двох хешів, незалежно від висоти пірамід.

Відкрийте ваш файл `mario.c` для виконання цього завдання, як описано вище!

## Правильність коду

Чи працює ваш код, як зазначено, коли ви вводите:

- `-1` (або інші від'ємні числа)?
- `0`?
- `1` до `8`?
- `9` (або інші додатні числа)?
- букви або слова?
- жодного вводу, коли ви лише натискаєте Enter?

Ви також можете виконати нижче наведене, щоб оцінити правильність вашого коду за допомогою `check50`. Але не забудьте також скомпілювати і протестувати його самостійно!

```bash
check50 cs50/problems/2023/x/mario/more
```

Виконайте нижче наведене, щоб оцінити стиль вашого коду за допомогою `style50`.

```bash
style50 mario.c
```
