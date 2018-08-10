## Welcome to use the CodeIgniter HMVC extension！


If you still don't know what HMVC is, please move to Wikipedia first:

[http://en.wikipedia.org/wiki/HMVC](http://en.wikipedia.org/wiki/HMVC)


一I have always felt that CodeIgniter lacks a good HMVC architecture, and I personally think that several current HMVC third-party libraries are not very good. Some have to modify the source code of CI, and some have to introduce new syntax. This is not my favorite. Way, so I thought about a plan myself, I hope that you can give us valuable advice. The feature of this HMVC is that it does not modify the CI source code, does not introduce a new syntax, and is fully utilizing the powerful extension mechanism of CI.

The current extension is to add the modules directory in the application directory, each module has its own directory, and the module can have a subdirectory, such as `application/modules/目录/模块名/....`

Each module has its own MVC architecture, such as `application/modules/模块名/controllers`，`application/modules/模块名/models`，`application/modules/模块名/views` the load module in view:

```php
$this->load->module('module_name/controller/method');
```

The default controller in URL routing can also be used here. The default method is the index() method, which is consistent with the normal controller. If you want to pass parameters：

```php
$this->load->module('module_name/controller/method', array('parameter1', 'parameter2', ...));
```

If you need to return the result of the module and do not want to output to the screen, you can set the third parameter to TRUE：

```php
$this->load->module('module_name', array('parameter1', 'parameter2', ...), TRUE);
```

If you need to access a method of a module from a URL, the URL rule looks like this：

```
http://domain/index.php/module/module_name/controller/method
```

In fact `/module` the contents of the front and rear of the incoming `$this->load->module()` consistent with the parameters。

If you want to pass a parameter via a URL, add it directly after the URL：

```
http://domain/index.php/module/module_name/controller/method/parameter 1/parameter 2/..../parameter n
```

In addition, the URI here can use routing rules, which means that any URL can be used, as long as the last route is in accordance with the above rules, such as to use such a URL：

```
http://domain/index.php/m/module_name/controller/method
```

You can add a routing rule in routers.php：

```php
$route['m/(:any)/(:any)/(:any)/(:any)'] = 'module/$1/$2/$3/$4';
```

or

```php
$route['m/(.*)'] = 'module/$1';
```

If you want to generate a URL in a module's view that accesses a method of the current controller's current controller, you can write it in the view：

```php
<?php echo $this->module_url('Method name/parameter 1/..../parameter n to be accessed'); ?>
```

If you want to generate the URL of the method of the other controller of the current module, you can do this：

```php
<?php echo $this->module_url('Method name to access/Parameter 1/..../Parameter n', 'Controller name'); ?>
```

Basically, if everyone is unclear, I will answer in detail in the forum:：

[http://codeigniter.org.cn/forums/thread-1319-1-1.html](http://codeigniter.org.cn/forums/thread-1319-1-1.html)

After the zip package is decompressed, there are simple examples of controllers, models, views, and modules, and they contain only the code required by the module, not the CI core code.。


### update record

-   2017.07.01 supports CodeIgniter 3.1.5。
-   2016.11.20 supports CodeIgniter 3.1.2 & fixes some bugs。
-   2016.4.25 supports CodeIgniter 3.0.6
-   2013.4.18 Fixed a bug in the module that could not access the current module variables。
-   2012.4.8 Fixes a bug in the module that cannot be used by such a library after automatically loading the class library。
-   2012.2.19 Added support for CodeIgniter CodeIgniter 2.1.0。
-   2011.8.9 Fixed a bug where autoload was invalid when accessing the Module from a URL。
-   2011.7.28 Added the ability to access the Module from a URL。
-   2011.4.13 Fixed the bug that autoload is invalid for module。
-   2011.4.11 supports the latest CI 2.0.0, completely rewriting all HMVC code for PHP5。
-   2011.1.8 supports loading one or more modules directly into the controller; repairing bugs that load the class library error in the module；
-   2010.12.15 supports direct loading of modules in the controller。
-   2010.8.7 Fixed a bug that loaded the Model error in the constructor of the Module。
