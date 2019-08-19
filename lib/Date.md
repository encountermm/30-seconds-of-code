## Contents
### ⏱️ Date

<details>
<summary>View contents</summary>

* [`dayOfYear`](#dayofyear)
* [`formatDuration`](#formatduration)
* [`getColonTimeFromDate`](#getcolontimefromdate)
* [`getDaysDiffBetweenDates`](#getdaysdiffbetweendates)
* [`getMeridiemSuffixOfInteger`](#getmeridiemsuffixofinteger)
* [`isAfterDate`](#isafterdate)
* [`isBeforeDate`](#isbeforedate)
* [`isSameDate`](#issamedate)
* [`isWeekday`](#isweekday)
* [`isWeekend`](#isweekend)
* [`maxDate`](#maxdate)
* [`minDate`](#mindate)
* [`tomorrow`](#tomorrow)
* [`yesterday`](#yesterday)

</details>

<!-- 2019年8月19日 22:14:34 -->
## ⏱️ Date

### dayOfYear

从`Date`对象获取一年中的某一天。

使用`new Date()`和`Date.prototype.getFullYear()`来获取一年中的第一天作为`Date`对象，从提供的`date`中减去它，然后除以每天的毫秒数得到 结果。
使用`Math.floor()`将生成的日计数适当地舍入为整数。

```js
const dayOfYear = date =>
  Math.floor((date - new Date(date.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);
```

<details>
<summary>Examples</summary>

```js
dayOfYear(new Date()); // 272
```

</details>

<br>[⬆ 返回顶部](#contents)

### formatDuration

返回给定毫秒数的可读格式。

将`ms`除以适当的值，以获得`day`，`hour`，`minute`，`second`和`millisecond`的适当值。
使用`Object.entries()`和`Array.prototype.filter()`来保持非零值。
使用`Array.prototype.map()`为每个值创建字符串，并进行适当的多元化。
使用`String.prototype.join（'，'）`将值组合成一个字符串。

```js
const formatDuration = ms => {
  if (ms < 0) ms = -ms;
  const time = {
    day: Math.floor(ms / 86400000),
    hour: Math.floor(ms / 3600000) % 24,
    minute: Math.floor(ms / 60000) % 60,
    second: Math.floor(ms / 1000) % 60,
    millisecond: Math.floor(ms) % 1000
  };
  return Object.entries(time)
    .filter(val => val[1] !== 0)
    .map(([key, val]) => `${val} ${key}${val !== 1 ? 's' : ''}`)
    .join(', ');
};
```

<details>
<summary>Examples</summary>

```js
formatDuration(1001); // '1 second, 1 millisecond'
formatDuration(34325055574); // '397 days, 6 hours, 44 minutes, 15 seconds, 574 milliseconds'
```

</details>

<br>[⬆ 返回顶部](#contents)

### getColonTimeFromDate

从`Date`对象返回`“HH：MM：SS”`形式的字符串。

使用`Date.prototype.toTimeString()`和`String.prototype.slice()`来获取给定`Date`对象的`HH：MM：SS`部分。
```js
const getColonTimeFromDate = date => date.toTimeString().slice(0, 8);
```

<details>
<summary>Examples</summary>

```js
getColonTimeFromDate(new Date()); // "08:38:00"
```

</details>

<br>[⬆ 返回顶部](#contents)

### getDaysDiffBetweenDates

返回两个日期之间的差异（以天为单位）。

计算两个`Date`对象之间的差异（以天为单位）。

```js
const getDaysDiffBetweenDates = (dateInitial, dateFinal) =>
  (dateFinal - dateInitial) / (1000 * 3600 * 24);
```

<details>
<summary>Examples</summary>

```js
getDaysDiffBetweenDates(new Date('2017-12-13'), new Date('2017-12-22')); // 9
```

</details>

<br>[⬆ 返回顶部](#contents)

### getMeridiemSuffixOfInteger

将整数转换为后缀字符串，根据其值添加“am”或“pm”。

使用模运算符（`％`）和条件检查将整数转换为带有meridiem后缀的字符串化12小时格式。

```js
const getMeridiemSuffixOfInteger = num =>
  num === 0 || num === 24
    ? 12 + 'am'
    : num === 12
      ? 12 + 'pm'
      : num < 12
        ? (num % 12) + 'am'
        : (num % 12) + 'pm';
```

<details>
<summary>Examples</summary>

```js
getMeridiemSuffixOfInteger(0); // "12am"
getMeridiemSuffixOfInteger(11); // "11am"
getMeridiemSuffixOfInteger(13); // "1pm"
getMeridiemSuffixOfInteger(25); // "1pm"
```

</details>

<br>[⬆ 返回顶部](#contents)

### isAfterDate

检查日期是否在另一个日期之后。

使用大于运算符（`>`）来检查第一个日期是否在第二个日期之后。

```js
const isAfterDate = (dateA, dateB) => dateA > dateB;
```

<details>
<summary>Examples</summary>

```js
isAfterDate(new Date(2010, 10, 21), new Date(2010, 10, 20)); // true
```

</details>

<br>[⬆ 返回顶部](#contents)

### isBeforeDate

检查日期是否在另一个日期之前。

使用小于运算符（`<`）来检查第一个日期是否在第二个日期之前。

```js
const isBeforeDate = (dateA, dateB) => dateA < dateB;
```

<details>
<summary>Examples</summary>

```js
isBeforeDate(new Date(2010, 10, 20), new Date(2010, 10, 21)); // true
```

</details>

<br>[⬆ 返回顶部](#contents)

### isSameDate

检查日期是否与另一个日期相同。

使用`Date.prototype.toISOString()`和严格的等式检查（`===`）来检查第一个日期是否与第二个日期相同。

```js
const isSameDate = (dateA, dateB) => dateA.toISOString() === dateB.toISOString();
```

<details>
<summary>Examples</summary>

```js
isSameDate(new Date(2010, 10, 20), new Date(2010, 10, 20)); // true
```

</details>

<br>[⬆ 返回顶部](#contents)

### isWeekday

导致特定日期的布尔表示。

首先传递特定日期对象。
使用`Date.getDay()`通过使用模运算符然后返回布尔值来检查工作日。

```js
const isWeekday = (t = new Date()) => {
  return t.getDay() % 6 !== 0;
};
```

<details>
<summary>Examples</summary>

```js
isWeekday(); // true (if current date is 2019-07-19)
```

</details>

<br>[⬆ 返回顶部](#contents)

### isWeekend

判断指定日期是否为周末，返回一个`布尔值`。

首先传递特定日期对象。
使用`Date.getDay()`根据返回的日期检查周末为0  -  6，使用模运算然后返回一个布尔值。

```js
const isWeekend = (t = new Date()) => {
  return t.getDay() % 6 === 0;
};
```

<details>
<summary>Examples</summary>

```js
isWeekend(); // 2018-10-19 (if current date is 2018-10-18)
```

</details>

<br>[⬆ 返回顶部](#contents)

### maxDate

返回给定日期数组的最大值。

使用带有`Math.max`的ES6扩展语法来查找最大日期值，`new Date()`将其转换为`Date`对象。
```js
const maxDate = dates => new Date(Math.max(...dates));
```

<details>
<summary>Examples</summary>

```js
const array = [
  new Date(2017, 4, 13),
  new Date(2018, 2, 12),
  new Date(2016, 0, 10),
  new Date(2016, 0, 9)
];
maxDate(array); // 2018-03-11T22:00:00.000Z
```

</details>

<br>[⬆ 返回顶部](#contents)

### minDate

返回给定日期数组的最小值。

使用ES6扩展语法查找最小日期值，`new Date()`将其转换为`Date`对象。

```js
const minDate = dates => new Date(Math.min(...dates));
```

<details>
<summary>Examples</summary>

```js
const array = [
  new Date(2017, 4, 13),
  new Date(2018, 2, 12),
  new Date(2016, 0, 10),
  new Date(2016, 0, 9)
];
minDate(array); // 2016-01-08T22:00:00.000Z
```

</details>

<br>[⬆ 返回顶部](#contents)

### tomorrow

返回明天的日期。

使用`new Date()`获取当前日期，使用`Date.getDate()`递增1，并使用`Date.setDate()`将值设置为结果。
使用`Date.prototype.toISOString()`以`yyyy-mm-dd`格式返回一个字符串。

```js
const tomorrow = () => {
  let t = new Date();
  t.setDate(t.getDate() + 1);
  return t.toISOString().split('T')[0];
};
```

<details>
<summary>Examples</summary>

```js
tomorrow(); // 2018-10-19 (if current date is 2018-10-18)
```

</details>

<br>[⬆ 返回顶部](#contents)

### yesterday

返回昨天的日期。

使用`new Date()`获取当前日期，使用`Date.getDate()`递减1，并使用`Date.setDate()`将值设置为结果。
使用`Date.prototype.toISOString()`以`yyyy-mm-dd`格式返回一个字符串。

```js
const yesterday = () => {
  let t = new Date();
  t.setDate(t.getDate() - 1);
  return t.toISOString().split('T')[0];
};
```

<details>
<summary>Examples</summary>

```js
yesterday(); // 2018-10-17 (if current date is 2018-10-18)
```

</details>

<br>[⬆ 返回顶部](#contents)


---


