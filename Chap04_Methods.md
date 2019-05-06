## Methods
1. `go`中，没有类
1. `method`是带有`type`的`function`, 该`type`为这个`function`的`receiver`。可以理解为分散的类？或者是各种接口？
1. `method`的`receiver`必须和`method`在同一个`package`内，连`build in`的`type`也不行。
1. 当`receiver`是一个非指针类型时， `method`作用于`receiver`的一个副本，如果你要修改`receiver`，必须使用过一个指针
1. `function`的指针参数，必须显示传递；而`method`的`receiver`，只要声明了是指针，则无论是使用指针，还是使用`receiver`值本身都可以。
1. 反之亦然。即：对于`method`，如果`receiver`是一个值，你也可以传指针给他，而`function`不行。

```go

// 这是一个method，与普通function相比，在func关键词后， 多了一个receiver
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

```