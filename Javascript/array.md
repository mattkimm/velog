# forEach
- does not return anything
- affects the original array


it will call a function one time for each element i9n the array. this dwarves.forEach is going to call the output function once for each element in the array and there are three pices of information threee parameters that the for each method is going to pass in .

foEach method look to the array for each time it's going to call this function it'll pass in the item the actualy string, it'll pass index (0~11), passes in the entire array. if you wanted to manipulate it somehow

So this behavior could be replicated with a for loop with a for in loop with while loop but it's a built in method now for the arfray object. it jsut simplfies for us.

```javascript
let dwarves = ['Bifur','Bofur','Bombur','Fili', 'Killi','Oin','Gloin','Thorin','Balin','Dwalin','Nori','Dori'];

dwarves.forEach(output);
function output(item,index,array){
  console.log(index, item); // 0 'Bifur'
}
//put anonymous function write inside
dwarves.forEach((function(item,index,array){
	if(item === 'Thorin'){
      item = item.toUpperCase();
    }else{
      item = item.toLowerCase();
      
    }
})
```


//conver all the names to lowercase execept Thorin
// and console.log them
// anonymous function

# Array Map Method

his is almost identifical the only difference is the name of the method
Map will do the same thing as the forEach
It will call the anonymous function once for every element inside the array.

Difference between forEach and map is that the forEach doesn't return anything to us, it just goes through and lets us do something to each element in the array But it is affecting the original array.

The map method will give us back a NEW ARRAY. so it lets us go thorught he array looking at each one of the items we'll have access to the item
the index and the entire array. We can do things with each element in the array. But inside this function we need to have a return statement.
Whatever we return nameLengths becomes the contents of the new Array
It's going to run 12 times it's going to call return 12 times . the nameLength array will have 12 elmenets in it.

```javascript
let dwarves = ['Bifur','Bofur','Bombur','Fili', 'Killi','Oin','Gloin','Thorin','Balin','Dwalin','Nori','Dori'];

let nameLengths = dwarves.map(function(item,index,array){
	return index;
});

let nameLengths = dwarves.map(function(item,index,array){
	let len = item.length;
  	return len; 
});
console.log(nameLengths); // 
let nameLengths = dwarves.map(function(item,index,array){
     return item.length; // more efficient
});
```