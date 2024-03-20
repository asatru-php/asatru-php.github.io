# Form helper

The Form helper class extends the Html helper class and provides a convenient way to
render forms into the document. It provides the following methods:

```php
<?php

public static function begin(array $attr); //Begins the form. You can optionally specify attributes via the array param.
public static function putElement($name, array $attr); //Put a form element. You can optionally specify element attributes via the array param
public static function closeElement($name); //Close the current form element
public static function end(); //Finish form rendering
```

Note that each method returns a string with the related content.