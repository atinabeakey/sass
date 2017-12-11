# sass
There are some example of sass
***
[README in English]() 
***
##### Sass在线转换 [https://www.sassmeister.com/]()
### Step 1:安装sass以及sass的环境搭建
    具体过程百度一下
***
### Step 2:使用
    SASS文件就是普通的文本文件，里面可以直接使用CSS语法。文件后缀名是.scss
***    
### Step 3:SASS提供四个编译风格的选项：
    　　* nested：嵌套缩进的css代码，它是默认值。
    　　* expanded：没有缩进的、扩展的css代码。
    　　* compact：简洁格式(紧凑输出方式)的css代码。
    　　* compressed：压缩后的css代码。
        生产环境当中，一般使用最后一个选项：
        sass --style compressed test.sass test.css
### Step 4:SASS监听某个文件或者某个目录  
```
//监听文件(watch a file)
sass --watch sass文件scss:css文件.css eg:sass --watch index.scss:style.css

//监听目录(watch a directory)
sass --watch sass文件夹名:css文件夹名 eg:sass --watch app/index:public/style
```
 ### Step 5:基本用法  
   #### 5.1>.嵌套
 ```
 //选择器嵌套
 div p{
    color:#000
 }
 上面css可写为
 div{
    p{
        color:#000
    }    
 }
 //属性嵌套(background-color)
 p {
 　　　border: {
 　　　　　color: red;
 　　　}
 　}
 注意，border后面必须加上冒号。
 在嵌套的代码块内，可以使用&引用父元素。比如a:link,a:visited,a:hover,a:active伪类，可以写成：
 　　a {
        &:link {color: #f00;}
        &:visited {color: #0f0;}
        &:hover {color: #ffb3ff;}
        &:active {color: #000;}
 　　}
 ```
 #### 5.2>. 变量
         SASS允许使用变量，所有变量以$开头。
         　　$color : #1875e7;　
         　　div {
         　　　color : $color ;
         　　}
         如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中。
         　　$side : left;
         　　.rounded {
         　　　　border-#{$side}-radius: 5px;
         　　}
#### 5.3>. 计算
        $Right =2
         body {
     　　　　margin: (14px/2);
     　　　　top: 50px + 100px;
     　　　　right: $Right * 10%;
     　　}
### Step 6:代码的重用
        SASS允许一个选择器继承另一个选择器,例如：
            .box1{
         　　　　border: 2px solid #f00;
         　　}
        box2继承box1 ：
            .box2 {
                @extend .box1;
                background:#1abfad
            }
### Step 7:mixin(重用的代码块)
        使用@mixin命令，定义一个代码块。
        　　@mixin left {
        　　　　float: left;
        　　　　margin-left: 10px;
        　　}
        使用@include命令，调用这个mixin。
        　　div {
        　　　　@include left;
        　　}
        mixin的强大之处，在于可以指定参数和缺省值。
        　　@mixin left($value: 10px) {
        　　　　float: left;
        　　　　margin-right: $value;
        　　}
        使用的时候，根据需要加入参数：
        　　div {
        　　　　@include left(20px);
        　　}
        下面是一个mixin的实例，用来生成浏览器前缀。
        　　@mixin rounded($vert, $horz, $radius: 10px) {
        　　　　border-#{$vert}-#{$horz}-radius: $radius;
        　　　　-moz-border-radius-#{$vert}#{$horz}: $radius;
        　　　　-webkit-border-#{$vert}-#{$horz}-radius: $radius;
        　　}
        使用的时候，可以像下面这样调用：
        　　#navbar li { @include rounded(top, left); }
        　　#footer { @include rounded(top, left, 5px); }
### Step 8:高级用法
#### 8.1：循环语句
        a>、支持for循环
            @for $i from 1 to 10{
                .border-#{$i} {
                    border: #{$i}px #dashed #e4e4e4
                }   
            }
            特别注意：再次提醒使用变量时加 $ ,引用变量时使用 #{} 包起来
        b>、支持while循环
            $i:6
            @while $i>0{
                .box#{$i} {
                    width： 20px * $i;
                }
                $i: $i - 2;
            }
        c>、each命令，作用与for类似：
           @each $num in a,b,c,d{
                .#{$num} {
                    background-image: url('img/#{$num}.jpg')
                }
           } 
#### 8.2：自定义函数
        SASS允许编写自己的函数
            @function even($n){
                @return $n*2;
            }
            li.navbar {
                width:even(50px) 
            }
       