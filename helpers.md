# Helpers

The framework provides some basic helper functions in order to ease your workflow.

```php
//Returns the full path to your projects root directory with additional path
function base_path($path = '') {}

//Returns the full path to your app directory with additional path
function app_path($path = '') {}

//Returns the full path to your public directory with additional path
function public_path($path = '') {}

//Returns the full URL to your projects folder. If port is not false then the port will be included in the URL.
function base_url($port = false) {}

//Return the full URL to the given destination or the URL root if none specified
function url($to = '') {}

//Return the full URL to the specified asset. When in debug mode and the asset does not exist then the framework throws an exception. Set $mt to true in order to include last modification time. This is useful when you want the browser to update its cache when the asset has been updated.
function asset($to = '', $mt = false) {}

//Returns the current CSRF token of your session
function csrf_token() {}

//Adds a new template command. First param
//is the name of the command, second param is a callback of type: function (string
//$code, array $args):string. $code contains the code line with the template. $args
//contains the arguments of the template command if any (must be wrapped in
//brackets like valid PHP code). Return value is a string with the code that the
//template command line shall be replaced with.
function template_command($ident, $callback) {}

//Short way of spawning a ViewHandler instance. $yields is either a single array with yield and include file, or an array containing arrays with multiple such info
function view($layout, array $yields, $vars = array()) {}

//Short way of returning JSON content
function json(array $content) {}

//Short way of returning XML content
function xml(array $content, $root = 'data') {}

//Short way of returning CSV content
function csv(array $content, array $header = null) {}

//Short way of returning plain text content
function text($content) {}

//Short way of returning custom content
function custom($type, $content) {}

//Short way of redirecting to an URL
function redirect($to) {}

//Return from POST route to the related GET route
function back() {}

//Short way of letting the client download a resource
function download($resource) {}

//Shortname function to call env_get()
function env($item, $fallback = null) {}

//If $value is provided and not null the values are checked, otherwise it just indicates if the env var exists
function envck($item, $value = null) {}

//Used to handle server error response codes. Triggers a call to an associated special route handler that handles the error.
function abort($code, $ctrl = null) {}

//Return old POST data. Useful if form data shall not be lost if the form data is invalid and the user has to re-submit it.
function old($key) {}

//Create a slug from a source content string using the given delimiter
function slug($content, $delimiter = '-') {}

//Get a named route and optionally set all variables via the key-value paired array
function route($name, $values = []); 
```

If you want to use localized Carbon then you can use the Carbon helper to automatically
use the current locale. Therefore just create an instance from Carbon (global namespace)
instead of Carbon\Carbon.
