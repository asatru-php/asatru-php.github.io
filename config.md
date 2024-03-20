# Config management

The framework offers the possibility to load configuration data from config scripts
from the <b>app/config</b> directory. 

For instance you can have the config file <b>app/config/test.php</b> with the following content:
```php
<?php

return [
    'attr' => 'value',
    'more' => [
        //More data
    ]
];
```

You can now query the config data like this:
```php
<?php

$data = config('test');

//Or if in a sub directory
$data = config('folder/test');
```

If the config script returns an array then it is returned as object by default. In order to turn off this behaviour and return the array instead, simply pass ‚false‘ as second argument.

```php
<?php

$data = config('test', false);
```