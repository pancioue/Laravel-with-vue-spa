laravel with vue spa
===============
* php 7.2.5  
* laravel 7.30.4

建置專案
---------------
```
composer create-project --prefer-dist laravel/laravel [project-name]
```
* `--prefer-dist`不會保留版本控制，等於`git clone; rm -fr dir/.git`
  不加--prefer-dist也不會有git，所以其實不需要特別加此參數
* `--prefer-source` 會保留版控，等於`git clone`

> 版控不專指git，svn也是一樣


安裝 laravel/ui
----------------
```
composer require laravel/ui
```

安裝完laravel/ui之後，安裝frontend scaffolding(腳手架)
```
// Generate basic scaffolding...
// 修改package.json
php artisan ui bootstrap
php artisan ui vue
php artisan ui react

// Generate login / registration scaffolding...
// 除了修改package.json之外，產生登入auth相關檔案(包含頁面及controller等)
php artisan ui bootstrap --auth
php artisan ui vue --auth
php artisan ui react --auth
```
之後下npm install安裝套件


安裝 Vue Router
------------------
```
npm install vue-router --save-dev
```
> 這個指令只會安裝vue router，還是要另外執行`npm install`才行


vue component
----------------
在```resources/js/components```新增Home.vue及About.vue頁面  
```
<template>
    <div>
        this is home vue
    </div>
</template>
```

新增vue router設定
--------------
在`resources/js`底下新增`routes.js`
```
import Home from './components/Home.vue'
import About from './components/About.vue'

const routes = [
    {
        path: '/', component: Home
    },
    { 
        path: '/about', component: About
    }
]

export default routes
```

app.js載入routes設定
-----------------
```
import VueRouter from 'vue-router'
Vue.use(VueRouter)

import routes from './routes'
const router = new VueRouter({
    routes,
    mode: 'history'
})

const app = new Vue({
    el: '#app',
    router
});
```
可以看到`webpack.mix.js`
```
mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css');
```
resources/js/app.js是webpack開始編譯的載入點


產生blade掛載vue組件
---------------
新增`app.blade.php`
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="/css/app.css">
</head>
<body>
    <div id="app">
        <router-view></router-view>
    </div>

    <script src="/js/app.js"></script>
</body>
</html>
```


修改路由
--------------
`routes/web.php`把非api的路由導到app.blade
```
Route::get('/{path}', function () {
    return view('app');
})->where('path', '^((?!api).)*$');
```

測試
-------------
下`npm run dev`或`npm run watch`編譯  
一樣由`webpack.mix.js`
```
mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css');
```
可以看到編譯過後的檔案會放到`public/js`底下  

PHP's built-in development server
`php artisan serve`啟動serve  
web輸入`http://localhost:8000/`  

> vue-router的history模式是使用HTML5的`history.pushState`使的url轉跳無須重新加載頁面


參考網站:  
https://blog.johnsonlu.org/building-a-vue-spa-with-laravel/  
https://stackoverflow.com/questions/16205100/difference-between-composer-prefer-dist-and-prefer-source/46641804  
https://github.com/laravel/ui  
https://learnku.com/articles/4054/when-using-laravel-to-develop-spa-routing-correct-posture  
https://stackoverflow.com/questions/16205100/difference-between-composer-prefer-dist-and-prefer-source/46641804
