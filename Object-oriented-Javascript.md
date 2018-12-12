# Object-Oriented Javascript

## Contents
- [Basics](#basics)

_______________

## Basics
- ***Object literals*** are useful when modelling one single, specific thing. E.g.:
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
