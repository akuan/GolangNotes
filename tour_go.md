# GO指南

原文网址 https://tour.go-zh.org

## 类型转换

表达式 `T(v)` 将值 `v` 转换为类型 `T`。 例如：

```go
var i int = 42
var f float64 = float64(i)
```

## Switch
```go
switch time.Saturday {
	case today + 0:
		fmt.Println("Today.")
	case today + 1:
		fmt.Println("Tomorrow.")
	case today + 2:
		fmt.Println("In two days.")
	default:
		fmt.Println("Too far away.")
	}
```
```go
switch {
 	case t.Hour() < 12:
 		fmt.Println("Good morning!")
 	case t.Hour() < 17:
 		fmt.Println("Good afternoon.")
 	default:
 		fmt.Println("Good evening.")
 	}
```

## defer

defer 语句会将函数推迟到外层函数返回之后执行。defer栈按照后进先出的顺序调用。

## 指针

类型 `*T` 是指向 `T` 类型值的指针。其零值为 `nil`。`&` 操作符会生成一个指向其操作数的指针

```go
var p *int
i := 42
p = &i
```

`*` 操作符表示指针指向的底层值。与 C 不同，Go 没有指针运算。

```go
fmt.Println(*p) // 通过指针 p 读取 i
*p = 21         // 通过指针 p 设置 i
```

## 切片

`make` 创建切片，append追加元素到切片末尾。 append 返回更新后的切片。因此必须存储追加后的结果，通常为包含该切片自身的变量。语法 func append(s []T, vs ...T) []T

```go
a := make([]int, 5)  // len(a)=5
b := make([]int, 0, 5) // len(b)=0, cap(b)=5
b = b[:cap(b)] // len(b)=5, cap(b)=5
b = b[1:]      // len(b)=4, cap(b)=4

var s []int 
// append works on nil slices.
s = append(s, 0)

```

让编译器统计数组字面值中元素的数目：

```go
b := [...]string{"Penn", "Teller"} //等同 b := [2]string{"Penn", "Teller"}
```

`for` 循环的 `range` 形式可遍历切片或映射
```go
for i, v := range pow {
	fmt.Printf("2**%d = %d\n", i, v)
}

for i := range pow {  //若你只需要索引，去掉 , value 的部分即可
	pow[i] = 1 << uint(i) // == 2**i
}
for _, value := range pow {  //可以将下标或值赋予 _ 来忽略它。
   fmt.Printf("%d\n", value)  
}
```

## 映射

```go
var m map[string]Vertex

func main() {
	m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])
}
```

