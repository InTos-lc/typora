### Shell

#### Shell 变量

##### 使用变量

在Shell编程中，变量是用于存储数据值的名称，定义变量时，变量名不加**$**符号

```shell
your_name="lc"
```

**注意**：

1. shell编程的变量名命名规则与C语言一致

2. 变量名等号两边避免使用空格

3. 除了显示地直接赋值，还可以用语句给变量赋值，如：

   ```shell
   for file in 'ls /etc'
   for file in $(lc /etc)
   ```

##### 只读变量

```shell
#!/bin/bash

name="lc"
readonly name
```

##### 删除变量

```shell
#!/bin/bash
name="lc"
unset name
```

##### 变量类型

Shell支持不同类型的变量，其中一些主要类型包括：

1. **字符串变量**

   在shell中，变量通常被视为字符串。你可以使用单引号‘ ’或双引号” “来定义字符串

   ```shell
   name='lc'
   name_again="lc"
   ```

2. **整数变量**

   在一些shell中，你可以使用**declare**或**typeset**命令来声明整数变量。

   ```shell
   delcare -i my_integer=42
   ```

   如果将非整数数值赋给他，shell会尝试将其转换为整数

3. **数组变量**

   Sehll也支持数组，允许你在一个变量中存储多个值。

   ```shell
   my_array=(1 2 3 4 5)
   ```

   关联数组

   ```shell
   declare -A associative_array //声明关联数组
   associative_array["name"]="John" //用字符串”name“当键
   associative_array["age"]=30	//用字符串”age“当键
   
   echo ${associative_array["name"]}  //输出John
   echo ${associative_array["age"]} //输出30
   ```

   ```shell
   declare -A colors
   colors["red"]="#FF0000"
   colors["green"]="#00FF00"
   colors["blue"]="0000FF"
   
   echo "所有值 ${colors[@]}"
   echo "所有键 ${!colors[@]}"
   echo "数组长度 ${#colors[@]}"
   
   for key in "${!colors[@]}"; do
           echo "$key -> ${colors[$key]}"
   done
   
   ```

4. **环境变量**

   是由操作系统或用户设置的特殊变量，用于配置Shell的行为和影响其执行环境。例如，PATH变量包含了操作系统搜索可执行文件的路径：

   ```shell
   echo $PATH
   ```

5. ##### 特殊变量

   有一些特殊变量在Shell中具有特殊含义，例如**$0**表示脚本名称，**$1,$2**等表示脚本的参数。**$#**表示传递给脚本的参数数量，**$?**表示上一个命令的退出状态等。

   ```Shell
   ./hello.sh arg1 arg2 arg3
   ```

   | 特殊变量    | 含义                                                        |
   | ----------- | :---------------------------------------------------------- |
   | $0          | 脚本本身的名称                                              |
   | $1,$2,$3... | 第一，第二，第三个参数（最多9个时直接写，超过9个需用${10}） |
   | $#          | 传递给脚本参数个数                                          |
   | $@          | 所有参数(每个参数独立成串，推荐使用”$@“保留空格)            |
   | $*          | 所有参数（合并成一个字符串，默认以空格分隔）                |
   | $?          | 上一条命令的退出状态（0 表示成功）                          |
   | Shift       | 命令可以将位置参数向左移动，丢弃$1,原来的$2变成$1           |

   ```shell
   #!/bin/bash
   # 文件: sum_shift.sh
   total=0
   while [ $# -gt 0 ]; do
       total=$((total + $1))
       shift
   done
   echo "总和: $total"
   ```

   **shift**变量求和示例

   ```Shell
   $ ./sum_shift.sh 10 20 30 40
   总和: 100
   ```

#### Shell字符串

##### 单引号

```shell
str="this is a string"
```

单引号字符串的限制：

- 单引号里的任何字符串都会原样输出，单引号字符串中的变量是无效的；

- 单引号字符串中不能出现单独一个的单引号(对单引号使用转义符后也不行)，但可成对出现，作为字符串拼接使用

  ```Shell
  echo "It's a str"
  echo 'It'\''s a str'
  echo $'It\'s a str'
  ```

  输出结果

  ```Shell
  It's a str
  It's a str
  It's a str
  ```

##### 双引号

实例

```Shell
name="liangchao"
str="I know your name \"$name\"!\n"
echo -e $str
```

输出结果

```Shell
I know your name "liangchao"!
```

优点：

1. 双引号里可以有变量
2. 双引号里可以出现转义字符

##### 拼接字符串

实例:

1. 使用双引号拼接

   ```Shell
   #源字符串
   name="liangchao"
   #使用双引号拼接
   str="hello, "${name}"  !"
   str_1="hello, "$name" !"
   echo "$str" "$str_1"
   ```

   输出结果

   ```Sehll
   hello, liangchao !
   hello, liangchao !
   ```

2. 使用单引号拼接

   ```Shell
   #源字符串
   name='liangchao'
   str='hello, '$name' !'
   str_1='hello ,${name} !'
   echo "$str" "$str_1"
   ```

   输出结果

   ```shell
   hello, liangchao ! hello ,${name} !
   ```

##### 获取字符串长度

实例：

```Shell
string="liangchao"
echo ${#string}
```

输出结果

```
9
```

变量为字符串时，${#string}等价于${#string[0]};

```Shell
string="liangchao"
echo ${#string[0]}
```

输出结果

```
9
```

##### 提取字符串

以下实例从字符串第2个字符开始截取4个字符：

```
string="Liang Chao is so handsome"
```

