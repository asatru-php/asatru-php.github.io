# SMTP mailing

The framework provides an interface to the PHPMailer package. Like the mail() wrapper
you can send HTML content by specifying views. Except it uses SMTP protocol to send
mails. This requires an SMTP service running on a server.

The following environment variables need to be adjusted:
<ul>
    <li><b>SMTP_HOST</b>: Hostname or address of the SMTP server</li>
    <li><b>SMTP_PORT</b>: Port to connect through, e.g. 587 for TLS encrypted connection</li>
    <li><b>SMTP_USERNAME</b>: Login name for the server</li>
    <li><b>SMTP_PASSWORD</b>: Login password for the server</li>
    <li><b>SMTP_ENCRYPTION</b>: Either ‚tls‘ or ‚smtps‘.</li>
</ul>

The following example demonstrates how to use the functionality
```php
<?php

//Instantiate class instance
$mailer = new Asatru\SMTPMailer\SMTPMailer();

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

$mailer->send(); //Send the e-mail
```

Of course you can directly access PHPMailer class for custom e-mailing.
