# Javascript notebook

### Single line if
```js
if (value) return true
```

### Length of an object
Grabs the keys of the object and using array.length to retrieve te amount.
```js
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1).length);
// expected output: 3

```


### Move element in an array
```js
const array = ['Tesla', 'Audi', 'BMW']

const selectedItemIndex = 1
const selectedItem = array[selectedItemIndex] //Audi

// Remove element from array
array.splice(selectedItemIndex, 1)

//Insert element back into the array at a different position
const newItemPosition = 0
array.splice(newItemPosition, 0, selectedItem)

// outcome: ['Audi', 'Tesla', 'BMW']
```
