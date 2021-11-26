### 导出名
1. Go语言中，如果名字以大写字母开头，那就意味这是导出名，即包里有对其的定义，例如Pi是math包中的导出名，如果使用 math.pi 就会报错，需要使用math.Pi.
```
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Pi) // Pi的首字符大写。 
}
```

### 类型
1. 注意变量或者函数的类型都是放在后面的。如下面的代码
```
func add (x int, y int) int {
	return x + y
}

```
2. 当连续2个或者多个函数的已命名形参类型相同，只需要写最后一个类型即可
```
package main

import "fmt"

func add(x, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(42, 13))
}
```

### 常量 const
1. go中使用const 表示常量
2. iota 经常和const 一起使用，表示枚举类型， 这里要注意iota 从0开始，每1行后加1. 具体看代码
```
	const (
		beijng = iota
		shanghai 
		tianjin 
	)
	fmt.Println("beiging=", beijng, "shanghai= ", shanghai, "tianjin= ", tianjin)

	const (
		beijing = iota * 10
		wuhai
		chengdu
	)
	fmt.Println("beijing=", beijing, "wuhai=", wuhai, "chengdu=", chengdu)

	输出结果：
	beiging= 0 shanghai= 1 tianjin= 2
	beijing= 0 wuhai= 10 chengdu= 20

	const (
		a, b = iota + 1, iota + 2
		c, d
		e,f
		g,h = iota * 2, iota * 3
		i,k
	)
	fmt.Println("a=", a, "b=", b, "c=", c, "d=", d, "e=", e, "f=",f, "g=",g, "h=", h, "i=", i, "k=", k)
	输出结果:
	a= 1 b= 2 c= 2 d= 3 e= 3 f= 4 g= 6 h= 9 i= 8 k= 12
```

### 函数返回值
1. 函数可以返回任意多的返回值,匿名返回
```
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```
2. 函数返回多个返回值，可以给返回值起名字
```
func  func3(a string, b int) (ret1 int, ret2 int)  {
	fmt.Println("====func3====");
	fmt.Println("a=", a)
	fmt.Println("b=", b);
	ret1 = 1000
	ret2 = 2000
	return 
}
```
3. 函数返回多个值的类型是一样的，可以只给最后一个变量指定类型
```
func func4(a string, b int) (r1, r2 int) {
	fmt.Println("====func4=====")
	fmt.Println("a=", a)
	fmt.Println("b=", b)
	r1 = 3000
	r2 = 4000
	return
}
```

### init 函数
1. go代码中，在main之前还有个init函数先于main执行。
2. 对外提供的api首字符要大写
详见下面代码的运行情况
```
lib1.go
```
package lib1

import "fmt"
// 要给外界调用的接口，首字符要大写
func Lib1test()  {
	fmt.Println("lib1 test enter...")
}

func init() {
	fmt.Println("lib1 init enter+++")
}
```
lib2.go
```
package lib2

import "fmt"
// 要给外界调用的接口，首字符要大写
func Lib2test()  {
	fmt.Println("lib2 test enter...")
}

func init() {
	fmt.Println("lib2 init enter+++")
}
```
main.go 代码
package main

import (
	"userProject/packageTmp/lib1"  // 注意导包的格式
	"userProject/packageTmp/lib2"
)

func main() {
	lib1.Lib1test() // 包内的对外的API首字符是大写
	lib2.Lib2test() // 包内的对外的API首字符是大写
}
输出结果：
lib1 init enter+++
lib2 init enter+++
lib1 test enter...
lib2 test enter...
```
