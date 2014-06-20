Стандарты оформления кода
=========================

Это руководство наследует и расширяет [PSR-1], основной стандарт написания кода.

Целью данного руководства является уменьшение недовольства во время чтения кода другого автора. Этого удается достичь
путем следования перечисленному общему набору правил и рекомендаций по оформлению PHP кода.

Правила стилизации, приведенные здесь, выводятся из сходства между различными проектами. Когда авторы разных проектов
сотрудничают между собой, это помогает иметь один набор руководящих принципов для использования во всех этих проектах.
Таким образом, преимущество этого руководства не в самих правилах, а в обмене этими правилами.

Ключевые слова "НЕОБХОДИМО", "НЕДОПУСТИМО", "ТРЕБУЕТСЯ", "НУЖНО", "НЕ ПОЗВОЛЯЕТСЯ", "СЛЕДУЕТ", "НЕ СЛЕДУЕТ",
"РЕКОМЕНДУЕТСЯ", "ВОЗМОЖНО" и "НЕОБЯЗАТЕЛЬНЫЙ" в этом документе СЛЕДУЕТ интерпретировать в соответствии с [RFC 2119].


1. Обзор
--------

- НЕОБХОДИМО следовать основным стандартам написания кода [PSR-1].

- В коде НЕОБХОДИМО использовать 4 пробела для отступа, а не символы табуляции.

- НЕДОПУСТИМО жесткое ограничение на длину строки; мягкое ограничение на длину строки — 120 символов; однако СЛЕДУЕТ
  не выходить за рамки 80 символов на строку.

- НЕОБХОДИМО оставлять одну пустую строку после объявления `namespace`, и одну пустую строку после объявления блока
  `use`.

- Открывающую фигурную скобку при описании классов НЕОБХОДИМО рахмещать на следующей строке, а закрывающую — 
  на следующей строке после тела класса.

- Открывающую фигурную скобку при описании методов НЕОБХОДИМО рахмещать на следующей строке, а закрывающую — 
  на следующей строке после тела метода.

- Область видимости НЕОБХОДИМО объявлять для всех свойств и методов; `abstract` and `final` НЕОБХОДИМО объявлять перед
  областью видимости; `static` НЕОБХОДИМО объявлять после области видимости.
  
- После ключевых слов управляющих структур НЕОБХОДИМО добавлять один пробел; после методов и функций — это НЕДОПУСТИМО.

- Открывающую фигурную скобку для управляющих структур НЕОБХОДИМО рахмещать на той же строке, а закрывающую — 
  на следующей строке после тела управляющей структуры.

- После открывающей круглой скобки для управляющих структур НЕДОПУСТИМО ставить пробел, и так же НЕДОПУСТИМО ставить
  пробел перед закрывающей круглой скобкой.

### 1.1. Пример

Следующий код представляет собой краткий пример верного следования правилам:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // тело метода
    }
}
```

2. Общее
--------

### 2.1 Основной стандарт написания кода

При написании кода НЕОБХОДИМО следовать всем правилам, указанным в [PSR-1].

### 2.2 Файлы

Во всех PHP файлах НЕОБХОДИМО использовать Unix LF (перевод строки) для указания завершения строки.

Все PHP файлы НЕОБХОДИМО заканчивать одной пустой строкой.

Закрывающий тег `?>` НЕОБХОДИМО исключить из всех файлов, содержащих только PHP.

### 2.3. Строки

НЕДОПУСТИМО жесткое ограничение на длину строки.

НЕОБХОДИМО выставить мягкие ограничения на длину строки — 120 символов; автоматическую проверку стиля НЕОБХОДИМО
настроить так, чтобы она предупреждала о пересечении мягкого предела, однако НЕДОПУСТИМО считать это ошибкой.

НЕ СЛЕДУЕТ писать строки длинее 80 символов; строки длинее СЛЕДУЕТ разбить на несколько строк, не более 80 символов
каждая.

НЕДОПУСТИМО оставлять пробелы в конце непустых строк.

Пустые строки ВОЗМОЖНО добавить для улучшения читабельности кода и для определения взаимосвязанных блоков кода.

НЕДОПУСТИМО размещать более одного оператора в одной строке.

### 2.4. Отступы

В коде НЕОБХОДИМО использовать 4 пробела, и НЕДОПУСТИМО использовать символы табуляции для отступов.

> Использование только пробелов, и не смешивание пробелов с табами, помогает избежать проблем с различиями, патчами,
> историей и аннотациями VCS. Использование пробелов также позволяет легко вставить мелкозернистый суботступ
> для межстрочного выравнивания.

### 2.5. Ключевые слова и true/false/null

[Ключевые слова] PHP НЕОБХОДИМО записывать в нижнем регистре.

Константы PHP `true`, `false`, и `null` НЕОБХОДИМО записывать в нижнем регистре.


3. Объявление пространств имен и блока Use
------------------------------------------

Если используется пространство имен, НЕОБХОДИМО оставить одну пустую строку после объявления `namespace`.

Если используется блок `use`, объявлять его НЕОБХОДИМО после объявления `namespace`.

НЕОБХОДИМО использовать одно ключевое слово `use` на каждое объявление.

НЕОБХОДИМО оставить одну пустую строку после блока `use`.

Например:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... дополнительный PHP код ...

```


4. Классы, свойства и методы
----------------------------

Термин «класс» относится ко всем классам, интерфейсам и трейтам.

### 4.1. Наследование и реализация

Ключевые слова `extends` и `implements` НЕОБХОДИМО объявлять на той же строке, что и класс.

Открывающую фигурную скобку при описании классов НЕОБХОДИМО рахмещать на отдельной строке; а закрывающую — на следующей
строке после тела класса.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // константы, свойства, методы
}
```

Список `implements` ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка записывается с одним отступом.
При этом первый элемент списка НЕОБХОДИМО размещать на новой строке, и НЕОБХОДИМО записывать не более одного интерфейса
на строку.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // константы, свойства, методы
}
```

### 4.2. Свойства

Область видимости НЕОБХОДИМО объявлять для всех свойств.

НЕДОПУСТИМО использовать ключевое слово `var` для объявления свойства.

НЕДОПУСТИМО объявление более одного свойства за выражение.

НЕ СЛЕДУЕТ начинать имя свойства с символа нижнего подчёркивания для защищенной или приватной области видимости.

Объявление свойств должно выглядеть, как в примере:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

### 4.3. Методы

Область видимости НЕОБХОДИМО объявлять для всех методов.

НЕ СЛЕДУЕТ начинать имя метода с символа нижнего подчёркивания для защищенной или приватной области видимости.

НЕДОПУСТИМО ставить пробел после названия метода. Открывающую фигурную скобку при описании методов НЕОБХОДИМО
рахмещать на отдельной строке, а закрывающую — на следующей строке после тела метода. После открывающей круглой скобки
НЕДОПУСТИМО ставить пробел, и так же НЕДОПУСТИМО ставить пробел перед закрывающей круглой скобкой.

Объявление методов должно выглядеть, как в примере. Обратите внимание на расположение скобок, запятых и пробелов:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // тело метода
    }
}
```    

### 4.4. Аргументы методов

В списке аргументов НЕДОПУСТИМО ставить пробелы перед запятой, и НЕОБХОДИМО ставить один пробел после каждой запятой.

Аргументы методов со значениями по умолчанию НЕОБХОДИМО размещать в конце списка.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // тело метода
    }
}
```

Список аргументов ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка записывается с одним отступом.
При этом первый элемент списка НЕОБХОДИМО размещать на новой строке, и НЕОБХОДИМО записывать не более одного аргумента
на строку.

Когда список аргументов разделен на несколько строк, закрывающую круглую скобку и открывающую фигурную скобку НЕОБХОДИМО
размещать вместе на отдельной строке с одним пробелом между ними.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // тело метода
    }
}
```

### 4.5. `abstract`, `final`, и `static`

Если присутствует объявление `abstract` или `final`, их НЕОБХОДИМО размещать перед объявлением области видимости.

Если присутствует объявление `static`, его НЕОБХОДИМО размещать после объявлением области видимости.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // тело метода
    }
}
```

### 4.6. Вызов метода или функции

Когда происходит вызов метода или функции, между названием функции или метода и открывающей круглой скобкой НЕДОПУСТИМО
ставить пробел. Так же НЕДОПУСТИМО ставить пробелы после открывающей круглой скобки и перед закрывающей круглой скобкой.
В списке аргументов НЕДОПУСТИМО ставить пробелы перед запятой, и НЕОБХОДИМО ставить один пробел после каждой запятой.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Список аргументов ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка записывается с одним отступом.
При этом первый элемент списка НЕОБХОДИМО размещать на новой строке, и НЕОБХОДИМО записывать не более одного аргумента
на строку.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

5. Управляющие Структуры
------------------------

Глвавные правила стиля для управляющих структур следующие:

- НЕОБХОДИМО ставить один пробел после ключевого слова управляющих структур
- НЕДОПУСТИМО ставить пробелы после открывающей круглой скобки
- НЕДОПУСТИМО ставить пробелы перед закрывающей круглой скобкой
- НЕОБХОДИМО ставить один пробел между закрывающей круглой и открывающей фигурной скобками
- Тело структуры НЕОБХОДИМО выделять одним отступом
- Закрывающую фигурную скобку НЕОБХОДИМО ставить на следующей строке после тела структуры

Тело каждой структуры НЕОБХОДИМО заключать в фигурные скобки. Это стандартизирует вид структур, а так-же уменьшает
вероятность получения ошибок при добавление новых строк к телу.


### 5.1. `if`, `elseif`, `else`

Управляющая структура `if` должна выглядеть, так, как показано. Обратите внимание на размещение круглых скобок, пробелов
и фигурных скобок; так-же обратите внимание, что `else` и `elseif` находятся на той же линии, что закрывающая фигурная
скобка предыдущего тела:

```php
<?php
if ($expr1) {
    // тело if
} elseif ($expr2) {
    // тело elseif
} else {
    // тело else;
}
```

Ключевое слово `elseif` СЛЕДУЕТ использовать вместо `else if` так чтобы не было ключевых слов, состоящих более, чем
из одного слова.


### 5.2. `switch`, `case`

Управляющая структура `switch` должна выглядеть так, как показано ниже. Обратите внимание на расположение круглых
скобок, пробелов и фигурных скобок. Для выражений `case` НЕОБХОДИМО делать один отступ от `switch`. Ключевое слово
`break` (как и любое другие прерывающее ключевое слово) НЕОБХОДИМО размещать на том же уровне, что и тело `case`.
НЕОБХОДИМО добавлять коментарий в тело непустых выражений `case` если они не имеют прерывающих ключевых слов,
например `// нет остановки`.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // нет остановки
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


### 5.3. `while`, `do while`

Выражение `while` должно выглядеть, как показано ниже. Обратите внимание на расположение скобок и пробелов:

```php
<?php
while ($expr) {
    // тело структуры
}
```

Выражение `do while` должно выглядеть, как показано ниже. Обратите внимание на расположение скобок и пробелов:

```php
<?php
do {
    // тело структуры
} while ($expr);
```

### 5.4. `for`

Выражение `for` должно выглядеть, как показано ниже. Обратите внимание на расположение скобок и пробелов:

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // тело for
}
```

### 5.5. `foreach`
    
Выражение `foreach` должно выглядеть, как показано ниже. Обратите внимание на расположение скобок и пробелов:

```php
<?php
foreach ($iterable as $key => $value) {
    // тело foreach
}
```

### 5.6. `try`, `catch`

Блок `try catch` должен выглядеть, как показано ниже. Обратите внимание на расположение скобок и пробелов:

```php
<?php
try {
    // тело try
} catch (FirstExceptionType $e) {
    // тело catch
} catch (OtherExceptionType $e) {
    // тело catch
}
```

6. Замыкания
------------

Замыкания НЕОБХОДИМО объявлять с одним пробелом после ключевого слова `function`, а так-же с пробелом до и после
ключевого слова `use`.

Открывающую фигурную скобку НЕОБХОДИМО рахмещать на следующей строке, а закрывающую — на следующей строке после тела
замыкания.

После открывающей круглой списка аргументов или списка переменных скобки НЕДОПУСТИМО ставить пробел, и так же
НЕДОПУСТИМО ставить пробел перед закрывающей круглой скобкой.

В списке аргументов и списке переменных НЕДОПУСТИМО ставить пробелы перед запятыми, и НЕОБХОДИМО ставить один пробел
после каждой запятой.

Аргументы замыкания со значениями по умолчанию НЕОБХОДИМО размещать в конце списка аргументов.

Объявление замыкания должно выглядеть, как показано ниже. Обратите внимание на расположение скобок, запятых и пробелов:

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // тело замыкания
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // тело замыкания
};
```

Список аргументов и переменных ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка записывается с одним
отступом. При этом первый элемент списка НЕОБХОДИМО размещать на новой строке, и НЕОБХОДИМО записывать не более одного
аргумента или переменной на строку.

Когда конец списка (в независимости от того аргументы это, или переменные) разделен на несколько строк, закрывающую
круглую скобу и открывающую фигурную НЕОБХОДИМО расположить вместе на отдельной линии с одним пробелом между ними.

иже приведены примеры замыканий со списком аргументов и без него, а так-же с разделением списка переменных на несколько
строк.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
    // тело замыкания
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // тело замыкания
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // тело замыкания
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
    // тело замыкания
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // тело замыкания
};
```

Обратите внимание, что правила форматирования также сохраняются, когда замыкания используются непосредственно в вызове
функции или метода в качестве аргумента.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // тело замыкания
    },
    $arg3
);
```


7. Вывод
--------

Есть очень много элементов стиля и практики, которые намеренно опущены в этом руководстве. Они включают, но не
ограничиваются:

- Объявление глобальных переменных и констант

- Объявление функций

- Операторы и присваивание

- Выравнивание

- Комментарии и документация блоков

- Преффиксы и суффиксы названий классов

- Лучшие практики

ВОЗМОЖНО в будущем руководство будет пересмотрено или расширено для решения тех или иных элементов стиля и практики.


Appendix A. Survey
------------------

При написании этого руководства, группа провела опрос представителей проектов чтобы определить общие практики.
Результаты сохраним здесь для потомков.

### A.1. Данные опроса

    url,http://www.horde.org/apps/horde/docs/CODING_STANDARDS,http://pear.php.net/manual/en/standards.php,http://solarphp.com/manual/appendix-standards.style,http://framework.zend.com/manual/en/coding-standard.html,http://symfony.com/doc/2.0/contributing/code/standards.html,http://www.ppi.io/docs/coding-standards.html,https://github.com/ezsystems/ezp-next/wiki/codingstandards,http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html,https://github.com/UnionOfRAD/lithium/wiki/Spec%3A-Coding,http://drupal.org/coding-standards,http://code.google.com/p/sabredav/,http://area51.phpbb.com/docs/31x/coding-guidelines.html,https://docs.google.com/a/zikula.org/document/edit?authkey=CPCU0Us&hgd=1&id=1fcqb93Sn-hR9c0mkN6m_tyWnmEvoswKBtSc0tKkZmJA,http://www.chisimba.com,n/a,https://github.com/Respect/project-info/blob/master/coding-standards-sample.php,n/a,Object Calisthenics for PHP,http://doc.nette.org/en/coding-standard,http://flow3.typo3.org,https://github.com/propelorm/Propel2/wiki/Coding-Standards,http://developer.joomla.org/coding-standards.html
    voting,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,no,no,no,?,yes,no,yes
    indent_type,4,4,4,4,4,tab,4,tab,tab,2,4,tab,4,4,4,4,4,4,tab,tab,4,tab
    line_length_limit_soft,75,75,75,75,no,85,120,120,80,80,80,no,100,80,80,?,?,120,80,120,no,150
    line_length_limit_hard,85,85,85,85,no,no,no,no,100,?,no,no,no,100,100,?,120,120,no,no,no,no
    class_names,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,lower_under,studly,lower,studly,studly,studly,studly,?,studly,studly,studly
    class_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,next,next,next,next,next,next,same,next,next
    constant_names,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper
    true_false_null,lower,lower,lower,lower,lower,lower,lower,lower,lower,upper,lower,lower,lower,upper,lower,lower,lower,lower,lower,upper,lower,lower
    method_names,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,lower_under,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel
    method_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,same,next,next,next,next,next,same,next,next
    control_brace_line,same,same,same,same,same,same,next,same,same,same,same,next,same,same,next,same,same,same,same,same,same,next
    control_space_after,yes,yes,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes
    always_use_control_braces,yes,yes,yes,yes,yes,yes,no,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes
    else_elseif_line,same,same,same,same,same,same,next,same,same,next,same,next,same,next,next,same,same,same,same,same,same,next
    case_break_indent_from_switch,0/1,0/1,0/1,1/2,1/2,1/2,1/2,1/1,1/1,1/2,1/2,1/1,1/2,1/2,1/2,1/2,1/2,1/2,0/1,1/1,1/2,1/2
    function_space_after,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no
    closing_php_tag_required,no,no,no,no,no,no,no,no,yes,no,no,no,no,yes,no,no,no,no,no,yes,no,no
    line_endings,LF,LF,LF,LF,LF,LF,LF,LF,?,LF,?,LF,LF,LF,LF,?,,LF,?,LF,LF,LF
    static_or_visibility_first,static,?,static,either,either,either,visibility,visibility,visibility,either,static,either,?,visibility,?,?,either,either,visibility,visibility,static,?
    control_space_parens,no,no,no,no,no,no,yes,no,no,no,no,no,no,yes,?,no,no,no,no,no,no,no
    blank_line_after_php,no,no,no,no,yes,no,no,no,no,yes,yes,no,no,yes,?,yes,yes,no,yes,no,yes,no
    class_method_control_brace,next/next/same,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/next,same/same/same,same/same/same,same/same/same,same/same/same,next/next/next,next/next/same,next/same/same,next/next/next,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/same,next/next/next

### A.2. Расшифровка опроса

`indent_type`:
Тип отступа. `tab` = "символ табуляции", `2` или `4` = "число пробелов"

`line_length_limit_soft`:
Мягкие ограничения на длину строки, в символах. `?` = воздержались от ответа, `no` — без ограничений.

`line_length_limit_hard`:
Жесткие ограничения на длину строки, в символах. `?` = воздержались от ответа, `no` — без ограничений.

`class_names`:
Как именовать классы? `lower` = только в нижнем регистре, `lower_under` = в нижнем регистре с символами нижнего
подчёркивания для разделения слов, `studly` = StudlyCase.

`class_brace_line`:
Размещение открывающей фигурной скобки для классов. `same` — на той же строке, `next` — на следующей.

`constant_names`:
Как именовать константы? `upper` = в верхнем регистре с символами нижнего подчёркивания для разделения слов.

`true_false_null`:
Константы `true`, `false` и `null`. `lower` — в нижнем регистре, `upper` — в верхнем?

`method_names`:
Как именовать методы? `camel` = `camelCase`, `lower_under` = в нижнем регистре с символами нижнего подчёркивания для
разделения слов.

`method_brace_line`:
Размещение открывающей фигурной скобки для методов. `same` — на той же строке, `next` — на следующей.

`control_brace_line`:
Размещение открывающей фигурной скобки для управляющих структур. `same` — на той же строке, `next` — на следующей.

`control_space_after`:
Нужно ли ставить пробел после ключевого слово управляющей структуры?

`always_use_control_braces`:
Всегда ли управляющие структуры должны использовать фигурные скобки?

`else_elseif_line`:
Как записывать структуры `else` и `elseif`? `same` — на той же строке, что и закрывающая фигурная скобка, `next` — на
следующей строке.

`case_break_indent_from_switch`:
Сколько отступов от `switch` делать для `case` и `break`?

`function_space_after`:
Ставить ли пробел после имени функции и перед открывающей круглой скобкой?

`closing_php_tag_required`:
Ставить ли в файлах, содержащих только PHP, закрывающий тег `?>`?

`line_endings`:
Какой тип окончания строки использовать?

`static_or_visibility_first`:
Что следует первым при определении метода — `static` или область видимости?

`control_space_parens`:
Ставить ли внутренние пробелы для круглых скобок управляющих конструкций? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Оставлять ли пустую строку после открывающего тега PHP?

`class_method_control_brace`:
На какой строке ставить открывающую фигурную скобку для классов, методов и управляющих структур?

### A.3. Результаты опроса

    indent_type:
        tab: 7
        2: 1
        4: 14
    line_length_limit_soft:
        ?: 2
        no: 3
        75: 4
        80: 6
        85: 1
        100: 1
        120: 4
        150: 1
    line_length_limit_hard:
        ?: 2
        no: 11
        85: 4
        100: 3
        120: 2
    class_names:
        ?: 1
        lower: 1
        lower_under: 1
        studly: 19
    class_brace_line:
        next: 16
        same: 6
    constant_names:
        upper: 22
    true_false_null:
        lower: 19
        upper: 3
    method_names:
        camel: 21
        lower_under: 1
    method_brace_line:
        next: 15
        same: 7
    control_brace_line:
        next: 4
        same: 18
    control_space_after:
        no: 2
        yes: 20
    always_use_control_braces:
        no: 3
        yes: 19
    else_elseif_line:
        next: 6
        same: 16
    case_break_indent_from_switch:
        0/1: 4
        1/1: 4
        1/2: 14
    function_space_after:
        no: 22
    closing_php_tag_required:
        no: 19
        yes: 3
    line_endings:
        ?: 5
        LF: 17
    static_or_visibility_first:
        ?: 5
        either: 7
        static: 4
        visibility: 6
    control_space_parens:
        ?: 1
        no: 19
        yes: 2
    blank_line_after_php:
        ?: 1
        no: 13
        yes: 8
    class_method_control_brace:
        next/next/next: 4
        next/next/same: 11
        next/same/same: 1
        same/same/same: 6

[RFC 2119]: http://rfc2.ru/2119.rfc/print
[PSR-0]: PSR-0.md
[PSR-1]: PSR-1-basic-coding-standard.md
[Ключевые слова]: http://php.net/manual/ru/reserved.keywords.php
