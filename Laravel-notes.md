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
Project::create(request(['title', 'description']));
```


### Auth helper
```php
auth()->id() //4
auth()->user() //user instance
auth()->check() //boolean
auth()->guest() //boolean
auth()->hasUser() //boolean
```

# Testing

Display exceptions
```php
$this->withoutExceptionHandling()
```

Disable csrfToken
```php
use Illuminate\Foundation\Testing\WithoutMiddleware;
use App\Http\Middleware\VerifyCsrfToken;

$this->withoutMiddleware(VerifyCsrfToken::class);
```

or alter the file VerifyCsrfToken.php and alter the $except array
```php
 protected $except = [
        '*'
    ];
```

