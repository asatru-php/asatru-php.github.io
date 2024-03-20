# CLI tool

Asatru PHP comes with a handy CLI interface which allows you to perform some
operations.

Just open your prefered terminal and cd to the directory of your project. Then run the
command „php asatru“ to get a list of commands.

## The following commands exist:

Displays the help text
```sh
php asatru help
```

Creates a model and migration file where name is
the name of the model and table is the associated table of the database
```sh
php asatru make:model <name> <database_table_name>
```

Creates a new module that is dedicated to your business logic. Arguments can be –base to create a base class, --extends <opt:name> to extend a base class and –final to create a final class.
```sh
php asatru make:module <name> <opt:args[]>
```

Creates a new controller
```sh
php asatru make:controller <name>
```

Creates a new language folder structure with an app.php
```sh
php asatru make:language <locale>
```

Creates a new validator with the given name and
the associated validator ident
```sh
php asatru make:validator <name> <ident>
```

Creates a new event handler with name as class name and an initial handler method called (initial_method)
```sh
make:event <name> <initial_method>
```

Creates a new command class
```sh
make:command <name>
```

Creates a model and migration used for authentication
```sh
php asatru make:auth
```

Creates a model and migration used for caching
```sh
php asatru make:cache
```

Creates a new test case with the given name
```sh
php asatru make:test <name>
```

Creates a fresh migration of your database. Warning: This will erase
all previously inserted data, so please be careful.
```sh
php asatru migrate:fresh
```

This will only run the newly created migrations
```sh
php asatru migrate:list
```

This drops all migrations
```sh
php asatru migrate:drop
```

Starts a development server. If port is not provided it uses the port 8000
```sh
php asatru serve <opt:port>
```

## Availability
The CLI interface is only available in debug mode.
