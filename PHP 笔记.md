---
typora-root-url: ./
---

 ###  PHP 笔记

[TOC]



#### 1. 静态变量

   ```php
   // 静态变量
   function fn() {
       static $i=0;
       $i++;
       echo '该函数一共被调用'.$i.'次<br/>';
   
   }
   fn();
   fn();
   fn();
   fn();
   fn();
   fn();
   ```

   ![](/images/Snipaste_2021-05-11_16-06-19.png)

#### 2.函数内部和外部是两个世界，外面的变量和里面的变量完全没有关系

```php
$a = 100;
function fn1() {
    echo $a;
}
fn1(); // 拿不到 100
echo $a; //100
```

#### 2.1 如果想让函数外部的变量方进函数内部使用

 1. 传参
    
    ```php
    $a = 100;
    function fn1($a) {
        echo $a;
    }
    fn1($a); // 100
    echo $a; // 100
    ```
    
2. global（推荐使用）
   
   ```php
   echo '<hr/>';
   $a = 100;
   function fn1() {
    global $a;
    echo $a;
   }
   fn1(); // 100
   ```

####  2.2 里面的变量放到外面使用只能靠 ==return==

```php
function fn1() {
    $b = 100;
    return $b;
}
$b = fn1();
```

#### 函数库

>将所有的函数单独放在同一个文件内，这个文件就叫函数库 引入函数库的方法（引入php文件的方法）<span style=' font-weight: 700;color:red;background:yellow;font-size:18px;font-family:\5FAE\8F6F\96C5\9ED1;'>4种</span> 

```php
include_once ('functions.php');
require_once ('functions.php');
require ('functions.php');
include ('functions.php');
	include 和 require 的区别：
    include 即使引入错误，也不影响下面的代码继续输出
 		require 引入错误，会终止页面所有代码的继续执行
    
    【注⭐】为了避免重复引入产生的报错，可以使用 include_once 和 require_once 来代替
```

#### array_rand() 随机输出数组的键值

```php 
$arr = array(
    '1' => 'a',
    '2' => 'b',
    '3' => 'c',
);
echo  array_rand($arr); // 1 或 2 或 3
echo $arr[array_rand($arr)]; // 随机输出关联数组的值
```

#### 数组的排序 ⭐

```php
$arr = array(
    '1' => 'a',
    '2' => 'b',
    '3' => 'c',
);
sort($arr); // 值的顺序排序 
p($arr); // p是封装好的打印函数
function p($arr) {
  echo '<pre>';
  echo print_r($arr);
  echo '</pre>'
}
有以下方法：⭐
  sort						 值的顺序排序，丢弃键值，排序之后变成索引数组
  rsort 					 值按照倒序排序,不会丢弃值，值会跟着键值（索引）一起
  krost						 键值按照倒序排序
```

#### 数组和字符串之间的转换 ⭐

```php
explode() 字符串转为数组 ⭐
  
$str = 'a,b,c|c|c|dd,ss|ee';
$str = explode('c|',$str);
p($str);
explode 第一个参数的字符串位置切开字符串
$str = explode('',$str); // 第一个参数不能为空
$str = str_split($str1); // 相当于 explode　方法的第一个参数为空

implode() 数组转换为字符串 ⭐
$arr1 = array('a','b','c');
$str1 = implode('&&',$arr1); //第一个参数是元素变成字符串后元素和元素之间的分割的字符
$str = implode('',$arr1); // 第一个参数可以为空
```

![](/images/Snipaste_2021-05-11_18-29-26.png)

#### 格式化输出，将字符串转换为需要的数据类型输出

~~~php
/*
 * 格式：
 *      小数格式      %f
 *      字符串格式    %s
 *      整数格式     %d
 * */
$str2 = 26.4130;
echo sprintf('%.2f',$str2).'元'; // 26.41元
							'%.3f' 保留3为小数						

printf()直接输出，类似 echo
sprintf()把结果保存到变量中，类似 return
 一般常用 sprintf()
  
用整数格式输出
  	echo sprintf('%d',$str2);
	保留两位小数，自动四舍五入
~~~

#### 字符串查找strpos() ⭐

```php
	$str4='hello world';
	echo strpos($str4,'o');//4,字符o在字符串$str4中第一次出现的索引位置
	echo strpos($str4,'w');//6,空格也算一个字符位置
	echo strpos($str4,'a');//false,找不到的字符返回false
	echo strpos($str4,'h');//0

		if(strpos($str4,'h')!==false){
		//echo 1;
	}else{
		//echo 2;
	}
解决查找到的索引为0位置的值，在if 判断中出现 fales的问题
  
	//strpos区分大小写
	//echo strpos($str4,'W');//false,区分大小写
 
	//stripos不区分大小写
	//echo stripos($str4,'W');//6
```

