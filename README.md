# design-pattern
In this repository, you will find examples of popular design patterns such as Singleton, Factory, Strategy, Decorator, Observer, and many more. Each example comes with a detailed description of how to apply that design pattern in Golang, along with reference materials so that you can better understand them.


<h2>&#9733; Creational Patterns (6) &#9733;</h2>
<h3> Singleton Pattern </h3>
<p> Level of difficult: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Singleton Pattern cho phép tạo duy nhất một đối tượng (object) của một lớp (class) trong toàn bộ ứng dụng. Ý tưởng của Mẫu Singleton là đảm bảo rằng một lớp chỉ có một đối tượng duy nhất và cung cấp một điểm truy cập toàn cục cho đối tượng này. Thường được sử dụng trong các tình huống mà bạn muốn đảm bảo rằng chỉ một đối tượng duy nhất sẽ được tạo trong hệ thống, ví dụ: quyền truy cập cơ sở dữ liệu, đối tượng tài nguyên hoặc cài đặt hệ thống. </p>
<div align="center">
    <img src="images/singleton_design_pattern.png" style="width: 50%; height: auto;" alt="singleton-pattern-image" />
</div>

```go
package singleton

import (
	"sync"
)

type Singleton struct {
	// Your singleton struct fields here
}

var instance *Singleton
var once sync.Once

func GetInstance() *Singleton {
	once.Do(func() {
		instance = &Singleton{
			// Initialize your singleton struct fields here
		}
	})
	return instance
}

```


```go
package main

import (
	"fmt"
	"yourpackage/singleton"
)

func main() {
	instance := singleton.GetInstance()
	// Use the singleton instance as needed
	fmt.Println(instance)
}
```


<h3> Simple Factory Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Factory Method Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>

<h3> Abstract Factory Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>

<h3> Prototype Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Builder Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>



<h2>&#9733; Structural Patterns (7) &#9733;</h2>
<h3> Adapter Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>

<h3> Bridge Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Composite Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>

<h3> Decorator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Facade Pattern </h3>
<p> Level of difficult: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>

<h3> Flyweight Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>

<h3> Proxy Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>



<h2>&#9733; Behavioral Patterns (11)&#9733;</h2>
<h3> Strategy Pattern </h3>
<p> Level of difficult: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>

<h3> Observer Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733; </p>

<h3> Iterator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606; </p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733; </p>

<h3> Command Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>

<h3> State Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Template Method Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>

<h3> Chain of Responsibility Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>

<h3> Mediator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>

<h3> Mementor Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>

<h3> Interpreter Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#9733; </p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>

<h3> Visitor Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>

