## For
go语言中只有一个循环结构，就是`for`

`for`循环由3部分组成，由分号分割：
1. 初识语句，在第一次循环前执行，一般是一个短赋值语句，该变量仅在`for`循环中可见；
2. 条件表达式，每次循环前执行；
3. 后语句，在每次循环后执行；
4. 初识语句和后语句是可以省略的；
5. 如果没有分号，可以直接把`for`当作`while`；
> `for`后的3个语句没有括号，而且大括号是必须的。

## if

和`for`语句类似，没有括号，但是必须有大括号;
`if`开始处可以有一个短赋值语句，产生的变量的作用域只有`if`和他相应的`else`语句本身
```go
if v := math.Pow(x, y); v < lim {
    return v
}
```
## 循环及函数
```go

package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	z := 1.0
	delta := 0.000000000001
	for {
		// 注意导数的使用方法
		if  math.Abs(z*z - x) <= delta{
			fmt.Println(z*z - x)
			break
		}else{
			fmt.Println(z)
			z = z - (z * z -x)/(2*z)
		}
		
	}
	return z
}

func main() {
	fmt.Println(Sqrt(2))
}
```




