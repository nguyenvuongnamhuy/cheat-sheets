Reference: https://www.freecodecamp.org/news/solid-design-principles-in-software-development

# Table of Contents

- [Definition](#definition)
- [SOLID](#solid)
  - [S](#single-responsibility-principle-srp)
  - [O](#open-closed-principle-ocp)
  - [L](#liskov-substitution-principle-lsp)
  - [I](#interface-segregation-principle-isp)
  - [D](#dependency-inversion-principle-dip)

# Definition

- SOLID is a set of five design principles that help software developers design robust, testable, extensible, and maintainable object-oriented software systems.

# SOLID

## Single Responsibility Principle (SRP)

### Intent

- The single responsibility principle states that a class, module, or function should have only one reason to change, meaning it should do one thing.

### Example

```bash
class Order {
	constructor (userId) {
		this.userId = userId;
		this.orderTime = new Date();
		this.products = [];
	}
}

class OrderManagement {
	constructor() {
		this.order = null;
	}

	createOrder(userId) {
		this.order = new Order(userId);
	}

	addProducts(product) {
		this.order.products.push(product);
	}

	getOrder() {
		return this.order;
	}

	validateOrder() {
		return this.order.products.length > 0;
	}

	lastActionBeforeSendMail() {
		// must
		if (!this.validateOrder()) {
			throw new Error('error');
		}

		// must not
		// if (!this.order.products.length > 0) {
		//   throw new Error('error');
		// }

		// must
		const emailHandler = new EmailHandler();
		emailHandler.sendMail(this.order);

		// must not
		// console.log('Send confirmation mail to customer success', this.order);
	}
}

class EmailHandler {
	sendMail(order) {
		console.log('Send confirmation mail to customer success', order);
	}
}

const orderManagement = new OrderManagement();

orderManagement.createOrder('u001');

orderManagement.addProducts({ id: 'p001', name: 'Milk', quantity: 1, price: '7000', unit: 'vnd' });
orderManagement.addProducts({ id: 'p002', name: 'Cake', quantity: 2, price: '10000', unit: 'vnd' });

orderManagement.getOrder();

orderManagement.lastActionBeforeSendMail();
```

## Open-Closed Principle (OCP)

### Intent

- The open-closed principle states that classes, modules, and functions should be open for extension but closed for modification.

### Example

```bash
class Animal {
  constructor(name, speedRate) {
    this.name = name;
    this.speedRate = speedRate;
  }

  getSpeed() {
    return this.speedRate.getSpeed();
  }
}

class SpeedRate {
  getSpeed() {
		return 0;
	}
}

class LionSpeedRate extends SpeedRate {
  getSpeed() {
    return 80;
  }
}

class ElephantSpeedRate extends SpeedRate {
  getSpeed() {
    return 40;
  }
}

const lion = new Animal('Lion', new LionSpeedRate());
console.log(`${lion.name} runs up to ${lion.getSpeed()} mph`);

const elephant = new Animal('Elephant', new ElephantSpeedRate());
console.log(`${elephant.name} runs up to ${elephant.getSpeed()} mph`);
```

## Liskov Substitution Principle (LSP)

### Intent

- The principle states that child classes or subclasses must be substitutable for their parent classes or super classes.
- In other words, the child class must be able to replace the parent class.
- This has the advantage of letting you know what to expect from your code.

### Example

```bash
class Animal {
  constructor(name) {
    this.name = name;
  }

  makeSound() {
    console.log(`${this.name} makes a sound`);
  }
}

class Cat extends Animal {
  makeSound() {
    console.log(`${this.name} meows`);s
  }
}

function makeAnimalSound(animal) {
  animal.makeSound();
}

const cheetah = new Animal('Cheetah');
makeAnimalSound(cheetah); // Cheetah makes a sound

const cat = new Cat('Khloe');
makeAnimalSound(cat); // Khloe meows

// must
class Bird extends Animal {
  makeSound() {
    console.log(`${this.name} chirps`);
  }

  fly() {
    console.log(`${this.name} flaps wings`);
  }
}

const parrot = new Bird('Titi the Parrot');
makeAnimalSound(parrot); // Titi the Parrot chirps
parrot.fly(); // Titi the Parrot flaps wings

// must not
// class Bird extends Animal {
// 	 fly() {
//     console.log(`${this.name} flaps wings`);
//   }
// }

// const parrot = new Bird('Titi the Parrot');
// makeAnimalSound(parrot); // Titi the Parrot makes a sound
// parrot.fly(); // Titi the Parrot flaps wings
```

## Interface Segregation Principle (ISP)

### Intent

- The interface segregation principle states that clients should not be forced to implement interfaces or methods they do not use.

### Example

```bash
class User {
	constructor(name) {
		this.name = name;
	}

	displayProfile() {
		console.log(`User: ${this.name}`);
	}
}

class NormalUser extends User {
	constructor(name) {
		super(name);
	}

	displaySettings() {
		console.log(`${this.name}: Displaying settings`);
	}
}

class Admin extends User {
	constructor(name) {
		super(name);
	}

	manageUsers() {
		console.log(`${this.name}: Managing users`);
	}
}

class Messageable extends Admin {
	constructor(name) {
		super(name);
	}

	sendMessage() {
		console.log(`${this.name}: Sending message`);
	}
}

const normalUser = new NormalUser("Normal User");
normalUser.displayProfile();
normalUser.displaySettings();

const admin = new Messageable("Admin");
admin.displayProfile();
admin.manageUsers();
admin.sendMessage();
```

## Dependency Inversion Principle (DIP)

### Intent

- The dependency inversion principle is about decoupling software modules. That is, making them as separate from one another as possible.

### Example

```bash
class Animal {
  constructor(name) {
    this.name = name;
  }

  getName() {
    return this.name;
  }
}

class Dog extends Animal {
  bark() {
    console.log('woof! woof!! woof!!!');
  }
}

class Cat extends Animal {
  meow() {
    console.log('meooow!');
  }
}

class Ape extends Animal {
  meow() {
    console.log('woo! woo! woo!');
  }
}

function printAnimalNames(animals) {
  for (let i = 0; i < animals.length; i++) {
		// must
    console.log(animals[i].getName());

		// must not
		// console.log(animals[i].name);
  }
}

const dog = new Dog('Jack');
const cat = new Cat('Zoey');

const animals = [dog, cat];
printAnimalNames(animals);
```

---
