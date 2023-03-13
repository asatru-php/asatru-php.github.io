# Database access

In order to perform database access you may want to create models and migrations. The
models are the interface between your app and the database. It uses prepared statements
in order to prevent SQL injection. The migrations are used to create a fresh database with
fresh tables.

In order to create a migration go to the app/migrations folder and create a new file, e.g.
example_migration.php. Now add a class with the name Example_migration_Migration.
The „_Migration“ will be appended to the script file name (ucfirst, too) in order to resolve
the class name. Inside the class you specify two methods: up() and down(). The down
method is used to remove the table and the up method is used to create the table. Your
class must provide a constructor where it recieves the PDO connection handler instance.
Save it to a private member variable. Then in the up() method you instantiate a Asatru\
Database\Migration object passing the name of the table as first argument and the
connection handler reference as second argument. After that you can call the methods of
the created object to define your table. At first you may want to drop the old table via the
drop() method. Then you will want to define the columns. Therefore you use the add()
method. You pass an SQL query string in order to create a column, e.g. „text varchar(260)
not null“. When you have added all your desired columns then you call the create() method
in order to create the table. In order to alter a table you just use the method append() in
order to insert a new column. Note that you may not mix creation of new tables with
altering tables.

In your down() method you call the drop() method of a database object.

Next step is to create a model for that migration. These are created in the app/models
folder. Create a file called, for instance, MyModel.php. Then open the script file and create
a class MyModel. It must have the same name as the script file to be resolved. Also it
extends the Asatru\Database\Model class. You have to implement the static method
tableName() which returns a string that identifiers the migration associated with this model.
After that you can implement your static getters and setters. You can perform select,
update, insert, delete and raw queries:
```php
public static function Model::where(name, comparision, value): Use a conditional and-query. Call the method for each condition
public static function Model::whereOr(name, comparision, value): Use a conditional or-query. Call the method for each condition
public static function Model::limit(count): Limit the query result
public static function Model::groupBy(ident): Group items by ident
public static function Model::orderBy(ident, type): Order items by ident. Type is either asc or desc.
public static function Model::first(): Get first item
public static function Model::get(): Perform the query and get the items
public static function Model::all(): Get the entire table
public static function Model::find(id, key): Find an entry by id. Use key parameter if you want to specify the name of the key so look for
public static function Model::count(): Get the amount of found items
public static function Model::aggregate(type, column, opt:name): Find an aggregate of the column (avg, min, max, sum, etc.)
public static function Model::whereBetween(column, value1, value2): Use a conditional between andquery. Call the method for each condition
public static function Model::whereBetweenOr(column, value1, value2): Use a conditional between orquery. Call the method for each condition
public static function Model::update(ident, value): Add this item to the updated item list
public static function Model::insert(ident, value): Add this item to the inserted item list
public static function Model::go(): Perform either an update or insert operation
public static function Model::delete(): Perform a delete operation
public static function Model::raw(qry, args): Perform a raw database operation
```

The result of the operation depends of the its kind:
+ For fetching data it returns an instance of Asatru\Database\Collection. The Collection class implements Iterator and Countable, so you can use the count() function and also use a class instance with the foreach iteration loop.
  - Call the count() method to get the amount of collected entries
  - Call the get(<ident>) method to get the related item. This can be an instance of the collection class, too.
  - Call the first() method to get the first item in list
  - Call the last() method to get the last item in list
  - Call each(<callback>) in order to iterate through all collected items
+ For inserting, updating and deleting it returns a boolean indicating whether the operation could be executed
+ For getting the count it returns the amount of found entries

In order to manage migrations you can use the following functions:
+ migrate_fresh(): Drops all tables and recreates them
+ migrate_list(): Runs only newly created migration scripts
+ migrate_drop(): Drops all migrations

The database connection is adjusted via the .env file. 
```
# Set to true to enable database functionality
DB_ENABLE=false

# Hostname or address of the database service
DB_HOST=localhost

# Username for authentication
DB_USER=root

# Password for authentication
DB_PASSWORD=""

# Used service port, normally you won't need to change this
DB_PORT=3306

# Database name to be used within the database service
DB_DATABASE=asatru

# Driver to be using. Currently only MySQL is supported
DB_DRIVER=mysql
```

You can create a new model along with a migration via:
```plaintext
php asatru make:model <model name> <table name>
```
