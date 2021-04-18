laravel with vue
================

### Create project
```
composer create-project --prefer-dist laravel/laravel:~7.0 [project-name]

```

### Install laravel/ui
```
composer require laravel/ui:~2.4
```

### Install vue scaffolding
```
php artisan ui vue
```

### Install dependencies
```
npm install
```

### Build code
```
npm run dev
```
or
```
npm run watch
```

### Add new blade file
add `app.blade.php` file
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <example-component></example-component>
    </div>
    <script src="/js/app.js"></script>
</body>
</html>
```

### Modify routes
```
Route::get('/', function () {
    return view('app');
});
```

### Testing
```
php artisan serve
```
