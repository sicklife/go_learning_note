## 指针
1. `go`中的指针没有指针算术操作
1. `*` 和 `&`与 `C`中相同。
1. 指针的0值为`nil`。


## 结构体
```go
type Vertex struct {
    X int
    Y int
}
```
1. 可以直接通过指针获取`field`值，而不需要显式的`dereference`


## 列表与切片
```go
var a[10] int
primes := [6]int{2, 3, 5, 7, 11, 13}

// 切片
var []int s = primes[1:4]

//直接定义一个切片，不用实现定义列表
var q []int
// 或者
q := []int{2, 3, 5, 7, 9, 11}

//切片的切片
q = q[:2]

// 添加元素
s = append(s, 1, 2, 3, 4)
```
1. 列表长度不可变
1. 切片长度是动态的
1. 切片比列表更常用
1. 切片的0值是`nil`
1. 切片的长度`len(s`，是指切片自身的元素个数；切片的容量`cap(s)`是指切片所在`Arrar`的长度，可以通过`s[:len(s)+4]`的操作，扩展切片长度
1. `s[2:]`会修改`cap(s)`， `s[:0]`则不会

## 使用make创建动态长度切片
```go
a := make([]int, 5)  // len(a) = 5

b := make([]int, 0, 5) //len(b)=0, cap(b)=5
```

## Range
1. 当对切片进行`range`操作时，返回两个值，第一个值是index，第二个是对应的元素
1. 可以用`_`忽略对应的值
1. 如果只想要`index`，可以忽略第二个变量

## Exercise: Slices
```go
package main

import (

	"golang.org/x/tour/pic")

func Pic(dx, dy int) [][]uint8 {
	var q [][]uint8
	for i:=0; i<dy; i++ {
		var tmp []uint8
		for j:=0; j<dx; j++ {
			tmp = append(tmp, uint8((i+j)/2))
		}
		q = append(q, tmp)
	}
	return q
}

func main() {
	pic.Show(Pic)
}
```
solution 2 use make
```go
package main

import "golang.org/x/tour/pic"

func Pic(dx, dy int) [][]uint8 {
	img := make([][]uint8, dy)
	for i := range img {
		row := make([]uint8, dx)
		for j := range row {
			row[j] = uint8(i^j)
		}
		img[i] = row
	}
	return img
}

func main() {
	pic.Show(Pic)
}

```

## map 
1. `map`类型的0值是`nil`
1. 可以用`make(map[KeyType]ValueType)`来生成/初始化一个map
1. `delete(m, key)`删除key
1. `elem, ok = m[key]`判断`key`是否在`m`中，如果在， `ok`为`true`；否则`ok`为`false`, `elem`为对应元素类型的0值。
```go
// 方式1
m := make(map[String]Vertex)

//方式2
var m = map[String]Vertex{
    "Bell Labs": Vertext{40, -70},
    "Google": Vertex{37, -122},
}

//方式3 元素的类型声明可以省略
var m = map[String]Vertex{
    "Bell Labs": {40, -70},
    "Google": {37, -122},
}
```

## Exercise Map
```go
package main

import (
	"golang.org/x/tour/wc"
	"strings"
)

func WordCount(s string) map[string]int {
	words := strings.Fields(s)
	m := make(map[string]int)
	for _, word := range words{
		m[word] +=  1
	}
	return m
}

func main() {
	wc.Test(WordCount)
}

```
