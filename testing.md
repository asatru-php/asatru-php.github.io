# Testing

Asatru PHP utilizes PHPUnit in order to perform tests. Tests shall be located in the
app/tests directory. A test file has to have the postfix ‚Test‘. For example if you have the
test „Example“ then the file must be named „ExampleTest.php“ and the class of the test
case must be named „ExampleTest“.

A test case class should be derived from Asatru\Testing\Test class. This way your test is
well suited for testing your application so you can also test your routes.

For testing the .env is not parsed, but instead a .env.testing which you have to create. The
APP_DEBUG is ignored because for testing it is forced to true.

If you want to test a route you can simply call 
```php
Asatru\Testing\Test::route($type, $url, $data)
```

Type is the type of request, e.g. POST or GET. The URL is the same as someone would
type it in your browser (without domain names, port or protocol). Data is an array where you can set GET and POST data. For
instance:
```php
array(
    "GET" => array("somevar" => somevalue), 
    "POST" => array("somevar" => somevalue)
)
```

Example
```php
$result = Asatru\Testing\Test::route('GET', '/my/route', array(
    'GET' => array('value' => 'Hello World'))
);

//Now you can do assertions with $result. It contains the data that
//has been returned by the controller action.
```

You can use the Asatru CLI to create a new test case:
```plaintext
php asatru make:test example
```

This will generate the following testcase:
```php
<?php

/*
    Testcase for Test Example
*/

use PHPUnit\Framework\TestCase;

/**
 * This class holds your test methods
 */
class ExampleTest extends Asatru\Testing\Test
{
    //
}
```

You can then add your test methods:
```php
class ExampleTest extends Asatru\Testing\Test
{
    public function testExample()
    {
        //Just an example
        $this->assertTrue(true);
    }
}
```

Refer to the documentation of PHPUnit in order to get to know how to make assertions.
