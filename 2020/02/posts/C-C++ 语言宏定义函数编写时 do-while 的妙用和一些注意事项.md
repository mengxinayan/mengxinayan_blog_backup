标题：C/C++ 语言宏定义函数编写时 do-while 的妙用和一些注意事项
分类：编程.C
Tag：C语言，宏定义，技巧
-------------------------------------------
在 C/C++ 语言中，我们都知道可以用宏定义来编写函数，一般称为宏函数。如果一个宏函数比较复杂，那么在编写这样的宏函数是有一定技巧和注意事项的。文章给出一些我认为值得关注的地方，以及一些注意事项（个人建议），最后介绍了一种使用 do-while 语句来编写宏定义函数的技巧。下面我将从简单到复杂，以便于大家理解。下面的例子均采用 C 语言，C++与 C 语言相同，就不再赘述。

## 一个简单的例子

宏定义函数最简单的情况便是只有一条语句。下面我给出了四个例子，请仔细观察各个例子之间的区别，并尝试思考哪些是可以正确运行的。

```c
/* 例子 1 */
#include <stdio.h>

#define MACRO_FUNC() printf("Hello!\n")

int main()
{
    if(2 > 1)
        MACRO_FUNC()
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 2 */
#include <stdio.h>

#define MACRO_FUNC() printf("Hello!\n");

int main()
{
    if(2 > 1)
        MACRO_FUNC();
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 3 */
#include <stdio.h>

#define MACRO_FUNC() printf("Hello!\n");

int main()
{
    if(2 > 1)
        MACRO_FUNC()
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 4 */
#include <stdio.h>

#define MACRO_FUNC() printf("Hello!\n")

int main()
{
    if(2 > 1)
        MACRO_FUNC();
    else
        printf("Fail.\n");
    return 0;
}
```

相信细心的你已经发现了，它们的区别在于宏定义函数末尾有无分号，以及调用宏定义函数时末尾有无分号。宏定义可以简单的理解为直接替换，这样的替换是 **包括宏定义函数中的分号** ，那么想知道哪些例子是可以运行的，那么只需要将调用宏定义函数的语句，替换为宏定义函数的内容即可，替换后的结果如下：

```c
/* 例子 1 */
#include <stdio.h>

int main()
{
    if(2 > 1)
        printf("Hello!\n") /* 语句没有以分号结束，错误 */
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 2 */
#include <stdio.h>

int main()
{
    if(2 > 1)
        printf("Hello!\n");; 
/* 语句以两个分号结束，第二个分号使得 if 语句结束，else 语句无法找到对应的 if 语句，会产生错误 */
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 3 */
#include <stdio.h>

int main()
{
    if(2 > 1)
        printf("Hello!\n"); /* 正确 */
    else
        printf("Fail.\n");
    return 0;
}
```

```c
/* 例子 4 */
#include <stdio.h>

int main()
{
    if(2 > 1)
        printf("Hello!\n"); /* 正确 */
    else
        printf("Fail.\n");
    return 0;
}
```

根据上面代码中的注释和分析可以得知，上述示例中例 3、例 4 是正确的。二者的共同点是宏定义函数和调用宏定义函数后面分号的总数为 1，二者的区别是例 3 是在调用宏函数时后面没有添加分号，而例 4 是宏定义函数的定义后面没有添加分号。那么这两种方法更好一些呢？ 我个人的建议是例 4 的方法更好一些，下面我来解释一下原因：

一个宏函数可能会被多次调用，如果选择例 3 的方法，那么每次调用宏定义函数时都不需要写分号，看起来省事一点儿，但潜在的隐患很多，试想当你看到别人代码中一条语句是这样的 `MACRO_FUNC()` 而后面没有分号时，你会觉得很奇怪，可能会为其后面增加分号，在某些时刻它可以正常工作，但在上面的例子中会直接产生一个编译错误。如果你想采取例 3 那样的做法，那么你需要在编写代码时刻考虑是否应该添加分号。

而选用例 4 方法，虽然每次调用函数都需要添加分号，但是至少当你编写好宏定义函数后，你在编写其他代码时就不再需要考虑是否可以添加分号。同样地，用宏定义来定义一个常量时，例如：`#define SIZE 100`。我们也应该不在数字后面添加分号。

## 稍微复杂的例子

宏定义函数可以像正常的函数一样，执行一些复杂的功能，里面可以包含有多条语句。我们都知道，函数的语句都需要用花括号 { ... } 包围起来，宏定义函数也不例外。值得注意的是：宏定义中如果需要换行，那么需要在行尾添加续行符 —— 反斜杠 '\\'。最后一行因为已经到了结束，因此并不需要添加此符号 '\\'。续行符没有实际作用，只是为了宏定义函数方便阅读和编写。
示例代码如下：

```c
#include <stdio.h>

#define MACRO_FUNC() \
{ \
    printf("Hello\n"); \
    printf("World\n"); \
} /* 根据上面例子的描述，我们不应该在宏定义末尾添加分号 */

int main()
{
    if(2 > 1)
        MACRO_FUNC();
    else
        printf("Fail.\n");
    return 0;
}
```

根据上面提到的替换规则，宏定义的替换是所有内容的替换，包括分号，花括号等，注意，**续行符在替换时需要被忽略**。替换后的结果如下：

```c
#include <stdio.h>

int main()
{
    if(2 > 1)
    {
        printf("Hello\n");
        printf("World\n");
    }; /* 这个分号是调用 MACRO_FUNC(); 时末尾的分号 */
    else
        printf("Fail.\n");
    return 0;
}
```

if 后面的语句块右花括号又有了分号，导致 else 语句又无法找到对应的 if 语句而产生错误。看来还是需要用例 3 那样的写法，代码如下：

```c
#include <stdio.h>

#define MACRO_FUNC() \
{ \
    printf("Hello\n"); \
    printf("World\n"); \
} /* 根据上面例子的描述，我们不应该在宏定义末尾添加分号 */

int main()
{
    if(2 > 1)
        MACRO_FUNC() /* 末尾不添加分号 */
    else
        printf("Fail.\n");
    return 0;
}
```

上面的代码是可以正常运行的。可以自己思考一下。可是我还想用例 4 那样的写法，下面会讲到一个技巧来达到这个目的。

## 采用 do-while 语句

do-while 语句的一个特点便是，会优先执行一次语句块，而后再判断 while 中的条件是否成立。当我们把 while 设置为 `while(0)` 时，那么 while 条件永不成立，do 后面语句块中的代码只会执行一次。因此，宏定义多行代码用 `do { /* ... */ } while(0)` 包围起来便可以达到目的，来试一试吧。示例代码如下：

```c
#include <stdio.h>

#define MACRO_FUNC() \
    do \
    { \
        printf("Hello\n"); \
        printf("World\n"); \
    } while(0)
/* 根据上面例子的描述，我们不应该在宏定义末尾添加分号 */

int main()
{
    if(2 > 1)
        MACRO_FUNC();
    else
        printf("Fail.\n");
    return 0;
}
```

我们将调用宏定义函数的部分替换为宏定义中的内容来看一看：

```c
#include <stdio.h>

int main()
{
    if(2 > 1)
        do
        {
            printf("Hello\n");
            printf("World\n");
        } while(0); /* 分号来自调用宏定义函数末尾的分号 */
    else
        printf("Fail.\n");
    return 0;
}
```

可以发现上面替换后的结果是可以正常执行的。

## 总结

总结一下，文章中涉及到的内容:
1. 宏定义函数编写时需要换行时，需要使用续行符——反斜杠 '\\'
2. 宏定义函数可以理解为简单的替换，这样的替换包括分号，花括号等，但不包含分号。
3. 为了避免考虑在调用宏定义函数时末尾是否需要加分号，我们在宏定义结束处不添加分号
4. 可以使用 `do { /* ... */ } while(0)` 将宏定义中的多行代码包围起来。

