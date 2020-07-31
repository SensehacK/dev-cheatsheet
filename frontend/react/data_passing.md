# Data passing

This file adds how data is being passed correct way so that it could be easy reference for my notes or future projects.

## Props Passing

We would document the property parameters passing via different sources like parent to child and vice versa.

### Props Parent to child variables

```markup
<Counters
  counters="{this.state.counters}"
  onReset="{this.resetCounters}"
  onIncrement="{this.handleIncrement}"
  onDelete="{this.handleDelete}"
/>
```

Counters, OnReset.. are the props variables to pass data from Parent to child

In Counters component, if they want to pass back data from child “Counters” to Parent “App” they would use Method of “Props Child to Parent”

### Props Child to Parent passing parameters

Just normal function callback would be

```javascript
Class Counter {
 render() {
    return (
     <div>
   key={counter.id}
   onIncrement={this.props.onIncrement}
   onDelete={this.props.onDelete}
   counter={counter}
  </div>
  );
 }
}
```

#### This is when passing data Parameter from child to Parent props or method

```javascript
Class CounterChildClass {
 render() {
  return (
   onClick={() => this.props.onIncrement(this.props.counter)}
   );
  }
 }
```

Context : ‘onIncrement’ defined in Class “Counter” so calling onIncrement method from CounterChildClass to Counter Class for passing data to parent function. Expression would add

> { \(\) =&gt; this.props.methodName\(variableOrParameterData\)}

### Object De structuring

This phenomenon is known as Object De Structuring as per YouTube r Mosh Instructor in React. I’m not sure how it works but it looks like a shorthand and the compiler is understanding or skimming the variables in those objects for shorter syntax compiled to longer syntax after compilation for browser.

Object Defined as

```javascript
state = {
  counters: [
    { id: 1, value: 0 },
    { id: 2, value: 3 },
    { id: 3, value: 2 },
    { id: 4, value: 3 }
  ]
};
```

Accessing the property directly thus avoiding extra verbose and cleaner code.

```javascript
> const { counters } from this.state.counters;
Replace with Shorthand
> const { counters }  from this.state;
```

Replacing the new array for React State management to register the change event

```javascript
// Creating a new variable with different array
const counters = this.state.counters.filter(c => c.id !== counterID);

> this.setState({ counters: counters });
Replace with Shorthand
> this.setState({ counters });
```

