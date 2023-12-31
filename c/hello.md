# Hello

Згадайте, що Visual Studio Code (також відомий як VS Code) є популярним "інтегрованим середовищем розробки" (IDE), через яке ви можете писати код. Щоб вам не потрібно було завантажувати, встановлювати та налаштовувати свою власну копію VS Code, ми замість цього використовуватимемо його хмарну версію, в якій все, що вам потрібно, вже попередньо встановлено.

Увійдіть у [cs50.dev](https://cs50.dev/) за допомогою свого облікового запису GitHub. Після завантаження вашого "codespace" ви повинні побачити, що за замовчуванням VS Code розділений на три області. У верхній частині VS Code знаходиться ваш "текстовий редактор", де ви будете писати всі свої програми. У нижній частині знаходиться "термінальне вікно", інтерфейс командного рядка (CLI), який дозволяє компілювати код та запускати програми. Зліва є "провідник файлів".

Почніть, натиснувши всередині вашого термінального вікна, ви повинні побачити, що ваш "курсор" виглядає так:

```plaintext
$
```

Клацніть всередині цього термінального вікна, а потім введіть:

```plaintext
mkdir hello
```

і натисніть Enter, щоб створити папку з назвою `hello` у вашому codespace. При цьому не допускайте помилок, наприклад, пропуск пробілу між `mkdir` та `hello` чи будь-яких інших символів!

Відтепер, виконання команди (тобто запуск) означає, що ви набираєте її в термінальне вікно, а потім натискаєте Enter. Команди реагують на "регістр", тому переконайтеся, що не вводите заголовні літери, коли маєте на увазі малі, і навпаки.

Тепер виконайте:

```plaintext
cd hello
```

щоб перейти в цю папку. Ваш курсор тепер повинен виглядати наступним чином:

```plaintext
hello/ $
```

Якщо цього не сталося, поверніться назад і спробуйте з'ясувати, де ви помилилися!

Чи не час спробувати написати свою першу програму? Виконайте:

```plaintext
code hello.c
```

щоб створити новий файл з назвою `hello.c`, який автоматично відкриється у текстовому редакторі вашого codespace. Як тільки ви збережете файл за допомогою "Command + S" (на macOS) або "Ctrl + S" (на Windows), він також з'явиться у провіднику вашого codespace.

Продовжуйте, додавши свою першу програму, точно вписавши ці рядки у `hello.c`:

```c
#include <stdio.h>

int main(void)
{
    printf("hello, world\n");
}
```

Зверніть увагу, як VS Code додає "синтаксичне виділення" (тобто кольорову підсвітку) під час набору коду. Хоча вибір кольорів VS Code може відрізнятися від кольорів цієї задачі, вони фактично не зберігаються у файлі; вони додаються VS Code, щоб виділити певний синтаксис. Якби ви не зберегли файл з назвою `hello.c` відразу з початку, VS Code не знав би (за розширенням імені файлу), що ви пишете код на мові C, і тоді ці кольори були б відсутніми.

## Список файлів

Далі, у вашому термінальному вікні, якраз праворуч від запиту (`hello/ $`), виконайте:

```plaintext
ls
```

Ви повинні побачити лише `hello.c`? Це тому, що ви щойно перелічили файли у вашому каталозі `hello`. Зокрема, ви виконали команду під назвою `ls`, яка є скороченням від "list". (Це настільки часто використовувана команда, що її автори назвали її просто `ls`, щоб економити час.)

## Компіляція програм

Тепер, перш ніж ви можете виконати програму `hello.c`, згадайте, що ви повинні спочатку *скомпілювати* її за допомогою *компілятора*, перекладаючи її з *вихідного коду* у *машинний код* (тобто нулі та одиниці). Виконайте наведену нижче команду, щоб зробити це:

```plaintext
make hello
```

А потім виконайте ще раз цю команду:

```plaintext
ls
```

На цей раз ви повинні побачити не тільки `hello.c`, але також `hello` у списку. Ви щойно переклали вихідний код з `hello.c` у машинний код у `hello`.

Тепер виконайте саму програму, виконавши наведене нижче:

```plaintext
./hello
```

## Завдання

### Отримання введення користувача

Незалежно від того, як ви компілюєте або виконуєте цю програму, вона завжди виводить лише `hello, world`. Давайте зробимо її більш особистою, так само, як ми робили на заняттях.

Змініть цю програму таким чином, щоб спочатку вона просила користувача ввести своє ім'я, а потім виводила `hello, такий-то`, де `такий-то` - це їхнє справжнє ім'я.

Як і раніше, переконайтеся, що компілюєте свою програму за допомогою:

```plaintext
make hello
```

І переконайтеся, що ви виконуєте свою програму, перевіряючи її кілька разів з різними вхідними даними:

```plaintext
./hello
```

## Підказки

### Не пам'ятаєте, як просити користувача ввести своє ім'я?

Пам'ятайте, що ви можете використовувати `get_string` таким чином, зберігаючи її значення у змінну з назвою `name` типу `string`.

```c
string name = get_string("What's your name? ");
```

### Не пам'ятаєте, як форматувати рядок?

Не пам'ятаєте, як об'єднати (тобто з'єднати) ім'я користувача з привітанням? Пам'ятайте, що ви можете використовувати `printf` не тільки для друку, але і для форматування рядка (літера `f` у `printf`), на приклад:

```c
printf("hello, %s\n", name);
```

### Use of undeclared identifier?

Бачите таке повідомлення про помилку?:

```plaintext
error: use of undeclared identifier 'string'; did you mean 'stdin'?
```

Пам'ятайте, що для використання `get_string` вам потрібно включити `cs50.h` (в якому визначено `get_string`) на початку файлу, наприклад:

```c
#include <cs50.h>
```

## Як перевірити свій код?

Виконайте нижченаведене, щоб перевірити правильність вашого коду за допомогою `check50`, командної програми, яка виводить усміхнені обличчя, коли ваш код успішно проходить автоматизовані тести CS50, і сумні обличчя, коли це не вдається! Але не забудьте також скомпілювати та перевірити свій код самостійно!

```plaintext
check50 cs50/problems/2023/x/hello
```
