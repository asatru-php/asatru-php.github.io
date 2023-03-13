# Caching

Via the Asatru CLI you can create a caching model and migration. 
```plaintext
php asatru make:cache
```

Be sure to run the migration command (preferably list) after you have issued the command.
This will then create the database table.
```plaintext
php asatru migrate:list
```

The cache model provides you with the following methods:

```php
//To fetch a value either from cache or directly depending on the item existence / expiring status
public static function remember($ident, $timeInSeconds, $closure) {}

//To check if an item exists in the cache
public static function has($ident) {}

//To obtain and remove an item from the cache
public static function pull($ident) {}

//To remove an item from the cache
public static function forget($ident) {}
```

Example of using the remember method
```php
$value = Cache::remember('my_value', 60, function() {
    return AnotherModel::getMyValue();
});
```
