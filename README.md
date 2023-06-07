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
<p> Simple Factory Pattern là một mô hình thiết kế phần mềm thuộc nhóm mô hình Factory (Công ty). Mô hình Simple Factory được sử dụng để tạo ra đối tượng mà không tiết lộ logic cụ thể của việc khởi tạo cho người dùng, giúp giảm sự phụ thuộc giữa người dùng và quá trình khởi tạo đối tượng. Thay vì người dùng phải chịu trách nhiệm khởi tạo đối tượng trực tiếp, họ chỉ cần gọi Simple Factory và cung cấp thông tin đầu vào.</p>

```go
package main

import "fmt"

// Product interface
type Product interface {
	Use()
}

// ConcreteProductA is a concrete implementation of the Product interface
type ConcreteProductA struct{}

// Use implements the Use method of the Product interface for ConcreteProductA
func (p *ConcreteProductA) Use() {
	fmt.Println("Using ConcreteProductA")
}

// ConcreteProductB is another concrete implementation of the Product interface
type ConcreteProductB struct{}

// Use implements the Use method of the Product interface for ConcreteProductB
func (p *ConcreteProductB) Use() {
	fmt.Println("Using ConcreteProductB")
}

// SimpleFactory is the factory responsible for creating the products
type SimpleFactory struct{}

// CreateProduct is the method of the SimpleFactory that creates the products
func (f *SimpleFactory) CreateProduct(productType string) Product {
	switch productType {
	case "A":
		return &ConcreteProductA{}
	case "B":
		return &ConcreteProductB{}
	default:
		return nil
	}
}

func main() {
	factory := &SimpleFactory{}

	// Create a product of type A
	productA := factory.CreateProduct("A")
	productA.Use()

	// Create a product of type B
	productB := factory.CreateProduct("B")
	productB.Use()
}

```

<h3> Factory Method Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>
<p> Factory Method là một mô hình thiết kế phần mềm cho phép các lớp con quyết định loại đối tượng cụ thể sẽ được tạo. Nó cho phép linh hoạt trong việc mở rộng và mở rộng với các đối tượng khác nhau mà không cần thay đổi lớp gốc.</p>

```go
package main

import "fmt"

// Product is the interface that declares the common method for products
type Product interface {
	Use()
}

// ConcreteProductA is a concrete implementation of the Product interface
type ConcreteProductA struct{}

// Use implements the Use method of the Product interface for ConcreteProductA
func (p *ConcreteProductA) Use() {
	fmt.Println("Using ConcreteProductA")
}

// ConcreteProductB is another concrete implementation of the Product interface
type ConcreteProductB struct{}

// Use implements the Use method of the Product interface for ConcreteProductB
func (p *ConcreteProductB) Use() {
	fmt.Println("Using ConcreteProductB")
}

// Creator is the interface that declares the factory method
type Creator interface {
	CreateProduct() Product
}

// ConcreteCreatorA is a concrete implementation of the Creator interface for creating ConcreteProductA
type ConcreteCreatorA struct{}

// CreateProduct implements the factory method of the Creator interface for creating ConcreteProductA
func (c *ConcreteCreatorA) CreateProduct() Product {
	return &ConcreteProductA{}
}

// ConcreteCreatorB is another concrete implementation of the Creator interface for creating ConcreteProductB
type ConcreteCreatorB struct{}

// CreateProduct implements the factory method of the Creator interface for creating ConcreteProductB
func (c *ConcreteCreatorB) CreateProduct() Product {
	return &ConcreteProductB{}
}

func main() {
	// Create a ConcreteCreatorA
	creatorA := &ConcreteCreatorA{}
	productA := creatorA.CreateProduct()
	productA.Use()

	// Create a ConcreteCreatorB
	creatorB := &ConcreteCreatorB{}
	productB := creatorB.CreateProduct()
	productB.Use()
}


```


<h3> Abstract Factory Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>
<p> Abstract Factory là một mô hình thiết kế phần mềm cho phép tạo ra các họ đối tượng liên quan mà không tiết lộ logic khởi tạo cụ thể.</p>

```go
package main

import "fmt"

// AbstractProductA declares the interface for ProductA
type AbstractProductA interface {
	UseA()
}

// ConcreteProductA1 represents a concrete implementation of ProductA
type ConcreteProductA1 struct{}

// UseA implements the UseA method of AbstractProductA for ConcreteProductA1
func (p *ConcreteProductA1) UseA() {
	fmt.Println("Using ConcreteProductA1")
}

// ConcreteProductA2 represents another concrete implementation of ProductA
type ConcreteProductA2 struct{}

// UseA implements the UseA method of AbstractProductA for ConcreteProductA2
func (p *ConcreteProductA2) UseA() {
	fmt.Println("Using ConcreteProductA2")
}

// AbstractProductB declares the interface for ProductB
type AbstractProductB interface {
	UseB()
}

// ConcreteProductB1 represents a concrete implementation of ProductB
type ConcreteProductB1 struct{}

// UseB implements the UseB method of AbstractProductB for ConcreteProductB1
func (p *ConcreteProductB1) UseB() {
	fmt.Println("Using ConcreteProductB1")
}

// ConcreteProductB2 represents another concrete implementation of ProductB
type ConcreteProductB2 struct{}

// UseB implements the UseB method of AbstractProductB for ConcreteProductB2
func (p *ConcreteProductB2) UseB() {
	fmt.Println("Using ConcreteProductB2")
}

// AbstractFactory declares the interface for creating product objects
type AbstractFactory interface {
	CreateProductA() AbstractProductA
	CreateProductB() AbstractProductB
}

// ConcreteFactory1 represents a concrete implementation of the AbstractFactory for creating ProductA1 and ProductB1
type ConcreteFactory1 struct{}

// CreateProductA implements the CreateProductA method of AbstractFactory for ConcreteFactory1
func (f *ConcreteFactory1) CreateProductA() AbstractProductA {
	return &ConcreteProductA1{}
}

// CreateProductB implements the CreateProductB method of AbstractFactory for ConcreteFactory1
func (f *ConcreteFactory1) CreateProductB() AbstractProductB {
	return &ConcreteProductB1{}
}

// ConcreteFactory2 represents another concrete implementation of the AbstractFactory for creating ProductA2 and ProductB2
type ConcreteFactory2 struct{}

// CreateProductA implements the CreateProductA method of AbstractFactory for ConcreteFactory2
func (f *ConcreteFactory2) CreateProductA() AbstractProductA {
	return &ConcreteProductA2{}
}

// CreateProductB implements the CreateProductB method of AbstractFactory for ConcreteFactory2
func (f *ConcreteFactory2) CreateProductB() AbstractProductB {
	return &ConcreteProductB2{}
}

func main() {
	// Create a ConcreteFactory1
	factory1 := &ConcreteFactory1{}

	// Use products created by ConcreteFactory1
	productA1 := factory1.CreateProductA()
	productB1 := factory1.CreateProductB()
	productA1.UseA()
	productB1.UseB()

	// Create a ConcreteFactory2
	factory2 := &ConcreteFactory2{}

	// Use products created by ConcreteFactory2
	productA2 := factory2.CreateProductA()
	productB2 := factory2.CreateProductB()
	productA2.UseA()
	productB2.UseB()
}

```

<h3> Prototype Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Mô hình Prototype là một mô hình thiết kế phần mềm trong đó chúng ta tạo ra các đối tượng mới bằng cách sao chép một đối tượng đã tồn tại.</p>

```go
package main

import "fmt"

// Cloneable is the interface that declares the Clone method
type Cloneable interface {
	Clone() Cloneable
}

// ConcretePrototype is a concrete implementation of the Cloneable interface
type ConcretePrototype struct {
	data string
}

// Clone creates and returns a new instance of ConcretePrototype by performing a shallow copy
func (p *ConcretePrototype) Clone() Cloneable {
	return &ConcretePrototype{data: p.data}
}

func main() {
	// Create a prototype object
	prototype := &ConcretePrototype{data: "Prototype Data"}

	// Clone the prototype to create a new object
	clone := prototype.Clone().(*ConcretePrototype)

	// Verify that the clone is a separate object with the same data
	fmt.Println(clone.data) // Output: Prototype Data
}

```

<h3> Builder Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p>Builder Pattern là một mô hình thiết kế phần mềm giúp xây dựng và tạo ra các đối tượng phức tạp bằng cách sử dụng một quy trình từng bước.</p>

``` go
package main

import "fmt"

// Product represents the complex object being built
type Product struct {
	partA string
	partB string
	partC string
}

// Builder defines the interface for building the product
type Builder interface {
	BuildPartA()
	BuildPartB()
	BuildPartC()
	GetResult() Product
}

// ConcreteBuilder implements the Builder interface
type ConcreteBuilder struct {
	product Product
}

// BuildPartA builds PartA of the product
func (b *ConcreteBuilder) BuildPartA() {
	b.product.partA = "Part A"
}

// BuildPartB builds PartB of the product
func (b *ConcreteBuilder) BuildPartB() {
	b.product.partB = "Part B"
}

// BuildPartC builds PartC of the product
func (b *ConcreteBuilder) BuildPartC() {
	b.product.partC = "Part C"
}

// GetResult returns the final built product
func (b *ConcreteBuilder) GetResult() Product {
	return b.product
}

// Director controls the construction process using the builder
type Director struct {
	builder Builder
}

// Construct builds the product step by step using the builder
func (d *Director) Construct() Product {
	d.builder.BuildPartA()
	d.builder.BuildPartB()
	d.builder.BuildPartC()
	return d.builder.GetResult()
}

func main() {
	// Create a builder
	builder := &ConcreteBuilder{}

	// Create a director and set the builder
	director := &Director{builder: builder}

	// Construct the product using the director
	product := director.Construct()

	// Print the parts of the built product
	fmt.Println("Part A:", product.partA)
	fmt.Println("Part B:", product.partB)
	fmt.Println("Part C:", product.partC)
}

```

<h2>&#9733; Structural Patterns (7) &#9733;</h2>
<h3> Adapter Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p>Adapter Pattern: Chuyển đổi giao diện của một lớp thành một giao diện khác mà khách hàng mong muốn sử dụng.</p>

```go
package main

import "fmt"

// Target interface defines the expected interface for the client
type Target interface {
	Request()
}

// Adaptee represents the existing component with incompatible interface
type Adaptee struct {
	name string
}

func NewAdaptee(name string) *Adaptee {
	return &Adaptee{name: name}
}

func (a *Adaptee) SpecificRequest() {
	fmt.Printf("Adaptee %s performs specific request.\n", a.name)
}

// Adapter adapts the Adaptee to the Target interface
type Adapter struct {
	adaptee *Adaptee
}

func NewAdapter(adaptee *Adaptee) *Adapter {
	return &Adapter{adaptee: adaptee}
}

func (a *Adapter) Request() {
	a.adaptee.SpecificRequest()
}

func main() {
	// Create an adaptee
	adaptee := NewAdaptee("Adaptee 1")

	// Create an adapter with the adaptee
	adapter := NewAdapter(adaptee)

	// Call the target method on the adapter
	adapter.Request()
}

```

<h3> Bridge Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p>Bridge Pattern: Tách rời một lớp trừu tượng từ các lớp thực hiện để chúng có thể thay đổi độc lập.</p>

```go
package main

import "fmt"

// Implementor defines the interface for the implementation classes
type Implementor interface {
	OperationImpl() string
}

// ConcreteImplementorA represents one of the concrete implementation classes
type ConcreteImplementorA struct{}

func (c *ConcreteImplementorA) OperationImpl() string {
	return "ConcreteImplementorA"
}

// ConcreteImplementorB represents another concrete implementation class
type ConcreteImplementorB struct{}

func (c *ConcreteImplementorB) OperationImpl() string {
	return "ConcreteImplementorB"
}

// Abstraction defines the interface for the abstraction
type Abstraction interface {
	Operation() string
}

// RefinedAbstraction represents the refined abstraction class
type RefinedAbstraction struct {
	impl Implementor
}

func (a *RefinedAbstraction) SetImplementor(impl Implementor) {
	a.impl = impl
}

func (a *RefinedAbstraction) Operation() string {
	return fmt.Sprintf("RefinedAbstraction: %s", a.impl.OperationImpl())
}

func main() {
	// Create an implementation object
	implA := &ConcreteImplementorA{}

	// Create the abstraction object with the implementation object
	abstraction := &RefinedAbstraction{}
	abstraction.SetImplementor(implA)

	// Call the operation on the abstraction
	result := abstraction.Operation()
	fmt.Println(result)

	// Change the implementation object
	implB := &ConcreteImplementorB{}
	abstraction.SetImplementor(implB)

	// Call the operation again on the same abstraction
	result = abstraction.Operation()
	fmt.Println(result)
}

```

<h3> Composite Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p>Composite Pattern: Tạo ra một cấu trúc cây phân cấp để đại diện cho một nhóm đối tượng tương tự nhau và xử lý chúng như một đối tượng đơn lẻ.</p>

```go
```

<h3> Decorator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733;  &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p>Decorator Pattern: Đóng gói một đối tượng bên trong các đối tượng decorator để mở rộng chức năng của đối tượng gốc mà không thay đổi giao diện.</p>

<h3> Facade Pattern </h3>
<p> Level of difficult: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733;</p>
<p>Facade Pattern: Cung cấp một giao diện đơn giản để tương tác với một hệ thống phức tạp bên dưới.</p>

```go
package main

import "fmt"

// Subsystem1 represents one of the subsystems
type Subsystem1 struct{}

func (s *Subsystem1) Operation1() string {
	return "Subsystem1: Operation1"
}

func (s *Subsystem1) Operation2() string {
	return "Subsystem1: Operation2"
}

// Subsystem2 represents another subsystem
type Subsystem2 struct{}

func (s *Subsystem2) Operation3() string {
	return "Subsystem2: Operation3"
}

func (s *Subsystem2) Operation4() string {
	return "Subsystem2: Operation4"
}

// Facade represents the facade that simplifies the subsystems
type Facade struct {
	subsystem1 *Subsystem1
	subsystem2 *Subsystem2
}

func NewFacade() *Facade {
	return &Facade{
		subsystem1: &Subsystem1{},
		subsystem2: &Subsystem2{},
	}
}

func (f *Facade) Operation() string {
	result := "Facade:\n"
	result += f.subsystem1.Operation1() + "\n"
	result += f.subsystem1.Operation2() + "\n"
	result += f.subsystem2.Operation3() + "\n"
	result += f.subsystem2.Operation4()
	return result
}

func main() {
	// Create a facade
	facade := NewFacade()

	// Call the facade's operation
	result := facade.Operation()
	fmt.Println(result)
}

```

<h3> Flyweight Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p>Flyweight Pattern: Chia sẻ các đối tượng nhẹ (flyweight) giữa các đối tượng để giảm bộ nhớ và tăng hiệu suất.</p>

```go
```

<h3> Proxy Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p>Proxy Pattern: Cung cấp một đại diện (proxy) cho một đối tượng để kiểm soát quyền truy cập và thực hiện các hành động bổ sung.</p>

```go
```



<h2>&#9733; Behavioral Patterns (11)&#9733;</h2>
<h3> Strategy Pattern </h3>
<p> Level of difficult: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p>Strategy Pattern: Cho phép chọn một thuật toán từ một tập hợp các thuật toán khác nhau dựa trên yêu cầu cụ thể, mà không làm ảnh hưởng đến code sử dụng thuật toán đó.</p>

```go
```

<h3> Observer Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733; </p>
<p>Observer Pattern: Định nghĩa một mối quan hệ "một-nhiều" giữa các đối tượng để khi một đối tượng thay đổi trạng thái, tất cả các đối tượng liên quan sẽ được thông báo và cập nhật.</p>

```go
```

<h3> Iterator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606; </p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#9733; </p>
<p>Iterator Pattern: Cung cấp một cách duyệt qua các phần tử của một tập hợp mà không tiết lộ chi tiết cấu trúc bên trong.</p>

```go
```

<h3> Command Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p>Command Pattern: Đóng gói một yêu cầu thành một đối tượng độc lập, cho phép thực hiện yêu cầu đó với các tham số khác nhau, hoãn hoặc hủy yêu cầu.</p>

```go
package main

import "fmt"

// Command interface declares the execution method
type Command interface {
	Execute()
}

// Receiver represents the receiver of the command
type Receiver struct {
	name string
}

func NewReceiver(name string) *Receiver {
	return &Receiver{name: name}
}

func (r *Receiver) Action() {
	fmt.Printf("Receiver %s performs action.\n", r.name)
}

// ConcreteCommand represents a concrete command
type ConcreteCommand struct {
	receiver *Receiver
}

func NewConcreteCommand(receiver *Receiver) *ConcreteCommand {
	return &ConcreteCommand{receiver: receiver}
}

func (c *ConcreteCommand) Execute() {
	c.receiver.Action()
}

// Invoker represents the invoker of the command
type Invoker struct {
	command Command
}

func NewInvoker() *Invoker {
	return &Invoker{}
}

func (i *Invoker) SetCommand(command Command) {
	i.command = command
}

func (i *Invoker) ExecuteCommand() {
	i.command.Execute()
}

func main() {
	// Create a receiver
	receiver := NewReceiver("Receiver 1")

	// Create a concrete command with the receiver
	command := NewConcreteCommand(receiver)

	// Create an invoker
	invoker := NewInvoker()

	// Set the command for the invoker
	invoker.SetCommand(command)

	// Execute the command
	invoker.ExecuteCommand()
}

```

<h3> State Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p>State Pattern: Cho phép đối tượng thay đổi hành vi của nó khi trạng thái nội bộ của nó thay đổi.</p>

```go
package main

import "fmt"

// State represents the interface for the different states
type State interface {
	HandleState(context *Context)
}

// Context represents the context in which the state is maintained
type Context struct {
	state State
}

func (c *Context) SetState(state State) {
	c.state = state
}

func (c *Context) Request() {
	c.state.HandleState(c)
}

// ConcreteStateA represents one of the concrete states
type ConcreteStateA struct{}

func (s *ConcreteStateA) HandleState(context *Context) {
	fmt.Println("ConcreteStateA handles the state.")
	// Perform state-specific logic here
	context.SetState(&ConcreteStateB{})
}

// ConcreteStateB represents another concrete state
type ConcreteStateB struct{}

func (s *ConcreteStateB) HandleState(context *Context) {
	fmt.Println("ConcreteStateB handles the state.")
	// Perform state-specific logic here
	context.SetState(&ConcreteStateA{})
}

func main() {
	context := &Context{}

	// Set the initial state
	context.SetState(&ConcreteStateA{})

	// Perform state transitions
	context.Request()
	context.Request()
	context.Request()
}

```

<h3> Template Method Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p>Template Method Pattern: Xác định cấu trúc của một thuật toán trong một phương thức mẹ và cho phép các lớp con triển khai các bước cụ thể của thuật toán đó.
</p>

```go
package main

import "fmt"

// AbstractClass defines the template method and abstract methods
type AbstractClass interface {
	TemplateMethod()
	PrimitiveOperation1()
	PrimitiveOperation2()
}

// ConcreteClass implements the AbstractClass interface
type ConcreteClass struct{}

func (c *ConcreteClass) TemplateMethod() {
	c.PrimitiveOperation1()
	c.PrimitiveOperation2()
}

func (c *ConcreteClass) PrimitiveOperation1() {
	fmt.Println("ConcreteClass: Primitive Operation 1")
}

func (c *ConcreteClass) PrimitiveOperation2() {
	fmt.Println("ConcreteClass: Primitive Operation 2")
}

func main() {
	// Create an instance of ConcreteClass
	concrete := &ConcreteClass{}

	// Call the template method
	concrete.TemplateMethod()
}

```

<h3> Chain of Responsibility Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p>Chain of Responsibility Pattern: Cho phép nhiều đối tượng xử lý một yêu cầu theo một chuỗi, cho đến khi yêu cầu được xử lý hoặc đi qua toàn bộ chuỗi.</p>

```go
package main

import "fmt"

// Request represents a request to be processed
type Request struct {
	message string
}

// Handler defines the interface for handling requests
type Handler interface {
	SetNext(handler Handler)
	HandleRequest(request Request)
}

// ConcreteHandler1 handles requests of type 1
type ConcreteHandler1 struct {
	nextHandler Handler
}

func (h *ConcreteHandler1) SetNext(handler Handler) {
	h.nextHandler = handler
}

func (h *ConcreteHandler1) HandleRequest(request Request) {
	if request.message == "Type1" {
		fmt.Println("ConcreteHandler1 handles the request.")
	} else if h.nextHandler != nil {
		h.nextHandler.HandleRequest(request)
	} else {
		fmt.Println("No handler can process the request.")
	}
}

// ConcreteHandler2 handles requests of type 2
type ConcreteHandler2 struct {
	nextHandler Handler
}

func (h *ConcreteHandler2) SetNext(handler Handler) {
	h.nextHandler = handler
}

func (h *ConcreteHandler2) HandleRequest(request Request) {
	if request.message == "Type2" {
		fmt.Println("ConcreteHandler2 handles the request.")
	} else if h.nextHandler != nil {
		h.nextHandler.HandleRequest(request)
	} else {
		fmt.Println("No handler can process the request.")
	}
}

// ConcreteHandler3 handles requests of type 3
type ConcreteHandler3 struct {
	nextHandler Handler
}

func (h *ConcreteHandler3) SetNext(handler Handler) {
	h.nextHandler = handler
}

func (h *ConcreteHandler3) HandleRequest(request Request) {
	if request.message == "Type3" {
		fmt.Println("ConcreteHandler3 handles the request.")
	} else if h.nextHandler != nil {
		h.nextHandler.HandleRequest(request)
	} else {
		fmt.Println("No handler can process the request.")
	}
}

func main() {
	// Create the chain of handlers
	handler1 := &ConcreteHandler1{}
	handler2 := &ConcreteHandler2{}
	handler3 := &ConcreteHandler3{}

	handler1.SetNext(handler2)
	handler2.SetNext(handler3)

	// Process the requests
	request1 := Request{message: "Type1"}
	handler1.HandleRequest(request1)

	request2 := Request{message: "Type2"}
	handler1.HandleRequest(request2)

	request3 := Request{message: "Type3"}
	handler1.HandleRequest(request3)

	request4 := Request{message: "Type4"}
	handler1.HandleRequest(request4)
}

```

<h3> Mediator Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Mediator Pattern là một mô hình thiết kế phần mềm giúp quản lý sự tương tác giữa các đối tượng thông qua một đối tượng trung gian gọi là Mediator.</p>

```go
package main

import "fmt"

// Mediator interface declares the communication methods
type Mediator interface {
	SendMessage(message string, colleague Colleague)
}

// Colleague interface declares the methods for the colleagues
type Colleague interface {
	Send(message string)
	Receive(message string)
}

// ConcreteMediator implements the Mediator interface
type ConcreteMediator struct {
	colleague1 Colleague
	colleague2 Colleague
}

func (m *ConcreteMediator) SendMessage(message string, colleague Colleague) {
	if colleague == m.colleague1 {
		m.colleague2.Receive(message)
	} else if colleague == m.colleague2 {
		m.colleague1.Receive(message)
	}
}

// ConcreteColleague1 implements the Colleague interface
type ConcreteColleague1 struct {
	mediator Mediator
}

func (c *ConcreteColleague1) Send(message string) {
	fmt.Println("Colleague 1 sends:", message)
	c.mediator.SendMessage(message, c)
}

func (c *ConcreteColleague1) Receive(message string) {
	fmt.Println("Colleague 1 receives:", message)
}

// ConcreteColleague2 implements the Colleague interface
type ConcreteColleague2 struct {
	mediator Mediator
}

func (c *ConcreteColleague2) Send(message string) {
	fmt.Println("Colleague 2 sends:", message)
	c.mediator.SendMessage(message, c)
}

func (c *ConcreteColleague2) Receive(message string) {
	fmt.Println("Colleague 2 receives:", message)
}

func main() {
	mediator := &ConcreteMediator{}

	colleague1 := &ConcreteColleague1{mediator: mediator}
	colleague2 := &ConcreteColleague2{mediator: mediator}

	mediator.colleague1 = colleague1
	mediator.colleague2 = colleague2

	colleague1.Send("Hello from Colleague 1")
	colleague2.Send("Hi from Colleague 2")
}

```

<h3> Mementor Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p> Popular: &#9733; &#9733; &#x2606; &#x2606; &#x2606;</p>
<p>Memento Pattern là một mô hình thiết kế giúp lưu trữ và khôi phục trạng thái của một đối tượng.</p>

```go
package main

import "fmt"

// Memento represents the stored state of the originator
type Memento struct {
	state string
}

// Originator represents the object whose state needs to be saved and restored
type Originator struct {
	state string
}

func (o *Originator) SetState(state string) {
	fmt.Println("Setting state to:", state)
	o.state = state
}

func (o *Originator) Save() *Memento {
	fmt.Println("Saving state.")
	return &Memento{state: o.state}
}

func (o *Originator) Restore(m *Memento) {
	fmt.Println("Restoring state.")
	o.state = m.state
}

// Caretaker manages the memento objects
type Caretaker struct {
	memento *Memento
}

func (c *Caretaker) SetMemento(m *Memento) {
	c.memento = m
}

func (c *Caretaker) GetMemento() *Memento {
	return c.memento
}

func main() {
	originator := &Originator{}
	caretaker := &Caretaker{}

	originator.SetState("State 1")
	caretaker.SetMemento(originator.Save())

	originator.SetState("State 2")

	// Restore to previous state
	originator.Restore(caretaker.GetMemento())

	fmt.Println("Current state:", originator.state)
}

```

<h3> Interpreter Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#9733; </p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p>Mô hình Interpreter là một mô hình thiết kế phần mềm dùng để định nghĩa cách diễn giải và thực thi một ngôn ngữ hoặc biểu diễn cú pháp đặc biệt.</p>

```go
package main

import (
	"fmt"
	"strconv"
	"strings"
)

// Expression interface declares the Interpret method for interpreting expressions
type Expression interface {
	Interpret() int
}

// Number represents a numeric expression
type Number struct {
	value int
}

func (n *Number) Interpret() int {
	return n.value
}

// Add represents an addition expression
type Add struct {
	left  Expression
	right Expression
}

func (a *Add) Interpret() int {
	return a.left.Interpret() + a.right.Interpret()
}

// Subtract represents a subtraction expression
type Subtract struct {
	left  Expression
	right Expression
}

func (s *Subtract) Interpret() int {
	return s.left.Interpret() - s.right.Interpret()
}

// Multiply represents a multiplication expression
type Multiply struct {
	left  Expression
	right Expression
}

func (m *Multiply) Interpret() int {
	return m.left.Interpret() * m.right.Interpret()
}

// Divide represents a division expression
type Divide struct {
	left  Expression
	right Expression
}

func (d *Divide) Interpret() int {
	return d.left.Interpret() / d.right.Interpret()
}

// Parser represents the expression parser
type Parser struct {
	tokens []string
}

func (p *Parser) Parse() Expression {
	token := p.nextToken()

	if isNumber(token) {
		value, _ := strconv.Atoi(token)
		return &Number{value: value}
	} else if token == "+" {
		left := p.Parse()
		right := p.Parse()
		return &Add{left: left, right: right}
	} else if token == "-" {
		left := p.Parse()
		right := p.Parse()
		return &Subtract{left: left, right: right}
	} else if token == "*" {
		left := p.Parse()
		right := p.Parse()
		return &Multiply{left: left, right: right}
	} else if token == "/" {
		left := p.Parse()
		right := p.Parse()
		return &Divide{left: left, right: right}
	}

	return nil
}

func (p *Parser) nextToken() string {
	if len(p.tokens) > 0 {
		token := p.tokens[0]
		p.tokens = p.tokens[1:]
		return token
	}
	return ""
}

func isNumber(token string) bool {
	_, err := strconv.Atoi(token)
	return err == nil
}

func main() {
	expression := "3 * (4 + 2) / 6"
	tokens := strings.Split(expression, " ")

	parser := &Parser{tokens: tokens}
	result := parser.Parse().Interpret()

	fmt.Printf("Expression '%s' evaluates to %d\n", expression, result)
}

```

<h3> Visitor Pattern </h3>
<p> Level of difficult: &#9733; &#9733; &#9733; &#9733; &#x2606;</p>
<p> Popular: &#9733; &#x2606; &#x2606; &#x2606; &#x2606;</p>
<p>Visitor Pattern là một mô hình thiết kế phần mềm cho phép thực hiện các thao tác trên các đối tượng trong một cấu trúc đối tượng mà không làm thay đổi cấu trúc đó.</p>

```go
package main

import "fmt"

// Component interface represents the elements that can be visited
type Component interface {
	Accept(Visitor)
}

// ConcreteComponent represents a concrete element that can be visited
type ConcreteComponent struct {
	Name string
}

func (c *ConcreteComponent) Accept(visitor Visitor) {
	visitor.VisitConcreteComponent(c)
}

// Visitor interface declares the Visit methods for each element type
type Visitor interface {
	VisitConcreteComponent(*ConcreteComponent)
}

// ConcreteVisitor1 implements Visitor and defines the behavior for visiting ConcreteComponent
type ConcreteVisitor1 struct{}

func (v *ConcreteVisitor1) VisitConcreteComponent(c *ConcreteComponent) {
	fmt.Printf("ConcreteVisitor1 visited %s\n", c.Name)
}

// ConcreteVisitor2 implements Visitor and defines the behavior for visiting ConcreteComponent
type ConcreteVisitor2 struct{}

func (v *ConcreteVisitor2) VisitConcreteComponent(c *ConcreteComponent) {
	fmt.Printf("ConcreteVisitor2 visited %s\n", c.Name)
}

func main() {
	component1 := &ConcreteComponent{Name: "Component 1"}
	component2 := &ConcreteComponent{Name: "Component 2"}

	visitor1 := &ConcreteVisitor1{}
	visitor2 := &ConcreteVisitor2{}

	component1.Accept(visitor1) // Output: ConcreteVisitor1 visited Component 1
	component2.Accept(visitor2) // Output: ConcreteVisitor2 visited Component 2
}

```

