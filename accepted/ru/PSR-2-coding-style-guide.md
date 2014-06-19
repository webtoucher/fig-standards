Стандарты оформления кода
=========================

Это руководство наследует и расширяет [PSR-1], основной стандарт написания кода.

Целью данного руководства является уменьшение недовольства во время чтения кода
другого автора. Этого удается достичь путем следования перечисленному общему
набору правил и рекомендаций по оформлению PHP кода.

Правила стилизации, приведенные здесь, выводятся из сходства между различными
проектами. Когда авторы разных проектов сотрудничают между собой, это помогает
иметь один набор руководящих принципов для использования во всех этих проектах.
Таким образом, преимущество этого руководства не в самих правилах, а в обмене
этими правилами.

Ключевые слова "НЕОБХОДИМО", "НЕДОПУСТИМО", "ТРЕБУЕТСЯ", "НУЖНО",
"НЕ ПОЗВОЛЯЕТСЯ", "СЛЕДУЕТ", "НЕ СЛЕДУЕТ", "РЕКОМЕНДУЕТСЯ", "ВОЗМОЖНО",
и "НЕОБЯЗАТЕЛЬНЫЙ" в этом документе СЛЕДУЕТ интерпретировать в соответствии
с [RFC 2119].

[RFC 2119]: http://rfc2.ru/2119.rfc/print
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/ru/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/ru/PSR-1-basic-coding-standard.md


1. Обзор
--------

- НЕОБХОДИМО следовать основным стандартам написания кода PSR [[PSR-1]].

- В коде НЕОБХОДИМО использовать 4 пробела для отступа, а не символы табуляции.

- НЕДОПУСТИМО жесткое ограничение на длину строки; мягкое ограничение на длину строки — 120
  символов; однако СЛЕДУЕТ не выходить за рамки 80 символов на строку.

- НЕОБХОДИМО оставлять одну пустую строку после объявления `namespace`, и
  НЕОБХОДИМО оставлять одну пустую строку после объявления блока `use`.

- Открывающую фигурную скобку при описании классов НЕОБХОДИМО рахмещать на следующей строке, а закрывающую — 
  на следующей строке после тела класса.

- Открывающую фигурную скобку при описании методов НЕОБХОДИМО рахмещать на следующей строке, а закрывающую — 
  на следующей строке после тела метода.

- Область видимости НЕОБХОДИМО объявлять для всех свойств и методов; `abstract` and
  `final` НЕОБХОДИМО объявлять перед областью видимости; `static` НЕОБХОДИМО объявлять после области видимости.
  
- После ключевых слов управляющих структур НЕОБХОДИМО добавлять один пробел; после методов и функций — НЕДОПУСТИМО.

- Открывающую фигурную скобку для управляющих структур НЕОБХОДИМО рахмещать на той же строке, а закрывающую — 
  на следующей строке после тела управляющей структуры.

- После открывающей круглой скобки для управляющих структур НЕДОПУСТИМО ставить пробел,
  и так же НЕДОПУСТИМО ставить пробел перед закрывающей круглой скобкой.

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

НЕОБХОДИМО выставить мягкие ограничения на длину строки — 120 символов; автоматическую проверку стиля
НЕОБХОДИМО настроить так, чтобы она предупреждала о пересечении мягкого предела, но НЕДОПУСТИМО считать это ошибкой.

НЕ СЛЕДУЕТ писать строки длинее 80 символов; строки длинее СЛЕДУЕТ разбить на несколько строк,
не более 80 символов каждая.

НЕДОПУСТИМО оставлять пробелы в конце непустых строк.

Пустые строки ВОЗМОЖНО добавить для улучшения читабельности кода и для определения взаимосвязанных блоков кода.

НЕДОПУСТИМО размещать более одного оператора в одной строке.

### 2.4. Отступы

В коде НЕОБХОДИМО использовать 4 пробела, и НЕДОПУСТИМО использовать символы табуляции для отступов.

> Использование только пробелов, и не смешивание пробелов с табами, помогает
> избежать проблем с различиями, патчами, историей и аннотациями VCS.
> Использование пробелов также позволяет легко вставить мелкозернистый суботступ
> для межстрочного выравнивания.

### 2.5. Ключевые слова и true/false/null

[Ключевые слова] PHP НЕОБХОДИМО записывать в нижнем регистре.

Константы PHP `true`, `false`, и `null` НЕОБХОДИМО записывать в нижнем регистре.

[Ключевые слова]: http://php.net/manual/ru/reserved.keywords.php



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

Открывающую фигурную скобку при описании классов НЕОБХОДИМО рахмещать на отдельной строке;
а закрывающую — на следующей строке после тела класса.

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

Список `implements` ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка
записывается с одним отступом. При этом первый элемент списка НЕОБХОДИМО размещать на новой
строке, и НЕОБХОДИМО записывать не более одного интерфейса на строку.

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
рахмещать на отдельной строке; а закрывающую — на следующей строке после тела метода.
После открывающей круглой скобки НЕДОПУСТИМО ставить пробел, и так же НЕДОПУСТИМО ставить пробел перед
закрывающей круглой скобкой.

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

Список аргументов ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка
записывается с одним отступом. При этом первый элемент списка НЕОБХОДИМО размещать на новой
строке, и НЕОБХОДИМО записывать не более одного аргумента на строку.

Когда список аргументов разделен на несколько строк, закрывающую круглую скобку и открывающую
фигурную скобку НЕОБХОДИМО размещать вместе на отдельной строке с одним пробелом между ними.

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

Когда происходит вызов метода или функции, между названием функции или метода
и открывающей круглой скобкой НЕДОПУСТИМО ставить пробел. Так же НЕДОПУСТИМО
ставить пробелы после открывающей круглой скобки и перед закрывающей круглой скобкой.
В списке аргументов НЕДОПУСТИМО ставить пробелы перед запятой, и НЕОБХОДИМО ставить
один пробел после каждой запятой.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Список аргументов ВОЗМОЖНО разделить на несколько строк, в таком случае, каждая строка
записывается с одним отступом. При этом первый элемент списка НЕОБХОДИМО размещать на новой
строке, и НЕОБХОДИМО записывать не более одного аргумента на строку.

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

Тело каждой структуры НЕОБХОДИМО заключать в фигурные скобки. Это стандартизирует вид
структур, а так-же уменьшает вероятность получения ошибок при добавление новых строк к телу.


### 5.1. `if`, `elseif`, `else`

Управляющая структура `if` должна выглядеть, так, как показано. Обратите внимание
на размещение круглых скобок, пробелов и фигурных скобок; так-же обратите внимание,
что `else` и `elseif` находятся на той же линии, что закрывающая фигурная скобка предыдущего тела.

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

Ключевое слово `elseif` СЛЕДУЕТ использовать вместо `else if` так чтобы все ключевые слова
выглядели, как отдельные слова.


### 5.2. `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement НЕОБХОДИМО be indented once
from `switch`, and the `break` keyword (or other terminating keyword) НЕОБХОДИМО be
indented at the same level as the `case` body. There НЕОБХОДИМО be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
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

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
while ($expr) {
    // structure body
}
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`
    
A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

### 5.6. `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

6. Closures
-----------

Closures НЕОБХОДИМО be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace НЕОБХОДИМО go on the same line, and the closing brace НЕОБХОДИМО go on
the next line following the body.

There НЕДОПУСТИМО be a space after the opening parenthesis of the argument list
or variable list, and there НЕДОПУСТИМО be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there НЕДОПУСТИМО be a space before each
comma, and there НЕОБХОДИМО be one space after each comma.

Closure arguments with default values НЕОБХОДИМО go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

Argument lists and variable lists ВОЗМОЖНО be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list НЕОБХОДИМО be on the next line, and there НЕОБХОДИМО be only one argument or variable
per line.

When the ending list (whether or arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace НЕОБХОДИМО be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
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
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


7. Conclusion
--------------

There are many elements of style and practice intentionally omitted by this
guide. These include but are not limited to:

- Declaration of global variables and global constants

- Declaration of functions

- Operators and assignment

- Inter-line alignment

- Comments and documentation blocks

- Class name prefixes and suffixes

- Best practices

Future recommendations ВОЗМОЖНО revise and extend this guide to address those or
other elements of style and practice.


Appendix A. Survey
------------------

In writing this style guide, the group took a survey of member projects to
determine common practices.  The survey is retained herein for posterity.

### A.1. Survey Data

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

### A.2. Survey Legend

`indent_type`:
The type of indenting. `tab` = "Use a tab", `2` or `4` = "number of spaces"

`line_length_limit_soft`:
The "soft" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`line_length_limit_hard`:
The "hard" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`class_names`:
How classes are named. `lower` = lowercase only, `lower_under` = lowercase with underscore separators, `studly` = StudlyCase.

`class_brace_line`:
Does the opening brace for a class go on the `same` line as the class keyword, or on the `next` line after it?

`constant_names`:
How are class constants named? `upper` = Uppercase with underscore separators.

`true_false_null`:
Are the `true`, `false`, and `null` keywords spelled as all `lower` case, or all `upper` case?

`method_names`:
How are methods named? `camel` = `camelCase`, `lower_under` = lowercase with underscore separators.

`method_brace_line`:
Does the opening brace for a method go on the `same` line as the method name, or on the `next` line?

`control_brace_line`:
Does the opening brace for a control structure go on the `same` line, or on the `next` line?

`control_space_after`:
Is there a space after the control structure keyword?

`always_use_control_braces`:
Do control structures always use braces?

`else_elseif_line`:
When using `else` or `elseif`, does it go on the `same` line as the previous closing brace, or does it go on the `next` line?

`case_break_indent_from_switch`:
How many times are `case` and `break` indented from an opening `switch` statement?

`function_space_after`:
Do function calls have a space after the function name and before the opening parenthesis?

`closing_php_tag_required`:
In files containing only PHP, is the closing `?>` tag required?

`line_endings`:
What type of line ending is used?

`static_or_visibility_first`:
When declaring a method, does `static` come first, or does the visibility come first?

`control_space_parens`:
In a control structure expression, is there a space after the opening parenthesis and a space before the closing parenthesis? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Is there a blank line after the opening PHP tag?

`class_method_control_brace`:
A summary of what line the opening braces go on for classes, methods, and control structures.

### A.3. Survey Results

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
