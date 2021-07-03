# Typescript
- Typescript is a language build on top of Javascript , it is also known as Superset of Javascript
- Built and developed by Micrsoft.
- Typescript allows us to add type definitiosn

```javascript
let name = "test";

// typescript allows us to do is to add type definition
// in the below example we are defining type of the variable
// : [type defintion]
let name:string ="test"


name.firstName 
// this is invalid 

name.firstName // javascript will break however in typescript because it knows type of name it's string it will tell right away.

```

# benefits
1) Catch Errors Early in Development
2) Serves as Documentation



# create-react-app
-normal
```bash
$npx create-react-app react-app
```
-typescript
```bash
$npx create-react-app --template typescript react-with-typescript
```


 #

 jsx -> tsx (utilize typescript)
 js -> ts

![](https://images.velog.io/images/matt85kim53/post/9a57217c-d633-4fb5-b380-6d551ce70697/image.png)
![](https://images.velog.io/images/matt85kim53/post/fd5b3676-0ad7-4a63-bdfd-8f9d8960b027/image.png)

When we set our state we passed number as default value and typescript is smart enough to basically infer that this number is going to be of type number and in the above it shows type error
```javascript
const number : number
```
![](https://images.velog.io/images/matt85kim53/post/288acfa1-a79e-41f8-9291-6535873a449c/image.png)

With Larger application when we're passing down props and state and all things of that nature these type checking are really important and allows us to catch erros really fast.



# Pipe 

What if we wanted it to either to be a number or a string?

What we could do is we could essentially declare the the `type` so we can override the inference that it made


```javascript
const [ number, setNumber] = useState<number | string >(5);


const changeNumber = () => {
    setNumber("10");
}
```
Now typescript is completely happy!

)![](https://images.velog.io/images/matt85kim53/post/d44024bb-483c-495c-bbd0-ea2fe7457228/image.png)




> Now  with something like this when you just have number you really don't have to kind of declare type
you would just let typescript infer it however, if you want to have one type or another type that's when you would actually have to go ahead and declare it.
```javascript
const [ number, setNumber] = useState(5);
```


# handling state

```javascript
import React , { useState }  from 'react';
import './App.css';

function App() {

  const [people, setPeople]  = useState([{
    name : "Lebron James",
    url : "",
    age : 36,
    note : "alergic to staying on the same team"
  },

]);

  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
    </div>
  );
}

export default App;

```

If I hover people it actually defined the type for me right away. 

It's saying that people is of type an Array of Objects and then within object we have name string...


![](https://images.velog.io/images/matt85kim53/post/cb150490-5dfa-487d-ae30-b5643dc40a8f/image.png)



```javascript
const [people, setPeople]  = useState([{
    name : "Lebron James",
    url : "",
    age : 36,
    note : "alergic to staying on the same team"
  },
  {
    name : "Kobe Brant",
    url : "",
    age : 36
  }
]);


// map through people.
people.map(person => {
    // i can access properties
   person.
 })

```
![](https://images.velog.io/images/matt85kim53/post/e9323228-84c7-42e1-b47e-bd2a8e2bb32a/image.png)



Start off with empty array
![](https://images.velog.io/images/matt85kim53/post/3ebc7a9d-d3a1-42a4-adba-6ec4e85da211/image.png)

```javascript

const [people, setPeople]  = useState([]);


const [people, setPeople]  = useState<{age : number, name : string}[]>([])
```

However, in the application you don't define complicated state right inside of <>
The way we do it is we would create something known as interface

```javascript
import React , { useState }  from 'react';
import './App.css';


interface IState {
  people : {
    name : string
    age : number
    url : string
    note?: string
  }[]
}

function App() {

const [people, setPeople]  = useState<IState["people"]>([]);


   people.map(person => {
       person.name
   })

  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
    </div>
  );
}

export default App;

```
.


# Handling Props

```javascript
import React , { useState }  from 'react';
import './App.css';
import List from './components/List'

interface IState {
  people : {
    name : string
    age : number
    url : string
    note?: string
  }[]
}

function App() {

const [people, setPeople]  = useState<IState["people"]>([]);

  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
      <List
        people={people}
      />
    </div>
  );
}

export default App;

```

```javascript
import React from "react";


const List = () => {
    return (
        <div>I am List</div>
    )
}

export default List;
```

![](https://images.velog.io/images/matt85kim53/post/48b9b832-5c7d-48c1-9e07-3fff20684bd8/image.png)

The error is saying that this type is not defined anywhere in our component

Right now, the List component is not expecting any sort of Props, because we haven't defined the type defintions for the props for List component. So Basically is expecting I shouldn't get any props.

The list component is expecting "hey I'm not getting any props but we're passing in props of people"
So that is the problem that is happening. 

To SOLVE THIS problem in a very similiar manner to the way that we solve the App type problem we had in the beginning.


We can basically DEFINE **interface** defining the type of PROP and then we can basically set it in this component.


```javascript

import React from "react";


interface IProps {
    people : {
      name : string
      age : number
      url : string
      note?: string
    }[]
  }

  
const List = (props : IProps) => {
    return (
        <div>I am List</div>
    )
}

export default List;
```

Now in App.js <List people={people}/> error is now completely gone.

However if I remove people Prop from List component it is unhappy..


CAN ALSO DESTRUCT

```javascript

interface IProps {
    people : {
      name : string
      age : number
      url : string
      note?: string
    }[]
  }

  
const List = ({people} : IProps) => {
    return (
        <div>I am List</div>
    )
}


```


One thing we can  possibly do is essentially be a little bit more specific
as to what we are doing here with the types.


Instead of passing the type right here defining the prop what we could possibly do is
define the type of this(List) element right over here
![](https://images.velog.io/images/matt85kim53/post/5eef1b0f-c834-4dc5-9d01-411ccc5694cc/image.png)


## More Specific

```javascript


interface IProps {
    people : {
      name : string
      age : number
      url : string
      note?: string
    }[]
  }
// this is of Type React Function Component and it contains Props of IProps
const List:React.FC<IProps>= ({people}) => {
    return (
        <div>I am List</div>
    )
}

export default List;
```



# Handling Functions


```javascript
import React , { useState }  from 'react';
import './App.css';
import List from './components/List'

interface IState {
  people : {
    name : string
    age : number
    url : string
    note?: string
  }[]
}

function App() {

const [people, setPeople]  = useState<IState["people"]>([
  {
    name : "Lebron James",
    url : "https://cdn.nba.com/headshots/nba/latest/1040x760/2544.png",
    age : 36,
    note : "Allergic to staying on the same team";
  }
]);

  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
      <List
        people={people}
      />
    </div>
  );
}

export default App;

```


```javascript
import React from "react";


interface IProps {
    people : {
      name : string
      age : number
      url : string
      note?: string
    }[]
  }

  
const List:React.FC<IProps>= ({people}) => {

    const renderList = () => {
        return people.map(person => {
            <li className="List">
                <div className="List-header">
                    <img className="List-img" src={person.url}/>
                    <h2>{person.name}</h2>
                </div>
                <p>
                    {person.age} years old
                </p>
                <p className="List-note">
                    {person.note}
                </p>
            </li>
        })
    }


    return (
        <ul>
            {renderList()}
        </ul>
    )
}

export default List;
```
Doesn't show anything  because we didn't return jsx

![](https://images.velog.io/images/matt85kim53/post/df512540-37e7-412e-adec-ef1a90b8450b/image.png)


Essentially with a function I could potentially want something, I can accidently return something else and Typescript would really have no idea because it's going to infer that hey maybe that's what 
he wanted all along. So this is why it's super important to actually define ultimately what you want to return 



```javascript
import React from "react";


interface IProps {
    people : {
      name : string
      age : number
      url : string
      note?: string
    }[]
  }

  
const List:React.FC<IProps>= ({people}) => {
    

    // return an Array of JSX Element 
    const renderList = ():JSX.Element[] => {
        return people.map(person => {
            return (
                <li className="List">
                <div className="List-header">
                    <img className="List-img" src={person.url}/>
                    <h2>{person.name}</h2>
                </div>
                <p>
                    {person.age} years old
                </p>
                <p className="List-note">
                    {person.note}
                </p>
            </li>
            )
          
        })
    }


    return (
        <ul>
            {renderList()}
        </ul>
    )
}

export default List;

```


TIP
 once you are absolutely sure that this function is workign correctly
 you can go ahead and hover over this and you can see that it is inferring that it is 
 returning a type of jsx.element  that is an array.

 This is really how you would figure out the types in something as complicated as react

 ![](https://images.velog.io/images/matt85kim53/post/fa792498-a153-4fea-943d-1c355857b32e/image.png)



# handling events


```javascript
App.js
  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
      <List
        people={people}
      />
      <AddToList/>
    </div>
  );

///

import React from 'react';




const AddToList:React.FC = () => {



    return (
        <div className="AddToList">
            <input 
                type="text" 
                placeholder="Name"
                className="AddToList-input"
            />
            <input 
                type="text" 
                placeholder="Age"
                className="AddToList-input"
            />
            <input 
                type="text" 
                placeholder="Image Url"
                className="AddToList-input"
            />
            <textarea 
                // type="text" 
                placeholder="Notes"
                className="AddToList-input"
            />
        </div>
    )
}

export default AddToList;

```

​with textarea typescript is complaining , that we don't have type text for textarea
![](https://images.velog.io/images/matt85kim53/post/b9de22e7-6811-4785-93ae-5328c1ab9c74/image.png)




```javascript
import React, { useState } from 'react';




const AddToList:React.FC = () => {

    
    const [ input, setInput ] = useState({
        name : "",
        age : "",
        note : "",
        img : "",
    })
       

    const handleChange = (e) => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
    }
    
    return (
        <div className="AddToList">
            <input 
                type="text" 
                placeholder="Name"
                className="AddToList-input"
                value = {input.name}
                onChange = {handleChange}
                name = "name"
            />
            <input 
                type="text" 
                placeholder="Age"
                className="AddToList-input"
                value = {input.age}
                onChange = {handleChange}
                name ="age"
            />
            <input 
                type="text" 
                placeholder="Image Url"
                className="AddToList-input"
                value = {input.img}
                onChange = {handleChange}
                name ="image"
            />
            <textarea 
                // type="text" 
                placeholder="Notes"
                className="AddToList-input"
                value = {input.note}
                name ="note"

            />
        </div>
    )
}

export default AddToList;
```


![](https://images.velog.io/images/matt85kim53/post/d07e29f0-8e19-48ad-aacd-b82acc2ae8c3/image.png)

```javascript
   const handleChange = (e:any) => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
    }

```

IT doesn't knwo what e is ,  essentailly we're saying here that it is implied any
when we see soemthing like any , I tcan literally be anything Typescript has no idea,
that's why it's giving us this error.
We can basically say we want this to be any and it's completed fine with it


Hover over onChange and essentailly see the type that this onChange is responsible for.


Declare a function right ehere.

```javascript
    <input 
                type="text" 
                placeholder="Name"
                className="AddToList-input"
                value = {input.name}
                // onChange = {handleChange}
                onChange = {(e)=>{}}
                name = "name"
            />

```

As you can see this is not triggering any error like it does over here.
That's because if we actually write the function in line . Typescript has a great idea of 
exactly what the type is goign to be .



![](https://images.velog.io/images/matt85kim53/post/b1a5924e-e192-4cc8-ab80-b0ae0c1c4629/image.png)


```javascript

    const handleChange = (e:React.ChangeEvent<HTMLInputElement>) => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
    }
```



for textarea 

As you can see the typescript error, 

the e target is suppose to be <HTML InputElement>  however this is <HTMLTextAreaElements> 
this is where the problem arises.

![](https://images.velog.io/images/matt85kim53/post/a2872a9c-1d73-46e3-b1bb-b5e129b91ef0/image.png)
![](https://images.velog.io/images/matt85kim53/post/883b9398-02bc-4d89-a876-005a728ed17d/image.png)


To fix this problem, we can basically copy this and essentially we can say 


```javascript

const handleChange = (e:React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement> ) : void => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
    }
```


Another thing we specify that it will return void, but when we return string it will throw an Error
```javascript
   const handleChange = (e:React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement> ) : void => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
        return "d"
    }


```

![](https://images.velog.io/images/matt85kim53/post/2b48b397-2c4c-4983-9084-402aa78b36ca/image.png)





Basically all we want to now, Is we want to get all of the elements right here

 const [ input, setInput ] = useState({
        name : "",
        age : "",
        note : "",
        img : "",
    })

and essentially append them to people

const [people, setPeople]  = useState<IState["people"]>([
  {
    name : "Lebron James",
    url : "https://cdn.nba.com/headshots/nba/latest/1040x760/2544.png",
    age : 36,
    note : "Allergic to staying on the same team",
  }
]);


Basically what we need is access to setPeople function inside of AddToList Component
and of course we're going to do that via props.



If I'm using bascialyl Interface that I defined in the Parent and I'm passing down to props


App.jsx
Make interface export

export interface IState {
  people : {
    name : string
    age : number
    url : string
    note?: string
  }[]
}

List.jsx

Instead of defining this interface which I basically defined over here , this is very repetitive,

```javascript
List.jsx

import React from "react";
import { IState as IProps} from '../App';

// interface IProps {
//     people : {
//       name : string
//       age : number
//       url : string
//       note?: string
//     }[]
//   }

  
const List:React.FC<IProps>= ({people}) => {
    
```




# Final
```javascript
import React , { useState }  from 'react';
import './App.css';
import List from './components/List'
import AddToList from './components/AddToList';

export interface IState {
  people : {
    name : string
    age : number
    url : string
    note?: string
  }[]
}

function App() {

const [people, setPeople]  = useState<IState["people"]>([
  {
    name : "Lebron James",
    url : "https://cdn.nba.com/headshots/nba/latest/1040x760/2544.png",
    age : 36,
    note : "Allergic to staying on the same team",
  }
]);

  return (
    <div className="App">
      <h1>People Invited to my Party</h1>
      <List
        people={people}
      />
      <AddToList
        people ={people}
        setPeople = {setPeople}
      />
    </div>
  );
}

export default App;


```


```javascript
AddToList.tsx
import React, { useState } from 'react';
import { IState as Props} from '../App';


interface IProps {
    people : Props["people"]
    setPeople : React.Dispatch<React.SetStateAction<Props["people"]>>
}

const AddToList:React.FC<IProps> = ({people, setPeople}) => {

    
    const [ input, setInput ] = useState({
        name : "",
        age : "",
        note : "",
        img : "",
    })
       

    const handleChange = (e:React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement> ) : void => {
        setInput({
            ...input, 
            [e.target.name] : e.target.value,
        })
     
    }

    const handleClick = (): void => {
        if(!input.name  || !input.age ||!input.img ){
            return 
         }

         setPeople([
             ...people,
             {
                 name : input.name,
                 age : input.age,
                 img : input.img,
                 note : input.note,
             }
            ])
    }
    
    return (
        <div className="AddToList">
            <input 
                type="text" 
                placeholder="Name"
                className="AddToList-input"
                value = {input.name}
                onChange = {handleChange}
                name = "name"
            />
            <input 
                type="text" 
                placeholder="Age"
                className="AddToList-input"
                value = {input.age}
                onChange = {handleChange}
                name ="age"
            />
            <input 
                type="text" 
                placeholder="Image Url"
                className="AddToList-input"
                value = {input.img}
                onChange = {handleChange}
                name ="img"
            />
            <textarea 
                placeholder="Notes"
                className="AddToList-input"
                value = {input.note}
                onChange = {handleChange}
                name ="note"

            />
            <button
                className="AddToList-btn"
                onClick = {handleClick}
            >
                Add to List
            </button>
        </div>
    )
}

export default AddToList;

```

![](https://images.velog.io/images/matt85kim53/post/9b8f6a01-e34a-47ad-bd40-2efdce8585d9/image.png)

When you define a number in input element, what ends up happening is that  the number itself is actually Typed String, once we get it back e.target.value is actually types tring event though it is actually a number


```javascript
 const handleClick = (): void => {
        if(!input.name  || !input.age ||!input.img ){
            return 
         }

         setPeople([
             ...people,
             {
                 name : input.name,
                 age : parseInt(input.age),
                 url : input.img,
                 note : input.note,
             }
            ])
    }
    

```

Typescript actually serves as documentation and allows you to catch errors in early in development
