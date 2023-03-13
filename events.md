# Events

On certain occassions you may want to raise an event and thus perform specific tasks for that event.
You can do that with the inbuilt event functionality.

First go to /app/events and create a new file with a given name
(for example ExampleEventHandler). The content will be as follows:
```php
<?php

class ExampleEventHandler {
    public function handle($data = null)
    {
        //Do something here
    }
}
```
The class name must match the PHP script file name. Of course you can add multiple methods for 
different events of a specific topic.

Next step is to add the handler to the list of events. Therefore open
the /app/config/events.php file and add the handler:
```php
<?php

return [
    'event_name' => 'ExampleEventHandler@handle'
];
```

You can now fire the event whenever you want using the event function:
```php
event('event_name', [
    'some_variable' => 'some value'
]);
```
