# laravel-notebook
This is a personal notebook with quick references and undocumented examples.





Refresh a database instance
```php
$link = $link->fresh()
```

## Eloquent

Where doesn't Have

```php
Person::whereDoesntHave('items')
```


## Controller tricks
Clean store request
```php
Project::create([request('title', 'description')]);
```
