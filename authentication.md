# Authentication

Via the Asatru CLI you can create an authentication model and migration. 
```plaintext
php asatru make:auth
```

Be sure to run the migration command (preferably list) after you have issued the command.
This will then create the database table.
```plaintext
php asatru migrate:list
```

The authentication model provides you with the following methods:

```php
//To register a new user
public static function register($username, $email, $password) {}

//To log a user in
public static function login($email) {}

//To log a user out
public static function logout($email) {}

//Check if a user is logged in by email or by session ID
public static function isUserLoggedIn($email = null) {}

//Get a user data object by email
public static function getByEmail($email) {}

//Get a user data object by session (only when logged in)
public static function getBySession() {}
```
