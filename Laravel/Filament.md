# Filament (v2)
Here are some interesting tips on Filament 2.

## Resource view
If you are creating a [View Page](https://filamentphp.com/docs/2.x/admin/resources#view-page) for your resource here are some pointer to help you out.

### Accessing record data from your View page
You can access you data from within you views with `$record`. This will return the current Model you are viewing. You have also the `$data` variable available which has some more data about the current resource you are viewing.

#### Example
***laravel-app/resources/views/filament/resources/announcement-resource/pages/view-announcement.blade.php***
```blade
<x-filament::page>
 <h1>Announcement date {{ $record->created_at }}</h1>
 <p>Description {{ $record->description }}</h1>
</x-filament::page>

```

### Displaying resource table in view-only mode on View page
If you want to display the table of your resource in *View only* mode you can simply access the `$this->form` property from your blade file.

#### Example
***laravel-app/resources/views/filament/resources/announcement-resource/pages/view-announcement.blade.php***
```blade
<x-filament::page>
    <div class="p-6 space-y-4 bg-white rounded-xl border border-gray-300 filament-forms-card-component">
        <div>
            <h1 class="font-bold text-lg">Submitted by</h1>
             <p class="mt-2">{{ $record->guest->name }}</p>
        </div>
        <div>
            <p>Department • <strong>{{ $record->department->name }}</strong></p>
        </div>
    </div>
    
    <!-- You form will be rendere here -->
    {{ $this->form }}
</x-filament::page>

```
