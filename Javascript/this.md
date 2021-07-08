
# 1. `this`

`this` 는 현재 함수를 실행하는 객체이다.

MDN : 대부분의 경우 `this`의 값은 함수를 호출한 방법에 의해 결정됩니다. 실행중에는 할당으로 설정할 수 없고 함수를 호출할 때 마다 다를 수 있습니다

# 2. `this` 상황별 작동 방법

## 2-1. 💡 function (일반 함수)

```javascript
function playVideo(){
	console.log(this);
}

playVideo(); // Window {...}
```

**일반 함수**인 경우 `this` 는 Global Object를 가르킨다. 

+ Browser 경우 Window Object
+ Node 환경인 경우 Global Object


## 2-2. 💡 생성자 함수의 this
```javascript
function Video(title){
	this.title = title;
	console.log(this);
}

const v = new Video('a');  // Video { title : 'a'} 

```
`new` 연산자를 사용하여 객체를 만들면 `this`는 해당 `object`를 가르키게된다.

1. new 연산자는 빈 객체(empty object)를 생성한다
2. `this`를 빈 객체로 가르키게 한다.
3. 새로운 `object`에 `title` property 를 추가한다.
new 연산자를 사용하면 `this`는 해당 `object`를 가르키게된다.



## 2-3. 💡 메소드

-`Object` 안에 `function` 이  있으면 `this` 는 **해당 `Object`** 를 참조합니다.

```javascript
const video = {
	title : 'a',
    play() {
    	console.log(this);
    }
}

video.play();          // {title : "a", play : f }
```
- video object 에 play는 **method** 이기 때문에 `this` 는 video object 를 가리킨다. 


## 2-4. 💡 method 안에 callBack

```javascript
const video = {
    title : '[A]',
    tags : ['a','b','c'],
    showTags() {
    	this.tags.forEach(function(tag){
        	console.log(tag);
        })
    }
}
video.showTags(); 
/*
a
b
c
*/
```
참고 : ECMA 2015 에서 추가된 shorter syntax로 변환했다.



```javascript
const video = {
  	tags : ['a','b','c'],
	showTags : function(){
      	this.tags.forEach(function(tag){
        	console.log(tag)
        }
}

```

> 하지만 각각의 태그 옆에 `title`을 보여주고 싶다면?

```javascript
const video = {
    title : '[A]',
    tags : ['tag1','tag2','tag3'],
    showTags() {
    	this.tags.forEach(function(tag){
        	console.log(this.title, tag);
        }
    }
}
video.showTags();
  
```

> video.showTags()를 호출하면 this.title 은 **undefined** 값이 나온다.



```javascript
const video =  {
    title : 'a',
    tags : ['a','b','c'],
    showTags() {
    	this.tags.forEach(function(tag){
        	console.log(this, tag);
        }
    }
}
video.showTags(); // Window{} "a" 
```

- 여기서 `this`는 **Window Object** 를 가르키는걸 볼 수 있다.

- 이전에 `object` 내에 선언된 함수 (메소드)의 `this`는 해당 객체를 가르킨다고 말했지만 **`this`의 위치를 보면  callback function 안에서 `this`를 호출하고 있다. **

- 이는 **일반 함수** 로 인식이되고 `object`에 선언된 `method`라고 할 수 없다.

- 일반 함수이기 때문에 `this`는 `Global object`를 가르키는게 맞다.


# 3. this 문제 해결하기



## 3-1. 💡 forEach 문제 해결하기
> foEach 는 2가지 파라미터를 받을 수 있다.  (callback & thisArg[optional])
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

```javascript
const video = {
	title : 'a',
    tags : ['a','b','c'],
    showTags() {
    	this.tags.forEach(function(tag){
        	console.log(this, tag);
        },{ firstName : 'test'})     // 2번째 parameter에 object추가
    }
}


video.showTags();  
/*
{firstName : "test"} "a"
{firstName : "test"} "b"
{firstName : "test"} "c"
*/
```
> 두 번째 인자로 `object` 를 넣으면 **`this`는 forEach 의 두번째 parameter를 참조하게된다.**  

---

```javascript
const video = {
	title : '[TITLE]',
    tags : ['tag1','tag2','tag3'],
    showTags() {
    	this.tags.forEach(function(tag){
        	console.log(this.title, tag);
        }, this); // this <-- video object
    }
}
video.showTags();  
// [TITLE] tag1 
// [TITLE] tag2
// [TITLE] tag3
```
> 그렇기 떄문에 forEach 두 번째 인자로 `this`를 가르키면 현재 object (video객체)를 가르키게된다.

forEach에 두번째로 전달된 `this`는 callback function 에 있는게 아니고 showTags메소드의 실행 컨텍스트에 있다.


> forEach 처럼 Javascript의 모든 메소드가 this 인수를 전달할 수있는 것은 아닙니다.


## 3-2. this 해결 방법 

### 3-2-1. 🤔 해결 방법  (비추천) 

```javascript
const video = {
	title : 'a',
    tags : ['a','b','c'],
    showTags() {
    	const that = this;  
    	this.tags.forEach(function(tag){
        	console.log(that.title, tag);
        });
    }
}
```

### 3-2-2. 🟢 apply, bind, call
자바스크립트에서 함수는 객체다

```javascript
function playVideo(){
	console.log(this);
}
```
- Javascript 에서 함수는 객체입니다. (추후 추가할 예정)
그렇기 때문에 객체 property 및 method 에 접근할 수 있습니다.

`this` 값을 변경하기 위해 3 가지 Methods 사용 할 수 있습니다.

- apply
- bind 
- call

# call

MDN : call() 메소드는 주어진 this 값 및 각각 전달된 인수와 함께 함수를 호출합니다.

```javascript
function playVideo(){
	console.log(this);
}

playVideo();                    // Window

playVideo.call({name : 'Ash'}); // {name : 'Ash`}


/* -------------------------------------------- */ 
const mike = {
    name : "Mike"
}


function update(birthYear, occupation){
	this.birthYear = birthYear;
  	this.occupation = occupation;
}
update.call(mike, 1991, 'singer');
console.log(mike); 

//{name: "Mike", birthYear: 1991, occupation: "singer"}
```
Strict Mode 에 this 별도로 정리 필요!

## apply

`apply` 는 함수 매개변수를 처리하는 방법을 제외하면 `call` 과 비슷하다.

`call` 은 일반적인 함수와 마찬가지로 **매개변수를 직접받지만 apply는 매개변수를 배열로 받습니다.**

`apply` 는 배열 요소를 함수 매개변수로 사용할떄 유용하다.
```javascript
function playVideo(){
	console.log(this);
}

playVideo(); // Window
playVideo.apply({name : 'Ash'}); // {name : 'Ash}


//thisArg  : can pass an object and this will refernce that object.
```


> call 과 apply는 동작 방법이 같다.
 매개변수를 받는 방법만 다를 뿐이다, Call은 순서대로 이렇게 직접 받고 apply는 배열 형태로 받는다. 

```javascript
playVideo.apply({name : 'Ash'}, 1,2); 
//Uncaught TypeError: CreateListFromArrayLike called on non-object at <anonymous>:1:8

playVideo.apply({name : 'Mosh'}, [1,2]); // {name : 'Ash}
///
const mike = {
  name : 'Mike"
}

function update(birthYear, occupation){
	this.birthYear = birthYear;
  	this.occupation = occupation;
}
update.apply(mike, [1991, 'singer']);
console.log(mike); //


/**********************/
function sum (a,b) {
    return a + b;
}
const result = sum.apply(null, [5,10])  // set 'this' to null
console.log(result); // 15


/**********************/
function sum () {
    console.log(this);
    let sum  = 0;
    for(let i = 0; i < arguments.length ; i ++){
        sum+=arguments[i];
    })
    return sum
}
const result = sum.apply({name : 'Test'}, [5,25,1]);
console.log(result); // {name : 'TEst'} 31
  ```



# bind
bind() 메소드가 호출되면 새로운 함수를 생성하고 Object를 가르키도록 'this'를 설정한다.

```javascript
function playVideo(){
	console.log(this);
}

playVideo.bind({name : 'test'}); 

playVideo.bind({name : 'test'}); 

this returns a new function we can store this result and call that fucntion.

ƒ playVideo(){
	console.log(this);
}
/*-----------------------------------------*/

// 꼭 변수에 안 담아도된다 바로 호출도 가능하다.
const fn = playVideo.bind({name : 'test'});
fn();
playVideo.bind({name :'Mosh'})();
```



### bind 메소드를 호출하고이 값으로 사용할 객체를 전달합니다.
```javascript
const video = {
	title : 'a',
    tags : ['a','b','c'],
    showTags() {
    
    	this.tags.forEach(function(tag){
        	console.log(this.title, tag);
        }.bind(this));
    }
}
```

```javascript

const user = {
	name : "Mike",
    showName : function() {
    	console.log(`hello, ${this.name}`);
        },
 };
 user.showName();
 let fn = user.showName; 

 fn(); //'hello, '    
 
 fn.call(user); // hello , Mike
 fn.apply(user); // hello,  Mike
 
 let boundFn = fn.bind(user);
 boundFn(); // hello,  Mike
 
```


## 3.3 🟢 Arrow Function 사용하기 

화살표 함수는 자체적으로 바인딩하지 않고 대신 "어휘 범위 지정"이라고하는 부모 범위에서 상속합니다. 이로 인해 화살표 기능은 일부 시나리오에서는 훌륭한 선택이지만 다른 시나리오에서는 나쁜 선택입니다.


```javascript
const video {
	title : 'a',
    tags : ['a','b','c'],
    showTags() {
    	this.tags.forEach((tag=> {
        	console.log(this.title, tag);
        });
    }
}
```
## 3.4 🟡 Arrow Function 사용 시 주의점

```
let cities = ["Seoul","Busan", "LA", "NY","LV"];
let person = {
	id : 123,
    name : 'test',
 	town : 'Busan',  
}


let match3 = cities.find(function(item){
	if(item === this.town) return true;
}, person);
console.log(person.name, "lives in matching town", match3);


let match4 = cities.find((item) => {
	if(item === this.town) return true;
}, person);
gets undefined
```





reference
https://dev.to/hebashakeel/difference-between-call-apply-and-bind-4p98
https://dmitripavlutin.com/when-not-to-use-arrow-functions-in-javascript/
