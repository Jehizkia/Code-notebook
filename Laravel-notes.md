# laravel-notebook
This is a personal notebook with quick references, troubleshooting tips and undocumented examples.

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


# Trouble shooting

### Uploaded files/images to the storage folder are not accessable and return a 404 when viewed in the browser.

##### Solution 1 
This specific stackoverflow issue helped me solve the described problem:
https://stackoverflow.com/questions/50730143/laravel-storage-link-wont-work-on-production

Try to delete storage folder
run:
```bash
php artisan storage:link
```

If that didn't do the trick try to also delete other folder you want to be acceccable through a symlink.
And your issue should be solved. 

