# Table of Contents

- [Introduce](#introduce)
- [Patterns](#patterns)
  - [Creational Patterns](#creational-patterns)
    - [Abstract Factory](#abstract-factory-★★★★★)
    - [Factory](#factory-★★★★★)
    - [Singleton](#singleton-★★★★)
    - [Prototype](#prototype-★★★)
    - [Builder](#builder-★★)
  - [Structural Patterns](#structural-patterns)
    - [Facade](#facade-★★★★★)
    - [Proxy](#proxy-★★★★)
    - [Adapter](#adapter-★★★★)
    - [Composite](#composite-★★★★)
    - [Bridge](#bridge-★★★)
    - [Decorator](#decorator-★★★)
    - [Flyweight](#flyweight-★)
  - [Behavioral Patterns](#behavioral-patterns)
    - [Iterator](#iterator-★★★★★)
    - [Observer](#observer-★★★★★)
    - [Strategy](#strategy-★★★★)
    - [Command](#command-★★★★)
    - State(★★★)
    - Template Method(★★★)
    - Chain of Responsibility(★★)
    - Mediator(★★)
    - Memento(★★)
    - Interpreter(★)
    - Visitor(★)
- [References](#references)

# Introduce

- Design patterns are typical solutions to commonly occurring problems in software design.
- They are like pre-made blueprints that you can customize to solve a recurring design problem in your code.

# Patterns

## Creational Patterns

### Abstract Factory (★★★★★)

#### Intent

- Abstract Factory pattern lets you produce families of related objects without specifying their concrete classes.

#### Example

```bash
class ShapeFactory {
  createShape() {
    throw new Error('createShape method must be implemented.');
  }
}

class CircleFactory extends ShapeFactory {
  createShape() {
    return new Circle();
  }
}

class SquareFactory extends ShapeFactory {
  createShape() {
    return new Square();
  }
}

class Shape {
  draw() {
    console.log('Drawing a shape.');
  }
}

class Circle extends Shape {
  draw() {
    console.log('Drawing a circle.');
  }
}

class Square extends Shape {
  draw() {
    console.log('Drawing a square.');
  }
}

const circleFactory = new CircleFactory();
const circle = circleFactory.createShape();
circle.draw(); // Output: Drawing a circle.

const squareFactory = new SquareFactory();
const square = squareFactory.createShape();
square.draw(); // Output: Drawing a square.
```

### Factory (★★★★★)

Also known as: Virtual Constructor.

#### Intent

- Factory pattern provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.
- 3 main characters:
  - Factory (Ex: ShapeFactory)
  - Product (Ex: Shape)
  - Concrete product (Ex: Square, Circle)

#### Example

- Example 1 (easy):

```bash
class ShapeFactory {
  static createShape(type) {
    switch (type) {
      case 'square':
        return new Square();
      case 'circle':
        return new Circle();
      default:
        throw new Error('Invalid shape type.');
    }
  }
}

class Shape {
  draw() {
    console.log("Drawing a shape.");
  }
}

class Square extends Shape {
  draw() {
    console.log("Drawing a square.");
  }
}

class Circle extends Shape {
  draw() {
    console.log("Drawing a circle.");
  }
}

const square = ShapeFactory.createShape('square');
square.draw();

const circle = ShapeFactory.createShape('circle');
circle.draw();
```

- Example 2 (medium):

```bash
class Transport {
  constructor(cargoVolume) {
    const cargoVolumeMap = new Map([
      ['5kg', 'bike'],
      ['10kg', 'car'],
      ['20kg', 'truck']
    ]);
    this.transport = cargoVolumeMap.get(cargoVolume);
  }

  getTransport() {
    return this.transport;
  }
}

class TransportService {
  transport = Transport;
  getTransport(cargoVolume) {
    return new this.transport(cargoVolume).getTransport();
  }
}

const service = new TransportService();
console.log('Transport:', service.getTransport('10kg'));

// just insert new transport, no need to edit the class above
class Shipping extends Transport {
  constructor(cargoVolume) {
    super(cargoVolume);
    const cargoVolumeMap = new Map([
      ['50kg', 'boat'],
      ['100kg', 'ship'],
      ['200kg', 'mothership']
    ]);
    this.transport = cargoVolumeMap.get(cargoVolume);
  }
}

class ShippingService extends TransportService {
  transport = Shipping;
}

const shipping = new ShippingService();
console.log('Transport:', shipping.getTransport('50kg'));
```

### Singleton (★★★★)

#### Intent

- Singleton pattern lets you ensure that a class has only one instance, while providing a global access point to this instance.

#### Example

Example 1:

```bash
class Singleton {
  static instance;

  constructor() {
    this.message = "Hello world!";
  }

  static getInstance() {
    if (!this.instance) {
      this.instance = new Singleton();
    }
    return this.instance;
  }
}

const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2, instance1.message);
```

Example 2: Round Robin (Load balancing architecture)

```bash
class RoundRobin {
  constructor() {
    if (RoundRobin.instance) {
      return RoundRobin.instance;
    }
    RoundRobin.instance = this;

    this.servers = [];
    this.index = 0;
  }

  addServer(server) {
    this.servers.push(server);
  }

  getNextServer() {
    if(!this.servers.length) {
      throw new Error('No server available !');
    }

    const server = this.servers[this.index];
    this.index = (this.index + 1) % this.servers.length;

    return server;
  }
}

const loadBalancer1 = new RoundRobin();
const loadBalancer2 = new RoundRobin();

console.log(loadBalancer1, loadBalancer2, loadBalancer1 === loadBalancer2);

loadBalancer1.addServer('Server 1');
loadBalancer1.addServer('Server 2');
loadBalancer1.addServer('Server 3');

const REQUEST_LENGTH = 10;

for(let i = 0; i < REQUEST_LENGTH; i++) {
  console.log(loadBalancer1.getNextServer());
}
```

### Prototype (★★★★)

#### Intent

- Prototype pattern lets you copy existing objects without making your code dependent on their classes.

#### Example

```bash
class Shape {
  constructor(type) {
    this.type = type;
  }

  shallowClone() {
    return new this.constructor(this.type);
  }

  deepClone() {
    const cloned = new this.constructor(this.type);
    for (let key in this) {
      if (typeof this[key] === 'object' && this[key] !== null) {
        cloned[key] = this[key].deepClone();
      } else {
        cloned[key] = this[key];
      }
    }
    return cloned;
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super('Rectangle');
    this.width = width;
    this.height = height;
  }
}

class Circle extends Shape {
  constructor(radius) {
    super('Circle');
    this.radius = radius;
  }
}

const rectangle = new Rectangle(10, 5);
const circle = new Circle(8);

const rectangleShallowClone = rectangle.shallowClone();
const circleShallowClone = circle.shallowClone();

console.log(rectangleShallowClone); // Output: Rectangle { type: 'Rectangle', width: 'Rectangle', height: undefined }
console.log(circleShallowClone); // Output: Circle { type: 'Circle', radius: 'Circle' }

const rectangleDeepClone = rectangle.deepClone();
const circleDeepClone = circle.deepClone();

console.log(rectangleDeepClone); // Output: Rectangle { type: 'Rectangle', width: 10, height: 5 }
console.log(circleDeepClone); // Output: Circle { type: 'Circle', radius: 8 }
```

### Builder (★★)

#### Intent

- Builder pattern lets you construct complex objects step by step
- Builder pattern allows you to produce different types and representations of an object using the same construction code.

#### Example

```bash
class Player {
  constructor(builder) {
    this.name = builder.name;
    this.age = builder.age;
    this.nationality = builder.nationality;
  }

  toString() {
    const result = [];
    if (this.name) {
      result.push(`Name: ${this.name}`);
    }
    if (this.age) {
      result.push(`Age: ${this.age}`);
    }
    if (this.nationality) {
      result.push(`Nationality: ${this.nationality}`);
    }
    return result.join(', ');
  }
}

class PlayerBuilder {
  constructor() {
    this.name = '';
    this.age = 0;
    this.nationality = '';
  }

  addName(name) {
    this.name = name;
    return this;
  }

  addAge(age) {
    this.age = age;
    return this;
  }

  addNationality(nationality) {
    this.nationality = nationality;
    return this;
  }

  createBuilder() {
    return new PlayerBuilder();
  }

  build() {
    return new Player(this);
  }
}

const builder = new PlayerBuilder();
const cr7 = builder.createBuilder().addName('CR7').addAge(38).addNationality('Portugal').build();
console.log(cr7.toString());

const m10 = builder.createBuilder().addName('M10').addAge(36).build();
console.log(m10.toString());
```

## Structural Patterns

### Facade (★★★★★)

#### Intent

- Facade pattern provides a simplified interface to a library, a framework, or any other complex set of classes.

#### Example

```bash
class Discount {
  calc (value) {
    return value * 0.9;
  }
}

class Shipping {
  calc () {
    return 5;
  }
}

class Fees {
  calc (value) {
    return value * 1.05;
  }
}

class ShopeeFacadePattern {
  constructor() {
    this.discount = new Discount();
    this.shipping = new Shipping();
    this.fees = new Fees();
  }

  calc(price) {
    price = this.discount.calc(price);
    price = this.fees.calc(price);
    price += this.shipping.calc();
    return price;
  }
}

function buy(price) {
  const shopee = new ShopeeFacadePattern();
  console.log('Price: ', shopee.calc(price));
}

buy(100000);
```

### Proxy (★★★★)

#### Intent

- Proxy pattern lets you provide a substitute or placeholder for another object.
- Proxy pattern controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

#### Example

```bash
class Boss {
  receiveRequest(offer) {
    console.log('Developer offer::::', offer);
  }
}

class Manager {
  constructor() {
    this.boss = new Boss();
  }

  receiveRequest(offer) {
    this.boss.receiveRequest(offer);
  }
}

class Developer {
  constructor(offer) {
    this.offer = offer;
  }

  request(target) {
    target.receiveRequest(this.offer);
  }
}

const developer = new Developer('2000$');
developer.request(new Manager());
```

### Adapter (★★★★)

#### Intent

- Adapter pattern allows objects with incompatible interfaces to collaborate.

#### Example

```bash
class OldShipping {
  request(zipStart, zipEnd, weight) {
    // ...
    return "$49.75";
  }
}

class NewShipping {
  login(credentials) {
    // ...
  }
  setStart(start) {
    // ...
  }
  setDestination(destination) {
    // ...
  }
  calculate(weight) {
    return "$39.50";
  }
}

class Adapter {
  constructor(credentials) {
    this.credentials = credentials;
  }

  adapt() {
    const shipping = new NewShipping();
    shipping.login(this.credentials);

    return {
      request: function (zipStart, zipEnd, weight) {
        shipping.setStart(zipStart);
        shipping.setDestination(zipEnd);
        return shipping.calculate(weight);
      },
    };
  }
}

function run() {
  const oldShipping = new OldShipping();

  const oldCost = oldShipping.request("78701", "10010", "2 lbs");
  console.log("Old cost: " + oldCost);

  // new shipping object with adapted interface
  const credentials = { token: "30a8-6ee1" };
  const adapter = new Adapter(credentials);

  const newCost = adapter.adapt().request("78701", "10010", "2 lbs");
  console.log("New cost: " + newCost);
}
run();
```

### Composite (★★★★)

#### Intent

- Composite pattern lets you compose objects into tree structures and then work with these structures as if they were individual objects.

#### Example

```bash
class MenuItem {
  constructor(name) {
    this.name = name;
  }

  display(depth) {
    console.log('-'.repeat(depth) + this.name);
  }
}

class Menu extends MenuItem {
  constructor(name) {
    super(name);
    this.children = [];
  }

  add(menuItem) {
    this.children.push(menuItem);
  }

  remove(menuItem) {
    const index = this.children.indexOf(menuItem);
    if (index !== -1) {
      this.children.splice(index, 1);
    }
  }

  display(depth = 0) {
    super.display(depth);
    this.children.forEach((child) => {
      child.display(depth + 2);
    });
  }

  listChildren() {
    console.log(this.children);
  }
}

const children = new Menu("Share");
children.add(new MenuItem("Import"));
children.add(new MenuItem("Export"));

const fileMenu = new Menu("File");
fileMenu.add(new MenuItem("New"));
fileMenu.add(new MenuItem("Open"));
fileMenu.add(new MenuItem("Save"));
fileMenu.add(new MenuItem("Exit"));
fileMenu.add(children);

const editMenu = new Menu("Edit");
editMenu.add(new MenuItem("Cut"));
editMenu.add(new MenuItem("Copy"));
editMenu.add(new MenuItem("Paste"));
editMenu.add(new MenuItem("Undo"));
editMenu.add(new MenuItem("Redo"));

const mainMenu = new Menu("Main Menu");
mainMenu.add(fileMenu);
mainMenu.add(editMenu);

mainMenu.listChildren();
mainMenu.display();
```

### Bridge (★★★)

#### Intent

- Bridge pattern lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently of each other.

#### Example

```bash
class PaymentProcess {
  pay(amount) {}
}

class VisaPaymentProcess extends PaymentProcess {
  constructor(cardNumber, cvv, expired) {
    super();
    this.cardNumber = cardNumber;
    this.cvv = cvv;
    this.expired = expired;
  }

  pay(amount) {
    console.log(`Paying ${amount}USD by visa card ${this.cardNumber} ...`);
  }
}

class MomoPaymentProcess extends PaymentProcess {
  constructor(phoneNumber) {
    super();
    this.phoneNumber = phoneNumber;
  }

  pay(amount) {
    console.log(`Paying ${amount}VND by momo ${this.phoneNumber} ...`);
  }
}

class MemberRegistration {
  constructor(paymentProcessor) {
    this.paymentProcessor = paymentProcessor;
  }

  register(amount) {
    this.paymentProcessor.pay(amount);
    console.log('Register Youtube membership success.')
  }
}

const visaPaymentProcess = new VisaPaymentProcess('0000-1111-2222-3333', '123', '12/25');
const visaRegistration = new MemberRegistration(visaPaymentProcess);
visaRegistration.register(1.5);


const momoPaymentProcess = new MomoPaymentProcess('0123456789');
const momoRegistration = new MemberRegistration(momoPaymentProcess);
momoRegistration.register(30000);
```

### Decorator (★★★)

#### Intent

- Decorator pattern lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

#### Example

```bash
class Coffee {
  cost() {
    return 10;
  }

  description() {
    return 'Coffee';
  }
}

// Decorator: Decorator base class
class CoffeeDecorator extends Coffee {
  constructor(coffee) {
    super();
    this.coffee = coffee;
  }

  cost() {
    return this.coffee.cost();
  }

  description() {
    return this.coffee.description();
  }
}

// Concrete Decorator: Milk
class Milk extends CoffeeDecorator {
  constructor(coffee) {
    super(coffee);
  }

  cost() {
    return this.coffee.cost() + 2;
  }

  description() {
    return this.coffee.description() + ', Milk';
  }
}

// Concrete Decorator: Sugar
class Sugar extends CoffeeDecorator {
  constructor(coffee) {
    super(coffee);
  }

  cost() {
    return this.coffee.cost() + 1;
  }

  description() {
    return this.coffee.description() + ', Sugar';
  }
}

let coffee = new Coffee();
console.log(coffee.description(), '$', coffee.cost());

coffee = new Milk(coffee);
console.log(coffee.description(), '$', coffee.cost());

coffee = new Sugar(coffee);
console.log(coffee.description(), '$', coffee.cost());
```

### Flyweight (★)

#### Intent

- Flyweight pattern lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.

#### Example

```bash
class Flyweight {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }
}

class FlyweightFactory {
  constructor() {
    this.flyweights = {};
  }

  get(brand, model) {
    const key = brand + " - " + model;
    if (!this.flyweights[key]) {
      this.flyweights[key] = new Flyweight(brand, model);
    }
    return this.flyweights[key];
  }

  getAll() {
    return JSON.stringify(this.flyweights, null, 2);
  }

  count() {
    return Object.keys(this.flyweights).length;
  }
}

class ComputerCollection {
  constructor() {
    this.computers = {};
  }

  add(id, brand, model, ram) {
    this.computers[model + " - " + ram] = new Computer(id, brand, model, ram);
  }

  get(model, ram) {
    return this.computers[model + " - " + ram];
  }

  getAll() {
    return JSON.stringify(this.computers, null, 2);
  }

  count() {
    return Object.keys(this.computers).length;
  }
}

class Computer {
  constructor(id, brand, model, ram) {
    this.id = id;
    this.ram = ram;
    this.flyweight = globalFlyweightFactory.get(brand, model);
  }
}

function run() {
  const computers = new ComputerCollection();

  computers.add("001", "Asus", "ExpertBook", "8GB");
  computers.add("002", "Asus", "ExpertBook", "16GB");
  computers.add("003", "Asus", "VivoBook", "8GB");
  computers.add("004", "Asus", "VivoBook", "16GB");
  computers.add("005", "Apple", "Macbook Air", "8GB");
  computers.add("006", "Apple", "Macbook Air", "16GB");
  computers.add("007", "Apple", "Macbook Pro", "8GB");
  computers.add("008", "Apple", "Macbook Pro", "16GB");
  computers.add("009", "Apple", "Macbook Pro", "32GB");

  console.log("Count Computers: " + computers.count());
  console.log("Count Models: " + globalFlyweightFactory.count());

  console.log("Total Computers: " + computers.getAll());
  console.log("Total Models: " + globalFlyweightFactory.getAll());
}

const globalFlyweightFactory = new FlyweightFactory();
run();
```

## Behavioral Patterns

### Iterator (★★★★★)

#### Intent

- Iterator pattern lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).

#### Example

```bash
class CustomList {
  constructor() {
    this.list = [];
  }

  add(item) {
    this.list.push(item);
  }

  getIterator() {
    return new ListIterator(this);
  }
}

class ListIterator {
  constructor(list) {
    this.list = list.list;
    this.index = 0;
  }

  hasNext() {
    return this.index < this.list.length;
  }

  next() {
    return this.list[this.index++];
  }
}

const customList = new CustomList();
customList.add("item1");
customList.add("item2");
customList.add("item3");

const iterator = customList.getIterator();
while (iterator.hasNext()) {
  console.log(iterator.next());
}
```

### Observer (★★★★★)

Also known as: Event-Subscriber, Listener (Publish - Subscribe pattern).

#### Intent

- Observer pattern lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.

#### Example

```bash
class Observer {
	constructor(name) {
		this.namePick = name;
	}

	updateStatus(location) {
		this.goToHelp(location);
	}

	goToHelp(location) {
		console.log(`${this.namePick}::::PING::::${location}`);
	}
}

class Subject {
	constructor(name) {
		this.observers = [];
	}

	addObserver(observer) {
		this.observers.push(observer);
	}

	notify(location) {
		this.observers.forEarch(observer => observer.updateStatus(location));
	}
}

const ob1 = new Observer('Observer1');
const ob2 = new Observer('Observer2');

const subject = new Subject();
subject.addObserver(ob1);
subject.addObserver(ob2);

subject.notify('TPHCM');
```

### Strategy (★★★★)

#### Intent

- Strategy pattern lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.

#### Example

```bash
function normalPrice(originalPrice) {
	return originalPrice * 1;
}

function preOrderPrice(originalPrice) {
	return originalPrice * 0.8;
}

function blackFridayPrice(originalPrice) {
	return originalPrice * 0.5;
}

const getPriceStrategies = {
	normal: normalPrice,
	preOrder: preOrderPrice,
	blackFriday: blackFridayPrice
}

function getPrice(type, originalPrice) {
	return getPriceStrategies[type](originalPrice);
}

getPrice('normal', 100000);
```

### Command (★★★★)

#### Intent

- Command pattern turns a request into a stand-alone object that contains all information about the request.
- This transformation lets you pass requests as a method arguments, delay or queue a request’s execution, and support undoable operations.

#### Example

```bash
class Command {
  execute() {}
}

class TurnOnCommand extends Command {
  constructor(receiver) {
    super();
    this.receiver = receiver;
  }

  execute() {
    this.receiver.turnOn();
  }
}

class TurnOffCommand extends Command {
  constructor(receiver) {
    super();
    this.receiver = receiver;
  }

  execute() {
    this.receiver.turnOff();
  }
}

class Light {
  turnOn() {
    console.log("Light is on");
  }

  turnOff() {
    console.log("Light is off");
  }
}

class RemoteControl {
  constructor() {
    this.command = null;
  }

  setCommand(command) {
    this.command = command;
  }

  pressButton() {
    this.command.execute();
  }
}

const light = new Light();
const turnOnCommand = new TurnOnCommand(light);
const turnOffCommand = new TurnOffCommand(light);

const remote = new RemoteControl();

remote.setCommand(turnOnCommand);
remote.pressButton();

remote.setCommand(turnOffCommand);
remote.pressButton();
```

# References

- https://refactoring.guru/design-patterns
- https://www.youtube.com/watch?v=l84-JRQ95V4&list=PLw0w5s5b9NK7TSuHpxOMvVtRuaEgHQczQ&ab_channel=TipsJavascript

---
