# Localization

The framework supports localization. Language phrases are defined
in the /app/lang directory.

Let us create a new language for german. Therefore run the following command:
```plaintext
php asatru make:language de
```

This will create a folder structure in /app/lang. You will now see
a new folder inside it: /app/lang/de.

By default you will then have an app.php file where your application phrases should be placed inside.
Of course you can create more files, for instance errors.php where you can place your error phrases.

Open the app.php file and add your phrases there:
```php
<?php

/*
    Asatru PHP - Language file for de
*/

return [
    'phrase_1' => 'Das ist ein Test.', //A simple phrase
    'phrase_2' => 'Diesmal mit Variable: {var}' //You can specify variables with brackets {}
];
```

You can now query the phrase as follows:
```php
$phrase1 = __('app.phrase_1');
$phrase2 = __('app.phrase_2', ['var' => 'Hallo Welt!']);

//Or your errors in errors.php:
$errorMsg = __('errors.error_1');
```

The __() function queries the language phrases of the current locale.

You can get and set the current locale like follows:
```php
//Get the current locale
$currentLocale = getLanguage();

//Set the locale
setLanguage('de');
```
