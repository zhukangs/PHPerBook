# 问题与简答

## PHP篇

### echo、print、print_r、var_dump 区别

> `echo`和`print`是语言结构、`print_r`和`var_dump`是普通函数

- echo：输出一个或多个字符串
- print：输出字符串
- print_r：打印关于变量的易于理解的信息
- var_dump：打印关于变量的易于理解的信息(带类型)

### isset 和 empty 的区别

isset：检测变量是否已设置并且非 NULL

empty：判断变量是否为空，变量为 0/false 也会被认为是空；变量不存在，不会产生警告

### static、self、$this 的区别

static：static 可以用于静态或非静态方法中，也可以访问类的静态属性、静态方法、常量和非静态方法，但不能访问非静态属性

self：可以用于访问类的静态属性、静态方法和常量，但 self 指向的是当前定义所在的类，这是 self 的限制

$this：指向的是实际调用时的对象，也就是说，实际运行过程中，谁调用了类的属性或方法，$this 指向的就是哪个对象。但 $this 不能访问类的静态属性和常量，且 $this 不能存在于静态方法中

### include、require、include_once、require_once 的区别

require 和 include 几乎完全一样，除了处理失败的方式不同之外。require 在出错时产生 E_COMPILE_ERROR 级别的错误。换句话说将导致脚本中止而 include 只产生警告（E_WARNING），脚本会继续运行

include_once 语句在脚本执行期间包含并运行指定文件。此行为和 include 语句类似，唯一区别是如果该文件中已经被包含过，则不会再次包含。如同此语句名字暗示的那样，只会包含一次

### 常见数组函数

array_count_values — 统计数组中所有的值

array_flip — 交换数组中的键和值

array_merge — 合并一个或多个数组

array_multisort — 对多个数组或多维数组进行排序

array_pad — 以指定长度将一个值填充进数组

array_pop — 弹出数组最后一个单元(出栈)

array_push — 将一个或多个单元压入数组的末尾(入栈)

array_rand — 从数组中随机(伪随机)取出一个或多个单元

array_keys — 返回数组中部分的或所有的键名

array_values — 返回数组中所有的值

count — 计算数组中的单元数目，或对象中的属性个数

sort — 对数组排序

拓展阅读  [《PHP基础函数》](https://www.zam9.com/blog/php_basic01)

### Cookie 和 Session

Cookie：PHP 透明的支持 HTTP cookie 。cookie 是一种远程浏览器端存储数据并以此来跟踪和识别用户的机制

Session：会话机制(Session)在 PHP 中用于保持用户连续访问Web应用时的相关数据

### 预定义变量

对于全部脚本而言，PHP 提供了大量的预定义变量

超全局变量 — 超全局变量是在全部作用域中始终可用的内置变量

```
$GLOBALS — 引用全局作用域中可用的全部变量
$_SERVER — 服务器和执行环境信息
$_GET — HTTP GET 变量
$_POST — HTTP POST 变量
$_FILES — HTTP 文件上传变量
$_REQUEST — HTTP Request 变量
$_SESSION — Session 变量
$_ENV — 环境变量
$_COOKIE — HTTP Cookies
$php_errormsg — 前一个错误信息
$HTTP_RAW_POST_DATA — 原生POST数据
$http_response_header — HTTP 响应头
$argc — 传递给脚本的参数数目
$argv — 传递给脚本的参数数组

```

- 超全局变量

PHP 中的许多预定义变量都是“超全局的”，这意味着它们在一个脚本的全部作用域中都可用。在函数或方法中无需执行 global $variable; 就可以访问它们

超全局变量：$GLOBALS、$_SERVER、$_GET、$_POST、$_FILES、$_COOKIE、$_SESSION、$_REQUEST、$_ENV

### 传值和传引用的区别

传值导致对象生成了一个拷贝，传引用则可以用两个变量指向同一个内容

### 构造函数和析构函数

构造函数：PHP 5 允行开发者在一个类中定义一个方法作为构造函数。具有构造函数的类会在每次创建新对象时先调用此方法，所以非常适合在使用对象之前做一些初始化工作

析构函数：PHP 5 引入了析构函数的概念，这类似于其它面向对象的语言，如 C++。析构函数会在到某个对象的所有引用都被删除或者当对象被显式销毁时执行

### 魔术方法

__construct()， __destruct()， __call()， __callStatic()， __get()， __set()， __isset()， __unset()， __sleep()， __wakeup()， __toString()， __invoke() 等方法在 PHP 中被称为"魔术方法"（Magic methods）

拓展阅读 [《PHP魔术方法》](https://www.zam9.com/blog/php_margic)

### public、protected、private、final 区别

对属性或方法的访问控制，是通过在前面添加关键字 public（公有），protected（受保护）或 private（私有）来实现的。被定义为公有的类成员可以在任何地方被访问。

public: 公有类型

- 在子类中可以通过 self::属性名(或方法名)  调用public方法或属性,parent::方法名 调用父类方法
- 在实例中可以能过 $obj->属性名(或方法名) 来调用　public类型的方法或属性

protected: 受保护类型

- 在子类中可以通过 self::属性名(或方法名) 调用protected方法或属性,parent::属性名(或方法名) 调用父类方法。
- *在实例中不能通过 $obj->属性名(或方法名) 来调用  protected类型的方法或属性*

private: 私有类型

- 该类型的属性或方法只能在该类中使用


- *在该类的实例、子类中、子类的实例中都不能调用私有类型的属性和方法*

PHP 5 新增了一个 final 关键字。如果父类中的方法被声明为 final，则子类无法覆盖该方法。如果一个类被声明为 final，则不能被继承。

### 类的静态调用和实例化调用

- 占用内存

静态方法在内存中只有一份，无论调用多少次，都是共用的

实例化不一样，每一个实例化是一个对象，在内存中是多个的

- 不同点

静态调用不需要实例化即可调用

静态方法不能调用非静态属性，因为非静态属性需要实例化后，存放在对象里

静态方法可以调用非静态方法，使用 self 关键字。php 里，一个方法被 `self::` 后，自动转变为静态方法

调用类的静态函数时不会自动调用类的构造函数

### php.ini 配置选项

- 配置选项

| 名字                  | 默认   | 备注                                       |
| ------------------- | ---- | ---------------------------------------- |
| short_open_tag      | "1"  | 是否开启缩写形式(`<? ?>`)                        |
| precision           | "14" | 浮点数中显示有效数字的位数                            |
| disable_functions   | ""   | 禁止某些函数                                   |
| disable_classes     | ""   | 禁用某些类                                    |
| expose_php          | ""   | 是否暴露 PHP 被安装在服务器上                        |
| max_execution_time  | 30   | 最大执行时间                                   |
| memory_limit        | 128M | 每个脚本执行的内存限制                              |
| error_reporting     | NULL | 设置错误报告的级别 `E_ALL` & ~`E_NOTICE` & ~`E_STRICT` & ~`E_DEPRECATED` |
| display_errors      | "1"  | 显示错误                                     |
| log_errors          | "0"  | 设置是否将错误日志记录到 error_log 中                 |
| error_log           | NULL | 设置脚本错误将被记录到的文件                           |
| upload_max_filesize | "2M" | 最大上传文件大小                                 |
| post_max_size       | "8M" | 设置POST最大数据限制                             |

```
php -ini | grep short_open_tag //查看 php.ini 配置
```

- 动态设置

```
ini_set(string $varname , string $newvalue);

ini_set('date.timezone', 'Asia/Shanghai'); //设置时区
ini_set('display_errors', '1'); //设置显示错误
ini_set('memory_limit', '256M'); //设置最大内存限制
```

### php-fpm.conf 配置

| 名称                      | 默认                                | 备注                                       |
| ----------------------- | --------------------------------- | ---------------------------------------- |
| pid                     |                                   | PID文件的位置                                 |
| error_log               |                                   | 错误日志的位置                                  |
| log_level               | notice                            | 错误级别 alert:必须立即处理、error:错误情况、warning:警告情况、notice:一般重要信息、debug:调试信息 |
| daemonize               | yes                               | 设置 FPM 在后台运行                             |
| listen                  | ip:port、port、/path/to/unix/socket | 设置接受 FastCGI 请求的地址                       |
| pm                      | static、ondemand、dynamic           | 设置进程管理器如何管理子进程                           |
| request_slowlog_timeout | '0'                               | 慢日志记录阀值                                  |
| slowlog                 |                                   | 慢请求的记录日志                                 |

### 502、504 错误产生原因及解决方式

#### 502

502 表示网关错误，当 PHP-CGI 得到一个无效响应，网关就会输出这个错误

- `php.ini` 的 memory_limit 过小
- `php-fpm.conf` 中 max_children、max_requests 设置不合理
- `php-fpm.conf` 中 request_terminate_timeout、max_execution_time 设置不合理
- php-fpm 进程处理不过来，进程数不足、脚本存在性能问题

#### 504

504 表示网关超时，PHP-CGI 没有在指定时间响应请求，网关将输出这个错误

- Nginx+PHP 架构，可以调整 FastCGI 超时时间，fastcgi_connect_timeout、fastcgi_send_timeout、fastcgi_read_timeout

#### 500

php 代码问题，文件权限问题，资源问题

#### 503

超载或者停机维护

### 如何返回一个301重定向

```
header('HTTP/1.1 301 Moved Permanently');
header('Location: https://blog.maplemark.cn');
```

### PHP 与 MySQL 连接方式

#### MySQL

```
$conn = mysql_connect('127.0.0.1:3306', 'root', '123456');
if (!$conn) {
    die(mysql_error() . "\n");
}
mysql_query("SET NAMES 'utf8'");
$select_db = mysql_select_db('app');
if (!$select_db) {
    die(mysql_error() . "\n");
}
$sql = "SELECT * FROM `user` LIMIT 1";
$res = mysql_query($sql);
if (!$res) {
    die(mysql_error() . "\n");
}
while ($row = mysql_fetch_assoc($res)) {
    var_dump($row);
}
mysql_close($conn);
```

#### MySQLi

```
$conn = @new mysqli('127.0.0.1:3306', 'root', '123456');
if ($conn->connect_errno) {
    die($conn->connect_error . "\n");
}
$conn->query("set names 'utf8';");
$select_db = $conn->select_db('user');
if (!$select_db) {
    die($conn->error . "\n");
}
$sql = "SELECT * FROM `user` LIMIT 1";
$res = $conn->query($sql);
if (!$res) {
    die($conn->error . "\n");
}
while ($row = $res->fetch_assoc()) {
    var_dump($row);
}
$res->free();
$conn->close();
```

#### PDO

```
$pdo = new PDO('mysql:host=127.0.0.1:3306;dbname=user', 'root', '123456');
$pdo->exec("set names 'utf8'");
$sql = "SELECT * FROM `user` LIMIT 1";
$stmt = $pdo->prepare($sql);
$stmt->bindValue(1, 1, PDO::PARAM_STR);
$rs = $stmt->execute();
if ($rs) {
    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
        var_dump($row);
    }
}
$pdo = null;
```

### MySQL、MySQLi、PDO 区别

#### MySQL

- 允许 PHP 应用与 MySQL 数据库交互的早期扩展
- 提供了一个面向过程的接口，不支持后期的一些特性

#### MySQLi

- 面向对象接口
- prepared 语句支持
- 多语句执行支持
- 事务支持
- 增强的调试能力

#### PDO

- PHP 应用中的一个数据库抽象层规范
- PDO 提供一个统一的 API 接口，无须关心数据库类型
- 使用标准的 PDO API，可以快速无缝切换数据库

### 数据库持久连接

把 PHP 用作多进程 web 服务器的一个模块，这种方法目前只适用于 Apache。

对于一个多进程的服务器，其典型特征是有一个父进程和一组子进程协调运行，其中实际生成 web 页面的是子进程。每当客户端向父进程提出请求时，该请求会被传递给还没有被其它的客户端请求占用的子进程。这也就是说当相同的客户端第二次向服务端提出请求时，它将有可能被一个不同的子进程来处理。在开启了一个持久连接后，所有请求 SQL 服务的后继页面都能够重用这个已经建立的 SQL Server 连接。

### MVC 的理解

MVC 包括三类对象。模型 Model 是应用对象，视图 View 是它在屏幕上的表示，控制器 Controller 定义用户界面对用户输入的响应方式。不使用 MVC，用户界面设计往往将这些对象混在一起，而 MVC 则将它们分离以提高灵活性和复用性

### 主流 PHP 框架特点

#### Laravel

易于访问，功能强大，并提供大型，强大的应用程序所需的工具

- 简单快速的路由引擎
- 强大的依赖注入容器
- 富有表现力，直观的数据库 ORM
- 提供数据库迁移功能
- 灵活的任务调度器
- 实时事件广播

#### Symfony

- Database engine-independent
- Simple to use, in most cases, but still flexible enough to adapt to complex cases
- Based on the premise of convention over configuration--the developer needs to configure only the unconventional
- Compliant with most web best practices and design patterns
- Enterprise-ready--adaptable to existing information technology (IT) policies and architectures, and stable enough for long-term projects
- Very readable code, with phpDocumentor comments, for easy maintenance
- Easy to extend, allowing for integration with other vendor libraries

#### CodeIgniter

- 基于模型-视图-控制器的系统
- 框架比较轻量
- 全功能数据库类，支持多个平台
- Query Builder 数据库支持
- 表单和数据验证
- 安全性和 XSS 过滤
- 全页面缓存

#### ThinkPHP

- 采用容器统一管理对象
- 支持 Facade
- 更易用的路由
- 注解路由支持
- 路由跨域请求支持
- 验证类增强
- 配置和路由目录独立
- 取消系统常量
- 类库别名机制
- 模型和数据库增强
- 依赖注入完善
- 支持 PSR-3 日志规范
- 中间件支持
- 支持 Swoole/Workerman 运行

### 对象关系映射/ORM

#### 优点

- 缩短编码时间、减少甚至免除对 model 的编码，降低数据库学习成本
- 动态的数据表映射，在表结构发生改变时，减少代码修改
- 可以很方便的引入附加功能(cache 层)

#### 缺点

- 映射消耗性能、ORM 对象消耗内存
- SQL 语句较为复杂时，ORM 语法可读性不高(使用原生 SQL)