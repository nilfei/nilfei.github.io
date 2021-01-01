+++
author = "nilfei"
title = "Go教程-Day2"
date = "2019-03-05"
description = "Guide golang"
categories = [
    "go"
]
tags = [
    "go",
]
+++


## 断言

```
package main

import "fmt"
//自定义类型
type sw interface {
}

func main() {
  // 给类型赋值
  var s sw = 0x0D
  // 断言
  fmt.Println(s.(int))
}

```



## if-else

```


package main

import (
	"errors"
	"fmt"
)

func main() {
    var d int64 = 1200
	fmt.Println(d)
	if d%10 != 1 {
        fmt.Println("a")
	} else {
        fmt.Println("b")
	}
	// i32 测试
	var i32 int32 = 1200
	str, err := test(i32)
	fmt.Println(str)
	// 空字符串
	if err != nil {
		fmt.Println(err)
		// 无法判断类型
	}

	//i64 测试

	s, err := test(d)
	fmt.Println(s)
	// 您传入的是 ： 1200
	if err != nil {
		fmt.Println(err)
		// 不会发生错误
	}

}

func test(i interface{}) (str string, err error) {
	switch i.(type) {
	case int64:
		sprintf := fmt.Sprintf("您传入的是 ： %d", i)
		return sprintf, nil
	}
	return "", errors.New("无法判断类型")
}

```

## for 循环
// 循环一百次

```
for i:=1; i <=100; i++ { 
    // 大于50停止循环 
    if i > 50{
       break;
    }
    // 求于等于0 跳过
    if i %2 == 0{
      continue
    }
}
```

// 死循环
//for {
//	fmt.Println(time.Now().Second())
//	time.Sleep(time.Second * 3)
//}


## switch 选择

```
package main

import "fmt"

func main() {
	test := "A"
	switch test {
	case "A":
		fmt.Println(test)
	case "B":
		fmt.Println("B")
	case "C":
		fmt.Println("C")
	case "Q", "P":
		fmt.Println("Q,P")
	}

	switch num := 99; {
	case num < 50:
		fmt.Printf("%d 小于 %d\n", num, 50)
		//跳转到下一个case
		fallthrough
	case num < 100:
		fmt.Printf("%d 小于 %d\n", num, 100)
		//跳转到下一个case
		fallthrough
	case num < 200:
		fmt.Printf("%d 小于 %d", num, 200)
	}
}

```