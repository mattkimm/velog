![](https://images.velog.io/images/matt85kim53/post/2442dbe6-71ed-47bd-a0d8-856fde78889f/image.png)

# Stack

스택은 일종의 책 더미와 같으며 위에서만 추가 및 제거 만 가능하다.

LAST IN FIRST OUT 데이터 구조라고도도 불린다.

LAST ITEM THAT'S PUT IN IS THE FIRST ITEM THAT'S PUT OUT.

the way that we do this is using push and pop method.

Array has push and pop that do the same thing.

![](https://images.velog.io/images/matt85kim53/post/d6d32bcd-16a8-4aa4-8193-ef67f899e1e5/image.png)a

![](https://images.velog.io/images/matt85kim53/post/48f61e75-5a8d-4987-93ca-eb74de82a447/image.png)

```javascript
class Stack {
  constructor() {
    this.items = [];
    this.count = 0;
  }
}

const stack = new Stack();
```

constructor 를 생성자를 통해서 property를 설정한다.
construcotr is a method that runs when we instanciate an object from this Class. and we need place to store data so we need items and count ( where we are, the position of the element)

```javascript
class Stack {
  constructor() {
    this.items = [];
    this.count = 0;
  }

  // Add Elements to Top of Stack
  push(element) {
    this.items[this.count] = element;
    console.log(`${element} added to ${this.count}`);
    this.count++;
    return this.count - 1;
  }

  // Return and Remove top element in Stack
  // Return undefined if Stack is empty
  pop() {
    if (this.count === 0) return undefined;
    let deleteItem = this.items[this.count - 1];
    this.count--;
    console.log(`${deleteItem} removed`);
    return deleteItem;
  }

  // Check Top element in the STack
  peak() {
    console.log(`Top Element is ${this.items[this.count - 1]}`);
    return this.items[this.items.length - 1];
  }
  // Check if the Stack is Empty
  isEmpty() {
    console.log(this.count === 0 ? "Stack is Empty" : "Stack is not empty");
    return this.count === 0;
  }
  // Check Size of the Stack
  size() {
    console.log(`ELEMENTS IN STACK : ${this.count}`);
    return this.count;
  }
  // Print elements in Stack
  print() {
    let str = "";
    for (let i = 0; i < this.count; i++) {
      str += this.items + "";
    }
    return str;
  }
}

const stack = new Stack();
stack.isEmpty();
stack.push(100);
stack.push(200);
stack.peak();
stack.push(300);

// stack.pop();
// stack.pop();
// stack.pop();
```

this.items[0] = 100 을 추가한다
그리고 현재 count 를 1증가하여 다음 push 때 1번째 인덱스에 넣을 수 있도록 구현한다.

마지막에 return this.count -1 한 이유는 현재 카운트는 0 이고 this.count++한 시점에서
// return the position that this is being added to

100 added to 0
200 added to 1
