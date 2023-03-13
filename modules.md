# Modules

Where database models are solely dedicated to be a representation of a database table
you will also want to create business logic modules in order to keep your controllers clean.
As a general good coding practice you should not put everything into your controllers.
Business logic can be placed in modules. Modules are basically classes that are
autoloaded during application bootstrap process. Then you just need use the class as how
you wish. Modules are placed inside the modules directory. The file name must equal the
class name.

In order to create a new module you can use the console:
```plaintext
php asatru make:module name
```

This will create a base structure class file in:
```plaintext
/app/modules/name.php
```

It will contain the following code:
```php
<?php

    /*
        Asatru PHP - Module
    */

    /**
     * This class represents your module
     */
    class Example {
        public function __construct()
        {
            //
        }

        public function __destruct()
        {
            //
        }
    }
```

Now you can implement your business logic there.
