# Logging

The framework supports logging. When your app is in debug mode a logfile will
automatically be created inside the <b>/app/logs</b> directory.
Log content will be stored in text files per day.

Use the addLog() function in order to log to the buffer. 
```php
function addLog($type, $line);
```

You can use different log types:
<ul>
    <li><b>ASATRU_LOG_INFO</b>: An information message</li>
    <li><b>ASATRU_LOG_DEBUG</b>: A debug message</li>
    <li><b>ASATRU_LOG_WARNING</b>: A warning message</li>
    <li><b>ASATRU_LOG_ERROR</b>: An error message</li>
</ul>

An example log content can log like the following:
```
[2020-02-1 03:02:17 pm][Header] Asatru PHP log on 2020-02-1 03:02:17 pm
[2020-02-1 03:02:17 pm][Info] TestCase Info
[2020-02-1 03:02:17 pm][Debug] TestCase Debug
[2020-02-1 03:02:17 pm][Warning] TestCase Warning
[2020-02-1 03:02:17 pm][Error] TestCase Error
```

In order to clean the current log buffer use
```php
function clearLog();
``` 

In order to force storing the current log buffer use 
```php
function storeLog();
```
