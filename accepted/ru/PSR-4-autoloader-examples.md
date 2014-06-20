Пример реализации PSR-4
=======================

Ниже приведены примеры, которые иллюстрируют PSR-4 совместимый код:

Пример замыкания
----------------

```php
<?php
/**
 * Пример реализации для конкретного проекта.
 *
 * После регистрации этого атозагрузчика через SPL, следующая строка попытается загрузить класс \Foo\Bar\Baz\Qux
 * из файла /path/to/project/src/Baz/Qux.php:
 *
 *      new \Foo\Bar\Baz\Qux;
 *
 * @param string $class полное имя класса.
 * @return void
 */
spl_autoload_register(function ($class) {

    // префиксное пространство имён проекта
    $prefix = 'Foo\\Bar\\';

    // базовая директория для префиксного пространства имён
    $base_dir = __DIR__ . '/src/';

    // проверяем, использует ли класс префиксное пространство имён?
    $len = strlen($prefix);
    if (strncmp($prefix, $class, $len) !== 0) {
        // нет, переходим к следующему зарегистрированному автозагрузчику
        return;
    }

    // получаем относительное имя класса
    $relative_class = substr($class, $len);

    // заменяем префиксное пространство имён на базовую директорию, заменяем разделители пространств имён
    // разделителями директорий в относительном имени класса, добавляем .php
    $file = $base_dir . str_replace('\\', '/', $relative_class) . '.php';

    // если файл существует, подключаем его
    if (file_exists($file)) {
        require $file;
    }
});
```

Пример класса
-------------

Ниже приведен пример реализации класса для обработки нескольких пространств имен:

```php
<?php
namespace Example;

/**
 * Пример реализации общего назначения, включающий дополнительную возможность 
 * указывать несколько базовых директорий для одного префиксного пространства имён.
 *
 * Используем пакет классов foo-bar в файловой системе со следующими путями:
 *
 *     /path/to/packages/foo-bar/
 *         src/
 *             Baz.php             # Foo\Bar\Baz
 *             Qux/
 *                 Quux.php        # Foo\Bar\Qux\Quux
 *         tests/
 *             BazTest.php         # Foo\Bar\BazTest
 *             Qux/
 *                 QuuxTest.php    # Foo\Bar\Qux\QuuxTest
 *
 * ... добавляем путь к файлу класса для префиксного пространства имён \Foo\Bar\
 *
 *      <?php
 *      // экземпляр загрузчика
 *      $loader = new \Example\Psr4AutoloaderClass;
 *      
 *      // регистрируем автозагрузчик
 *      $loader->register();
 *      
 *      // регистрируем базовые дериктории для префиксного пространства имён
 *      $loader->addNamespace('Foo\Bar', '/path/to/packages/foo-bar/src');
 *      $loader->addNamespace('Foo\Bar', '/path/to/packages/foo-bar/tests');
 * 
 * Следующая строка попытается загрузить класс \Foo\Bar\Qux\Quux из файла /path/to/packages/foo-bar/src/Qux/Quux.php:
 * 
 *      <?php
 *      new \Foo\Bar\Qux\Quux;
 * 
 * Следующая строка попытается загрузить класс \Foo\Bar\Qux\QuuxTest из файла /path/to/packages/foo-bar/tests/Qux/QuuxTest.php:
 * 
 *      <?php
 *      new \Foo\Bar\Qux\QuuxTest;
 */
class Psr4AutoloaderClass
{
    /**
     * Ассоциативный массив, в котором ключ — префиксное простраство имён, а значение — массив базовых директорий
     * для классов в этом пространстве.
     *
     * @var array
     */
    protected $prefixes = array();

    /**
     * Регистрирует загрузчик через SPL.
     * 
     * @return void
     */
    public function register()
    {
        spl_autoload_register(array($this, 'loadClass'));
    }

    /**
     * Добавляет базовую директорию для префиксного пространства имён.
     *
     * @param string $prefix Префиксное простраство имён.
     * @param string $base_dir Базовая директория для префиксного пространства имён.
     * @param bool $prepend Если истина, базовая директория добавляется в начало списка, а не в конец; это позволит
     * проверять указанную директорию раньше, чем остальные
     * @return void
     */
    public function addNamespace($prefix, $base_dir, $prepend = false)
    {
        // нормализуем префиксное простраство имён
        $prefix = trim($prefix, '\\') . '\\';
        
        // нормализуем базовую директорию с конечным разделителем
        $base_dir = rtrim($base_dir, '/') . DIRECTORY_SEPARATOR;
        $base_dir = rtrim($base_dir, DIRECTORY_SEPARATOR) . '/';

        // инициализируем массив префиксных пространств имён
        if (isset($this->prefixes[$prefix]) === false) {
            $this->prefixes[$prefix] = array();
        }
        
        // сохраняем базовую директорию для префиксного пространства имён
        if ($prepend) {
            array_unshift($this->prefixes[$prefix], $base_dir);
        } else {
            array_push($this->prefixes[$prefix], $base_dir);
        }
    }

    /**
     * Загружает файл класса по выбранному имени класса.
     *
     * @param string $class Полное имя класса.
     * @return mixed Имя загруженного файла в случае успеха или false в случае неудачи.
     */
    public function loadClass($class)
    {
        // текущее префиксное простраство имён
        $prefix = $class;
        
        // проходим в обратном порядке по именам пространств имён полного имени класса чтобы найти файл
        while (false !== $pos = strrpos($prefix, '\\')) {

            // сохраняем конечный разделитель пространства имён в префикс
            $prefix = substr($class, 0, $pos + 1);

            // относительное имя класса
            $relative_class = substr($class, $pos + 1);

            // пробуем загрузить файл по префиксу и относительному имени класса
            $mapped_file = $this->loadMappedFile($prefix, $relative_class);
            if ($mapped_file) {
                return $mapped_file;
            }

            // удаляем конечный разделитель пространства имён для следующей итерации
            $prefix = rtrim($prefix, '\\');   
        }

        // не удалось найти файл
        return false;
    }

    /**
     * Загружает файл по префиксу и относительному имени класса.
     *
     * @param string $prefix Префиксное простраство имён.
     * @param string $relative_class Относительное имя класса.
     * @return mixed Имя загруженного файла в случае успеха или false в случае неудачи.
     */
    protected function loadMappedFile($prefix, $relative_class)
    {
        // исть ли базовые директории для этого префиксного пространства имён?
        if (isset($this->prefixes[$prefix]) === false) {
            return false;
        }

        // пробегаем по базовым директориям этого префиксного пространства имён
        foreach ($this->prefixes[$prefix] as $base_dir) {

            // заменяем префиксное пространство имён на базовую директорию, заменяем разделители пространств имён
            // разделителями директорий в относительном имени класса, добавляем .php
            $file = $base_dir
                  . str_replace('\\', DIRECTORY_SEPARATOR, $relative_class)
                  . '.php';

            // если файл существует, подключаем его
            if ($this->requireFile($file)) {
                // да, у нас получилось
                return $file;
            }
        }

        // не удалось найти файл
        return false;
    }

    /**
     * Подключает файл, если он существует.
     *
     * @param string $file Файл, который нужно подключить.
     * @return bool Истина, если файл существует, ложь — если нет.
     */
    protected function requireFile($file)
    {
        if (file_exists($file)) {
            require $file;
            return true;
        }
        return false;
    }
}
```

### Модульные тесты

Следующий пример — один из способов модульного тестирования для автозагрузчика классов:

```php
<?php
namespace Example\Tests;

class MockPsr4AutoloaderClass extends Psr4AutoloaderClass
{
    protected $files = array();

    public function setFiles(array $files)
    {
        $this->files = $files;
    }

    protected function requireFile($file)
    {
        return in_array($file, $this->files);
    }
}

class Psr4AutoloaderClassTest extends \PHPUnit_Framework_TestCase
{
    protected $loader;

    protected function setUp()
    {
        $this->loader = new MockPsr4AutoloaderClass;
    
        $this->loader->setFiles(array(
            '/vendor/foo.bar/src/ClassName.php',
            '/vendor/foo.bar/src/DoomClassName.php',
            '/vendor/foo.bar/tests/ClassNameTest.php',
            '/vendor/foo.bardoom/src/ClassName.php',
            '/vendor/foo.bar.baz.dib/src/ClassName.php',
            '/vendor/foo.bar.baz.dib.zim.gir/src/ClassName.php',
        ));
        
        $this->loader->addNamespace(
            'Foo\Bar',
            '/vendor/foo.bar/src'
        );
        
        $this->loader->addNamespace(
            'Foo\Bar',
            '/vendor/foo.bar/tests'
        );
        
        $this->loader->addNamespace(
            'Foo\BarDoom',
            '/vendor/foo.bardoom/src'
        );
        
        $this->loader->addNamespace(
            'Foo\Bar\Baz\Dib',
            '/vendor/foo.bar.baz.dib/src'
        );
        
        $this->loader->addNamespace(
            'Foo\Bar\Baz\Dib\Zim\Gir',
            '/vendor/foo.bar.baz.dib.zim.gir/src'
        );
    }

    public function testExistingFile()
    {
        $actual = $this->loader->loadClass('Foo\Bar\ClassName');
        $expect = '/vendor/foo.bar/src/ClassName.php';
        $this->assertSame($expect, $actual);
        
        $actual = $this->loader->loadClass('Foo\Bar\ClassNameTest');
        $expect = '/vendor/foo.bar/tests/ClassNameTest.php';
        $this->assertSame($expect, $actual);
    }
    
    public function testMissingFile()
    {
        $actual = $this->loader->loadClass('No_Vendor\No_Package\NoClass');
        $this->assertFalse($actual);
    }
    
    public function testDeepFile()
    {
        $actual = $this->loader->loadClass('Foo\Bar\Baz\Dib\Zim\Gir\ClassName');
        $expect = '/vendor/foo.bar.baz.dib.zim.gir/src/ClassName.php';
        $this->assertSame($expect, $actual);
    }
    
    public function testConfusion()
    {
        $actual = $this->loader->loadClass('Foo\Bar\DoomClassName');
        $expect = '/vendor/foo.bar/src/DoomClassName.php';
        $this->assertSame($expect, $actual);
        
        $actual = $this->loader->loadClass('Foo\BarDoom\ClassName');
        $expect = '/vendor/foo.bardoom/src/ClassName.php';
        $this->assertSame($expect, $actual);
    }
}
