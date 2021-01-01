+++
author = "nilfei"
title = "Go教程-Day1"
date = "2019-03-05"
description = "Guide golang"
categories = [
    "go"
]
tags = [
    "go",
]
+++

# 变量

`请注意阅读代码中的注释`

```
// main包
package main

// 导入 fmt包
import "fmt"

// 主函数
func main() {
	// int变量声明 默认值0填充
	var money int
	// 用fmt包进行输出
	fmt.Println("how much money you have left : ", money)
	// 输出 how much money you have left : 0

	// int变量声明 并赋值
	var money2 int = 1000
	// 用fmt包进行输出
	fmt.Println("how much money you have left : ", money2)
	// 输出 how much money you have left : 1000

	/**
	 *自动推断值类型
	 */
	var money3 = 9999
	// 简短自动推断类型 此用法最多
	money4 := 8888
	fmt.Println("money 3 is :", money3, "money4 is :", money4)
	// 批量声明推断变量
	var a1, a2, a3, a4 = 100, "0xFFFF", false, 0xFFFFFFF

	fmt.Println("a1 is ", a1, "; a2 is", a2, "; a3 is", a3, "; a4 is", a4)
	//a1 数值int, a2 字符串, a3 bool , a4 16进制
	//a1 is  100 ; a2 is 0xFFFF ; a3 is false ; a4 is 268435455

	// 使用16进制时需注意 溢出问题 0xFFFFFFFF 连续32个1的内存
	// var a = 0xFFFFFFFF
	// fmt.Println(a)
	// 上面的实例将输出 constant 4294967295 overflows int

	//批量声明固定类型的变量
	var k1, k2 = 100, 88
	fmt.Println("k1 is ", k1, "; k2 is", k2)

	// 涵盖声明
	var (
		version = "1.1.1"
		port    = 9501
		name    = "user-srv"
	)
	fmt.Printf("%v Server is starting in port %v. version : %v . ", name, port, version)
	// user-srv Server is starting in port 9501. version : 1.1.1 . 
}
```

## go语言中的类型

1. bool
2. 数字类型
3. int8, int16, int32, int64, int
4. uint8, uint16, uint32, uint64, uint
5. float32, float64
6. complex64, complex128
7. byte
8. rune
9. string

```

package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	// 布尔类型
	boolT := true
	boolT = false
	fmt.Println("布尔类型的输出: ", boolT)
	//布尔类型的输出:  false

	// 关于数值类型的说明
	// 凡是带 u + 类型的均为 无符号类型 例如 uint8 是无符号的8位正整数 0-255

	// int8类型 -128-127
	// uint8类型 0 ~ 255
	var int8T int8 = 127
	var uint8T uint8 = 255
	// 指定的类型不能超出数值范围，否则发生overflow 其他的类型同理
	//var int8T int8 = 128
	//constant 128 overflows int8
	fmt.Println("8位数值的类型的输出: ", int8T)
	fmt.Println("无符号8位数值的类型的输出: ", uint8T)
	/**
	8位数值的类型的输出:  127
	无符号8位数值的类型的输出:  255
	*/

	//int16 -32768～32767
	//uint16 0～65535
	var int16T int16 = 127
	var uint16T uint16 = 65535

	fmt.Println("int16T 的类型的输出: ", int16T)
	fmt.Println("uint16T 的类型的输出: ", uint16T)
	/**
	int16T 的类型的输出:  127
	uint16T 的类型的输出:  65535
	*/

	//int32 ：-2147483648～2147483647
	//uint32 :  0～4294967295
	var int32T int32 = 2147483647
	var uint32T uint32 = 4294967295

	fmt.Println("int32T 的类型的输出: ", int32T)
	fmt.Println("uint32T 的类型的输出: ", uint32T)
	/**
	int32T 的类型的输出:  2147483647
	uint32T 的类型的输出:  4294967295
	*/

	//int64 : -9223372036854775808～9223372036854775807
	//uint64: 0～18446744073709551615
	var int64T int64 = 9223372036854775807
	var uint64T uint64 = 18446744073709551615

	fmt.Println("int64T 的类型的输出: ", int64T)
	fmt.Println("uint64T 的类型的输出: ", uint64T)
	/**
	int64T 的类型的输出:  9223372036854775807
	uint64T 的类型的输出:  18446744073709551615
	*/

	// int 和 uint 都是根据系统的位数自行调节
	// 32 位系统 : -2147483648～2147483647
	// 64 位系统 : -9223372036854775808～9223372036854775807
	var intT int = 9223372036854775807

	//uint：表示 32 或 64 位无符号整型。(取决于系统的位数)
	// 32 位系统 ：  0～4294967295，
	// 64 位系统 ： 0～18446744073709551615
	var uintT uint = 18446744073709551615

	fmt.Println("intT 的类型的输出: ", intT)

	fmt.Println("uintT 的类型的输出: ", uintT)
	/**
	intT 的类型的输出:  9223372036854775807
	uintT 的类型的输出:  18446744073709551615
	*/

	/**
	Float 数值类型

	*/
	// float32 3.402823466385288598117041834516925440e +38	1.401298464324817070923729583289916131280e -45
	// float32 大约可提供6位小数 1 左移 24位

	var float32T float32 = 16777216
	// IEEE754
	// 因float32 累计计算扩散 请尽量使用float64
	fmt.Println("float32T 的类型的输出: ", float32T == float32T+1)

	var float64T float64 = 16777216
	fmt.Println("float64T 的类型的输出: ", float64T == float64T+1)

	const Avogadro = 6.02214129e23 // 阿伏伽德罗常数
	const Planck = 6.62606957e-34  // 普朗克常数
	fmt.Println("阿伏伽德罗常数：", Avogadro, "普朗克常数：", Planck)

	// 默认情况下 float推断 均为float64
	fl64 := 1.11
	fmt.Printf("Float 类型推断： %T \n", fl64)

	// 复数类型
	// 用途 ：  反常积分 ,分析系统稳定性的根轨迹法 ，奈奎斯特图法（Nyquist plot）和尼科尔斯图法（Nichols plot）都是在复平面上进行的

	//complex64：实和虚 都为 float32 类型的的复数。
	//complex128：实和虚 都为 float64 类型的的复数。
	c1 := complex(1, 2)
	c2 := 3 + 4i
	cadd := c1 + c2
	fmt.Println("复数和:", cadd)
	cmul := c1 * c2
	fmt.Println("复数:", cmul)

	// byte 是 uint8 的别名。 utf8编码
	// 声明数组
	// ASCII 码 49 50 51 52
	data := [4]byte{0x31, 0x32, 0x33, 0x34}
	str := string(data[:])
	fmt.Println("byte 转 string :", str)
	// 使用rune 和获取 字符串长度
	fmt.Println("rune string 长度 :", utf8.RuneCountInString(str))

	// rune 是 int32 的别名。
	str1 := "我叫MT"
	fmt.Println("rune 结果", []rune(str1))
	fmt.Println("byte 结果", []byte(str1))

	//const 关键字常量 初始化赋值
	// 常量结果不能通过函数 方法赋值给常量
	const constA = 100
	fmt.Println("constA 结果", constA)

	// IOTA 常量
	const (
		a = iota //a=0
		b = iota //b=1
		c        //c=2
		_        //3
		d        //d=4
	)
	fmt.Println(
		"a is :", a,
		"b is :", b,
		"c is :", c,
		"d is :", d,
	)

	// 实战用法
	type ByteSize float64
	const (
		_           = iota             // ignore first value by assigning to blank identifier
		KB ByteSize = 1 << (10 * iota) // 1 << (10*1)
		MB                             // 1 << (10*2)
		GB                             // 1 << (10*3)
		TB                             // 1 << (10*4)
		PB                             // 1 << (10*5)
		EB                             // 1 << (10*6)
		ZB                             // 1 << (10*7)
		YB                             // 1 << (10*8)
	)

	fmt.Println(
		"KB is ", KB,
		"\n MB is ", MB,
		"\n GB is ", GB,
		"\n TB is ", TB,
		"\n PB is ", PB,
		"\n EB is ", EB,
		"\n EB is ", EB,
		"\n ZB is ", ZB,
		"\n YB is ", YB,
	)

}
```
## 函数

```
package main

//引入包
import (
	"fmt"
	"github.com/pkg/errors"
)

func main() {
	fmt.Println(TestFunc(33))
	fmt.Println(TestFunc(10))
}
// 函数名称 （接受参数名称 接受参数类型） (返回参数名称 参数类型, 名称 类型)
func TestFunc(i int) (err error, d int) {
	if d := i % 10; d == 0 {
		return nil, d
	}
	return errors.New("无法对10取模"), 0
}
```