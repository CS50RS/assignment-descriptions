# Кредит

Відкрийте [VS Code](https://cs50.dev/).

Почніть, натиснувши на вашому терміналі, а потім виконайте команду `cd` самостійно. Ви повинні побачити, що ваша "курсор" виглядає наступним чином:

```plaintext
$
```

Клікніть всередині цього вікна терміналу і потім виконайте наступну команду:

```plaintext
wget https://cdn.cs50.net/2022/fall/psets/1/credit.zip
```

після чого натисніть Enter, щоб завантажити ZIP-архів з назвою `credit.zip` у вашу робочу область. Будьте уважні і не пропустіть пробіл між `wget` та URL, або будь-який інший символ!

Тепер виконайте:

```plaintext
unzip credit.zip
```

щоб створити папку з назвою `credit`. Ви більше не потребуєте ZIP-файл, тому ви можете виконати:

```plaintext
rm credit.zip
```

і відповісти "y", а потім натиснути Enter на запит про видалення завантаженого ZIP-файлу.

Тепер введіть:

```plaintext
cd credit
```

і натисніть Enter, щоб перейти (відкрити) в ту папку. Ваш "курсор" тепер повинен виглядати так:

```plaintext
credit/ $
```

Якщо все пройшло успішно, виконайте:

```plaintext
ls
```

і побачите файл з назвою `credit.c`. Виконання `code credit.c` має відкрити файл, в якому ви будете писати свій код для цього завдання. Якщо цього не сталося, повторіть свої дії та переконайтеся, чи не допустили ви помилок!

## Кредитні картки

Кредитна (або дебетова) карта, є пластиковою карткою, за допомогою якої можна оплачувати товари та послуги. На цій картці надруковано номер, який також зберігається у базі даних, так що, коли ви використовуєте картку для покупки, кредитор знає, кому виставити рахунок. У цьому світі є багато людей з кредитними картками, тому ці номери досить довгі: American Express використовує 15-значні номери, MasterCard - 16-значні номери, а Visa - 13- і 16-значні номери. І ці числа десяткові (від 0 до 9), а не двійкові, що означає, наприклад, що American Express може надрукувати стільки, скільки 10^15 = 1,000,000,000,000,000 унікальних карток! (Квадрильйон!)

Насправді це трохи перебільшено, оскільки номери кредитних карт дійсно мають певну структуру. Всі номери American Express починаються з 34 або 37; більшість номерів MasterCard починаються з 51, 52, 53, 54 або 55 (вони також мають ще деякі можливі початкові числа, які нас не стосуються в цьому завданні); і всі номери Visa починаються з 4. Проте у номерах кредитних карт також є "контрольна сума" (checksum), яка будується на основі математичного відношення між принаймні одним числом та іншими. Ця контрольна сума дозволяє комп'ютерам (або людям, які люблять математику) виявляти помилки (наприклад, транспозиції), та шахрайські номери, без необхідності запитувати базу даних, що може бути повільно. Звичайно, нечесний математик може зробити підроблений номер, який все ж дотримується математичного обмеження, тому перевірка бази даних все ще необхідна для більш ретельної перевірки.

## Алгоритм Луна

Що це за таємна формула? Більшість карток використовують алгоритм, винайдений Гансом Петером Луном з IBM. Згідно з алгоритмом Луна, ви можете визначити, чи є номер кредитної картки (синтаксично) дійсним, виконуючи такі дії:

1. Помножте кожну другу цифру на 2, починаючи з передостанньої цифри числа, а потім додайте цифри цих добутків разом.
2. Додайте отриману суму до суми цифр, які не були помножені на 2.
3. Якщо остання цифра суми є 0 (або, більш формально, якщо сума за модулем 10 конгруентна 0), номер є дійсним!

Давайте спробуємо приклад з карткою Візи Девіда: 4003600000000014.

1. Підкреслимо кожну другу цифру, починаючи з передостанньої цифри:

   ```
   4 0 0 3 6 0 0 0 0 0 0 0 0 0 1 4
   ```

   Помножимо кожну з підкреслених цифр на 2:

   ```
   1•2 + 0•2 + 0•2 + 0•2 + 0•2 + 6•2 + 0•2 + 4•2
   ```

   Це дасть нам:

   ```
   2 + 0 + 0 + 0 + 0 + 12 + 0 + 8
   ```

   Тепер додамо цифри цих добутків (тобто не самі добутки) разом:

   ```
   2 + 0 + 0 + 0 + 0 + 1 + 2 + 0 + 8 = 13
   ```

2. Тепер додамо цю суму (13) до суми цифр, які не були помножені на 2 (починаючи з кінця):

   ```
   13 + 4 + 0 + 0 + 0 + 0 + 0 + 3 + 0 = 20
   ```

3. Так, остання цифра цієї суми (20) є 0, отже карта Девіда дійсна!

Таким чином, перевірка номерів кредитних карток не є складною, але ручні операції можуть бути дещо нудними. Давайте напишемо програму.

## Деталі реалізації

У файлі `credit.c` в папці `credit` напишіть програму, яка запитує в користувача номер кредитної картки, а потім повідомляє (за допомогою `printf`), чи є вона дійсною кредитною карткою American Express, MasterCard або Visa, відповідно до визначень форматів кожної картки, які наведені нижче. Щоб ми могли автоматизувати деякі тести вашого коду, ми просимо, щоб останній рядок виводу вашої програми був `AMEX\n` або `MASTERCARD\n` або `VISA\n` або `INVALID\n`, нічого більше і нічого менше. Щоб спростити, ви можете припускати, що ввід користувача буде цілком числовим (тобто без дефісів, як це може бути надруковано на фактичній картці) і без передних нулів. Але не припускайте, що ввід користувача вміститься в тип даних `int`! Найкраще використовувати `get_long` з бібліотеки CS50 для отримання введення користувача. (Чому?)

Розгляньте наступне як приклад того, як повинна вести себе ваша програма при введенні дійсного номера кредитної картки (без дефісів).

```plaintext
$ ./credit
Number: 4003600000000014
VISA
```

Тепер, `get_long` сам по собі вже відкидає дефіси (та ще багато іншого):

```plaintext
$ ./credit
Number: 4003-6000-0000-0014
Number: foo
Number: 4003600000000014
VISA
```

Але вам потрібно перевіряти введені дані на те, що вони не є номерами кредитних карток (наприклад, номером телефону), навіть якщо цілком числові:

```plaintext
$ ./credit
Number: 6176292929
INVALID
```

Спробуйте свою програму з великою кількістю введених даних, як дійсних, так і недійсних (ми також це зробимо!). Ось кілька [номерів карток](https://developer.paypal.com/api/nvp-soap/payflow/integration-guide/test-transactions/#standard-test-cards), рекомендованих PayPal для тестування.

Якщо ваша програма неправильно працює з деякими введеними даними (або зовсім не компілюється), прийшов час налагодження!

## Як протестувати свій код

Ви також можете виконати наступне, щоб перевірити правильність вашого коду за допомогою `check50`. Але не забудьте зібрати і протестувати його самостійно!

```plaintext
check50 cs50/problems/2023/x/credit
```

Виконайте наступне, щоб оцінити стиль вашого коду за допомогою `style50`.

```plaintext
style50 credit.c
```