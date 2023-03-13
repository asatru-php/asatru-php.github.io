# mail() wrapper

The framework comes with a convenience wrapper for the PHP inbuilt mail() function. It
can be used to use views with templating as mail content.

The following example demonstrates how to use the functionality
```php
<?php

//Instantiate class instance
$mailer = new  Asatru\Mailwrapper\Mail();

//Here you set the recipient of the e-mail
$mailer->setRecipient('receiver@example.com');

//E-Mail subject
$mailer->setSubject('E-Mail subject');

//Specify a view
$mailer->setView('layout', array(array('yield', 'yieldfile')), [
    'some_var' => $some_value
]);

//Or directly set message content:
$mailer->setMessage($content);

//You can also optionally specify addition headers and parameters
$mailer->setAdditionalHeaders(headers);
$mailer->setAdditionalParameters(parameters);

$mailer->send(); //Send the e-mail
```
