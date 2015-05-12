Kettle by eleiva
======

Kettle is a lightweight object-dynamodb mapper for PHP5.
Kettle provides a simple interface to Amazon DynamoDB.

See Some Code
-------------------

```php
<?php
use Kettle\ORM;

$user = ORM::factory('User')->findOne(10);
$user->name = 'John';
$user->save();


$tweets = ORM::factory('Tweet')->where('user_id', 10)
                 ->findMany();

foreach ($tweets as $tweet) {
    echo $tweet->text . PHP_EOL;
}

```

1. Configuration
-------------------

use .env to configure this vars


```
AWS_REGION
AWS_ACCESS_KEY_ID
AWS_REGION
```


```

2. Create Model Class
-------------------

```php
<?php

class User extends ORM {
    protected $_table_name = 'user';
    protected $_hash_key   = 'user_id';
    protected $_schema = array(
      'user_id'    => 'N',  // user_id is number
      'name'       => 'S',  // name is string
      'age'        => 'N',
      'country'    => 'S',
     );
}


```

3. Create
-------------------

```php
<?php

$user = ORM::factory('User')->create();
$user->id = 1;
$user->name = 'John';
$user->age  = 20;
$user->save();

```

4. Retrieve
-------------------

```php
<?php

$user = ORM::factory('User')->findOne(1);
echo $user->name. PHP_EOL;

print_r($user->asArray());

```

5. Update
-------------------

```php
<?php

$user = ORM::factory('User')->findOne(1);
$user->age = 21;
$user->save();

```

6. Delete
-------------------

```php
<?php

$user = ORM::factory('User')->findOne(1);
$user->delete();

```


7. Find
-------------------

```php
<?php

$tweets = ORM::factory('Tweets')
        ->where('user_id', 1)
        ->where('timestamp', '>', 1397264554)
        ->findMany();

foreach ($tweets as $tweet) {
     echo $tweet->text . PHP_EOL;
}

```

8. Find first record
-------------------

```php
<?php

$tweet = ORM::factory('Tweets')
        ->where('user_id', 1)
        ->where('timestamp', '>', 1397264554)
        ->findFirst();

echo $tweet->text . PHP_EOL;

```


9. Find by Global Secondary Index
-------------------

```php
<?php

$users = ORM::factory('User')
        ->where('country', 'Japan')
        ->where('age', '>=', 20)
        ->index('country-age-index')  // specify index name
        ->findMany();

```


10. Query Filtering
-------------------

```php
<?php

$tweets = ORM::factory('Tweets')
          ->where('user_id', 1)
          ->filter('is_deleted', 0) // using filter
          ->findMany();

```

