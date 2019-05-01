## 带有初始化的变量
变量声明可带有变量初始化值。
如果初始化存在，则可以忽略类型，变量会自动接受初始化者的类型
```go
var i, j int = 1, 2
var c, python, java = true, false, "no"
```

## 短变量声明
在函数内，`:=`短赋值声明可以替代`var`声明，并带有隐式类型
在函数外，所有的声明，都以关键词开头， `var` 或者 `func`，所以`:=`结构是不可以

## 基本类型
go 的基本类型包括： 
```txt
bool
string 

int int8 int16 int32 int64
uint uint8 uint16 uint32 uint64

byte  // uint8的别名
rune  // int32的别名，代表一个unicode字符

float32 float64
complex64 complex128
```
int的位数跟随系统
int32的别名，代表一个unicode字符

float32 float64
complex64 complex128

## 0值
没有显式赋值的变量会被赋予0值： 整数类型为0，布尔为`false`，字符串为空字符串。

## 类型转换
