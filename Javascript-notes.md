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
