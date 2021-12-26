# 1-Scala-Basic

![](https://www.runoob.com/wp-content/uploads/2015/12/scala-icon.png)

## 环境配置和Scala安装

### Docker

这里的scala我选择在docker的 ubuntu 容器里面进行安装和之后学习。 所以需要先把docker里面的ubuntu环境先配置好。

1. **拉取和进入 ubuntu 镜像** `docker pull ubuntu:13.10` `docker run -it ubuntu` 由于从docker hub里面拉下来的ubuntu image里面基本什么包都没有， 需要自己安装一下一些常用工具, 比如 vim， curl, git `apt-get install vim curl git`
2. **在ubuntu里面安装java** `apt-get update` 安装 java jdk, 或者jre， 不过一般jdk已经包括了jre， 可以只安装jdk就好 `apt-get install default-jdk` `apt-get install default-jre` 检查java环境是否安装成功 `#: java`, `#: javac`
3. **安装scala** 默认安装scala 2.x 版本 `apt-get install scala` 测试scala `#: scala`， 退出scala时用 `:q` 或`:quit` 命令

安装scala的另外一种方式是安装`sbt`工具， 它是用来管理比较大的scala项目的， 可以参考[官网](https://docs.scala-lang.org/scala3/getting-started.html)

1. **安装Python 和spark** 由于学习scala的目的是学习大数据spark， 所以这里也一起把pyspark安装上去。

* 安装python `apt-get update` `apt-get install python3.8` `apt-get install pip`
*   安装pyspark 安装pyspark的方法有几种， 可以参考 [官网](https://spark.apache.org/docs/latest/api/python/getting\_started/install.html). 其中一种方法是直接下载源码来跑， 步骤如下

    1. 从[PySpark下载地址](https://spark.apache.org/downloads.html) 下载对应的版本pyspark， 比如 spark-3.2.0-bin-hadoop3.2.tgz
    2. 解压： `tar -xzvf spark-3.2.0-bin-hadoop3.2.tgz` 得到 spark-3.2.0-bin-hadoop3.2 目录
    3. 在 `~/.bashrc` 文件最后增加下面环境变量， 让python能够识别出pyspark的路径 `export SPARK_HOME=<your-pyspark-path>`

    `export PYTHONPATH=$(ZIPS=("$SPARK_HOME"/python/lib/*.zip); IFS=:; echo "${ZIPS[*]}"):$PYTHONPATH` 4. 进入python3.8 调用pyspark检查调用情况

## Scala 语法

### 定义包

Scala 使用 package 关键字定义包，在Scala将代码定义到某个包中有两种方式： 第一种方法和 Java 一样，在文件的头定义包名，这种方法就后续所有代码都放在该包中 可以在一个文件中定义多个包。

```scala
package com.runoob
class HelloWorld
//或者
package com.runoob {
  class HelloWorld 
}
```

### 数据类型

Scala 里面的所有类型都是class， 不是 原生类型。 除了Byte, Int, Char, String, Long, Boolean, Float, Short, Double外， 还有 Unit, Any, Null, Nothing, AnyRef.

* Unit 等同于void， 都是无值
* Null: null 或空引用
* Any: 所有其他类型的超类Super Class
* AnyRef： 是Scala里面所有引用类型的基类BaseClass
* Nothing: 是Scala如何其他类型的子类， 是最底层的类

### 变量

Scala 的变量用 `val`关键字定义。 Scala里面对变量的数据类型定义有下面3中方法：

1. 对变量定义以及赋值

```
val var_name: DataType = value
// 例子
val myVal: String = "Foo"；
```

1. 只对变量定义 不赋值

```
val myval: String；
```

1. 直接对变量赋值 **不定义变量类型的话，一定要赋值**

```scala
val myval = "value"；
```

另外Scala的语句的分割符`;`分号在语句最后可加可不加。

1. 多值赋值

* 同时赋予相同值

```scala
//同时给a, b 赋予100， 相同的值
val a, b= 100
```

* 同时赋予不同值， 使用**tuple** 这里和python不一样，**一定要加括号**

```scala
//同时给a, b 赋予100， 相同的值
val a, b= (100,200)
```

### 修饰词public， private， protected

和Java一样， Scala有public， private， protected 关键词对函数， 变量， 类进行修饰。 使用方法： `private [x] <被修饰对象>`, 这里的x指代某个所属的包、类或单例对象。如果写成private\[x],读作"这个成员除了对\[…]中的类或\[…]中的包中的类及它们的伴生对像可见外，对其它所有类都是private。

例子

```scala
package bobsrockets{
    package navigation{
        private[bobsrockets] class Navigator{
         protected[navigation] def useStarChart(){}
         class LegOfJourney{
             private[Navigator] val distance = 100
             }
            private[this] var speed = 200
            }
        }
        package launch{
        import navigation._
        object Vehicle{
        private[launch] val guide = new Navigator
        }
    }
}
```

类 Navigator 被标记为 private\[bobsrockets] 就是说这个类对包含在 bobsrockets 包里的所有的类和对象可见。

### 运算符

Scala的运算符和C， python一样， 支持 `!=`,`==`, `>=`, `<=`, `&`, `$$`, `>>`, `<<`等。 另外scala也支持自加， 自乘等表示式， 如 `a-=1`, `b*=3` 等

### 逻辑表达式

Scala 的 if, else, for, while, `do..while`等和C一样。但是Scala 不支持 `break`, `continue`的操作。 使用break时要用到类。 比如调用 Breaks 类的break

```scala
// 导入以下包
import scala.util.control._

// 创建 Breaks 对象
val loop = new Breaks;

// 在 breakable 中循环
loop.breakable{
    // 循环
    for(...){
       ....
       // 循环中断
       loop.break;
   }
}
```

### 函数定义

Scala 中使用 `val` 语句可以定义函数，`def` 语句定义方法

* Scala 类的方法定义

```scala
def functionName ([参数列表]) : [return type] = {
   function body
   return [expr]
}
```

方法声明

```scala
def functionName ([参数列表]) : [return type]
```

* 例子

```scala
class Test{
  //定义方法
  def m(x: Int) = x + 3
  //定义函数
  val f = (x: Int) => x + 3
  println(f(4))
}
```

Scala 这里用的 `val f = (x: Int) => x + 3` 中，`f` 为函数名， 后面接输入的参数列表和对应的类型， 再加 箭头`=>`， 最后是公式。 这个有点像python的`lambda x:x+3` 的匿名函数写法

## Reference

[Java 安装教程](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04#:\~:text=The%20easiest%20option%20for%20installing%20Java%20is%20using,Java%20installation%20called%20the%20JDK%20%28Java%20Development%20Kit%29.)

[scala 安装教程](https://medium.com/@josemarcialportilla/installing-scala-and-spark-on-ubuntu-5665ee4b62b1#:\~:text=Installing%20Scala%20and%20Spark%20on%20Ubuntu%20Step%201%3A,see%20the%20scala%20REPL...%20Step%203%3A%20Install%20Spark)

[PySpark 安装教程](https://spark.apache.org/docs/latest/api/python/getting\_started/install.html)

https://sparkbyexamples.com/spark/different-ways-to-create-a-spark-dataframe/
