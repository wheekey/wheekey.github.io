---
published: true
---
\#php

### Что делать, если выскакивает вот такая ошибка: 
```
	Entry "PDO" cannot be resolved: The parameter "options" of __construct() has no type defined or guessable.
    It has a default value, but the default value can't be read through Reflection because it is a PHP internal class.
```

### Ответ: в конфиге php-di контейнера создавать \DI\factory:
```php
return [
    'db.local' => \DI\factory(function() {
        return new PDO('mysql:host=' . getenv("DB_HOST") . ';dbname=' . getenv("DB_NAME") . ';charset=' . getenv("DB_CHARSET"), getenv("DB_USERNAME"), getenv("DB_PASSWORD"));
    })

];
```
