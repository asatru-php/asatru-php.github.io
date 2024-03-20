# Commands

You can also create custom commands that can be used via the asatru CLI tool.
Command handler classes are stored in the app/commands directory and they have to be
registered via the `app/config/commands.php` configuration script file.

For each command handler you can add an array item to the config array where the first
item specifies the name of the command, the second specifies a help description text and
the third item specifies the class and script name of the command handler.

```php
<?php

return [
    array('command:name', 'This is a description', 'TestCommand'),
];
```

Then there needs to be a TestCommand.php file in the app/commands directory defining a
class called TestCommand that needs to implement the Asatru\Commands\Command interface.

A command class has to at least implement the non-static handle($args) method. The
argument parameter recieves an object of Asatru\Commands\Arguments that is iterable
and countable. Each item is an Asatru\Commands\Argument class instance that you can
use to access the actual argument. The following methods are available:

```php
<?php

function getValue(); //Gets the current value
function getType(); //Gets the value type
function isNull(); //Indicates if the value is null
function isEmpty(); //Indicates if the value is empty
```

You can use the CLI tool to comfortably generate a custom command.
