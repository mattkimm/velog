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
```npm
npx create-react-app react-app
```
-typescript
npx create-react-app --template typescript react-with-typescript