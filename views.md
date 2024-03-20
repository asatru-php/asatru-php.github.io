# Views

When your controller method is called you will most of the times want to render a view.
There you can utilize the Asatru\View\ViewHandler class. You can specify three different
items:
```php
//Let‘s you pass variables to the view as key-value pairs
public function ViewHandler::setVars(<array>)

//Let‘s you specify the layout file to be used
public function ViewHandler::setLayout(<string>)

//Let‘s you specify various yields defined in your layout file.
public function ViewHandler::setYield(<string>, <string>)
```
Note: use the view() helper instead of the class for more convenient coding.

Alternatively you can call the static method create() with first argument the layout file, as
second argument a key-value pair of yields and as last argument the key-value paired
variables array.

A layout file is used as your basis view layout. There you can for instance specify the
header of the HTML document and a footer. A yield is defined via { % name % } where
„name“ is the name of the yield which is used via setYield(). Basically every yield token will
then be replaced with the content of the yield file.

Inside your view files you can also use the template engine. This is especially useful for
writing code faster. It saves you a bit of time. The following template commands exist
```
@if: Renders an if statement, for instance: @if ($myvar === true)
@elseif: Continue with an alternative if statement. For instance: @elseif ($myvar === false)
@else: Specify an else statement
@endif: Ends the if condition
@for: Renders a for loop. For instance: @for ($i = 0; $i < 10; $i++)
@endfor: Ends the for loop
@foreach: Renders a foreach loop. For instance: @foreach ($tokens as $token)
@endforeach: Ends the foreach statement
@while: Renders a while statement. For instance: @while ($a < 10)
@endwhile: Ends a while statement
@break: Renders a break statement
@continue: Renders a continue statement
@switch: Renders a switch statement. For instance @switch ($var)
@case: Renders a case condition. For instance @case 1
@default: Renders a default condition.
@endswitch: Ends the switch statement
@comment: Renders a comment. For instance @comment This is rendered as a comment
@include: Replaces the line with the rendered content of the specified file. For instance @include('my-file.php')
@isset: Checks whether an object is set
@isnotset: Checks whether an object is not set
@endset: Ends the block if an isset/isnotset statement
@empty: Checks if an expression is empty
@endempty: Ends the block of @empty
@notempty: Checks if an expression is not empty
@endnotempty: Ends the block of @notempty
@debug: Handles the block if in debug mode
@enddebug: Ends the block of @debug
@env(‚var‘, ‚opt:value‘): Either checks if an env var exists or if a non null value is provided it checks if it equals the value
@endenv: Ends the block of @env
@php: Start a PHP block
@endphp: End a PHP block
@end: Generic block ending
@csrf: Inserts a hidden input field with the current CSRF token used for forms
@method: Specifies the actual request method for your form. For instance @method('PATCH')
{ { <output> } }: This will output your code into the buffer. This can be used to output variables. Internally it uses htmlspecialchars in order to prevent XSS.
{ !! <output> !! }: This will output your code into the buffer, but without using 
htmlspecialchars. Useful if you want to render HTML into the document
@{ { expression } }: Will leave the expression wrapped in brackets.
```

You can also create custom template commands. Add them with the helper
template_command().

You can use flash messages. Flash messages are formatted messages that are showed only once
in the current view. If the page is then reloaded or changed the message won't be shown anymore.
This is useful if you want for example return feedback after form submit or a welcome message 
after logging in. There are dozens of use-cases.

The following methods of the FlashMessage helper exist:
```php
//Bind a message to an identifier. Use-case in controllers
public static function FlashMessage::setMsg($name, $text) {}

//Returns true if a message with the name exists, otherwise false. Use-case in views.
public static function FlashMessage::hasMsg($name) {}

//Gets the message by its name. Use-case in views.
public static function FlashMessage::getMsg($name) {}
```

Resources such as CSS or JavaScript files should be placed inside the app/resources
folder.
