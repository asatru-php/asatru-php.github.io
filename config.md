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
$attr = $data['attr'];
```