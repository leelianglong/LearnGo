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

### 函数返回值
1. 函数可以返回任意多的返回值
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