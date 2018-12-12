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


