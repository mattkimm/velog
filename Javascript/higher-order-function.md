Pure and Higher Order Functions

# Pure Functions.
1. Given the same input will always return the same output
2. Have no side effects (Only access the data that is passed to it)

# HIGHER-ORDER FUNCTIONS
1. May Accept functions as paramters
2. Will Return a Function 


So I Pass number to a function I can call the function million times
as long as I'm passing same number I'm going to get the same response back.  By doing this you're making the function really focus aon doing one thign and do one thing. Well that means I can start to combine them I can chain them together I can compose larger bits of functionality by putting together these small little pure functions.


Seocond property is that they have no side effects that means they're only really accessing the data you're passing to them. They're not affecting or changing anything else that's outside the function.




```javascript
let str = 'Some String';

// Given the same input we're always going to get the same output.
// If I pass string to it I'm always going to get the same ouput.
let f_pure = function(_input){
    let _output = _input.toUpperCase();
    return _output;
}

let out = f_pure(str);
console.log(out,str); // Some String SOME STRING

// original string did not get changed
```

```javascript
let str = 'Some String';




let f_impure = function(_input){
    let _output = _input.toUpperCase();
    // this is side effect, I'm accessing a variable that's outside of my scope. I have to return seomthing that's create insdie here and this is going to be something that takes the value that's passed in. 

    str = _ouptut;
    return _output;
}

let out = f_pure(str);
console.log(out,str); // SOME STRING SOME STRING
// original string got changed
```


If you pass in an object you have to be carful.
Javascript has a lot of shallow copying where it's not really going down into the object to copy everything soemtimes you're getting a reference to something else and that would be considered a side-effect


# higher order functions
You can pass in a function , so I can pass one function to another function and it's going to return a function. This is one of the cool things aboutg Javascript that we can do this we can create a function 


```javascript

let higher = function(f){
    /* can do these */
    f(); 
    f.call(null);
    return f_pure; 
    // this is side-effect but This is higher order function i can return this.
}



let higher = function(f){
   let _output = f();
   return _output; // if _output is a function then this is a higher order functgion

}

let x = function(){ // I am returning function from this one
    console.log('x');
    return function(){
        console.log('x returend value ');
    }
}


higher(x);

```

I'm calling higher
it's accepting this(x) function as an argument it's being passed inside of higher
I'm going to call that function so the (function inside x ) is going to run.
It's going to return a function as well
So this function this function that's being returned is 

 function(){
        console.log('x returend value ');
    }
}

going to be put into  the variable _ouput
and my higher order function is returning _output