---
title: go语言设计模式创建型设计模式
date: 2022-03-31 10:23:23
tags: 设计模式
---
# 创建型设计模式

## 抽象工厂模式
抽象工厂比较简单.
```golang
///ifacotry.go
package abstractFactory

type iMilkFactory interface {
	MakeMilk() iMilk
}

func GetFactory(s string) iMilkFactory {
	if s == "mengniu" {
		return &mengNiu{}
	}
	if s == "yili" {
		return &yili{}
	}
	return nil
}
///imilk.go
package abstractFactory

type iMilk interface {
	setSugar(s string)
}

type milk struct {
	Sugar string
}

func (m *milk) setSugar(s string) {
	m.Sugar = s
}

type mnMilk struct {
	milk
}

type ylMilk struct {
	milk
}
/// brand.go
package abstractFactory

type mengNiu struct {
}

func (m mengNiu) MakeMilk() iMilk {
	return &mnMilk{milk{Sugar: "mengniu"}}
}

type yili struct {
}

func (y yili) MakeMilk() iMilk {
	return &mnMilk{milk{Sugar: "yili"}}
}
/// main.go
package main

import (
	"developPattern/abstractFactory"
	"fmt"
)

func main() {
	mengniuFactory := abstractFactory.GetFactory("mengniu")
	fmt.Printf("#v", mengniuFactory.MakeMilk())
}
```







## 创建者模式
个人理解: 在抽象工厂模式上再封装一层，使之可以方便的调用工厂
```golang
///director.go
package builder

type director struct {
	Builder ibuild
}

func NewDirector(ibuild2 ibuild) *director {
	return &director{Builder: ibuild2}
}

func (d *director) SetBuilder(ibuild2 ibuild) {
	d.Builder = ibuild2
}

func (d *director) Build() Juice {
	return d.Builder.GetJuice()
}
/// builder.go
package builder

type ibuild interface {
	GetJuice() Juice
}

func GetBuilder(s string) ibuild {
	if s == "apple" {
		return &appjuice{}
	}
	if s == "orange" {
		return &orangejuice{}
	}
	return nil
}
//juice
package builder

type Juice struct {
	Color string
	Suger string
}

type appjuice struct {
	Juice
}

func (receiver *appjuice) GetJuice() Juice {
	return Juice{
		Color: "red",
		Suger: "app",
	}
}

type orangejuice struct {
	Juice
}

func (receiver *orangejuice) GetJuice() Juice {
	return Juice{
		Color: "yellow",
		Suger: "oran",
	}
}
//main.go
package main

import (
	"developPattern/builder"
	"fmt"
)

func main() {
	appjuice := builder.GetBuilder("apple")
	orajuice := builder.GetBuilder("orange")
	director := builder.NewDirector(appjuice)
	juice := director.Build()
	fmt.Printf("%#v", juice)

	director.SetBuilder(orajuice)
	juiceb := director.Build()
	fmt.Printf("%#v", juiceb)

}

```

## 工厂模式
感觉比抽象工厂少了个抽象的环节。哈哈哈
```golang
package factory

type iMilk interface {
	SetName(s string)
	SetPrice(s string)
	GetName() string
	GetPrice() string
}

type Milk struct {
	Name  string
	Price string
}

func (m *Milk) SetName(s string) {
	m.Name = s
}
func (m *Milk) SetPrice(s string) {
	m.Price = s
}
func (m *Milk) GetName() string {
	return m.Name
}
func (m *Milk) GetPrice() string {
	return m.Price
}

type MnMilk struct {
	Milk
}
type YlMilk struct {
	Milk
}

func NewMnMilk() iMilk {
	return &MnMilk{
		Milk: Milk{
			Name:  "mengniu",
			Price: "3",
		},
	}
}

func NewYlMilk() iMilk {
	return &YlMilk{
		Milk: Milk{
			Name:  "yili",
			Price: "4",
		},
	}
}
func GetMilk(s string) iMilk {
	if s == "mengniu" {
		return NewMnMilk()
	}
	if s == "yili" {
		return NewYlMilk()
	}
	return nil
}

```

## 单例模式
这个就直接上代码 go中有goroutine所以一般用锁创建单例或sync.once,或在init函数中创建
```golang
package singleinstance

import (
	"fmt"
	"sync"
)

var lock = &sync.Mutex{}

type Single struct {
}

var SingleInstance *Single

func GetSingleInstance() *Single {
	if SingleInstance == nil {
		lock.Lock()
		defer lock.Unlock()
		if SingleInstance == nil {
			SingleInstance = &Single{}
			fmt.Println("instance is creating")
		} else {
			fmt.Println("instance is created")
		}

	} else {
		fmt.Println("instance is created")
	}
	return SingleInstance
}
/// sync.once版本
var once sync.Once

type single struct {
}

var singleInstance *single

func getInstance() *single {
    if singleInstance == nil {
        once.Do(
            func() {
                fmt.Println("Creting Single Instance Now")
                singleInstance = &single{}
            })
    } else {
        fmt.Println("Single Instance already created-2")
    }
    return singleInstance
}
```