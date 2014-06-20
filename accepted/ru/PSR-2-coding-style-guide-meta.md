PSR-2 Meta Document
===================

1. Общее
--------

Целью данного руководства является уменьшение недовольства во время чтения кода
другого автора. Этого удается достичь путем следования перечисленному общему
набору правил и рекомендаций по оформлению PHP кода.

Правила стилизации, приведенные здесь, выводятся из сходства между различными
проектами. Когда авторы разных проектов сотрудничают между собой, это помогает
иметь один набор руководящих принципов для использования во всех этих проектах.
Таким образом, преимущество этого руководства не в самих правилах, а в обмене
этими правилами.


2. Голоса
---------

- **Приём голосов:** [ML](https://groups.google.com/d/msg/php-fig/c-QVvnZdMQ0/TdDMdzKFpdIJ)


3. Опечатки
-----------

### 3.1 - Многострочные аргументы (09/08/2013)

Using one or more multi-line arguments (i.e: arrays or anonymous functions) does not constitute 
splitting the argument list itself, therefore Section 4.6 is not automatically enforced. Arrays and anonymous 
functions are able to span multiple lines.

The following examples are perfectly valid in PSR-2:

```php
<?php
somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) { 
    return 'Hello '.$app->escape($name); 
});
```

### 3.2 - Многострочные аргументы (10/17/2013)

When extending multiple interfaces, the list of `extends` should be treated the same as a list
of `implements`, as declared in Section 4.1.

