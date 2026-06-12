# C

## 函数学习

### sscanf函数

```C
sscanf(const char *str, const char *format,.....);
```

功能：可以把字符串中的内容按不同格式提取出来；

参数1：需要提取的字符串

参数2：需要提取的参数类型如：%d%x%s%f,....格式之间不能有分隔符；

参数3：存放提取出来的参数2

返回值：成功解析和赋值的个数，如果解析失败或没有匹配的数据项，则返回0；

示例：

```c
int Ture_ip(char *ip)
{
    int Count[4] = {0};
	if(ip == NULL)
    {
        printf("ip address Invalid\r\n");
        return 0;
    }
    
    int count = sscanf(ip, ""%d.%d.%d.%d"， &Count[0], &Count[1], &Count[2], &Count[3]));
    if(count != 4)
    {
    	printf("解析失败\r\n");  
        return 0;
    }
    for(int i = 0; i < 4; i++)
    {
        if(Count[i] < 0 || Count[i] > 255)
        {
            printf("ip 格式错误\r\n")
            return 0;
        }
    }
    return 1;
}
```

## malloc clloc realloc区别

1.malloc ：

原型：void *malloc(unsigned int num_bytes) num_bytes为所要申请的内存

2.clloc：

原型：void *clloc(size_t n, size_t size) 

n:为需要申请类型空间的个数

size:为一个类型空间的大小

3.relloc：

原型：relloc(void *ptr, size_t new_Size)

*ptr:指已经分配好的动态内存基地址

new_Size:指需要再分配多少内存空间

返回值：指向新空间的指针

示例：

```c
char *str;
str = malloc(64);

char *str
str = clloc(20, sizeof(char));

str = relloc(str, (sizeof(char) * 20));
```

### strtok_r函数

#### 原型：

char *strtok_r(char *str, const char *delim, char **saveptr)

str:带分割的字符串， 在第一次调用时，这个参数指向你想要分割的字符串。在后续调用中，这个参数应设置为NULL。

delim:分割符字符串。这是一个字符串集合，函数会用它里面的任何一个字符作为分割点。

saveptr: 这是一个指向char*的指针，函数用它来在多次调用之间保存字符串的剩余部分。

返回值：

成功时：返回指向下一个分割出的令牌的指针。

如果字符串不可分割则返回NULL；

#### 原理：

1. 第一次调用：

   - 将待分割的字符串str作为第一个参数。

   - 提供一个指向char*的指针saveptr（通常初始化为NULL， 但并非必须）。函数会初始化saveptr以供后续使用

2. 后续调用：

   - 将第一个参数str设置为NULL。
   - 使用同一个saveptr变量，函数会从上次保存的位置继续分割。

3. 结束

   - 当函数返回NULL时，表示分割结束。

#### 代码示例：

分割字符串“Hello，world - from C programming”,使用空格，逗号和横杠（“ ,-”）作为分隔符。

```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int mian()
{
	char str[] = "Hello world - from C programming";
	//分隔符
	const char *delim = " ,-";
	//用于保存内部状态的指针
	char *saveptr = NULL;
	//获取第一个令牌
	char *token = strtok_r(str, delim, &saveptr);
	while(token != NULL)
	{
		printf("Tokeen :%s\r\n", token);
		token = strtok_r(NULL, delim, &saveptr);
	}
	printf("\nriginal string now: \"%s\"\n", str);
	return 0;
}
```

#### 结果：

```
Token: Hello
Token: world
Token: from
Token: C
Token:programming

original string now:"Hello"
```

#### 注意：

1. 修改原字符串：它会在找到的分隔符位置上写入‘\0’, 来种植每个令牌。因此不能多字符串常量使用这个函数，否则会导致程序崩溃，必须使用字符数组。
2. 连续分隔符：如果字符串中有连续的分隔符（例如："a,,b"）,strtok_r函数会将它们视为一个分隔符， 不会返回空字符串令牌。
3. saveptr作用：saveptr是由函数内部维护的，不需要在调用之间手动修改它，只需要在循环中一直传递它的地址即可。
4. 可重入性：因为使用了独立的saveptr，你可以在同一个线程中同时处理多个字符串，互不干扰。
