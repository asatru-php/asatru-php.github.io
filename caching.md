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

//Return the value of the given element if exists or the default value if not. Additionally you can return other column values specified via the dot- syntax. For instance: my_cache_item.updated_at returns the updated_at value of the item with ident „my_cache_item“ if it exists, otherwise the specified default value
public static function query($ident, $default = null) {}

//To check if an item exists in the cache
public static function has($ident) {}

//Returns true if the elements cache time is elapsed, otherwise false
public static function elapsed($ident, $timeInSeconds) {}

//To obtain and remove an item from the cache
public static function pull($ident) {}

//Write the given value to the cache with the given ident
public static function put($ident, $value);

//To remove an item from the cache
public static function forget($ident) {}
```

Example of using the remember method
```php
$value = Cache::remember('my_value', 60, function() {
    return AnotherModel::getMyValue();
});
```
