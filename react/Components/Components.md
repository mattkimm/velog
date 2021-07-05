```javascript

npx create-react-app counter-app
$ npm i bootstrap@4.1.1

```

By Convention we make [components] directory and put all the components in here. 
app/src/components


```javascript
import React, { Component } from 'react'

export default class Counter extends Component {
    render() {
        return (
            <h1>Hello World</h1>
        )
    }
}

```
 <h1>Hello World</h1>
This is a JSX Expression. which eventually gets compiled to calls
React.createElement that is why we have to import the React object on the top even though we are not going to directly use this in our code.


 
 JSX Expression Must have one Parent Element ?
 Why 
 It compiles to call 
 React.creatElement()

the first argument to this method is the type of the element
we want to create in this case h1
but when we have two elements side by side Babel doesn't know how 
to compile this long expression into a call to React.createElement.
>  `<h1>Hello World</h1><button>Increment</button>`

What is the type of React.element that should be return from the render method ? we can't tell.

1) wrap this with <div></div> or <></> <-- fragment >








```javascript
import React, { Component } from 'react'

export default class Counter extends Component {
    render() {
        return (
            </div>
            <h1>Hello World</h1>
            <button>Increment</button>
        )
    }
}


```



# <React.Fragment>

```javascript
  return (
            <div>
                <h1>Hello World</h1>
                <button>Increment</button>
            </div>
        )
```
![](https://images.velog.io/images/matt85kim53/post/63fd01ed-f10b-431f-bd06-20596ca71fcc/image.png)

<React.Fragment>

```javascript
return (
    <>
      <h1>Hello World</h1>
      <button>Increment</button>
    </>
)
```
![](https://images.velog.io/images/matt85kim53/post/6a61dc0d-b620-400c-83de-54b2bd29ea77/image.png)



# Embedded Expressions
Instead of hard coding Hello World I want to display value dynamically.

State is a special property in React Component, and it's an object
that includes any data that htis component needs.

State object inlcudes any data that the component needs


```javascript
import React, { Component } from 'react'
export default class Counter extends Component {
    state = {
        count : 0,
    }
    render() {
        return (
            <>
                <span>{this.state.count}</span>
                <button>Increment</button>
            </>
        )
    }
}

```
To reference the current object we need to write this.

In between the curly braces 
{this.state.value} we can write any valid Javascript expressions.

An expression is something that produces a value.
ex) {2 + 2}
or call a function that returns a value


```javascript
    render() {
        return (
            <>
                <span>{this.state.count}</span>
                <span>{this.formatCount()}</span>
                <button>Increment</button>
            </>
        )
    }

    // formatCount() {
    //     return this.state.count === 0 ? 'Zero' : this.state.count
    // }
    
    // After Refactoring
    formatCount() {
        const { count }  = this.state;
        const x = <h1>Zero</h1>
        return count === 0 ? x : count
    }
```

 JSX Expressions are just like normal Javascript Objects.
 You can return them from a function, you can pass them to a function.
 can define a constant and set it to jsx


# Setting Attributes


```javascript

    state = {
        count : 0,
        imageUrl : 'https://picsum.photos/200'
    }

    render() {
        return (
            <>
                <img src={this.state.imageUrl} alt=""/>
            </>
    }
```

Setting the class and style attribute

### class Attribute
 
> `<span class="test">`  X

These JSX Expression get compiled to React Elements which are esssentially plain Javascript OBjects. We cannot use class Property on a Object because that's a reserved keyword in Javascript.

> `<span className="test"></span>`


For the most part , it's best to use classes this is for performance and maintainability, but there are times  that you may want to break the rules if you knwo what you're doing and you may want to apply a style to a specific element. 

### 

> `<span style={}/>`

In JSX, we have this style attribute that we need to set to a plain Javascript object. So first we need to add curly braces 
In between these curly braces , we need to pass plain javascript objedct

> `<span style={{ fontWeight : 500 }}>`