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

## Styles

> `<span style={}/>`

In JSX, we have this style attribute that we need to set to a plain Javascript object. So first we need to add curly braces 
In between these curly braces , we need to pass plain javascript objedct

> `<span style={{ fontWeight : 500 }}>`


# Rendering Classes Dynamically

render one of the classes depending on the value of the count proeprty

```javascript
import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
    }
    render() {

        let classes = "badge m-2 badge-";
        classes+= (this.state.count === 0 ) ?"warning" : "primary"
        return (
            <>
               
                <span className={classes} >{this.formatCount()}</span>
                <button className="btn btn-secondary btn-sm">Increment</button>
            </>
        )
    }
    ...

```

![](https://images.velog.io/images/matt85kim53/post/775a06b3-d94d-4ade-8e62-9b3cd3777438/image.png)

Ctrl + shift + R\

```javascript
import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
    }
    render() {
        return (
            <>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button className="btn btn-secondary btn-sm">Increment</button>
            </>
        )
    }

    getBadgeClasses() {
        let classes = "badge m-2 badge-";
        classes += (this.state.count === 0) ? "warning" : "primary";
        return classes;
    }
```

# Rendering Lists

``` javascript
import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }
    render() {
        return (
            <>
                <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
                <button className="btn btn-secondary btn-sm">Increment</button>
                <ul>
                    { this.state.tags.map(tag => <li>
                        {tag}
                    </li>)}
                </ul>
            </>
        )
    }

```

index.js:1 Warning: Each child in a list should have a unique "key" prop.

Check the render method of `Counter`. See https://reactjs.org/link/warning-keys for more information.
    at li
    at Counter (http://localhost:3000/main.8b047c1f30f1ba7e7a95.hot-update.js:26:5)



IT NEEDS TO UNIQUELY IDENTIFY EACH ITEM IN THIS LIST. BECAUSE IF THE STATE OF THIS REACT ELEMENT IN THE VIRTUAL DOM changes , REACT wants to quickly figure out what element is changed, and where in the DOM it should make changes to keep the DOM in sync with the virtual DOM. 

```javascript
     <ul>
       { this.state.tags.map(tag => <li key={tag}>{tag} </li>)}
    </ul>
```


# Conditional Rendering
```javascript
export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }

    renderTags() {
        if(this.state.tags.length === 0 )  return <p>There are No TAGS</p>
        return <ul>{this.state.tags.map(tag => <li key={tag}>{tag}</li>)}</ul>
    }
    render() {
        return (
            <div>
                {this.state.tags.length === 0 && 'Please Create a new Tag'}
                {this.renderTags()}
            </div>
        )
    }

```

```javascript
import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }

    renderTags() {
        if(this.state.tags.length === 0 )  return <p>There are No TAGS</p>
        return <ul>{this.state.tags.map(tag => <li key={tag}>{tag}</li>)}</ul>
    }
    render() {
        return (
            <div>
                { this.state.tags.length === 0 && 'Please Create a new Tag'}
                {this.renderTags()}
            </div>
        )
    }

    getBadgeClasses() {
        let classes = "badge m-2 badge-";
        classes += (this.state.count === 0) ? "warning" : "primary";
        return classes;
    }

    formatCount() {
        const { count }  = this.state;
        const x = <h1>Zero</h1>
        return count === 0 ? x : count
    }
}

```
TECHNIQUE to conditional rendering content

image we want to render a separate message based =on a given condition.
So we have only a single if statement wihtout and else part
&& 
logical and operator whatever we want to render we add here


 > {this.state.tags.length === 0 && 'Please Create a new Tag'}

  the first value is the result of this expression which is a boolean, it's either true or false. And the second value is a string. In Javascript unlike other programming languages , you can add the logical and between non boolean values.

true && false   // false
true && 'Hi'    // Hi
true && 'Hi' && 1 // 1

When JAvascript engine tries to value this expression .
It looks at the first operand. In this case the first operand is true.
So it will look at the second operand. 
Second Operand is not a boolean true or false, so the Javascript
engine tries to convert this into what we call truthy or falsey.

So essentially we have two operands that are both trutyhy.
In that case our Javascript engine will return the second operand.,


#  Handling Events

All theses React Element have properties that are based on standard DOM events. 

for events we have all the STANDARD DOM EVENTS 
such as onKeyDown , onClick 

```javascript

    handleIncrement () {
        console.log('Increment Clicked')
    }

    render() {
        return (
            <>
            <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
            <button onClick={this.handleIncrement}  className="btn btn-secondary btn-sm">Increment</button>
            </>
        )
    }
```

1) Define a method (naming convention for this is  handle[something])
2) Pass a reference to this method in onClick Prop.
3) Note that we are not calling this method, we're simply passing reference to it. 

# Handling Events

![](https://images.velog.io/images/matt85kim53/post/5672225f-1a7c-4fc3-b577-7511d1100b66/image.png)


```javascript

export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }

    // this is undefined in this method.
    handleIncrement () {
        console.log('Increment Clicked', this.state.count)
    }

    render() {
        return (
            <div>
            <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
            <button onClick={this.handleIncrement}  className="btn btn-secondary btn-sm">Increment</button>
            </div>
        )
    }

```


>  handleIncrement () {
        console.log('Increment Clicked', this.state.count)
    } 

Increment Clicked undefined

Currently We don't have access to the state property why?

# Binding Event Handlers
In this Event Handler WE don't have ACCESS TO **this**.

Why is that?

Javascript behaves differently from other languages
depending on how a function is called **this** can reference different objects.


If a function is called as part of method in an object
this in that function would always a return a reference with an object.
//obj.method()

However, if that function is called as a stand alone function without an object reference.
// function()
**this**  by default retruns reference to the window object.

!!!! BUT IF THE STRICT MODE is enabled this will return undefined.


AND THATS THE REASON IN THIS event hadnler we don't have access to this.

SO SOLUTION??!


In this class , add constructor
This is a method that is called when an object of this type(class Counter)
is created.

```javascript
constructor(){
   // so at this point we do have access to this.
   console.log('Constructor', this);
}

```

![](https://images.velog.io/images/matt85kim53/post/f738e307-b066-4193-8973-63772950d1e4/image.png)


Because we added a constructor in this Child Class.
First we have to call the constructor of the Parent class
using the super keyword. Now We do have access to the Counter Object.
```javascript
constructor(){
   super();
   console.log('Constructor', this);
}

```
![](https://images.velog.io/images/matt85kim53/post/0bf4e84b-02f3-42d4-85c5-4a57c7d20c2f/image.png)


As you can see **this** is not undefined at this point.
This is a perfect opportunity to use this bind method


Earlier, functions in Javascript are objects.<다시 보기.>
So they have properties and Methods.

>     this.handleIncrement.bind(this);

this bind method will return a new Instance of the handleIncrement function.
And in that function this is always reference the current object.
No matter how that function is called, this is not going 
to change. It is always referencing the current counter ojbect. 

And this method right here returns a new function, we can get the function and reset handleIncrement




```javascript
import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }

    constructor(){
        super();
        // 1 solution
        this.handleIncrement = this.handleIncrement.bind(this);
    }

    handleIncrement () {
        console.log('Increment Clicked', this)
    }

    render() {
        return (
            <div>
            <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
            <button onClick={this.handleIncrement}  className="btn btn-secondary btn-sm">Increment</button>
            </div>
        )
    }

```

1) one solution to bind event handlers to this. But you might find this little bit noisy because in every component you have to add a consturcotr you have to call super (the base constructor) and for every handler you have to write event handler and have to write code like this. 
>this.handleIncrement = this.handleIncrement.bind(this);


2) Sceond way remove constructor
and Replace it with ARROW FUNCTION.


ARROW FUNCTIONS don't rebind with this keyword. they inherit IT!


```javascript

import React, { Component } from 'react'

export default class Counter extends Component {

    state = {
        count : 1,
        tags : ['tag1', 'tag2', 'tag3']
    }

    // constructor(){
    //     super();
    //     this.handleIncrement = this.handleIncrement.bind(this);
    // }
 
    handleIncrement = () => {
        console.log('Increment Clicked', this)
    }

    render() {
        return (
            <div>
            <span className={this.getBadgeClasses()}>{this.formatCount()}</span>
            <button onClick={this.handleIncrement}  className="btn btn-secondary btn-sm">Increment</button>
            </div>
        )
    }

```