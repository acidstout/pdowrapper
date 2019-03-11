# pdowrapper
Simple PDO wrapper class which is compatible with basic ADOdb features.

The goal was to migrate web-applications from ADOdb to plain PDO, when there's no need to have a fully featured database framework.

Especially if just a few basic features (CRUD) are used. In order to switch from ADOdb to PDO you just need to replace the way how you connect to the database (e.g. replace your ADOdb database connection object with the Wrapper object) and it should work out of the box.

Some features like setting ADOdb's fetch-mode are not implemented, and for now it's not planned to change that.

## Usage

### Establish database connection:
```php
$db = new PDO\Wrapper($host, $database, $username, $password);
```

### Fetch data from database:
```php
$sql = "SELECT * FROM users WHERE is_active = 1 ORDER BY surname ASC LIMIT 10;";
$users = $db->getAll();
```

### Iterate over the fetched result:
```php
foreach ($users as $user) {
	echo $user['surname'] . ', ' . $user['forename'];
}
```

### Insert data into database using prepared statements:
```php
$sql = "INSERT INTO users (surname, forename, is_active) VALUES (?, ?, 1);";
$db->execute($sql, array('Smith', 'Alice'));
```

### Update date in database using hardcoded values (e.g. don't use prepared statements):
```php
$sql = "UPDATE users SET is_active = 0 WHERE forename = 'Bob';";
$db->execute($sql);
```

## License
Licensed under the GPL-3, [http://www.gnu.org/licenses/](http://www.gnu.org/licenses/). See LICENSE for details.