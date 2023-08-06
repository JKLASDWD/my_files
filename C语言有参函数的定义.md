自定义函数 C语言

如果函数不接收用户传递的数据，那么定义时可以不带参数。如下所示：

dataType functionName()

{
  //body
}

- dataType 是返回值类型，它可以是C语言中的任意数据类型，例如 int、float、char 等。
- functionName 是函数名，它是[标识符](http://c.biancheng.net/view/1770.html)的一种，命名规则和标识符相同。函数名后面的括号`( )`不能少。
- body 是函数体，它是函数需要执行的代码，是函数的主体部分。即使只有一个语句，函数体也要由`{ }`包围。
- 如果有返回值，在函数体中使用 return 语句返回。return 出来的数据的类型要和 dataType 一样。

例如，定义一个函数，计算从 1 加到 100 的结果：

```
int sum(){
    int i, sum=0;
    for(i=1; i<=100; i++){
        sum+=i;
    }
    return sum;
}
```

## C语言有参函数的定义

如果函数需要接收用户传递的数据，那么定义时就要带上参数。如下所示：

dataType functionName( dataType1 param1, dataType2 param2 ... ){
  //body
}

`dataType1 param1, dataType2 param2 ...`是参数列表。函数可以只有一个参数，也可以有多个，多个参数之间由`,`分隔。参数本质上也是变量，定义时要指明类型和名称。与无参函数的定义相比，有参函数的定义仅仅是多了一个参数列表。