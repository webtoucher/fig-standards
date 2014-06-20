Стандарты автозагрузки
======================

Ниже описаны обязательные требования, необходимые для совместимости с классами автозагрузки.

Обязательные условия
--------------------

* Полностью совместимые пространство имен и класс должны иметь следующую структуру
  `\<VendorName>\(<Namespace>\)*<ClassName>`
* Каждое пространство имен должно иметь пространство верхнего уровня («Наименование производителя»).
* Каждое пространство имен может иметь столько подпространств, сколько необходимо.
* Каждый разделитель пространства имен, конвертируется в `DIRECTORY_SEPARATOR` при загрузке из файловой системы.
* Каждый символ `_` в имени класса конвертируется в `DIRECTORY_SEPARATOR`. Символ `_` не имеет особого значения
  в пространстве имен.
* К полностью совместимому пространству имен и классу во время загрузки из файловой системы добавляется расширение
  `.php`.
* Буквы в наименование производителя, пространствах имен, классах могут быть любым сочетанием букв нижнего и верхнего
  регистра.

Примеры
-------

* `\Doctrine\Common\IsolatedClassLoader` => `/путь/к/проекту/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/путь/к/проекту/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/путь/к/проекту/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/путь/к/проекту/lib/vendor/Zend/Mail/Message.php`

Подчеркивание в названиях пространств имен и классов
----------------------------------------------------

* `\namespace\package\Class_Name` => `/путь/к/проекту/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/путь/к/проекту/lib/vendor/namespace/package_name/Class/Name.php`

Это минимальный набор правил для обеспечения совместимой автозагрузки классов в PHP.

Пример реализации
-----------------

Ниже представлена функция для демонстрации стандартов автозагрузки, представленных выше.

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

Реализация класса автозагрузки (SplClassLoader)
-----------------------------------------------

По ссылке пример простой реализации класса SplClassLoader, который следует вышеперечисленным стандартам. Этот способ
рекомендуется для загрузки классов PHP 5.3, которые выполнены в соответствии с требованиями стандартов.

* [http://gist.github.com/221634](http://gist.github.com/221634)
