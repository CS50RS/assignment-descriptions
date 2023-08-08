# Читабельність

Для цієї задачі ви реалізуєте програму, яка обчислює приблизний рівень навчання, необхідний для зрозуміння деякого тексту, згідно з наведеним нижче.

```plaintext
$ ./readability
Текст: Вітаємо! Сьогодні - ваш день. Ви рушаєте до Великих Місць! Ви вирушаєте і зникнете!
Клас 3
```

Відкрийте [VS Code](https://cs50.dev/).

Почніть, натиснувши всередині вікна терміналу, а потім виконайте команду `cd` самостійно. Ви повинні побачити, що її "курсор" схожий на показаний нижче.

```plaintext
$
```

Клацніть всередині цього вікна терміналу, а потім виконайте

```plaintext
wget https://cdn.cs50.net/2022/fall/psets/2/readability.zip
```

після чого натисніть Enter, щоб завантажити ZIP-файл з назвою `readability.zip` у ваше простір кодів. При цьому слід пильно стежити за пробілом між `wget` та наступним URL-адресом або будь-яким іншим символом!

Тепер виконайте

```plaintext
unzip readability.zip
```

щоб створити папку з назвою `readability`. Тепер вам не потрібний ZIP-файл, тому ви можете виконати

```plaintext
rm readability.zip
```

і відповісти "y", а потім натиснути Enter в командному рядку, щоб видалити завантажений вами ZIP-файл.

Тепер наберіть

```plaintext
cd readability
```

і натисніть Enter, щоб перейти до (тобто відкрити) цього каталогу. Ваш курсор тепер повинен виглядати наступним чином.

```plaintext
readability/ $
```

Якщо все пройшло успішно, ви повинні виконати

```plaintext
ls
```

і побачити файл з назвою `readability.c`. Виконання команди `code readability.c` повинно відкрити файл, де ви будете писати код для цієї задачі. Якщо ні, перевірте свої дії та спробуйте визначити, де ви помилилися!

## Основи

Згідно з [Scholastic](https://www.scholastic.com/teachers/teaching-tools/collections/guided-reading-book-lists-for-every-level.html), книга Е.Б. Уайта "Charlotte’s Web" знаходиться між рівнем читання у другому та четвертому класах, а "The Giver" від Лоїс Лоурі — між рівнем читання у восьмому та дванадцятому класах. Що ж означає, що книга має певний рівень читання?

У багатьох випадках експерт може прочитати книгу та прийняти рішення щодо класу (тобто року в школі), для якого, на його думку, книга найбільше підходить. Але алгоритм, ймовірно, міг би це також зрозуміти!

Отже, які риси характерні для вищого рівня читання? Довші слова, ймовірно, корелюють з вищим рівнем читання. Подібним чином довші речення, ймовірно, також корелюють з вищим рівнем читання.

Протягом багатьох років було розроблено ряд «тестів читабельності», які визначають формули для обчислення рівня читання тексту. Одним із таких тестів на читабельність є індекс Коулмана-Ліау. Індекс Коулмана-Ліау тексту призначений для виведення того шкільного класу, який необхідний для розуміння певного тексту. Формула така:

```plaintext
index = 0.0588 * L - 0.296 * S - 15.8
```

де L – середня кількість літер на 100 слів у тексті, а S – середня кількість речень на 100 слів у тексті.

Давайте напишемо програму під назвою readability, яка бере текст і визначає його рівень читання. Наприклад, якщо користувач вводить рядок тексту з Dr. Seuss, програма повинна діяти так:

```plaintext
$ ./readability
Text: Congratulations! Today is your day. You're off to Great Places! You're off and away!
Grade 3
```

Текст, який ввів користувач, містить 65 літер, 4 речення та 14 слів. 65 літер на 14 слів — це в середньому приблизно 464,29 літер на 100 слів (оскільки 65/14 \* 100 = 464,29). А 4 речення на 14 слів — це в середньому приблизно 28,57 речень на 100 слів (оскільки 4/14 \* 100 = 28,57). Підставивши до формули Коулмана-Ліау та округливши до найближчого цілого числа, ми отримаємо відповідь 3 (оскільки 0,0588 \* 464,29 - 0,296 * 28,57 - 15,8 = 3): отже, цей уривок належить до рівня читання третього класу.

Давайте спробуємо інший:

```plaintext
$ ./readability
Text: Harry Potter was a highly unusual boy in many ways. For one thing, he hated the summer holidays more than any other time of year. For another, he really wanted to do his homework, but was forced to do it in secret, in the dead of the night. And he also happened to be a wizard.
Grade 5
```

Цей текст містить 214 літер, 4 речення та 56 слів. Це приблизно 382,14 літер на 100 слів і 7,14 речень на 100 слів. Підключаючись до формули Коулмана-Ліау, ми отримуємо рівень читання для п’ятого класу.

Коли середня кількість літер і слів у реченні збільшується, індекс Коулмана-Ліау дає тексту вищий рівень читання. Якщо ви візьмете, наприклад, цей абзац, який містить довші слова та речення, ніж будь-який із попередніх двох прикладів, формула дасть тексту рівень читання для дванадцятого класу.

```plaintext
$ ./readability
Text: As the average number of letters and words per sentence increases, the Coleman-Liau index gives the text a higher reading level. If you were to take this paragraph, for instance, which has longer words and sentences than either of the prior two examples, the formula would give the text an twelfth-grade reading level.
Grade 12
```

## Завдання

Розробити та реалізувати програму, читабельність, яка обчислює індекс Коулмана-Ліау тексту.

* Реалізуйте свою програму у файлі під назвою readability.c у папці під назвою readability.
* Ваша програма має запитувати у користувача рядок тексту за допомогою get_string.
* Ваша програма має підрахувати кількість букв, слів і речень у тексті. Ви можете припустити, що літера — це будь-який малий символ від a до z або будь-який великий символ від A до Z, будь-яка послідовність символів, розділених пробілами, повинна вважатися словом, і що будь-яка поява крапки, знака оклику або знака питання позначає кінець речення.
* Ваша програма має надрукувати як результат «Grade X», де X — клас, обчислений за формулою Коулмана-Ліау, округлений до найближчого цілого числа.
* Якщо отриманий індекс дорівнює 16 або вище (еквівалентно або більше, ніж рівень читання старшого бакалавра), ваша програма має вивести «Grade 16+» замість того, щоб надавати точний номер індексу. Якщо число індексу менше 1, ваша програма має вивести «Before Grade 1».

## Отримання вводу користувача

Давайте спочатку напишемо якийсь код на C, який просто отримує текстовий ввід від користувача та друкує його назад. Зокрема, реалізуйте в readability.c основну функцію, яка запитує користувача «Text:» за допомогою get_string, а потім друкує той самий текст за допомогою printf. І пам’ятайте, коли ви працюєте з цією програмою, якщо ви використовуєте будь-які функції бібліотеки, обов’язково #include будь-які відповідні файли заголовків.

Програма має діяти, як зазначено нижче.

```plaintext
$ ./readability
Text: In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since.
In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since.
```

## Літери

Тепер, коли ви зібрали речення від користувача, давайте почнемо аналізувати цей вхід, спочатку підрахувавши кількість літер у тексті. Вважайте літери великими або малими літерами алфавіту, а не знаками пунктуації, цифрами чи іншими символами.

Додайте до readability.c, нижче main, функцію під назвою count_letters, яка приймає один аргумент, рядок тексту, і повертає int, кількість літер у цьому тексті. Обов’язково додайте прототип функції також поверх вашого файлу, щоб main знав, як її викликати. Прототип має бути схожим на наведене нижче:

```c
int count_letters(string text)
```

Потім викличте цю функцію в main, щоб замість друку самого тексту ваша програма друкувала кількість літер у тексті.

Тепер програма має діяти, як зазначено нижче.

```plaintext
$ ./readability
Text: Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, "and what is the use of a book," thought Alice "without pictures or conversation?"
235 letters
```

У `ctype.h` є функція, яка може виявитися корисною. Якщо ви використовуєте її, обов’язково додайте цей файл заголовка до свого коду!

## Слова

Індекс Коулмана-Ліау хоче знати не лише кількість букв, але й кількість слів у реченні. Для цілей цієї задачі ми розглядатимемо будь-яку послідовність символів, розділених пробілом, як слово (тому слово через дефіс, наприклад темно-зелений, слід вважати одним словом, а не двома).

Додайте до readability.c нижче main функцію під назвою count_words, яка приймає один аргумент, рядок тексту, і повертає int, кількість слів у цьому тексті. Обов’язково додайте прототип функції також поверх вашого файлу, щоб main знав, як її викликати.

Потім викличте цю функцію в main, щоб ваша програма також надрукувала кількість слів у тексті.

Ви можете припустити, що речення:

* міститиме хоча б одне слово;
* не починається або закінчується пробілом; і
* не матиме кількох пробілів поспіль.

Ви, звичайно, можете спробувати зробити програму, яка допускатиме кілька пробілів між словами або навіть жодних слів!

Тепер програма має діяти, як зазначено нижче.

```plaintext
$ ./readability
Text: It was a bright cold day in April, and the clocks were striking thirteen. Winston Smith, his chin nuzzled into his breast in an effort to escape the vile wind, slipped quickly through the glass doors of Victory Mansions, though not quickly enough to prevent a swirl of gritty dust from entering along with him.
250 letters
55 words
```

## Речення

Останньою інформацією, яка має значення для формули Коулмана-Ліау, крім кількості букв і слів, є кількість речень. Визначити кількість речень може бути напрочуд хитро. Спочатку ви можете уявити, що речення — це будь-яка послідовність символів, яка закінчується крапкою, але, звичайно, речення також можуть закінчуватися знаком оклику або питання. Але, звісно, не всі крапки обов’язково означають закінчення речення. Наприклад, розглянемо речення нижче.

```plaintext
$ ./readability
Text: When he was nearly thirteen, my brother Jem got his arm badly broken at the elbow. When it healed, and Jem's fears of never being able to play football were assuaged, he was seldom self-conscious about his injury. His left arm was somewhat shorter than his right; when he stood or walked, the back of his hand was at right angles to his body, his thumb parallel to his thigh.
295 letters
70 words
3 sentences
```

## Збираємо все разом

Тепер настав час зібрати всі частини разом! Нагадаємо, що індекс Коулмана-Ліау обчислюється за формулою:
`index = 0,0588 * L - 0,296 * S - 15,8`
де L – середня кількість літер на 100 слів у тексті, а S – середня кількість речень на 100 слів у тексті.

Змініть main у readability.c так, щоб замість виводу кількості літер, слів і речень він виводив (тільки) клас, визначений індексом Коулмана-Ліо (наприклад, «Grade 2» або «Grade 8» або подібне). Не забудьте округлити отримане число індексу до найближчого цілого!

### Підказки

* Нагадаємо, що "round" можна знайти в math.h.
* Пам’ятайте, що під час ділення значень типу `int` у C результат також буде `int` із відкиданням залишків (тобто цифр після коми). Іншими словами, результат буде «урізаним». Можливо, вам захочеться перетворити одне чи кілька значень у `float` перед виконанням ділення під час обчислення L і S!

Якщо отримане число індексу дорівнює 16 або вище (еквівалентно або більше, ніж рівень читання старшого бакалавра), ваша програма має вивести «Grade 16+» замість того, щоб вивести точний номер індексу. Якщо число індексу менше 1, ваша програма має вивести «Before grade 1».

## Як перевірити свій код

Спробуйте запустити програму на наступних текстах, щоб переконатися, що бачите вказаний рівень оцінки. Обов’язково копіюйте лише текст, без зайвих пробілів.

* `One fish. Two fish. Red fish. Blue fish.` (Before Grade 1)
* `Would you like them here or there? I would not like them here or there. I would not like them anywhere.` (Grade 2)
* `Congratulations! Today is your day. You're off to Great Places! You're off and away!` (Grade 3)
* `Harry Potter was a highly unusual boy in many ways. For one thing, he hated the summer holidays more than any other time of year. For another, he really wanted to do his homework, but was forced to do it in secret, in the dead of the night. And he also happened to be a wizard.` (Grade 5)
* `In my younger and more vulnerable years my father gave me some advice that I've been turning over in my mind ever since.` (Grade 7)
* `Alice was beginning to get very tired of sitting by her sister on the bank, and of having nothing to do: once or twice she had peeped into the book her sister was reading, but it had no pictures or conversations in it, "and what is the use of a book," thought Alice "without pictures or conversation?"` (Grade 8)
* W`hen he was nearly thirteen, my brother Jem got his arm badly broken at the elbow. When it healed, and Jem's fears of never being able to play football were assuaged, he was seldom self-conscious about his injury. His left arm was somewhat shorter than his right; when he stood or walked, the back of his hand was at right angles to his body, his thumb parallel to his thigh.` (Grade 8)
* `There are more things in Heaven and Earth, Horatio, than are dreamt of in your philosophy.` (Grade 9)
* `It was a bright cold day in April, and the clocks were striking thirteen. Winston Smith, his chin nuzzled into his breast in an effort to escape the vile wind, slipped quickly through the glass doors of Victory Mansions, though not quickly enough to prevent a swirl of gritty dust from entering along with him.` (Grade 10)
* `A large class of computational problems involve the determination of properties of graphs, digraphs, integers, arrays of integers, finite families of finite sets, boolean formulas and elements of other countable domains.` (Grade 16+)

Виконайте наведені нижче дії, щоб далі оцінити правильність вашого коду за допомогою `check50`. Але обов’язково скомпілюйте та протестуйте його самостійно!

```plaintext
check50 cs50/problems/2023/x/readability
```

Виконайте наведені нижче дії, щоб оцінити стиль вашого коду за допомогою `style50`.

```plaintext
style50 readability.c
```
