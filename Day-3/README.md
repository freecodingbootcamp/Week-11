# Week-11 -- Day-3

## OBJECTS AND OBJECT CONSTRUCTORS

//**************************************************************************************************
//* PLEASE READ																																	                      
//* https://www.theodinproject.com/courses/javascript/lessons/objects-and-object-constructors.
//* ************************************************************************************************
### Regular Object

```javascript
const myObject = {
  property: 'Value!',
  otherProperty: 77,
  "obnoxious property": function() {
    // do stuff!
 }
}
```

Lot's going on here. This object has three properties. Also, don't forget that an object in JavaScript consist of key value pairs.

The keys here are:
property
otherProperty
"obnoxious property"

The values are:
"Value!"
77   
function()  {  // do stuff!  }

You can have different types for the values. Here we have a string, number and a function!

Just to review how to access a value of an object:

```myObject.property```

OR

```myObject.["property"]```


 ### Object Constructors

```javascript
function Player(name, marker) {
  this.name = name
  this.marker = marker
}
```

```javascript
const player = new Player('steve', 'X')
console.log(player.name) // 'steve'
```

If you are coming from a Java background this should look very familiar. Funny how upset JavaScript or even Java developers would get if you compared JavaScript to Java but it seems JavaScript is looking more and more like Java at least from my perspective.

The example above should make sense by just looking at it. The only the new parts are the ```this``` and ```new``` keywords.

### Prototype

Just a heads up it's going to get a lot more confusing before things become somewhat more clear.
With that said let's introduce prototypes.

```javascript
function Student(name, grade) {
  this.name = name
  this.grade = grade
}

Student.prototype.sayName = function() {
  console.log(this.name)
}
Student.prototype.goToProm = function() {
  // eh.. go to prom?
}
```

You might be wondering what exactly is going on here?
All we are doing is extending the Student object by adding two functions to it.

So if you create a new Person object you can call on ```sayName``` and ```gotToProm```.  Don't forget to add the paranthesis () when you call of on them.   

```
let mustafa = new Student("Mustafa", 11);
console.log(mustafa.sayName());
```

Wait, there is more in case you are not confused enough. You can make one object extend another object. What this means is that the second object will inherit all the properties and functions of the first object.

```javascript
function Student() {
}

Student.prototype.sayName = function() {
  console.log(this.name)
}

function EighthGrader(name) {
  this.name = name
  this.grade = 8
}

EighthGrader.prototype = Object.create(Student.prototype)

const carl = new EighthGrader("carl")
carl.sayName() // console.logs "carl"
carl.grade // 8
```

Here carl which is an EighthGrader will inherit sayName function from Student.

Please read the the odin project page on this topic. The link should be towards the top of this section.

## FACTORY FUNCTIONS AND THE MODULE PATTERN

//**************************************************************************************************
//* PLEASE READ																																	                      
//* https://www.theodinproject.com/courses/javascript/lessons/factory-functions-and-the-module-pattern
//* ************************************************************************************************

### Factory Functions

Let us continue with confusing you. Hey maybe if you are confused enough you might reach some sort of enlightment state. Let's continue. This time we are going to introduce Factory functions.

```javascript
const personFactory = (name, age) => {
  const sayHello = () => console.log('hello!');
  return { name, age, sayHello };
};

const jeff = personFactory('jeff', 27);

console.log(jeff.name); // 'jeff'

jeff.sayHello(); // calls the function and logs 'hello!'
```

The part that are important is that factory functions do not use the keyword ```new``` and the ``` return { name, age, sayHello }; ``` part. We are returning an object! Also super important

```{ name, age, sayHello }``` is the same as ```{ name:name, age:age, sayHello:sayHello }```

Those are all the fields that we expose to the outside world. If you do not include your attribute or function in this list we cannot call on it from the outside!

POP QUIZ:

What would ```console.log(badGuy.health)``` return if we placed at the very end of the following code?

```javascript
const Player = (name, level) => {
  let health = level * 2;
  const getLevel = () => level;
  const getName  = () => name;
  const die = () => {
    // uh oh
  };
  const damage = x => {
    health -= x;
    if (health <= 0) {
      die();
    }
  };
  const attack = enemy => {
    if (level < enemy.getLevel()) {
      damage(1);
      console.log(`${enemy.getName()} has damaged ${name}`);
    }
    if (level >= enemy.getLevel()) {
      enemy.damage(1);
      console.log(`${name} has damaged ${enemy.getName()}`);
    }
  };
  return {attack, damage, getLevel, getName}
};

const jimmie = Player('jim', 10);
const badGuy = Player('jeff', 5);
jimmie.attack(badGuy);
```

I would be very impressed if you got it right! If you want to know the answer or see if you got it right just run the above code in a JavaScript compiler such as repl (https://repl.it)

#### Inheritance

Be prepared for the ultimate confusion bomb.

```javascript
const Person = (name) => {
  const sayName = () => console.log(`my name is ${name}`)
  return {sayName}
}

```

```javascript
const Nerd = (name) => {
  const prototype = Person(name)
  const doSomethingNerdy = () => console.log('nerd stuff')
  return Object.assign({}, prototype, {doSomethingNerdy})
}
```

Here we made Nerd a type of Person...imagine that. The two lines that made a Nerd a Person are

```const prototype =  Person(name)``` **and**  
```return Object.assign({}, prototype,  {doSomethingNerdy})```

Good luck understanding what is happening there. Just kidding, I will try to explain it.
Remember that in ```const prototype =  Person(name) ``` ```Person(name)``` just returns an object. We take object along with the object ```{doSomethingNerdy}``` and place into ```{}``` and finally just returning it. All of this is happening in

```return Object.assign({}, prototype, {doSomethingNerdy})```

### Module Pattern   

Yet another pattern or way of representing an object!

```javascript
const calculator = (() => {
  const add = (a, b) => a + b;
  const sub = (a, b) => a - b;
  const mul = (a, b) => a * b;
  const div = (a, b) => a / b;
  return {
    add,
    sub,
    mul,
    div,
  };
})();

calculator.add(3,5) // 8
calculator.sub(6,2) // 4
calculator.mul(14,5534) // 77476
```

Notice we don't use the keyword ```function``` and have two paranthesis () at the end of the const initialization. This is saying when you use calculator, calcualtor is automatically calling on itself!

![kramer from Seinfeld mind blown gesture](https://media.giphy.com/media/OK27wINdQS5YQ/giphy.gif)

When it calls on itself it returns a ...object you got it. This object is just all the calculator functions
add, sub, mul, div.

Don't worry if everything doesn't quiet fit into place just yet. Being aware of the most important aspects of all the concepts we just went over is good enough for now. This stuff will come in handy when we are ready to go over react.
