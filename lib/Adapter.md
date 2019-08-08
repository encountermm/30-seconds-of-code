
## contents

### 🔌 Adapter

<details>
<summary>点击查看详情</summary>

* [`ary---数组`](#ary)
* [`call`](#call)
* [`collectInto`](#collectinto)
* [`flip`](#flip)
* [`over`](#over)
* [`overArgs`](#overargs)
* [`pipeAsyncFunctions`](#pipeasyncfunctions)
* [`pipeFunctions`](#pipefunctions)
* [`promisify`](#promisify)
* [`rearg`](#rearg)
* [`spreadOver`](#spreadover)
* [`unary`](#unary)

</details>

-----
## 🔌 Adapter

### ary

创建一个接受最多`n`参数，忽略任何其他参数的函数。

使用`Array.prototype.slice（0，n）`和扩展运算符（`...`）调用提供的函数`fn`，最多为`n`参数。

```js
const ary = (fn, n) => (...args) => fn(...args.slice(0, n));
```

<details>
<summary>Examples</summary>

```js
const firstTwoMax = ary(Math.max, 2);
[[2, 6, 'a'], [8, 4, 6], [10]].map(x => firstTwoMax(...x)); // [6, 8, 10]
```

</details>

<br>[⬆返回顶部](#contents)

### call

给定一个键和一组参数，在给定上下文时调用它们。主要用于~~组合物~~。

使用闭包来调用存储的参数的存储键。

```js
const call = (key, ...args) => context => context[key](...args);
```

<details>
<summary>Examples</summary>

```js
Promise.resolve([1, 2, 3])
  .then(call('map', x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
const map = call.bind(null, 'map');
Promise.resolve([1, 2, 3])
  .then(map(x => 2 * x))
  .then(console.log); // [ 2, 4, 6 ]
```

</details>

<br>[⬆返回顶部](#contents)

### collectInto

将接受数组的函数更改为可变参数的函数。

给定一个函数，返回一个将所有输入收集到接受函数数组中的闭包。

```js
const collectInto = fn => (...args) => fn(args);
```

<details>
<summary>Examples</summary>

```js
const Pall = collectInto(Promise.all.bind(Promise));
let p1 = Promise.resolve(1);
let p2 = Promise.resolve(2);
let p3 = new Promise(resolve => setTimeout(resolve, 2000, 3));
Pall(p1, p2, p3).then(console.log); // [1, 2, 3] (after about 2 seconds)
```

</details>

<br>[⬆返回顶部](#contents)