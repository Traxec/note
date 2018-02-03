# 流行的Laravel扩展包
## 1.验证码 [mews/captcha](https://github.com/mewebstudio/captcha)
```
$ composer require "mews/captcha:~2.0"
$ php artisan vendor:publish
```
## 2.语言包 [overtrue/laravel-lang](https://github.com/overtrue/laravel-lang/)
```
$ composer require "overtrue/laravel-lang:~3.0"
```
## 3.图片处理包 [Intervention/image](https://github.com/Intervention/image)
```
$ composer require intervention/image
$ php artisan vendor:publish --provider="Intervention\Image\ImageServiceProviderLaravel5"
```
## 4.Debugbar [laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)
```
$ composer require "barryvdh/laravel-debugbar:~3.1" --dev
$ php artisan vendor:publish --provider="Barryvdh\Debugbar\ServiceProvider"
```
打开 config/debugbar.php，将 enabled 的值设置为：
```
'enabled' => env('APP_DEBUG', false),
```
修改完以后, Debugbar 分析器的启动状态将由 .env文件中 APP_DEBUG 值决定。
## 5.Active状态 [hieu-le/active:~3.5](https://github.com/letrunghieu/active)
```
$ composer require "hieu-le/active:~3.5"
```
安装完成后，在模板中使用：
```
<div class="collapse navbar-collapse" id="app-navbar-collapse">
    <!-- Left Side Of Navbar -->
    <ul class="nav navbar-nav">
        <li class="{{ active_class(if_route('topics.index')) }}"><a href="{{ route('topics.index') }}">话题</a></li>
        <li class="{{ active_class((if_route('categories.show') && if_route_param('category', 1))) }}"><a href="{{ route('categories.show', 1) }}">分享</a></li>
        <li class="{{ active_class((if_route('categories.show') && if_route_param('category', 2))) }}"><a href="{{ route('categories.show', 2) }}">教程</a></li>
        <li class="{{ active_class((if_route('categories.show') && if_route_param('category', 3))) }}"><a href="{{ route('categories.show', 3) }}">问答</a></li>
        <li class="{{ active_class((if_route('categories.show') && if_route_param('category', 4))) }}"><a href="{{ route('categories.show', 4) }}">公告</a></li>
    </ul>
```
上面代码看起来很复杂，但都是些重复的代码。我们需先理解好 active_class 函数的用法，此函数的定义如下：
```
/**
 * Get the active class if the condition is not falsy
 *
 * @param        $condition
 * @param string $activeClass
 * @param string $inactiveClass
 *
 * @return string
 */
function active_class($condition, $activeClass = 'active', $inactiveClass = '')
```
如果传参满足指定条件 (`$condition`) ，此函数将返回 `$activeClass`，否则返回 `$inactiveClass`。

此扩展包提供了一批函数让我们更方便的进行 `$condition` 判断：

1. if\_route() - 判断当前对应的路由是否是指定的路由；
2. if\_route_param() - 判断当前的 url 有无指定的路由参数。
3. if\_query() - 判断指定的 GET 变量是否符合设置的值；
4. if\_uri() - 判断当前的 url 是否满足指定的 url；
5. if\_route_pattern() - 判断当前的路由是否包含指定的字符；
6. if\_uri_pattern() - 判断当前的 url 是否含有指定的字符；
