# PHP 考題

- 基本程式邏輯
- 程式語言基本特性
- PHP + client
- PHP + DB
- SQL 語法
- value / reference
- 物件導向
- interface / abstract class
- magic methods
- static / self
- namespace
- SPL
- composer
- 效能相關
- 設計模式


## 基本程式邏輯

判斷式：

```
function y($x) {
    if ($x < 10) {
        return 'small';
    } elseif ($x > 10) {
        return 'large';
    } else {
        return 'medium';    
    }
    return 'error';
}

當執行 y(10) 時，會得到什麼結果： C

(A) small
(B) large
(C) medium
(D) error
```


迴圈：

```
$index = 10;
$count = 0;
for ($index = 0; $index < 5; $index++) {
    $count++;
}

迴圈執行完成以後，$index 的數值為 ___5___，$count 的數值為 ___5___
```


string 特性：

```
$str = "Hello" . "World";

以下何者正確： D

(A) strlen($str) == 10
(B) $str == "HelloWorld"
(C) $str[0] == "H"
(D) 以上皆是
```


array 特性：

```
$list = array(
    0,
    1,
    "Hello",
    "name" => "John",
);

以下何者為 **非**： C

(A) 陣列大小為 4
(B) $list["name"] == "John"
(C) $list[2] == 1
(D) $list[2] == "Hello"
```

switch ... case

```
function getScore($rank) {
    switch ($rank) {
        case "A":
            $score = 90;
            break;
        case "B":
            $score = 80;
            break;
        case "C":
            $score = 70;
        case "D":
            $score = 60;
        default:
            $score = 0;
    }
    returen $score;
}

執行 getScore("C") 之後，會得到哪個回傳值？ D

(A) 90
(B) 70
(C) 60
(D) 0
```




## PHP 語言特性


認識

```
下列哪一項工作，**無法** 使用 PHP 來完成？ C

(A) 從文字記錄擋中找出有用的資訊
(B) 進行資料挖掘 (data mining) 相關計算
(C) 在瀏覽器上執行 PHP 撰寫的程式
(D) 用來建立 JPEG 等影像檔
```

弱型別：

```
function isEquals($a, $b) {
    if ($a == $b) {
        return true;
    } else {
        return false;
    }
    return "N/A";
}

請問執行 isEquals('100', 100) 時，執行結果為何者： A

(A) true
(B) false
(C) runtime error
(D) "N/A"
```

字串轉型：

```
$value = "100" + "400";

請問 $value 的數值為： C

(A) PHP error，無法執行
(B) "100400"
(C) 500
(D) 以上皆非
```

引號：

```
$name = "John"
echo "Hello, \$name";

以下何者為輸出結果： B

(A) Hello, John
(B) Hello, $name
(C) Hello, name
(D) 以上皆非
```

陣列：

```
$default = array(
    "host" => "localhost",
    "username" => "root",
    "password" => "123",
);

$config = array_merge(array(
    "password" => "secret",
    "port" => 3306
), $default);


下列何者為 **非**： D

(A) $config["host"] == "localhost"
(B) $config["port"] == 3306
(C) $config["username"] == "root"
(D) $config["password"] == "secret"
```


錯誤類型

```
PHP 的錯誤分成多種類型，請問下列哪一種錯誤會使得程式中斷執行？ C

(A) Notice
(B) Warning
(C) Fatal
(D) 以上皆是
```



ternary operator
```
$accessLevel = 3;

$isAdmin = ($accessLevel <= 2 && $accessLevel > 0) ? true : false;

請問下列何者為 $isAdmin 的數值？ A

(A) true
(B) false
(C) null
(D) runtime error
```


empty() ：

```
下列何者為正確： C

(A) empty(array(0)) == true
(B) empty("Hello") == true
(C) empty("0") == true
(D) 以上皆非
```

list():

```
list($b, $a) == array($a, $b);

請問以上寫法是否可以調換 $a, $b 的數值： A

(A) 可
(B) 語法錯誤
(C) 資料型態錯誤
```


除錯

```
<?php

    $output = file_get_contents("http://www.google.com.tw");
    
    // debug on $output
    _________($output);
    exit();
    
請問上述程式若要除錯，底線位置應該使用哪個函式？ 

print_r, var_dump, var_export
```


include / require:

```
<?php
    
    $adminId = "root";

    @include "file-not-exists.php"; // 不存在的檔案
    
    echo $adminId;

請問以下何者正確： B

(A) runtime error
(B) 輸出「root」
(C) syntax error
(D) 以上皆非
```




require 相對路徑：

```
專案的檔案結構如下：

.
├── config.php
├── index.php
└── lib
    └── lib.php
    
其中程式的內容為：

index.php

    <?php
    
    require_once "config.php";
    require_once "lib/lib.php";
    
    echo getEnvironment();
    
config.php

    <?php

    $env = "dev";
    
lib/lib.php

    <?php

    require_once "../config.php";
    
    function getEnvironment() {
        global $env;
        return $env;  
    }
    
請問在專案根目錄執行 php index.php 以後，會得到下列哪個結果： A

(A) runtime error
(B) dev
(C) null
(D) 以上皆非
```


function name 大小寫：

```
function test_a() { return 'lower case' };
function test_A() { ruturn 'upper case' };

echo test_A();

請問上述程式執行後，會回傳哪個數值？ C

(A) lower case
(B) upper case
(C) PHP error
```

PHP features
```
function set(string $key, $value): void { };

請問上方的語法，哪一個版本的 PHP 可以執行

- [ ] 5.3
- [ ] 5.6
- [v] 7.1
- [v] 7.2
```

PHP stand alone server
```
$ php -S localhost:8080

請問哪些幾個版本的 PHP 可以執行以上指令？

- [ ] 5.0
- [ ] 5.3
- [v] 5.4
- [v] 5.6
```

追蹤新聞
```
目前可供正式環境使用、最新的 PHP 版本是那一版？ 7.2
```



## PHP + client

session vs. cookie
```
請簡述 session 與 cookie 的差別？
```


session:
```
<html>
<header>
    <title>使用者設定</title>
</heder>
<body>
    <?php
		if ($isLoggined == false) {
			header('Location: login.php');
		}
	?>
</body></html>

請問當 $isLoggined == false 時，瀏覽器開啟網頁以後會？ B

(A) 瀏覽器自動導向 admin.php
(B) 網頁不會重新導向
(C) PHP syntax error
```



cookie
```
if ($isloggedin) {
    setcookie("user", $userId);
    setcookie("password", $userPassword);
    setcookie(
        "avatarPicture",
        base64_encode(file_get_contents($pathOfPicture))
    );
}

請問當使用者登入成功時，cookies 中的哪一些資料會遇到問題？請簡述問題。

(A) 不會遇到問題
(B) user：_______________________________
(C) password：___________________________
(D) avatarPicture：______________________
```

HTTP GET / POST, form input type
```
form.html

    <html>
    <body>
        <form method="GET" action="submit.php">
            <label>帳號：</label>
            <input type="TEXT" name="username"> <br />

            <label>密碼：</label>
            <input type="TEXT" name="password"> <br />

            <input type="SUBMIT" value="登入">
        </form>
    </body>
    </html>
    
    
submit.php

    <?php
    
    if (isUserExists($_GET["username"])) {
        if ($_GET["password"] === getUserPasswrod($_GET["username"])) {
            echo "登入成功";
        }
    }
    
    
請問上方的使用者登入表單、帳號密碼檢查程式，是否有問題？若有的話，請簡述之。

    - password 的 input type 建議改為 "password"
    - form method 應該要使用 POST
```




HTTP GET limitation

```
<form method="GET" action="submit.php">
    <label>暱稱：</label>
    <input type="TEXT" name="username"> <br />

    <label>留言：</label>
    <textarea rows="20" cols="80" placeholder="我想說 ...">
    </textarea>

    <input type="SUBMIT" value="送出留言">
</form>

請標示出上方 HTML 有需要修正的地方，並簡述之。

    - textarea 的文字可能很長，不建議使用 HTTP GET
```



MVC

```
MVC 為 Model、View、Controller 三個名詞的縮寫。

請簡單說明 Model、View 及 Controller 的定義

    - MVC 目的主要是希望可以將前端、資料處理、流程控制的程式拆開以便維護
    - Model: 負責處理資料
    - View: 負責畫面的呈現
    - Controller: 負責流程控制
```


XSS

```
請填寫需要使用到的 function name： htmlentities, htmlspecialchars

    <?php

    $keyword = $_POST["key"];
    echo "關鍵字「" . _________($keyword) . "」的查詢結果";

    /* 下略 */
```


## PHP + DB

Injection

```
$user = $_POST["user"];
$password = $_POST["password"];

$result = queryFromUserDb("
    SELECT *
    FROM users
    WHERE username = '$user'
        AND password = '$password'
");

上方為使用者登入程式，請標出需要修改的地方
```








## SQL

ER model understanding / basic SQL writing with JOIN 3 tables

![ER-diagram](https://i.imgur.com/Vc0Rr0y.png)
```
請參考上圖，依照下列要求，且出查詢用的 SQL：

    找出所有員工名稱 (name)，其所屬公司 ID 為 "100" 且部門名稱包含「IT」字串
    
    SELECT e.name
    FROM
        Employee as e,
        Department as d,
        Company as c
    WHERE
        e.d_id = d.id
        AND d.c_id = c.id
        
        AND c.id = "100"
        AND d.name like "%IT%"
```



## value / reference

陣列

```
$a = array(1, 2, 3);
$b = $a;

$b[] = 4;
$a = array();

echo count($a) . ", " . count($b);

請問下列何者為輸出結果？ C

(A) 4, 4
(B) 3, 4
(C) 0, 4
(d) 0, 0
```

pass by reference

```
<?php

function last(array &$list) {
    $last = null;
    foreach ($list as $val) {
        $last = $val;
    }
    $list = array($last);
}

$list = array(1, 2, 3);
last($list);

echo count($list);

請問下列何者為執行結果： C

(A) syntax error
(B) 3
(C) 1
(D) runtime error
```

## 物件導向

概念：

```
請問下列何者不是物件導向的特性： D

(A) 封裝
(B) 多型
(C) 繼承
(D) 以上皆是
```

建構子

```
class User { }

請問下列何者為正確的建構子 (constructor) 寫法？ B, C

(A) public function User() {}
(B) public function __construct() {}
(C) private function __construct() {}
(D) public function constructor() {}
```


預設 visibility

```
<?php

class User {
    function getName() {
        return "John";
    }
}

$user = new User();
echo $user->getName();

請問下列何者為程式執行結果： B

(A) syntax error
(B) John
(C) runtime error
(D) null
```

`$this` 關鍵字

```
class User {
    function set($name) {
        $name = $name;
    }

    function get() {
        return $name;
    }
}

$user = new User();
$user->set("John");
var_export( $user->get() );

請問程式執行結果為何？ C

(A) John
(B) syntax error
(C) null
(D) "" (空字串)
```

封裝、繼承

```
class A {
    private $property = "hello";
    
    private function getProperty() {
        echo $this->property;
    }
}
class B extends A {
    private $property = "world";
    
    public function say() {
        echo $this->getProperty();
    }
}

$user = new B();
$user->say();

請問下列何者為執行結果： D

(A) hello
(B) world
(C) syntax error
(D) runtime error
```

封裝
```
class User {
    public $name = "";

    public function set($name) {
        $this->name = $name;
    }

    public function get() {
        return $this->name;
    }
}

$user = new User();
$user->set('John');
$user->name = 'Bob';
echo $user->get();

請問下列何者為執行結果？ C

(A) "" (空字串)
(B) John
(C) Bob
(D) runtime error
```

PHP 沒有支援 多型

```
class Man {
    public function eat(string $food) {
        echo "Caz caz caz ... \n";
    }

    public function eat(array $foods) {
        foreach ($foods as $food) {
            echo "Caz caz caz ... \n";
        }
    }
}

請標記出上述程式有問題的地方，並簡述之。

    - PHP 不支援多型，以上程式等於於重複宣告相同的函式
```


object reference

```
class Man {
    public $name;
}

$man = new Man();
$john = $man;
$bob = $man;

$john->name = 'John';
$bob->name = 'Bob';

echo $john->name . ", " . $bob->name;

請問程式執行以後的結果為何？ D

(A) John, John
(B) John, Bob
(C) Bob, John
(D) Bob, Bob
```



## interface / abstract class

abstract class 繼承

```
abstract class Human {
    public function greeting() {
        echo 'yoo';
    }
}

class American extends Human {
}

$man = new American();
$man->greeting();

請問下列何者為執行結果： B

(A) runtime error
(B) yoo
(C) null
(D) syntax error
```

資料型別判斷
```
abstract class Human {
    public function greeting() {
        echo 'yoo';
    }
}

class American extends Human {
}

$man = new American();
$state = $man instanceof Human;

請問程式執行以後，$state 的數值為何？ A

(A) true
(B) false
(C) null
(D) runtime error
```

interface visibility

```
interface Talkable {
    public function greetings();
}

class American implements Talkable {
    protected function greetings() {
        echo "hello";
    }
}

$man = new American();
$man->greetings();

請問下列何者正確： C

(A) hello
(B) "" (空字串)
(C) runtime error
```



## magic methods

getter
```
class Man {
    private $name;
    private $weight;

    public function __construct() {
        $this->name = '';
        $this->weight = 60;
    }

    public function getName() {
        return $this->name;
    }

    public function setName($name) {
        $this->name = $name;
    }

    public function __get($variable) {
        return $this->$variable;
    }
}

$john = new Man();
echo $john->weight;

請問上述程式執行的結果為何？ (A)

(A) 60
(B) syntax error
(C) runtime error
```


## static / self

static variable in function
```
function check() {
    static $n = 0;

    return $n++;
}

echo check() . ", " . check() . ", " . check();

請順上述程式的執行結果為何？ (C)

(A) 0, 0, 0
(B) 1, 1, 1
(C) 0, 1, 2
(D) syntax or runtime error
```




## namespace



## SPL

Exceptions

```
$e = new InvalidArgumentException();

$state = $e instanceof Exception;

請問下列何者為 $state 的數值： A

(A) true
(B) false
(C) syntax error
(D) runtime error
```

## composer

系統需求

```
請問下列哪個 PHP 版本，可以使用 composer？

- [ ] 5.1
- [v] 5.4
- [v] 5.6
- [v] 7.0
```

用途

```
請簡述 composer 在 PHP 專案中的用途。

    - 管理 library 之間的依賴關係 (dependency)
    - 解決 library 版本衝突問題 (conflict)
```

## 效能相關


array hashed key
```
今天有 100 萬筆資料，未來可能需要查詢特定數值是否存在。
請問你會使用下列哪個方法儲存這些資料？ C

(A) array as value
(B) SplObjectStorage
(C) array as key
(B) string 並使用特殊字元分隔
```


## 其他

PSR

```
最近很紅的 PSR 是什麼？請簡述優缺點。

    - 制定基本開發規範 / interface，使協同作業 (co-work) 難度下降
    - 細節也有規範，導致實作彈性下降
```

## 設計模式

singleton
```
function getDbConnection() {
    static $conn = null;
    
    if ($conn === null) {
        $conn = new PDO("mysql:dbname=test;host=127.0.0.1");
    }
    return $conn;
}

請問上述程式，使用了哪一種設計模式 (design pattern)？ B

(A) 觀察者模式 (observer pattern)
(B) 獨體模式 (singleton pattern)
(C) 工廠模式 (fatocry pattern)
(D) 狀態模式 (state pattern)
```


# Reference

- [Awesome-interview](https://github.com/MaximAbramchuck/awesome-interview-questions#php)
