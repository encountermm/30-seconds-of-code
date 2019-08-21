## Contents

### 🎛️ Function

<details>
<summary>View contents</summary>

-   [`attempt`](#attempt)
-   [`bind`](#bind)
-   [`bindKey`](#bindkey)
-   [`chainAsync`](#chainasync)
-   [`checkProp`](#checkprop)
-   [`compose`](#compose)
-   [`composeRight`](#composeright)
-   [`converge`](#converge)
-   [`curry`](#curry)
-   [`debounce`](#debounce)
-   [`defer`](#defer)
-   [`delay`](#delay)
-   [`functionName`](#functionname)
-   [`hz`](#hz)
-   [`memoize`](#memoize-)
-   [`negate`](#negate)
-   [`once`](#once)
-   [`partial`](#partial)
-   [`partialRight`](#partialright)
-   [`runPromisesInSeries`](#runpromisesinseries)
-   [`sleep`](#sleep)
-   [`throttle`](#throttle-)
-   [`times`](#times)
-   [`uncurry`](#uncurry)
-   [`unfold`](#unfold)
-   [`when`](#when)

</details>

### 🎛️ Function

<!-- 2019年8月20日 22:31:51 -->

### attempt

尝试使用提供的参数调用函数，返回结果或捕获的错误对象。

使用`try ... catch`块返回函数的结果或适当的错误。

```js
const attempt = (fn, ...args) => {
	try {
		return fn(...args)
	} catch (e) {
		return e instanceof Error ? e : new Error(e)
	}
}
```

<details>
<summary>Examples</summary>

```js
var elements = attempt(function(selector) {
	return document.querySelectorAll(selector)
}, '>_>')
if (elements instanceof Error) elements = [] // elements = []
```

</details>

<br>[⬆ 返回顶部](#contents)

### bind

创建一个函数，该函数使用给定的上下文调用`fn`，可选地将任何其他提供的参数添加到参数的开头。

返回一个`function`，它使用`Function.prototype.apply()`将给定的`context`应用于`fn`。
使用`Array.prototype.concat()`将任何其他提供的参数添加到参数中。

```js
const bind = (fn, context, ...boundArgs) => (...args) => fn.apply(context, [...boundArgs, ...args])
```

<details>
<summary>Examples</summary>

```js
function greet(greeting, punctuation) {
	return greeting + ' ' + this.user + punctuation
}
const freddy = { user: 'fred' }
const freddyBound = bind(greet, freddy)
console.log(freddyBound('hi', '!')) // 'hi fred!'
```

</details>

<br>[⬆ 返回顶部](#contents)

### bindKey

创建一个函数，该函数在对象的给定键处调用该方法，可选地将任何其他提供的参数添加到参数的开头。

返回一个`function`，它使用`Function.prototype.apply()`将`context [fn]`绑定到`context`。
使用扩展运算符（`...`）将任何其他提供的参数添加到参数中。

```js
const bindKey = (context, fn, ...boundArgs) => (...args) =>
	context[fn].apply(context, [...boundArgs, ...args])
```

<details>
<summary>Examples</summary>

```js
const freddy = {
	user: 'fred',
	greet: function(greeting, punctuation) {
		return greeting + ' ' + this.user + punctuation
	}
}
const freddyBound = bindKey(freddy, 'greet')
console.log(freddyBound('hi', '!')) // 'hi fred!'
```

</details>

<br>[⬆ 返回顶部](#contents)

### chainAsync

链接异步函数。

循环遍历包含异步事件的函数数组，在每个异步事件完成时调用`next`。

```js
const chainAsync = fns => {
	let curr = 0
	const last = fns[fns.length - 1]
	const next = () => {
		const fn = fns[curr++]
		fn === last ? fn() : fn(next)
	}
	next()
}
```

<details>
<summary>Examples</summary>

```js
chainAsync([
	next => {
		console.log('0 seconds')
		setTimeout(next, 1000)
	},
	next => {
		console.log('1 second')
		setTimeout(next, 1000)
	},
	() => {
		console.log('2 second')
	}
])
```

</details>

<br>[⬆ 返回顶部](#contents)

### checkProp

给定一个`predicate`函数和一个`prop`字符串，这个 curried 函数将通过调用属性并将其传递给谓词来检查`object`。

在`obj`上调用`prop`，将它传递给提供的`predicate`函数,并返回一个布尔值。

```js
const checkProp = (predicate, prop) => obj => !!predicate(obj[prop])
```

<details>
<summary>Examples</summary>

```js

const lengthIs4 = checkProp(l => l === 4, 'length');
lengthIs4([]); // false
lengthIs4([1,2,3,4]); // true
lengthIs4(new Set([1,2,3,4])); // false (Set uses Size, not length)

const session = { user: {} };
const validUserSession = checkProps(u => u.active && !u.disabled, 'user');

validUserSession(session); // false

session.user.active = true;
validUserSession(session); // true

const noLength(l => l === undefined, 'length');
noLength([]); // false
noLength({}); // true
noLength(new Set()); // true
```

</details>

<br>[⬆ 返回顶部](#contents)

### compose

执行从右到左的功能组合。

使用`Array.prototype.reduce()`来执行从右到左的函数组合。
最后（最右边）函数可以接受一个或多个参数; 其余的功能必须是一元的。

```js
const compose = (...fns) => fns.reduce((f, g) => (...args) => f(g(...args)))
```

<details>
<summary>Examples</summary>

```js
const add5 = x => x + 5
const multiply = (x, y) => x * y
const multiplyAndAdd5 = compose(
	add5,
	multiply
)
multiplyAndAdd5(5, 2) // 15
```

</details>

<br>[⬆ 返回顶部](#contents)

### composeRight

执行从左到右的功能组合。

使用`Array.prototype.reduce()`来执行从左到右的函数组合。
第一个（最左边）函数可以接受一个或多个参数; 其余的功能必须是一元的。

```js
const composeRight = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)))
```

<details>
<summary>Examples</summary>

```js
const add = (x, y) => x + y
const square = x => x * x
const addAndSquare = composeRight(add, square)
addAndSquare(1, 2) // 9
```

</details>

<br>[⬆ 返回顶部](#contents)

### converge

接受聚合函数和分支函数列表，并返回将每个分支函数应用于参数的函数，并将分支函数的结果作为参数传递给聚合函数。

使用`Array.prototype.map()`和`Function.prototype.apply()`将每个函数应用于给定的参数。
使用扩展运算符（`...`）用所有其他函数的结果调用`coverger`。

```js
const converge = (converger, fns) => (...args) => converger(...fns.map(fn => fn.apply(null, args)))
```

<details>
<summary>Examples</summary>

```js
const average = converge((a, b) => a / b, [
	arr => arr.reduce((a, v) => a + v, 0),
	arr => arr.length
])
average([1, 2, 3, 4, 5, 6, 7]) // 4
```

</details>

<br>[⬆ 返回顶部](#contents)

### curry

使用递归。
如果提供的参数（`args`）的数量足够，则调用传递的函数`fn`。
否则，返回一个 curried 函数`fn`，它需要其余的参数。
如果你想要一个接受可变数量的参数的函数（一个可变函数，例如`Math.min()`），你可以选择将参数个数传递给第二个参数`arity`。

```js
const curry = (fn, arity = fn.length, ...args) =>
	arity <= args.length ? fn(...args) : curry.bind(null, fn, arity, ...args)
```

<details>
<summary>Examples</summary>

```js
curry(Math.pow)(2)(10) // 1024
curry(Math.min, 3)(10)(50)(2) // 2
```

</details>

<br>[⬆ 返回顶部](#contents)

### debounce

创建一个`debounced`函数，该函数延迟调用所提供的函数，直到自上次调用它以来至少经过了`ms`毫秒。

每次调用 debounced 函数时，使用`clearTimeout()`清除当前的挂起超时，并使用`setTimeout()`创建一个新的超时，延迟调用函数，直到至少经过`ms`毫秒。 使用`Function.prototype.apply()`将`this`上下文应用于函数并提供必要的参数。
省略第二个参数`ms`，将超时设置为默认值 0 ms。

```js
const debounce = (fn, ms = 0) => {
	let timeoutId
	return function(...args) {
		clearTimeout(timeoutId)
		timeoutId = setTimeout(() => fn.apply(this, args), ms)
	}
}
```

<details>
<summary>Examples</summary>

```js
window.addEventListener(
	'resize',
	debounce(() => {
		console.log(window.innerWidth)
		console.log(window.innerHeight)
	}, 250)
) // Will log the window dimensions at most every 250ms
```

</details>

<br>[⬆ 返回顶部](#contents)

<!-- 2019年8月21日 18:00:23 -->

### defer

延迟调用函数，直到当前调用堆栈清除为止。

使用超时为 1ms 的`setTimeout（）`将新事件添加到浏览器事件队列，并允许渲染引擎完成其工作。 使用 spread（`...`）运算符为函数提供任意数量的参数。

```js
const defer = (fn, ...args) => setTimeout(fn, 1, ...args)
```

<details>
<summary>Examples</summary>

```js
// Example A:
defer(console.log, 'a'), console.log('b') // logs 'b' then 'a'

// Example B:
document.querySelector('#someElement').innerHTML = 'Hello'
longRunningFunction() // Browser will not update the HTML until this has finished
defer(longRunningFunction) // Browser will update the HTML then run the function
```

</details>

<br>[⬆ 返回顶部](#contents)

### delay

在`wait`毫秒后调用提供的函数。

使用`setTimeout（）`来延迟执行`fn`。
使用 spread（`...`）运算符为函数提供任意数量的参数。

```js
const delay = (fn, wait, ...args) => setTimeout(fn, wait, ...args)
```

<details>
<summary>Examples</summary>

```js
delay(
	function(text) {
		console.log(text)
	},
	1000,
	'later'
) // Logs 'later' after one second.
```

</details>

<br>[⬆ 返回顶部](#contents)

### functionName

记录函数的名称。

使用`console.debug（）`和传递方法的`name`属性将方法的名称记录到控制台的`debug`通道。

```js
const functionName = fn => (console.debug(fn.name), fn)
```

<details>
<summary>Examples</summary>

```js
functionName(Math.max) // max (logged in debug channel of console)
```

</details>

<br>[⬆ 返回顶部](#contents)

### hz

返回每秒执行函数的次数。
`hz`是`hertz`的单位，频率单位定义为每秒一个周期。

使用`performance.now（）`来获取迭代循环之前和之后的毫秒差异，以计算执行函数`iterations`次所经过的时间。
通过将毫秒转换为秒并将其除以经过的时间来返回每秒的周期数。
省略第二个参数`iterations`，使用默认的 100 次迭代。

```js
const hz = (fn, iterations = 100) => {
	const before = performance.now()
	for (let i = 0; i < iterations; i++) fn()
	return (1000 * iterations) / (performance.now() - before)
}
```

<details>
<summary>Examples</summary>

```js
// 10,000 element array
const numbers = Array(10000)
	.fill()
	.map((_, i) => i)

// Test functions with the same goal: sum up the elements in the array
const sumReduce = () => numbers.reduce((acc, n) => acc + n, 0)
const sumForLoop = () => {
	let sum = 0
	for (let i = 0; i < numbers.length; i++) sum += numbers[i]
	return sum
}

// `sumForLoop` is nearly 10 times faster
Math.round(hz(sumReduce)) // 572
Math.round(hz(sumForLoop)) // 4784
```

</details>

<br>[⬆ 返回顶部](#contents)

### memoize ![advanced](/advanced.svg)

返回`memoized`（缓存）函数。

通过实例化一个新的`Map`对象来创建一个空缓存。
返回一个函数，它通过首先检查函数的特定输入值的输出是否已经被缓存，将一个参数提供给 memoized 函数，如果没有则存储并返回它。 必须使用`function`关键字，以便允许 memoized 函数在必要时更改其`this`上下文。
允许通过将其设置为返回函数的属性来访问`cache`。

```js
const memoize = fn => {
	const cache = new Map()
	const cached = function(val) {
		return cache.has(val)
			? cache.get(val)
			: cache.set(val, fn.call(this, val)) && cache.get(val)
	}
	cached.cache = cache
	return cached
}
```

<details>
<summary>Examples</summary>

```js
// See the `anagrams` snippet.
const anagramsCached = memoize(anagrams)
anagramsCached('javascript') // takes a long time
anagramsCached('javascript') // returns virtually instantly since it's now cached
console.log(anagramsCached.cache) // The cached anagrams map
```

</details>

<br>[⬆ 返回顶部](#contents)

### negate

否定传入函数。

获取传入函数并使用其参数将 not 运算符（`！`）应用于它。

```js
const negate = func => (...args) => !func(...args)
```

<details>
<summary>Examples</summary>

```js
;[1, 2, 3, 4, 5, 6].filter(negate(n => n % 2 === 0)) // [ 1, 3, 5 ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### once

确保只调用一次函数。

使用一个闭包，使用一个标志``called`，并在第一次调用该函数时将其设置为`true`，防止再次调用它。 为了允许函数更改其`this`上下文（例如在事件监听器中），必须使用`function`关键字，并且所提供的函数必须应用上下文。 允许使用rest / spread（`...`）运算符为函数提供任意数量的参数。

```js
const once = fn => {
	let called = false
	return function(...args) {
		if (called) return
		called = true
		return fn.apply(this, args)
	}
}
```

<details>
<summary>Examples</summary>

```js
const startApp = function(event) {
	console.log(this, event) // document.body, MouseEvent
}
document.body.addEventListener('click', once(startApp)) // only runs `startApp` once upon click
```

</details>

<br>[⬆ 返回顶部](#contents)

### partial

创建一个函数，调用`fn`并将`partials`添加到它接收的参数之前。

使用扩展运算符（```）将`partials`添加到`fn`的参数列表中。

```js
const partial = (fn, ...partials) => (...args) => fn(...partials, ...args)
```

<details>
<summary>Examples</summary>

```js
const greet = (greeting, name) => greeting + ' ' + name + '!'
const greetHello = partial(greet, 'Hello')
greetHello('John') // 'Hello John!'
```

</details>

<br>[⬆ 返回顶部](#contents)

### partialRight

创建一个函数，调用`fn`并将`partials`附加到它接收的参数上。

使用扩展运算符（```）将`partials`附加到`fn`的参数列表中。

```js
const partialRight = (fn, ...partials) => (...args) => fn(...args, ...partials)
```

<details>
<summary>Examples</summary>

```js
const greet = (greeting, name) => greeting + ' ' + name + '!'
const greetJohn = partialRight(greet, 'John')
greetJohn('Hello') // 'Hello John!'
```

</details>

<br>[⬆ 返回顶部](#contents)

### runPromisesInSeries

运行一系列承诺串联。

使用`Array.prototype.reduce（）`创建一个 promise 链，每个 promise 在解析时返回下一个 promise。

```js
const runPromisesInSeries = ps => ps.reduce((p, next) => p.then(next), Promise.resolve())
```

<details>
<summary>Examples</summary>

```js
const delay = d => new Promise(r => setTimeout(r, d))
runPromisesInSeries([() => delay(1000), () => delay(2000)]) // Executes each promise sequentially, taking a total of 3 seconds to complete
```

</details>

<br>[⬆ 返回顶部](#contents)
