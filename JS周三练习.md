## JS函数+期约与异步函数

### 一、箭头函数与普通函数的区别

1. 箭头函数没有argumens这个动态参数，但依然有剩余参数。

 	2. 箭头函数不能通过bind、call、apply来改变this的值，但依然可以调用这几个方法。
 	3. 箭头函数不能用new来创建构造函数的实例，普通函数可以。
 	4. 普通函数中的this是动态的，而箭头函数中的this指向的是上一层作用域。

### 二、说说闭包

 1.  闭包 = 内层函数+外层变量；

 2.  外部函数访问内部函数的变量；

     ```javascript
     function outer() {
           const a = 1
           function fn() {
             console.log(a)
           }
           return fn
         }
     const fun = outer();
     fun() //1
     
     //outer() == fn == function fn(){}
     ```

3. 实现数据的私有；

   ```javascript
   function count() {
       let i = 0;
       function fn() {
           i++;
           console.log(`函数调用了${i}次`);
       }
       return fn;
   }
   const result = count();
   result() //函数调用了1次
   result() //函数调用了2次
   result() //函数调用了3次
   ```

### 三、手写promise all

​		当处理多个promise时，可以创建一个promise数组，然后对这些promise集执行必要的操作，Promise.all(iterable) 方法返回一个Promise实例，此实例在iterable参数内所有的promise都完成（resolved）或参数中不包含promise时回调完成（resolve）。

​		如果参数中promise有一个失败（rejected），此实例回调失败（reject），失败原因的是第一个失败promise的结果。这里的异步操作是并行执行的，等到它们都执行完后才会进到then()里面， 并且all()方法会把所有异步操作的结果放进一个数组中传给then()。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then((values) => {
  console.log(values);
});
// [3,42,'foo']
```



