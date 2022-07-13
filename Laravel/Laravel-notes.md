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

## Blade

### Get all available variables in a php blade file
```php
dd(array_keys(get_defined_vars()));
```

## Zoho SMTP 2FA
If you want to send emails with your laravel application using the Zoho mail SMTP follow the steps. If your mailadress has 2FA activated you'll need to go to your zoho settings by going to [Zoho settings](https://accounts.zoho.eu). You'll need to create a ***Application-Specific Password***. You can't use your regular password because logging in will fail [see offical zoho page](https://www.zoho.com/mail/help/adminconsole/two-factor-authentication.html#alink5) and [zoho smtp](https://www.zoho.com/mail/help/pop-access.html?zredirect=f&zsrc=langdropdown&lb=nl).

After you have setup your *Application-Specific Password* you are able to use it in your .env file. 

***.env example***
```.env
MAIL_MAILER=smtp
MAIL_HOST=smtp.zoho.eu
MAIL_PORT=465
MAIL_USERNAME=yourmail@provider.com
MAIL_PASSWORD=your_application_specific_password_here
MAIL_ENCRYPTION=ssl
MAIL_FROM_ADDRESS=yourmail@provider.com
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

# Forge

### Deploy script

```bash

$FORGE_PHP artisan cache:clear
$FORGE_PHP artisan view:clear
$FORGE_PHP artisan route:clear
$FORGE_PHP artisan clear-compiled
$FORGE_PHP artisan optimize:clear

$FORGE_PHP artisan config:cache
$FORGE_PHP artisan route:cache
$FORGE_PHP artisan view:cache
$FORGE_PHP artisan optimize
$FORGE_PHP artisan storage:link

npm install
npm run prod

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

