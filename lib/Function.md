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
