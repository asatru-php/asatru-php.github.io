# Environment configuration

The app configuration in done via a .env file located in your projects root directory. It
covers installation related environment configurations. For example on your local machine
you can have a different .env file than on your webserver. Of if you have created an app
which ships to different users, each user has their own .env file. The .env file is automatically
parsed. There you can specify different variables.

To query an environment variable you can just use the $_ENV superglobal or use the
env_get() function.

The following environment functions exist:
```php
//Parse another environment file
function env_parse($file_name): bool {}

//Query an environment variable
function env_get($ident, $fallback = null): mixed {}

//Checks if an environment variable exists
function env_exists($ident): bool {}

//Clear all variables
function env_clear(): void {}

//Check if last parsing of an env file was errorneous
function env_has_error(): bool {}

//Query the last parsing error message string
function env_errorStr(): string {}
```

Feel free to add more environment variables to your .env file. Supported are strings,
integers, floats, booleans and null.
