# phper-knowledge
> 该仓库主要记录php开发遇到的知识点。
> 针对相应知识点，附上便于理解的链接，若有更好的资源，欢迎提交更正交流。

## 基础篇
* [了解大部分数组处理函数](http://php.net/manual/zh/ref.array.php)
* [字符串处理函数](http://php.net/manual/zh/ref.strings.php)  [区别 mb_ 系列函数](http://php.net/manual/zh/book.mbstring.php)
* [& 引用，结合案例分析](https://secure.php.net/manual/zh/language.references.php)
* [== 与 === 区别](https://stackoverflow.com/questions/80646/how-do-the-php-equality-double-equals-and-identity-triple-equals-comp)
* [isset 与 empty 区别](https://blog.csdn.net/jiaobuchong/article/details/41807011)
* [全部魔术函数理解](http://php.net/manual/zh/language.oop5.magic.php)
* [超全局变量 魔术变量 魔术函数总结](http://www.cnblogs.com/wangxin-king/p/5669336.html)
* [static、$this、self 区别](https://juejin.im/post/5af11926f265da0b9a69e80f)
* private、protected、public、final 区别 ```public实例能调用 protected实例不能直接调用 final不能继承和重写```
* OOP 思想
* 抽象类、接口 分别使用场景
* [Trait 是什么东西](http://php.net/manual/zh/language.oop5.traits.php)
* [echo、print、print_r 区别(区分出表达式与语句的区别)](https://stackoverflow.com/questions/1647322/whats-the-difference-between-echo-print-and-print-r-in-php)
* [__construct 与 __destruct 区别](http://php.net/manual/zh/language.oop5.decon.php)
* static 作用（区分类与函数内）[手册](http://php.net/manual/zh/language.oop5.static.php) 、[SOF](https://stackoverflow.com/questions/7508284/static-variables-in-php)
* [__toString() 作用](http://php.net/manual/en/language.oop5.magic.php#object.tostring)
* [单引号`'`与双引号`"`区别](https://stackoverflow.com/questions/3446216/what-is-the-difference-between-single-quoted-and-double-quoted-strings-in-php#answer-3446286)
* [常见 HTTP 状态码，分别代表什么含义](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)
* [301](https://zh.wikipedia.org/wiki/HTTP_301) 什么意思 [404](https://zh.wikipedia.org/wiki/HTTP_404) 呢?

## 进阶篇
* Autoload、Composer 原理 [PSR-4](https://laravel-china.org/topics/2081/psr-specification-psr-4-automatic-loading-specification) 、[原理](https://segmentfault.com/a/1190000014948542)
* Session 共享、存活时间
   * 存活: 默认存活gc_maxlifetime=1440s,默认gc概率1/100 gc_probability/gc_divisor 
   * 共享: 文件同步rsync，redis或mc存储，mysql存储
* 异常处理 [详情](https://juejin.im/entry/5987d2ff6fb9a03c314fe732)
* [如何 foreach 迭代对象](https://secure.php.net/manual/zh/class.iterator.php) Iterator 接口 或者 IteratorIterator 
* [如何数组化操作对象 `$obj[key];`](https://secure.php.net/manual/zh/class.arrayaccess.php) ArrayAccess接口 或者 
* [如何函数化对象 `$obj(123);`](http://php.net/manual/en/language.oop5.magic.php#object.invoke) __invoke()或者Closure 预定义接口
* yield 是什么，说个使用场景 [yield](https://www.oschina.net/translate/cooperative-multitasking-using-coroutines-in-php)
* [PSR 是什么，PSR-1, 2, 4, 7](http://psr.phphub.org/)
* 如何获取客户端 IP 和服务端 IP 地址
    * [客户端 IP](https://stackoverflow.com/questions/3003145/how-to-get-the-client-ip-address-in-php)    
    * [服务端 IP](https://stackoverflow.com/questions/5800927/how-to-identify-server-ip-address-in-php)
    * 了解代理透传 实际IP 的概念
* 如何开启 PHP 异常提示
    * php.ini 开启 `display_errors` 设置 `error_reporting` 等级
    * 运行时，使用 `ini_set(k, v);` 动态设置
* [如何返回一个301重定向](https://stackoverflow.com/questions/7324645/php-header-redirect-301-what-are-the-implications) 
    * **[WARNING]** 一定当心设置 301 后脚本会继续执行，不要认为下面不会执行，必要时使用 `die` or `exit`
* 如何获取扩展安装路径
    * `phpinfo();` 页面查找 `extension_dir`
    * 命令行 `php -i |grep extension_dir`
    * 运行时 `echo ini_get('extension_dir');`
* 字符串、数字比较大小的原理，注意 0 开头的8进制、0x 开头16进制
    * 字符串比较大小，从左(高位)至右，逐个字符 ASCII 比较
    * 注意字符串和数字组合比较 var_dump('10a' == 10); //true 10a转型10
* BOM 头是什么，怎么除去
    * win记事本保存默认开头`0xEF`,`0xBB`,`0xBF`（UTF8）
    * 导入含有BOM的html时，页面始终不置顶(php 当成字符串导入)
    * trim($str, "\xEF\xBB\xBF");[检测、去除](https://stackoverflow.com/questions/10290849/how-to-remove-multiple-utf-8-bom-sequences-before-doctype)
* 什么是 MVC 
* [依赖注入实现原理](https://segmentfault.com/a/1190000010846788)
* [如何异步执行命令](http://www.laruence.com/2008/04/14/318.html)
  * `<img src="xxx.php">` 
  * ajax异步 但需要onload后执行
  * 异步执行php脚本 如执行shell脚本exec() 但只能本机脚本
  * 使用curl 但是timeout最小是1s
  * 使用fsockopen 需要自己拼写发送内容
* [模板引擎是什么，解决什么问题、实现原理（Smarty、Twig、Blade）](https://www.kancloud.cn/bozoyan/app/212223)
* [如何实现链式操作 `$obj->w()->m()->d();`](https://segmentfault.com/a/1190000008159324)
  * __call() & call_user_func_array() 唤醒调用对象未知方法
  *  调用的函数return $this
* Xhprof 、Xdebug 性能调试工具使用
* [索引数组 `[1, 2]` 与关联数组 `['k1'=>1, 'k2'=>2]` 有什么区别](https://www.onmpw.com/m/view.php?aid=238)
  * 存在覆盖的问题 $arr1 = array('one','two','three',1=>'four'); // 'one four three'
  * 关联数组有限   $arr1 = array(1=>'four','one','two','three'); // '1=>four 2=>one 3=>two' 
* [缓存的使用方式、场景](https://zhuanlan.zhihu.com/p/40091810)
* [foreach 引用问题](https://www.cnblogs.com/eleven24/p/7422170.html?utm_source=debugrun&utm_medium=referral) 
```
   $a = [1,2,3];
   foreach ($a as $v){}
   var_dump($a); // 123
   foreach ($a as &$v){}
   var_dump($a); //123
   # unset($v); 或换了$v
   foreach ($a as $v){}
   var_dump($a); // 122
```

## 实践篇
* 给定二维数组，根据某个字段排序 [array_multisort() 多维数组排序](https://www.cnblogs.com/Dong-Ge/p/5583753.html)
  * `array_multisort($field1, SORT_DESC, $field2, SORT_ASC, $data);`
* 如何判断上传文件类型，如：仅允许 jpg 上传 [详情](http://www.111cn.net/phper/21/0742a78eb9237635bd6d2b8e2a7817a9.htm)
   ```$ext = $_FILES['file']['type']; 或者 解析文件名(explode()) ```
* 不使用临时变量交换两个变量的值 `$a=1; $b=2;`  =>  `$a=2; $b=1;` [传送门](https://blog.csdn.net/litchi_yang/article/details/78300562)
  ``` 
   方案一 int 相加后相减  
   方案二 先拼接$a .= $b; $b=str_replace($b,'',$a)...
  ```
* strtoupper 在转换中文时存在乱码，你如何解决？```php echo strtoupper('ab你好c'); ```
  * [方案传送门] https://blog.csdn.net/whd526/article/details/77871433
  ``` 方案一 mb_convert_case($str,MB_CASE_TITLE,'UTF-8');
      方案二 自定义函数，使用str_split()按一字节切割，然后ord()转asscii 判断字母asscii
  ```  
* Websocket、Long-Polling、Server-Sent Events(SSE) 区别 [传送门](https://www.jianshu.com/p/4aa085b9984b) 
* "Headers already sent" 错误是什么意思，如何避免 
  * [避免header('xxx')之前使用echo print等输出](https://www.kancloud.cn/iyouki/how_to_interview/566636)

## 算法篇
* 快速排序（手写）
* 冒泡排序（手写）
* 二分查找（了解）
* 查找算法 KMP（了解）
* 深度、广度优先搜索（了解）
* LRU 缓存淘汰算法（了解，Memcached 采用该算法）

## 数据结构篇（了解）
* 堆、栈特性 [详细](https://www.cnblogs.com/yanlingyin/archive/2011/12/10/2283303.html)
  * 堆 自行申请和释放空间，存放对象，空间比较大
  * 栈 系统自动申请释放，执行程序，随函数被调用时分配的空间
* 队列 
* 哈希表
* 链表

## 对比篇
* Cookie 与 Session 区别 (深入分析区别)[https://juejin.im/entry/5766c29d6be3ff006a31b84e]
  * cookie  存客户端 用户可见 仅支持字符串二进制 缓存时间长 服务器压力少 
  * session 存服务端 用户不可见 支持多种数据类型 缓存时间有限 服务器压力大
* `GET` 与 `POST` 区别 (传送门)[https://www.zhihu.com/question/28586791]
* `include` 与 `require` 区别
* `include_once` 与 `require_once` 区别
* Memcached 与 Redis 区别 [传送门](PHP include()和require()方法的区别)
  * mc   多线程非阻塞IO 只支持K-V类型 key有几率被刷走，非持久化 通过key hashmap分布式
  * redis 单线程阻塞复用IO 支持多类型 key不被刷走，持久化存储，redis-cluster分布式
* MySQL 各个存储引擎、及区别（一定会问 MyISAM 与 Innodb 区别）[传送门](https://blog.csdn.net/zgrgfr/article/details/74455547)
* HTTP 与 HTTPS 区别 [传送门](https://juejin.im/entry/58d7635e5c497d0057fae036)
* Apache 与 Nginx 区别 [传送门](https://blog.csdn.net/jcjc918/article/details/46665919)
* define() 与 const 区别 [传送门](https://segmentfault.com/a/1190000009559436)
  * define可用在条件判断中，不成立的条件中，定义的不生效，成功定义后全局可用，可是表达式赋值
  * const不可用在条件判断中，不过可定义在类中，不可表达式赋值，必须是标量
* traits 与 interfaces 区别 及 traits 解决了什么痛点？
  * traits 类似插件 use XXX 直接使用
  * interfaces 接口协议，不带实现方法
* Git 与 SVN 区别

## 数据库篇
* MySQL
    *[CRUD](https://blog.csdn.net/qq_28261343/article/details/53044019)
    * [50个基础sql](https://blog.csdn.net/fashion2014/article/details/78826299/) 
    * JOIN、LEFT JOIN 、RIGHT JOIN、INNER JOIN [传送门](https://www.cnblogs.com/blueoverflow/p/4714470.html)
    * join 索引等优化 [传送门](https://www.jianshu.com/p/6864abb4d885)
    * UNION， UNION ALL 
    * GROUP BY + COUNT + WHERE 组合案例
    * [常用 MySQL 函数，如：now()、md5()、concat()、uuid()等](https://www.w3schools.com/sql/sql_ref_mysql.asp)
    * `1:1`、`1:n`、`n:n` 各自适用场景
    * 了解触发器是什么，说个使用场景 [传送门](https://blog.csdn.net/qq_32575047/article/details/80305027)
    * 数据库优化手段
        * 索引、联合索引（命中条件）(传送门1)[https://blog.csdn.net/qq_21987433/article/details/79753551]
        * 分库分表（`水平分表`、`垂直分表`）
        * (分区)[http://mysql.taobao.org/monthly/2017/11/09/]
        * 会使用 `explain` 分析 SQL 性能问题，了解各参数含义 (传送门)[https://blog.csdn.net/wangyy130/article/details/51418880]
            * 重点理解 `type`、`rows`、`key`
        * Slow Log（有什么用，什么时候需要）(传送门)[https://www.cnblogs.com/kerrycode/p/5593204.html]
          * mysqldumoslow 日志汇总
          * show variables like '%slow_query_log%';
     * 锁了解 (传送门)[https://juejin.im/post/5b82e0196fb9a019f47d1823]
        * 悲观锁，排他锁，共享锁的了解
        * 死锁的出现和解决 
* MSSQL(了解)
    * 查询最新5条数据
* NOSQL
    * Redis、Memcached、MongoDB
    * 对比、适用场景（可从以下维度进行对比）
        * 持久化
        * 支持多钟数据类型
        * 可利用 CPU 多核心
        * 内存淘汰机制
        * 集群 Cluster
        * 支持 SQL
        * 性能对比
        * 支持事务
        * 应用场景
    * 你之前为了解决什么问题使用的什么，为什么选它？

## 服务器篇
* 查看 CPU、内存、时间、系统版本等信息
* find 、grep 查找文件
* awk 处理文本
* 查看命令所在目录
* 自己编译过 PHP 吗？如何打开 readline 功能
* 如何查看 PHP 进程的内存、CPU 占用
  ```
  ps -aux | grep php-fpm
  top -p pid
  ```
* 如何给 PHP 增加一个扩展 (phpize安装拓展)[https://blog.csdn.net/Aaroun/article/details/78225114]
* 修改 PHP Session 存储位置、修改 INI 配置参数(配置说明)[https://blog.csdn.net/soonfly/article/details/52175614]
* 负载均衡有哪几种，挑一种你熟悉的说明其原理 [4种](https://www.jianshu.com/p/da6e562fa3a6)
* 数据库主从复制 M-S 是怎么同步的？是推还是拉？会不会不同步？怎么办 
   *(传送门)[https://juejin.im/entry/592287ae128fe1005c2e4f6c]
   *(不同步解决)[https://blog.51cto.com/13407306/2067333]
* 如何保障数据的可用性，即使被删库了也能恢复到分钟级别。你会怎么做。
* 数据库连接过多，超过最大值，如何优化架构。从哪些方便处理？(传送门)[https://blog.csdn.net/comeoncomputer/article/details/78649988]
* 502 大概什么什么原因？ 如何排查  504呢？(传送门)[https://blog.51cto.com/silencezone/1703413]

## 架构篇
* 偏运维（了解）：
    * 负载均衡（Nginx、HAProxy、DNS）
    * 主从复制（MySQL、Redis）
    * 数据冗余、备份（MySQL增量、全量 原理）
    * 监控检查（分存活、服务可用两个维度）
    * MySQL、Redis、Memcached Proxy 、Cluster 目的、原理
    * 分片
    * 高可用集群
    * RAID
    * 源代码编译、内存调优
* 缓存
    * 工作中遇到哪里需要缓存，分别简述为什么
* 搜索解决方案
* 性能调优
* 各维度监控方案(传送门)[https://zhuanlan.zhihu.com/p/33470183]
* 日志收集集中处理方案(ELK)[https://www.ibm.com/developerworks/cn/opensource/os-cn-elk/index.html]
* 国际化(传送门)[]
* 数据库设计(传送门)[https://zhuanlan.zhihu.com/p/25960208]
* 静态化方案(传送门)[https://blog.csdn.net/qq_15096707/article/details/50809197]
* 画出常见 PHP 应用架构图(传送门)[https://segmentfault.com/a/1190000008016139]

## 框架篇
* ThinkPHP（TP）、CodeIgniter（CI）、Zend（非 OOP 系列）
* Yaf、Phalcon（C 扩展系）
* Yii、Laravel、Symfony（纯 OOP 系列）
* Swoole、Workerman （网络编程框架）
* 对比框架区别几个方向点
    * 是否纯 OOP
    * 类库加载方式（自己写 autoload 对比 composer 标准）
    * 易用性方向（CI 基础框架，Laravel 这种就是高开发效率框架以及基础组件多少） 
    * 黑盒（相比 C 扩展系）
    * 运行速度（如：Laravel 加载一大堆东西）
    * 内存占用

## 设计模式
* 单例模式（重点）(传送门)[https://segmentfault.com/a/1190000006062259]
* 工厂模式（重点）
* 观察者模式（重点）(传送门)[https://segmentfault.com/a/1190000007531552]
* 依赖注入（重点）(传送门)[https://segmentfault.com/a/1190000010846788]
* 装饰器模式(传送门)[https://segmentfault.com/a/1190000007544975]
* 代理模式(传送门)[https://segmentfault.com/a/1190000007547503]
* 组合模式

## 安全篇
* SQL 注入 (mysql_real_escape_string mysqli和pdo 预处理)[https://segmentfault.com/a/1190000008117968]
* XSS 与 CSRF (htmlspecialchars过滤 get post区分  token 和 referer校验)[http://jartto.wang/2017/12/15/xss-and-csrf/]
* 输入过滤 (goto)[https://laravelacademy.org/post/4610.html]
* Cookie 安全  ( | + 加密 httponly)[https://segmentfault.com/q/1010000007347730]
* 禁用 `mysql_` 系函数
* 数据库存储用户密码时，应该是怎么做才安全 (sha加密 md5+salt)
* 验证码 Session 问题 (验证通过后清空)[https://itopic.org/nonsense-captcha.html]
* 安全的 Session ID （让即使拦截后，也无法模拟使用）
   * (位数长，固定时间无效,重要业务加独立密码)[https://www.jianshu.com/p/c4b32eb24894]
* 目录权限安全 770 750 640
* 包含本地与远程文件
* 文件上传 PHP 脚本 (检查文件头部 后缀名，重命名文件)[https://thief.one/2016/09/22/%E4%B8%8A%E4%BC%A0%E6%9C%A8%E9%A9%AC%E5%A7%BF%E5%8A%BF%E6%B1%87%E6%80%BB-%E6%AC%A2%E8%BF%8E%E8%A1%A5%E5%85%85/]
* `eval` 函数执行脚本
* `disable_functions` 关闭高危函数
* FPM 独立用户与组，给每个目录特定权限
* 了解 Hash 与 Encrypt 区别

## 高阶篇
* PHP 数组底层实现 （HashTable + Linked list）
* Copy on write 原理，何时 GC
   (手册)[http://php.net/manual/zh/features.gc.php]
   (其余)[https://www.jianshu.com/p/d73b3ca418b0]
* PHP 进程模型，进程通讯方式，进程线程区别
  * (php 进程模型)[http://taobaofed.org/blog/2015/11/24/nodejs-php-process-manager/]
  * (php 进程通讯)[https://www.jianshu.com/p/08bcf724196b]
  * (进程线程区别)[http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html]
* yield 核心原理是什么 (传送门)[https://newt0n.github.io/2017/02/10/PHP-%E5%8D%8F%E7%A8%8B%E5%8E%9F%E7%90%86/]
* PDO prepare 原理 (绑定变量 相当于预设输入是字符串)
* PHP 7 与 PHP 5 有什么区别 (传送门)[http://www.runoob.com/php/php7-new-features.html]
* Swoole 适用场景，协程实现方式 (swoole文档)[https://wiki.swoole.com/wiki/page/760.html]

## 前端篇
* 原生获取 DOM 节点，属性
* 盒子模型
* CSS 文件、style 标签、行内 style 属性优先级
* HTML 与 JS 运行顺序（页面 JS 从上到下）
* JS 数组操作
* 类型判断
* this 作用域
* .map() 与 this 具体使用场景分析
* Cookie 读写
* JQuery 操作
* Ajax 请求（同步、异步区别）随机数禁止缓存
* Bootstrap 有什么好处
* 跨域请求 N 种解决方案
* 新技术（了解）
    * ES6
    * 模块化
    * 打包
    * 构建工具
    * vue、react、webpack、
    * 前端 mvc 
* 优化
    * 浏览器单域名并发数限制
    * 静态资源缓存 304 （If-Modified-Since 以及 Etag 原理）
    * 多个小图标合并使用 position 定位技术 减少请求
    * 静态资源合为单次请求 并压缩
    * CDN
    * 静态资源延迟加载技术、预加载技术
    * keep-alive
    * CSS 在头部，JS 在尾部的优化（原理）


## 网络篇

* IP 地址转 INT
* 192.168.0.1/16 是什么意思
* DNS 主要作用是什么？
* IPv4 与 v6 区别

## 网络编程篇
 
* TCP 三次握手流程 [传送门](https://www.cnblogs.com/buxiangxin/p/8336022.html)
* TCP、UDP 区别，分别适用场景(传送门)[https://blog.csdn.net/u013777351/article/details/49226101]
* [OSI七层协议](https://blog.csdn.net/yaopeng_2005/article/details/7064869)
* 有什么办法能保证 UDP 高可用性(了解)
* TCP 粘包如何解决？
* 为什么需要心跳？
* 什么是长连接？
* HTTPS 是怎么保证安全的？
* 流与数据报的区别
* 进程间通信几种方式，最快的是哪种？
* `fork()` 会发生什么？

## API 篇

* RESTful 是什么 (阮一峰)[https://www.ruanyifeng.com/blog/2011/09/restful.html]
  * 如何设计RESTful (阮一峰)[http://www.ruanyifeng.com/blog/2018/10/restful-api-best-practices.html]
  * (php 实现RESTful) [https://my.oschina.net/crazymus/blog/521523]
* 如何在不支持 `DELETE` 请求的浏览器上兼容 `DELETE` 请求
  * form表单添加 ```< input type = hidden name = _method value = DELETE>``` 
  (传送门)[< input type = hidden name = _method value = DELETE>]
* 常见 API 的 `APP_ID` `APP_SECRET` 主要作用是什么？阐述下流程 
   * app_id 开发者账号，app_key(账号权限)+app_secret(账号密码)  (传送门)[https://blog.csdn.net/fuxx__/article/details/68927764]
  
* API 请求如何保证数据不被篡改？
  * https，sign排序签名，数据加密
* JSON 和 JSONP 的区别 
* 数据加密和验签的区别 (传送门)[https://blog.csdn.net/simonchi/article/details/38531971]
  * 数据加密 公钥加密，私钥解密，保证接收方数据安全
  * 数据签名 私钥加密，公钥解密，保证发送方数据安全，确保自己发送而不是别人
* RSA 是什么
* API 版本兼容怎么处理 (传送门)[https://juejin.im/post/5977f8ba5188255b9a6ad820]
  * url参数加版本号?v=2, header头部添加版本号
  * 通过token参数 服务端确认权限和版本
  * token 生成原理(传送门)[https://blog.csdn.net/zhu_xiao_yuan/article/details/77017196]
* 限流（木桶、令牌桶）(传送门)[https://www.jianshu.com/p/a59c13e70582]
* OAuth 2 主要用在哪些场景下 
   * (oauth2 流程)[http://www.heibaiketang.com/blog/show/21.html]
   * 接口授权，用户权限
* JWT (传送门)[http://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html]
* PHP 中 `json_encode(['key'=>123]);` 与 `return json_encode([]);` 区别，会产生什么问题？如何解决
  * 输出
    ```
      json_encode(['key'=>123]);
      return json_encode([]);
      
      #输出
      string(11) "{"key":123}"
      string(2) "[]"
    ```
   * 区别 {}是对象（key是string），[]是数组（key是int） (传送门)[https://blog.csdn.net/weihuiblog/article/details/79124364]

## 拓展项
* 了解常用语言特性，及不同场景适用性。
   * PHP VS Golang
   * PHP VS Python
   * PHP VS JAVA
* 了解 PHP 扩展开发
* 熟练掌握 C
