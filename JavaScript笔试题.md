# JavaScript笔试题

## 1. 变量的声明

```javascript
var a = b = 0;
a = 10;
b = 10;
console.log(a);
console.log(b);

// result =>
// 10
// 10
```

```javascript
var a = b = c;
a = 10;
b = 10;
c = 10;
console.log(a);
console.log(b);
console.log(c);

// result =>
// throw an error!!!
// c is not defined
```

```javascript
var fn = 100;
fn();
function fn(){
    console.log('hello world')
}
fn();
fn();

// result =>
// throw an error!!!
```

## 2. 递归

```javascript
// 阶乘
// 5的阶乘

var res = fn(5)
function fn(n){
    if (n > 1) {
       return n * fn(--n) 
    } else if (n === 1) {
        return 1
    }
}
console.log(res)

// result => 
// 120
```

```javascript
// 斐波那契数列
function fb1(n){
    if(n<=2){
        return 1;
    }else{
        return fb1(n-1) + fb1(n-2)
    }
}
```

