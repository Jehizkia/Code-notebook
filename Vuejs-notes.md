# VueJs notebook

## Dynamically loading component into vue
This code example shows how to load components dynamically. 
This is useful for when you are using SSR and the library you are trying to import makes use of the ```Window``` object. 
When not dynamically importing the component it will result into a ```ReferenceError: window is not defined``` error.

references:

https://vuejs.org/v2/guide/components-registration.html#Global-Registration
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#Dynamic_Imports
https://stackoverflow.com/questions/52542703/vue-js-loading-js-file-in-mounted-hook

Inside the ```template``` tags:
```html
<div v-if="componentLoaded">
  <carousel>
    <slide>
      It's dangerous to go alone
    </slide>
    
    <slide>
      Take this!
    </slide>
    
     <slide>
      *sound effect*
    </slide>
  </carousel
</div>
```
Inside the ```script``` tags:
```js

data () {
  return {
    componentLoaded: false
  }
},

mounted () {
  const self = this
  import('vue-carousel'.then(module => {
    Vue.component('carousel', module.Carousel)
    Vue.component('slide', module.Slide)
    self.componentLoaded = true
  }
}

```

```tip: Use console.log(module) to see which components the module contains.```



## Length of an object
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
