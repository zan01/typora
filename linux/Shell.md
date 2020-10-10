> “#!”是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行。

```shell
#!/bin/bash
```



> 运行Shell脚本
>
> 作为可执行程序

```shell
chmod +x test.sh
./test.sh
```



> 定义变量
>
> 定义变量时，变量名不加美元符号
>
> 变量名和等号之间不能有空格

```shell
your_name="qinjx"
```



> 使用变量
>
> 变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界

```shell
your_name="qinjx"
echo $your_name
echo ${your_name}
```



> 单引号
>
> 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的
>
> 单引号字串中不能出现单引号（对单引号使用转义符后也不行）

```shell
str='this is a string'
```



> 获取字符串长度

```shell
string="abcd"
echo ${#string} #输出：4
```



> 截取字符串

```shell
string="alibaba is a great company"
echo ${string:1:4} #输出：liba
```

