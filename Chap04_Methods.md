## Methods
1. `go`中，没有类
1. `method`是带有`type`的`function`, 该`type`为这个`function`的`receiver`。可以理解为分散的类？或者是各种接口？
1. `method`的`receiver`必须和`method`在同一个`package`内，连`build in`的`type`也不行。
1. 当`receiver`是一个非指针类型时， `method`作用于`receiver`的一个副本，如果你要修改`receiver`，必须使用过一个指针
1. `function`的指针参数，必须显示传递；而`method`的`receiver`，只要声明了是指针，则无论是使用指针，还是使用`receiver`值本身都可以。
1. 反之亦然。即：对于`method`，如果`receiver`是一个值，你也可以传指针给他，而`function`不行。
1. 使用指针做为`receiver`的理由包括： 1）避免拷贝值；2）可以修改值的属性

```go

// 这是一个method，与普通function相比，在func关键词后， 多了一个receiver
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

```

## 接口
1. 接口是一系列方法签名的集合
1. 一个接口值，能够装载任何实现了该方法的值：这里需要注意，虽然一个`method`可以同时被一个值或其指针调用，但是接口值不可以。
1. 一个类型实现了某个接口，只需要定义该方法就行了，并不需要显式地声明。
1. 接口值可以看作是一个元组，包括`(值,类型)`，通过接口值调用方法，等同于通过该类型的值调用方法。
1. 一个接口方法可以接受`nil`值，而不会发生空指针错误；事实上在`go`中，处理`nil`值的方法很常见。但是，一个类型值为`nil`的接口值并不为`nil`。
1. 一个空接口值`var i interface{}`可以接受任何类型的值。
1. 最常见的接口是由`fmt`定义的`Stringer`接口，只要实现了`String`方法，即可被打印出来。
1. `assert`: `t := i.(Type)` 可以判断`i`是否为类型`Type`，如果不是，会触发一个`panic`；如果是，则把对应值赋给`t`。
1. 检测一个值是否为类型`Type`: `t, ok := i.(Type)`。`t`将会被赋值为对应值，`ok`为一个布尔值。

## 类型分支
```go
// 这里和assert是基本一致的，只是把assert的类型换成了type这个关键字
switch t := i.(type) {
    // 对不同的类型做处理
    case string:
        //  blabla
    case int:
        // blabla
}

```

## Stringer exercise
```go
package main

import "fmt"

type IPAddr [4]byte

// TODO: Add a "String() string" method to IPAddr.
func (ip IPAddr) String () string {
	return fmt.Sprintf("%v.%v.%v.%v", ip[0], ip[1], ip[2], ip[3])
}

func main() {
	hosts := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}
	for name, ip := range hosts {
		fmt.Printf("%v: %v\n", name, ip)
	}
}

```
