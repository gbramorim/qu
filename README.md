# Vue.js Project: Star Wars Planets

This project showcases a simple Vue.js application that fetches and displays data from the Star Wars API. It includes features like data fetching, sorting, and basic UI interactions.

## Questions and Answers

### 1. What's a Closure? Where in the Code is There a Closure?

A closure in JavaScript is when an inner function has access to the scope of an outer function, even after the outer function has completed execution. This feature allows the inner function to remember and access variables from the outer function's scope.

In my Vue.js application, a closure is present within the `mounted()` lifecycle hook, particularly in the `.then()` callback of the axios call. Here, the callback function forms a closure that accesses the `this.planets` variable from the component's data property. Despite the asynchronous nature of the axios call, the callback function can still refer to `this.planets`, demonstrating the closure's ability to retain access to its surrounding scope.

```javascript
mounted() {
  axios.get('https://swapi.dev/api/planets/')
    .then(response => {
      this.planets = response.data.results; // Closure accessing `this.planets`
    });
}
```

### 2. Which are the Potential Side-Effects in Any Function? Could You Point Out Any of These Cases in Your Code? Are They Expected? Can They Be Avoided?

Side-effects in a function occur when the function interacts with or modifies some state outside its local environment. This includes operations like changing global variables, modifying a component's state, or performing I/O operations.

In my code, the axios call in the `mounted()` lifecycle hook is a significant example of a function with side-effects. The `axios.get()` method performs an API request, interacting with an external system, which is a side-effect. Moreover, updating the component's state with `this.planets = response.data.results` also constitutes a side-effect as it alters the component's state.

```javascript
mounted() {
  axios.get('https://swapi.dev/api/planets/')
    .then(response => {
      this.planets = response.data.results; // Side-effect: modifying component state
    });
}
```

These side-effects are both expected and necessary for the component's functionality. While side-effects like these are integral to Vue.js components, it's essential to manage them properly. In Vue, this is often achieved through lifecycle hooks and the reactive system for state management, ensuring that such side-effects remain controlled and predictable.


# TO RUN THE PROJECT:

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```


