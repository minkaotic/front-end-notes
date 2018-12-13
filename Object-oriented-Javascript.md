# Object-Oriented Javascript

## Contents
- [Basics](#basics)
- [JS Class Syntax](#js-class-syntax)

_______________

## Basics
#### Object literals
- *Object literals* are useful when modelling one single, specific thing. E.g.:
  ```
  const ernie = {
    species: 'dog',
    age: 1,
    breed: 'pug',
    bark: function(){
      console.log('Woof!');
    }
  }
  ```
- To add a property or method to an object literal, simply assign it to the object: `ernie.color = 'black';`

#### Accessing object properties & methods
- Object properties can be accessed through either dot notation or bracket notation:

  | ***dot notation***         | ***bracket notation***        |
  | -------------------------- |-------------------------------|
  | `console.log(ernie.age);`  | `console.log(ernie['age']);`  |
  | `console.log(ernie.breed);`| `console.log(ernie['breed']);`|
  | `ernie.bark();`            | `ernie['bark']();`            |

- *Bracket notation* is useful when there is a need to generate dynamic properties, as the property name can be stored in a variable, and the objects property can then be accessed via that variable (*see example below*). It also allows you to create and access properties that may have spaces in the property key - perfect for handling JSON data.

  ```
  var prop = 'breed';
  console.log(ernie[prop]);
  ```
  
## JS Class Syntax
To represent types with the same (or similar) properties, classes are much more robust than object literals. Class syntax was **introduced to Javascript in ES2015**, and comprises syntactic sugar on top of its original prototype syntax.

***A simple example***
```
class Pet {
  constructor(species, age, breed, sound) {
    this.species = animal;
    this.age = age;
    this.breed = breed;
    this.sound = sound;
  }
  
  speak() {
    console.log(this.sound);
  }
}

const ernie = new Pet('dog', 1, 'pug', 'woof!');
ernie.speak();
```

***Things to note***
- In JS, a class *can only have one constructor*. 
- In order to create an instance without any arguments, you can however set defaults, for example:
  ```
  constructor(species = 'dog', age = 0, breed = 'unknown')
  ```
- **NB:** Declaring methods inside a class *doesn't* use the function keyword!
