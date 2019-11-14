## Contents

### ➗ Math

<details>
<summary>View contents</summary>

- [`approximatelyEqual`](#approximatelyequal)
- [`average`](#average)
- [`averageBy`](#averageby)
- [`binomialCoefficient`](#binomialcoefficient)
- [`clampNumber`](#clampnumber)
- [`degreesToRads`](#degreestorads)
- [`digitize`](#digitize)
- [`distance`](#distance)
- [`elo`](#elo-)
- [`factorial`](#factorial)
- [`fibonacci`](#fibonacci)
- [`gcd`](#gcd)
- [`geometricProgression`](#geometricprogression)
- [`hammingDistance`](#hammingdistance)
- [`inRange`](#inrange)
- [`isDivisible`](#isdivisible)
- [`isEven`](#iseven)
- [`isNegativeZero`](#isnegativezero)
- [`isPrime`](#isprime)
- [`lcm`](#lcm)
- [`luhnCheck`](#luhncheck-)
- [`mapNumRange`](#mapnumrange)
- [`maxBy`](#maxby)
- [`median`](#median)
- [`midpoint`](#midpoint)
- [`minBy`](#minby)
- [`percentile`](#percentile)
- [`powerset`](#powerset)
- [`primes`](#primes)
- [`radsToDegrees`](#radstodegrees)
- [`randomIntArrayInRange`](#randomintarrayinrange)
- [`randomIntegerInRange`](#randomintegerinrange)
- [`randomNumberInRange`](#randomnumberinrange)
- [`round`](#round)
- [`sdbm`](#sdbm)
- [`standardDeviation`](#standarddeviation)
- [`sum`](#sum)
- [`sumBy`](#sumby)
- [`sumPower`](#sumpower)
- [`toSafeInteger`](#tosafeinteger)
- [`vectorDistance`](#vectordistance)

</details>

---

<!-- 2019年11月14日 09:19:06 -->

## ➗ Math

### approximatelyEqual

检测两个数字是否近似相等。

使用 `Math.abs()` t 比较两个值的绝对差和 `epsilon`。省略第三个参数`epsilon`，则使用默认值`0.001`。

```js
const approximatelyEqual = (v1, v2, epsilon = 0.001) =>
  Math.abs(v1 - v2) < epsilon;
```

<details>
<summary>Examples</summary>

```js
approximatelyEqual(Math.PI / 2.0, 1.5708); // true
```

</details>
<br>[⬆ Back to top](#contents)

### average

返回两个或多个数字的平均值。

使用 `Array.prototype.reduce()` 将每个值添加到累加器中，并以值 0 初始化，再除以数组的长度。

```js
const average = (...nums) =>
  nums.reduce((acc, val) => acc + val, 0) / nums.length;
```

<details>
<summary>Examples</summary>

```js
average(...[1, 2, 3]); // 2
average(1, 2, 3); // 2
```

</details>

<br>[⬆ Back to top](#contents)

### averageBy

使用提供的函数将每个元素映射到一个值后，返回数组的平均值。

使用 `Array.prototype.map()` 将每个元素映射到`fn`返回的值, `Array.prototype.reduce()` 将每个值添加到累加器中，并以值 0 初始化，再除以数组的长度。

```js
const averageBy = (arr, fn) =>
  arr
    .map(typeof fn === "function" ? fn : val => val[fn])
    .reduce((acc, val) => acc + val, 0) / arr.length;
```

<details>
<summary>Examples</summary>

```js
averageBy([{ n: 4 }, { n: 2 }, { n: 8 }, { n: 6 }], o => o.n); // 5
averageBy([{ n: 4 }, { n: 2 }, { n: 8 }, { n: 6 }], "n"); // 5
```

</details>

<br>[⬆ Back to top](#contents)

### binomialCoefficient

**[二项式系数](https://baike.baidu.com/item/%E4%BA%8C%E9%A1%B9%E5%BC%8F%E7%B3%BB%E6%95%B0/6763242?fr=aladdin)**

Evaluates the binomial coefficient of two integers `n` and `k`.
计算两个整数 `n` 和 `k`的二项式系数。

Use `Number.isNaN()` to check if any of the two values is `NaN`.
使用`Number.isNaN()`检查两个值是否为`NaN`。
检查`k`是否小于 `0`，大于或等于 `n`，等于 `1` 或`n-1`，并返回适当的结果。
检查`n - k`是否小于`k`，并相应地切换其值。
从 `2` 到 `k` 循环并计算二项式系数。
使用`Math.round（）`来解决计算中的舍入误差。

```js
const binomialCoefficient = (n, k) => {
  if (Number.isNaN(n) || Number.isNaN(k)) return NaN;
  if (k < 0 || k > n) return 0;
  if (k === 0 || k === n) return 1;
  if (k === 1 || k === n - 1) return n;
  if (n - k < k) k = n - k;
  let res = n;
  for (let j = 2; j <= k; j++) res *= (n - j + 1) / j;
  return Math.round(res);
};
```

<details>
<summary>Examples</summary>

```js
binomialCoefficient(8, 2); // 28
```

</details>

<br>[⬆ Back to top](#contents)

### clampNumber

将 `num` 限制在边界值 `a` 和 `b` 指定的范围内。

如果 `num` 在此范围内，则返回 `num`。
否则，返回范围内最接近的数字。

```js
const clampNumber = (num, a, b) =>
  Math.max(Math.min(num, Math.max(a, b)), Math.min(a, b));
```

<details>
<summary>Examples</summary>

```js
clampNumber(2, 3, 5); // 3
clampNumber(1, -1, -5); // -1
```

</details>

<br>[⬆ Back to top](#contents)

### degreesToRads

将角度从度转换为弧度。

使用 `Math.PI` 和度数到弧度公式将角度从度数转换为弧度。

```js
const degreesToRads = deg => (deg * Math.PI) / 180.0;
```

<details>
<summary>Examples</summary>

```js
degreesToRads(90.0); // 1.5707963267948966
```

</details>

<br>[⬆ Back to top](#contents)

### digitize

将数字转换为数字数组。

使用扩展运算符（`...`）将数字转换为字符串以构建数组。
使用 `Array.prototype.map()` 和 `parseInt()`将每个值转换为 int。

```js
const digitize = n => [...`${n}`].map(i => parseInt(i));
```

<details>
<summary>Examples</summary>

```js
digitize(123); // [1, 2, 3]
```

</details>

<br>[⬆ Back to top](#contents)

### distance

返回两点之间的距离。

使用 [`Math.hypot()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/hypot) 计算两点之间的欧几里得距离。

```js
const distance = (x0, y0, x1, y1) => Math.hypot(x1 - x0, y1 - y0);
```

<details>
<summary>Examples</summary>

```js
distance(1, 1, 2, 3); // 2.23606797749979
```

</details>

<br>[⬆ Back to top](#contents)

### elo ![advanced](../advanced.svg)

使用[Elo 评分系统](https://en.wikipedia.org/wiki/Elo_rating_system)计算两个或多个对手之间的新评分。 它需要一个数组
的前评分，并返回包含后评分的数组。
阵列应从性能最佳到性能最差的顺序排列（优胜者->失败者）。

使用指数运算符`**`和数学运算符来计算预期分数（获胜机会）。
并计算每个对手的新等级。
循环浏览等级，使用每个排列以成对方式计算每个玩家的 Elo 后等级。
省略第二个参数以使用默认的`kFactor`值 32。

```js
const elo = ([...ratings], kFactor = 32, selfRating) => {
  const [a, b] = ratings;
  const expectedScore = (self, opponent) =>
    1 / (1 + 10 ** ((opponent - self) / 400));
  const newRating = (rating, i) =>
    (selfRating || rating) +
    kFactor * (i - expectedScore(i ? a : b, i ? b : a));
  if (ratings.length === 2) return [newRating(a, 1), newRating(b, 0)];

  for (let i = 0, len = ratings.length; i < len; i++) {
    let j = i;
    while (j < len - 1) {
      j++;
      [ratings[i], ratings[j]] = elo([ratings[i], ratings[j]], kFactor);
    }
  }
  return ratings;
};
```

<details>
<summary>Examples</summary>

```js
// Standard 1v1s
elo([1200, 1200]); // [1216, 1184]
elo([1200, 1200], 64); // [1232, 1168]
// 4 player FFA, all same rank
elo([1200, 1200, 1200, 1200]).map(Math.round); // [1246, 1215, 1185, 1154]
/*
For teams, each rating can adjusted based on own team's average rating vs.
average rating of opposing team, with the score being added to their
own individual rating by supplying it as the third argument.
*/
```

</details>

<br>[⬆ Back to top](#contents)

### factorial

计算数字的阶乘。

使用递归。
如果 n 小于或等于 1，则返回 1。
否则，返回 n 和阶乘 n-1 的乘积。
如果 n 为负数，则抛出异常。

```js
const factorial = n =>
  n < 0
    ? (() => {
        throw new TypeError("Negative numbers are not allowed!");
      })()
    : n <= 1
    ? 1
    : n * factorial(n - 1);
```

<details>
<summary>Examples</summary>

```js
factorial(6); // 720
```

</details>

<br>[⬆ Back to top](#contents)

### fibonacci

生成一个数组，其中包含斐波那契序列，直到第 `n` 个。

创建一个特定长度的空数组，初始化前两个值（`0`和`1`）。
使用`Array.prototype.reduce()`，使用前两个值（前两个值除外）之和将值添加到数组中。

```js
const fibonacci = n =>
  Array.from({ length: n }).reduce(
    (acc, val, i) => acc.concat(i > 1 ? acc[i - 1] + acc[i - 2] : i),
    []
  );
```

<details>
<summary>Examples</summary>

```js
fibonacci(6); // [0, 1, 1, 2, 3, 5]
```

</details>

<br>[⬆ Back to top](#contents)

### gcd

计算两个或多个数字/数组之间的最大公约数。

内部的`_gcd`函数使用递归。
`y` 等于 `0`时，返回`x`。
否则，返回 GCD 的所需参数 `y`和 `x % y`。

```js
const gcd = (...arr) => {
  const _gcd = (x, y) => (!y ? x : gcd(y, x % y));
  return [...arr].reduce((a, b) => _gcd(a, b));
};
```

<details>
<summary>Examples</summary>

```js
gcd(8, 36); // 4
gcd(...[12, 8, 32]); // 4
```

</details>

<br>[⬆ Back to top](#contents)

### geometricProgression

初始化一个数组，该数组包含指定范围内的数字，其中`start`和`end` 包括端值，并且两项之间的比率为`step`。
如果`step` 等于 1，则返回错误。

使用`Array.from()`, `Math.log()` and `Math.floor()`创建所需长度的数组， `Array.prototype.map()` 来填充所需长度的数组。 范围。
省略第二个参数`start`则使用默认值 1。
省略第三个参数`step`则使用默认值 2。

```js
const geometricProgression = (end, start = 1, step = 2) =>
  Array.from({
    length: Math.floor(Math.log(end / start) / Math.log(step)) + 1
  }).map((v, i) => start * step ** i);
```

<details>
<summary>Examples</summary>

```js
geometricProgression(256); // [1, 2, 4, 8, 16, 32, 64, 128, 256]
geometricProgression(256, 3); // [3, 6, 12, 24, 48, 96, 192]
geometricProgression(256, 1, 4); // [1, 4, 16, 64, 256]
```

</details>

<br>[⬆ Back to top](#contents)
