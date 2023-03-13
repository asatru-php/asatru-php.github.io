# Autoloading

The framework supports composer autoloading. But you can also use the frameworks own
autoloader. Therefore go to the app/config/autoload.php file and add your file to the array.
There you specify a path to your file relative to the app directory.

```php
<?php

return [
    '/helper/MyHelper.php'
];
```

This will autoload the file relative to the app directory.
