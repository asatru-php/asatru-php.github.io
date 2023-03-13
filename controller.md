# Controller

Controllers are PHP classes that handle a request of the client, e.g. the Browser.
Every registered URL is handled by a controller action.

First let's create a new controler:
```plaintext
php asatru make:controller example
```

The generated code will be something like:
```php
<?php

/*
    Asatru PHP - Controller
*/

/**
 * This class represents your controller
 */
class ExampleController {
    //
}
```

Now we want a controller action handle the URL <b>/example</b>

Therefore we add a new method to our class
```php
class ExampleController {
    public function example_action($request)
    {
        //Do something here
    }
}
```

A route must be registered to the system, so we go to /app/config/routes.php 
and add our route there
```php
<?php

return [
    array('/', 'GET', 'index@index'),
    array('/example', 'GET', 'example@example_action')
];
```

For each route we add an array item to the routes array whose first element
is the route, second element is the request type (GET, POST or ANY) and the third element
is a pair of the controller and the handler action. So example@example_action will be
resolved to ExampleController::example_action().

Now browse to http://localhost:8000/example and your controller action should be called.

You can also specify placeholder names inside routes. These can then dynamically be fetched via the $request
variable:
```php
<?php

return [
    array('/', 'GET', 'index@index'),
    array('/example/{var1}/complex/{var2}', 'GET', 'example@example_action')
];
```

This will lead to the fact that the controller action will be called when
the first element is 'example', the second element is variadic, the third element is
'complex' and the last element is variadic, too.

Then grab the values in the action in order to work with them
```php
class ExampleController {
    public function example_action($request)
    {
        $var1 = $request->arg('var1');
        $var2 = $request->arg('var2');
    }
}
```

You can also use the $request object to query POST and GET variables if you don't want
to use the superglobals $_POST or $_GET.
```php
class ExampleController {
    public function example_action($request)
    {
        $get_or_post_var = $request->params()->query('get_or_post_var');
    }
}
```

A controller action will usually control the returned response to the client. 
You can return instances of ViewInterface objects or just plain strings.

The following view classes exist:
```php
//Let‘s you return a view. See section ‚Views‘ for details
class Asatru\View\ViewHandler {}

//Let‘s you return plain text. No HTML is rendered
class Asatru\View\PlainHandler {}

//Let‘s you return Json content
class Asatru\View\JsonHandler {}

//Let‘s you return XML content
class Asatru\View\XmlHandler {}

//Let‘s you return CSV content
class Asatru\View\CsvHandler {}

//Let‘s you redirect to an URL
class Asatru\View\RedirectHandler {}

//Let the client download a file
class Asatru\View\DownloadHandler {}

//Let‘s you customize the type of output
class Asatru\View\CustomHandler {}
```
Note: Use the helper functions instead of the classes for more convenient coding.

If you want you can derive your controller class from 
```
Asatru\Controller\Controller
```

The class offers the following methods
```php
//Called before the actual action
public function preDispatch(): void {}

//Called after the actual action
public function postDispatch(): void {}
```

Or you can create a custom base controller which can serve for your common tasks. The base controller
must be named BaseController and be placed into <b>app/controllers/_base.php</b>. If it exists then it
will be automatically loaded.

## Validators
If your controller handles a form then you also want to verify the form data. Therefore you can use
the Asatru\Controller\PostValidator class. In the constructor you specify your verify tokens. After
that you can call the isValid() method of the class to check if the data is valid. It returns true on
success. If returned false it means that your form data is invalid. To get to know all invalid items
you can get an array of error messages via errorMsgs(). Every form will be checked for the CSRF
token, so don‘t forget to @csrf in your form markup. The constructor requires an array of form
items to be checked. The first token is the name of the form element and the second token is the
validation string. Each token can have multiple validators. The following validators exist

+ required: This item must be provided
+ email : The item must contain a valid E-Mail address
+ min:num : The item must contain at least num characters
+ max:num : The item must contain not more than num characters
+ datetime : The item needs to be in a valid datetime format
+ number : The item needs to be a valid number
+ regex:pattern : The item needs to match the regex pattern

Separate a validator with the | character, e.g. „required|email“.

You can also implement own validators. These are placed into the \app\validators folder. The script
file name must also be the class name (ucfirst) with „Validator“ appended. It extends the Asatru\
Controller\BaseValidator class. You need to provide the following methods:
```php
//Return the name of your validator ident. This is used in the 
//validation string identifying your validator.
public function getIdent() {}

//This method is used to validate the data. It
//recieves the value that needs to be checked and 
//optionally arguments that to adjust the validation
public function verify($value, $args = null) {}

//Here you need to return an error string describing the failure if
//the validation has failed
public function getError() {}
```

You can create a validator comfortably using the asatru CLI command.
```
//Name is the validator class name and ident is the identifier to be used for triggering the validator
php asatru make:validator <name> <ident>
```
