## contents
### 📚 Array

<details>
<summary>View contents</summary>

* [`all`](#all)
* [`allEqual`](#allequal)
* [`any`](#any)
* [`arrayToCSV`](#arraytocsv)
* [`bifurcate`](#bifurcate)
* [`bifurcateBy`](#bifurcateby)
* [`chunk`](#chunk)
* [`compact`](#compact)
* [`countBy`](#countby)
* [`countOccurrences`](#countoccurrences)
* [`deepFlatten`](#deepflatten)
* [`difference`](#difference)
* [`differenceBy`](#differenceby)
* [`differenceWith`](#differencewith)
* [`drop`](#drop)
* [`dropRight`](#dropright)
* [`dropRightWhile`](#droprightwhile)
* [`dropWhile`](#dropwhile)
* [`everyNth`](#everynth)
* [`filterFalsy`](#filterfalsy)
* [`filterNonUnique`](#filternonunique)
* [`filterNonUniqueBy`](#filternonuniqueby)
* [`findLast`](#findlast)
* [`findLastIndex`](#findlastindex)
* [`flatten`](#flatten)
* [`forEachRight`](#foreachright)
* [`groupBy`](#groupby)
* [`head`](#head)
* [`indexOfAll`](#indexofall)
* [`initial`](#initial)
* [`initialize2DArray`](#initialize2darray)
* [`initializeArrayWithRange`](#initializearraywithrange)
* [`initializeArrayWithRangeRight`](#initializearraywithrangeright)
* [`initializeArrayWithValues`](#initializearraywithvalues)
* [`initializeNDArray`](#initializendarray)
* [`intersection`](#intersection)
* [`intersectionBy`](#intersectionby)
* [`intersectionWith`](#intersectionwith)
* [`isSorted`](#issorted)
* [`join`](#join)
* [`JSONtoCSV`](#jsontocsv-)
* [`last`](#last)
* [`longestItem`](#longestitem)
* [`mapObject`](#mapobject-)
* [`maxN`](#maxn)
* [`minN`](#minn)
* [`none`](#none)
* [`nthElement`](#nthelement)
* [`offset`](#offset)
* [`partition`](#partition)
* [`permutations`](#permutations-)
* [`pull`](#pull)
* [`pullAtIndex`](#pullatindex-)
* [`pullAtValue`](#pullatvalue-)
* [`pullBy`](#pullby-)
* [`reducedFilter`](#reducedfilter)
* [`reduceSuccessive`](#reducesuccessive)
* [`reduceWhich`](#reducewhich)
* [`reject`](#reject)
* [`remove`](#remove)
* [`sample`](#sample)
* [`sampleSize`](#samplesize)
* [`shank`](#shank)
* [`shuffle`](#shuffle)
* [`similarity`](#similarity)
* [`sortedIndex`](#sortedindex)
* [`sortedIndexBy`](#sortedindexby)
* [`sortedLastIndex`](#sortedlastindex)
* [`sortedLastIndexBy`](#sortedlastindexby)
* [`stableSort`](#stablesort-)
* [`symmetricDifference`](#symmetricdifference)
* [`symmetricDifferenceBy`](#symmetricdifferenceby)
* [`symmetricDifferenceWith`](#symmetricdifferencewith)
* [`tail`](#tail)
* [`take`](#take)
* [`takeRight`](#takeright)
* [`takeRightWhile`](#takerightwhile)
* [`takeWhile`](#takewhile)
* [`toHash`](#tohash)
* [`union`](#union)
* [`unionBy`](#unionby)
* [`unionWith`](#unionwith)
* [`uniqueElements`](#uniqueelements)
* [`uniqueElementsBy`](#uniqueelementsby)
* [`uniqueElementsByRight`](#uniqueelementsbyright)
* [`uniqueSymmetricDifference`](#uniquesymmetricdifference)
* [`unzip`](#unzip)
* [`unzipWith`](#unzipwith-)
* [`without`](#without)
* [`xProd`](#xprod)
* [`zip`](#zip)
* [`zipObject`](#zipobject)
* [`zipWith`](#zipwith-)

</details>

---

## 📚 Array

### all

如果数组中的所有元素都基于函数`fn()`返回`true`，则返回`true`否则返回`false`

使用`Array.prototype.every()`来检测数组中的所有元素是否基于`fn`返回`true`。

省略第二个参数`fn`，使用`Boolean`作为默认值。

```js
const all = (arr, fn = Boolean) => arr.every(fn);
```

<details>
<summary>Examples</summary>

```js
all([4, 2, 3], x => x > 1); // true
all([1, 2, 3]); // true
```

</details>

<br>[⬆返回顶部](#contents)

### allEqual

检测数组中的所有元素是否相等。

使用`Array.prototype.every()`来检查数组的所有元素是否与第一个元素相同。
使用严格比较运算符(`===`)比较数组中的元素，该运算符不考虑“NaN”自不等式。

```js
const allEqual = arr => arr.every(val => val === arr[0]);
```

<details>
<summary>Examples</summary>

```js
allEqual([1, 2, 3, 4, 5, 6]); // false
allEqual([1, 1, 1, 1]); // true
```

</details>

<br>[⬆返回顶部](#contents)

### any

如果数组中至少有一个元素基于函数`fn()`返回`true`，则返回`true`否则返回`false`.

使用`array.prototype.some()`检测数组中的任何元素是否基于`fn`返回`true`.

省略第二个参数`fn`，将`boolean`用作默认值。

```js
const any = (arr, fn = Boolean) => arr.some(fn);
```

<details>
<summary>Examples</summary>

```js
any([0, 1, 2, 0], x => x >= 2); // true
any([0, 0, 1, 0]); // true
```

</details>

<br>[⬆返回顶部](#contents)

### arrayToCSV

将二维数组转换为逗号分隔值（csv）字符串。

使用`array.prototype.map()`和`array.prototype.join(delimiter)`将单个一维数组（行）组合为字符串。

使用`array.prototype.join('\n')`将所有元素（行）组合成一个csv字符串，用换行符分隔每一行。

省略第二个参数`delimiter`，使用`,`的默认分隔符。

```js
const arrayToCSV = (arr, delimiter = ',') =>
  arr.map(v => v.map(x => (isNaN(x) ? `"${x.replace(/"/g, '""')}"` : x)).join(delimiter))
    .join('\n');
```

<details>
<summary>Examples</summary>

```js
arrayToCSV([['a', 'b'], ['c', 'd']]); // '"a","b"\n"c","d"'
arrayToCSV([['a', 'b'], ['c', 'd']], ';'); // '"a";"b"\n"c";"d"'
arrayToCSV([['a', '"b" great'], ['c', 3.1415]]); // '"a","""b"" great"\n"c",3.1415'
```

</details>

<br>[⬆返回顶部](#contents)

### bifurcate

将值拆分为两组。 如果`filter`中的元素为`true`，则数组中的对应元素属于第一组; 否则属于第二组。

使用`Array.prototype.reduce()`和`Array.prototype.push()`基于`filter`向组添加元素。

```js
const bifurcate = (arr, filter) =>
  arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []]);
```

<details>
<summary>Examples</summary>

```js
bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```

</details>

<br>[⬆返回顶部](#contents)

### bifurcateBy

根据所传函数`fn`将数组元素分成两组，所传函数指定输入数组中某个元素所属的数组。如果函数`fn`返回`true`，则数组元素属于第一组；否则属于第二组。

使用`Array.prototype.reduce()`和`Array.prototype.push()`根据`fn`为每个元素返回的值向组添加元素。

```js
const bifurcateBy = (arr, fn) =>
  arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []]);
```

<details>
<summary>Examples</summary>

```js
bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b'); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```

</details>

<br>[⬆返回顶部](#contents)

### chunk

将数组块化为指定大小的较小数组。

Use `Array.from()` to create a new array, that fits the number of chunks that will be produced.

使用`array.from()`创建一个符合将生成的块的数量新数组。

使用`array.prototype.slice()`将新数组的每个元素映射到长度为`size`的块.

如果原始数组无法均匀分割，则最后一个块将包含其余元素。

```js
const chunk = (arr, size) =>
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
```

<details>
<summary>Examples</summary>

```js
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
```

</details>

<br>[⬆返回顶部](#contents)


### compact

从数组中过滤掉假值（`false`）。

使用`Array.prototype.filter()`来过滤掉假值(`false`，`null`，`0`，`""`，`undefined`和`NaN`)。

```js
const compact = arr => arr.filter(Boolean);
```

<details>
<summary>Examples</summary>

```js
compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); // [ 1, 2, 3, 'a', 's', 34 ]
```

</details>

<br>[⬆返回顶部](#contents)

### countBy

根据给定的函数对数组的元素进行分组，并返回每个组中元素的数量。

使用`Array.prototype.map()`将数组的值映射到函数或属性名称。使用`Array.prototype.map()`将数组的值映射到函数或属性名称。

使用`Array.prototype.reduce()`创建一个对象，其中的键是从映射的结果中生成的。

```js
const countBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val) => {
    acc[val] = (acc[val] || 0) + 1;
    return acc;
  }, {});
```

<details>
<summary>Examples</summary>

```js
countBy([6.1, 4.2, 6.3], Math.floor); // {4: 1, 6: 2}
countBy(['one', 'two', 'three'], 'length'); // {3: 2, 5: 1}
```

</details>

<br>[⬆返回顶部](#contents)

### countOccurrences

计算数组中某个值的出现次数。

每次遇到数组中的特定值时，使用`Array.prototype.reduce()`递增计数器。

```js
const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0);
```

<details>
<summary>Examples</summary>

```js
countOccurrences([1, 1, 2, 1, 2, 3], 1); // 3
```

</details>

<br>[⬆返回顶部](#contents)


### deepFlatten

将数组展平。

使用递归。使用带有空数组（`[]`）的`Array.prototype.concat()`和扩展运算符（`...`）来展平数组。

递归地展平作为数组的每个元素。

```js
const deepFlatten = arr => [].concat(...arr.map(v => (Array.isArray(v) ? deepFlatten(v) : v)));
```

<details>
<summary>Examples</summary>

```js
deepFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
```

</details>

<br>[⬆返回顶部](#contents)

### difference

返回两个数组之间的差异。

从`b`创建一个`Set`，然后在`a`上使用`Array.prototype.filter()`来保留不包含在`b`中的值。

```js
const difference = (a, b) => {
  const s = new Set(b);
  return a.filter(x => !s.has(x));
};
```

<details>
<summary>Examples</summary>

```js
difference([1, 2, 3], [1, 2, 4]); // [3]
```

</details>

<br>[⬆返回顶部](#contents)

### differenceBy

通过接收的函数`fn`，返回两个数组的差异。

通过将`fn`应用于`b`中的每个元素来创建`Set`，然后使用`Array.prototype.map()`将`fn`应用于`a`中的每个元素，然后应用`Array.prototype.filter()`

```js
const differenceBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.map(fn).filter(el => !s.has(el));
};
```

<details>
<summary>Examples</summary>

```js
differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [1]
differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], v => v.x); // [2]
```

</details>

<br>[⬆返回顶部](#contents)

### differenceWith

过滤掉数组()比较器函数未返回`true`的所有值。

使用`Array.prototype.filter()`和`Array.prototype.findIndex()`找到合适的值。

```js
const differenceWith = (arr, val, comp) => arr.filter(a => val.findIndex(b => comp(a, b)) === -1);
```

<details>
<summary>Examples</summary>

```js
differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b)); // [1, 1.2]
```

</details>

<br>[⬆返回顶部](#contents)

### drop

返回一个从左侧删除`n`个元素的新数组。

使用`Array.prototype.slice()`从左侧删除指定数量的元素。

```js
const drop=(arr,n=1)=>arr.slice(n)
```

<details>
<summary>Examples</summary>

```js
drop([1, 2, 3]); // [2,3]
drop([1, 2, 3], 2); // [3]
drop([1, 2, 3], 42); // []
```

</details>

<br>[⬆返回顶部](#contents)

### dropRight

返回一个从右侧删除`n`个元素的新数组。

使用`Array.prototype.slice()`从右侧删除指定数量的元素。

```js
const dropRight = (arr, n = 1) => arr.slice(0, -n);
```

<details>
<summary>Examples</summary>

```js
dropRight([1, 2, 3]); // [1,2]
dropRight([1, 2, 3], 2); // [1]
dropRight([1, 2, 3], 42); // []
```

</details>

<br>[⬆返回顶部](#contents)

### dropRightWhile

从数组末尾删除元素，直到传递的函数返回`true`。 返回数组中的其余元素。

循环遍历数组，使用`Array.prototype.slice()`删除数组的最后一个元素，直到函数返回的值为`true`,返回剩余的元素。

```js
const dropRightWhile = (arr, func) => {
  let rightIndex = arr.length;
  while (rightIndex-- && !func(arr[rightIndex]));
  return arr.slice(0, rightIndex + 1);
};
```

<details>
<summary>Examples</summary>

```js
dropRightWhile([1, 2, 3, 4], n => n < 3); // [1, 2]
```

</details>

<br>[⬆返回顶部](#contents)

### dropWhile

从数组左侧删除元素，直到传递的函数返回`true`。 返回数组中的其余元素。

循环遍历数组，使用`Array.prototype.slice()`删除数组的第一个元素，直到函数返回的值为`true`，返回剩余的元素。

```js
const dropWhile = (arr, func) => {
  while (arr.length > 0 && !func(arr[0])) arr = arr.slice(1);
  return arr;
};
```

<details>
<summary>Examples</summary>

```js
dropWhile([1, 2, 3, 4], n => n >= 3); // [3,4]
```

</details>

<br>[⬆返回顶部](#contents)

<!-- 2019年8月8日 23:29:58 -->
### everyNth

返回数组中序号（元素为数组的第几个元素）为n的倍数的所有元素。


使用`Array.prototype.filter()`创建一个包含给定数组中序号为n的倍数的所有元素的新数组。

```js
// const everyNth = (arr, nth) => arr.filter((e, i) => i % nth === nth - 1); 
// 上边为原函数，不易理解，自己处理为以下
const everyNth = (arr, nth) => arr.filter((e, i) => !((i+1) % nth) );
```

<details>
<summary>Examples</summary>

```js
everyNth([1, 2, 3, 4, 5, 6], 2); // [ 2, 4, 6 ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### filterFalsy

Filters out the falsy values in an array.
过滤掉数组中的假值`false`。

使用`Array.prototype.filter()`创建一个只包含真值`true`的新数组。

```js
const filterFalsy = arr => arr.filter(Boolean);
```

<details>
<summary>Examples</summary>

```js
filterFalsy(['', true, {}, false, 'sample', 1, 0]); // [true, {}, 'sample', 1]
```

</details>

<br>[⬆ 返回顶部](#contents)

### filterNonUnique

过滤掉数组中重复的值。

使用`Array.prototype.filter()`创建一个只包含唯一值的新数组。

```js
// indexOf 是查某个指定的字符串在字符串首次出现的位置（索引值） （也就是从前往后查）
// lastIndexOf 是从右向左查某个指定的字符串在字符串中最后一次出现的位置（也就是从后往前查）
// 如果两个值相等，可说明该元素在数组中只出现一次
const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
```

<details>
<summary>Examples</summary>

```js
filterNonUnique([1, 2, 2, 3, 4, 4, 5]); // [1, 3, 5]
```

</details>

<br>[⬆ 返回顶部](#contents)

### filterNonUniqueBy


根据给定的比较器函数，过滤掉数组中的重复元素

使用`Array.prototype.filter()`和`Array.prototype.every()`基于比较器函数`fn`创建一个只包含唯一值的数组。

比较器函数有四个参数：被比较的两个元素的值及其索引。

```js
const filterNonUniqueBy = (arr, fn) =>
  arr.filter((v, i) => arr.every((x, j) => (i === j) === fn(v, x, i, j)));
```

<details>
<summary>Examples</summary>

```js
filterNonUniqueBy(
  [
    { id: 0, value: 'a' },
    { id: 1, value: 'b' },
    { id: 2, value: 'c' },
    { id: 1, value: 'd' },
    { id: 0, value: 'e' }
  ],
  (a, b) => a.id == b.id
); // [ { id: 2, value: 'c' } ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### findLast

返回所提供函数返回`true`的最后一个元素。

使用`Array.prototype.filter()`删除`fn`返回falsy值的元素，'Array.prototype.pop()`来获取最后一个元素。

```js
const findLast = (arr, fn) => arr.filter(fn).pop();
```

<details>
<summary>Examples</summary>

```js
findLast([1, 2, 3, 4], n => n % 2 === 1); // 3
```

</details>

<br>[⬆ 返回顶部](#contents)

### findLastIndex

返回提供的函数返回`true`的最后一个元素的索引。

使用`Array.prototype.map()`将每个元素映射到具有索引和值的数组。

使用`Array.prototype.filter()`删除`fn`返回falsy值的元素，'Array.prototype.pop()`来获取最后一个。

```js
const findLastIndex = (arr, fn) =>
  arr
    .map((val, i) => [i, val])
    .filter(([i, val]) => fn(val, i, arr))
    .pop()[0];
```

<details>
<summary>Examples</summary>

```js
findLastIndex([1, 2, 3, 4], n => n % 2 === 1); // 2 (index of the value 3)
```

</details>

<br>[⬆ 返回顶部](#contents)

### flatten

将数组展平到指定的深度。

使用递归，每个深度级别将“深度”递减1。使用`Array.prototype.reduce()`和`Array.prototype.concat()`来合并元素或数组。

基本情况下，当depth 等于1时停止递归。 忽略第二个参数的情况下， depth 默认为1（单层展开）。

```js
const flatten = (arr, depth = 1) =>
  arr.reduce((a, v) => a.concat(depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v), []);
```

<details>
<summary>Examples</summary>

```js
flatten([1, [2], 3, 4]); // [1, 2, 3, 4]
flatten([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]
```

</details>

<br>[⬆ 返回顶部](#contents)

### forEachRight

从右向左遍历数组

使用`Array.prototype.slice（0）`来克隆给定的数组，使用`Array.prototype.reverse()`来反转它，使用`Array.prototype.forEach()`迭代反转的数组。

```js
const forEachRight = (arr, callback) =>
  arr
    .slice(0)
    .reverse()
    .forEach(callback);
```

<details>
<summary>Examples</summary>

```js
forEachRight([1, 2, 3, 4], val => console.log(val)); // '4', '3', '2', '1'
```

</details>

<br>[⬆ 返回顶部](#contents)

### groupBy

根据给定的函数对数组的元素进行分组。

使用`Array.prototype.map()`将数组的值映射到函数或属性名称。
使用`Array.prototype.reduce()`创建一个对象，其中的键是从映射的结果中生成的。

```js
const groupBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
    acc[val] = (acc[val] || []).concat(arr[i]);
    return acc;
  }, {});
```

<details>
<summary>Examples</summary>

```js
groupBy([6.1, 4.2, 6.3], Math.floor); // {4: [4.2], 6: [6.1, 6.3]}
groupBy(['one', 'two', 'three'], 'length'); // {3: ['one', 'two'], 5: ['three']}
```

</details>

<br>[⬆ 返回顶部](#contents)

### head

返回数组的头部（第一个元素）。

使用`arr [0]`返回传递数组的第一个元素。

```js
const head = arr => arr[0];
```

<details>
<summary>Examples</summary>

```js
head([1, 2, 3]); // 1
```

</details>

<br>[⬆ 返回顶部](#contents)

<!-- 2019年8月9日 21:33:55 -->

### indexOfAll

返回数组中`某元素val`的所有索引。

如果`元素val`从未出现，则返回“[]”。

使用`array.prototype.reduce()`循环元素并存储匹配元素的索引。
返回索引数组。

```js
const indexOfAll = (arr, val) => arr.reduce((acc, el, i) => (el === val ? [...acc, i] : acc), []);
```

<details>
<summary>Examples</summary>

```js
indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
indexOfAll([1, 2, 3], 4); // []
```

</details>

<br>[⬆ 返回顶部](#contents)

### initial

返回一个包含除数组的最后一个元素之外的所有元素的数组。

使用`arr.slice（0，-1）`返回除数组的最后一个元素之外的所有元素。

```js
const initial = arr => arr.slice(0, -1);
```

<details>
<summary>Examples</summary>

```js
initial([1, 2, 3]); // [1,2]
```

</details>

<br>[⬆ 返回顶部](#contents)

### initialize2DArray

初始化给定宽度和高度以及值的二维数组。

使用`Array.prototype.map()`生成h行，其中每行都是一个大小为w的新数组，用value初始化。 如果未提供该值，则默认为“null”。

```js
const initialize2DArray = (w, h, val = null) =>
  Array.from({ length: h }).map(() => Array.from({ length: w }).fill(val));
```

<details>
<summary>Examples</summary>

```js
initialize2DArray(2, 2, 0); // [[0,0], [0,0]]
```

</details>

<br>[⬆ 返回顶部](#contents)

### initializeArrayWithRange

初始化一个数组，其中包含指定范围内的数字，其中`start`、`end`及其它们的差值`step`。

使用`Array.from()`创建一个所需长度的数组，`（end  -  start + 1）/ step`，以及一个map函数，用给定范围内的所需值填充它。
`start`不传则使用默认值`0`。
`step`不传则使用默认值`1`。

```js
const initializeArrayWithRange = (end, start = 0, step = 1) =>
  Array.from({ length: Math.ceil((end - start + 1) / step) }, (v, i) => i * step + start);
```

<details>
<summary>Examples</summary>

```js
initializeArrayWithRange(5); // [0,1,2,3,4,5]
initializeArrayWithRange(7, 3); // [3,4,5,6,7]
initializeArrayWithRange(9, 0, 2); // [0,2,4,6,8]
```

</details>

<br>[⬆ 返回顶部](#contents)

### initializeArrayWithRangeRight

初始化一个数组，其中包含指定范围内的数字（反向），其中`start`、`end`及其它们的差值`step`。

使用`Array.from（Math.ceil（（end + 1-start）/ step））`来创建一个所需长度的数组（元素的数量等于`（end-start）/ step`或`（ end + 1-start）/ step` for inclusive end），`Array.prototype.map()`用于填充范围内的所需值。

`start`不传则默认值`0`。

`step`不传则默认值`1`。

```js
const initializeArrayWithRangeRight = (end, start = 0, step = 1) =>
  Array.from({ length: Math.ceil((end + 1 - start) / step) }).map(
    (v, i, arr) => (arr.length - i - 1) * step + start
  );
```

<details>
<summary>Examples</summary>

```js
initializeArrayWithRangeRight(5); // [5,4,3,2,1,0]
initializeArrayWithRangeRight(7, 3); // [7,6,5,4,3]
initializeArrayWithRangeRight(9, 0, 2); // [8,6,4,2,0]
```

</details>

<br>[⬆ 返回顶部](#contents)

### initializeArrayWithValues

使用指定的值初始化并填充数组。

使用`Array（n）`创建一个所需长度的数组，`fill（v）`用所需的值填充它。
`val`不传则默认`0`。

```js
const initializeArrayWithValues = (n, val = 0) => Array(n).fill(val);
```

<details>
<summary>Examples</summary>

```js
initializeArrayWithValues(5, 2); // [2, 2, 2, 2, 2]
```

</details>

<br>[⬆ 返回顶部](#contents)

### initializeNDArray

创建具有给定值的n维数组。

使用递归。
使用`Array.prototype.map()`生成行，其中每个行都是使用`initialize NDArray`初始化的新数组。

```js
const initializeNDArray = (val, ...args) =>
  args.length === 0
    ? val
    : Array.from({ length: args[0] }).map(() => initializeNDArray(val, ...args.slice(1)));
```

<details>
<summary>Examples</summary>

```js
initializeNDArray(1, 3); // [1,1,1]
initializeNDArray(5, 2, 2, 2); // [[[5,5],[5,5]],[[5,5],[5,5]]]
```

</details>

<br>[⬆ 返回顶部](#contents)

### intersection

返回一个包含两个数组交集元素的数组。

从`b`创建一个`Set`，然后在`a`上使用`Array.prototype.filter()`来保存`b`中包含的值。

```js
const intersection = (a, b) => {
  const s = new Set(b);
  return a.filter(x => s.has(x));
};
```

<details>
<summary>Examples</summary>

```js
intersection([1, 2, 3], [4, 3, 2]); // [2, 3]
```

</details>

<br>[⬆ 返回顶部](#contents)

### intersectionBy

将提供的函数应应用到两个数组的每个元素上，然后返回两个数组中都存在的元素列表

通过将 `fn` 应用到`b`的所有元素来创建一个`Set`，然后在`a`上调用 `Array.prototype.filter()` 来只保留调用` fn` 后 `b` 中包含的元素。

```js
const intersectionBy = (a, b, fn) => {
  const s = new Set(b.map(fn));
  return a.filter(x => s.has(fn(x)));
};
```

<details>
<summary>Examples</summary>

```js
intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [2.1]
```

</details>

<br>[⬆ 返回顶部](#contents)

### intersectionWith

使用提供的比较器函数返回两个数组中存在的元素列表。

使用`Array.prototype.filter()`和`Array.prototype.findIndex()`结合提供的比较器来确定交叉值。

```js
const intersectionWith = (a, b, comp) => a.filter(x => b.findIndex(y => comp(x, y)) !== -1);
```

<details>
<summary>Examples</summary>

```js
intersectionWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0, 3.9], (a, b) => Math.round(a) === Math.round(b)); // [1.5, 3, 0]
```

</details>

<br>[⬆ 返回顶部](#contents)

<!-- 2019年8月10日 22:51:40 -->
### isSorted

如果数组按升序排序，则返回“1”;如果按降序排序，则返回“-1”;如果未排序，则返回“0”。

计算前两个元素的排序`方向`。
使用`Object.entries()`循环遍历数组对象并成对比较它们。
如果`direction`改变则返回`0`或如果到达最后一个元素则返回`direction`。

```js
const isSorted = arr => {
  let direction = -(arr[0] - arr[1]);
  for (let [i, val] of arr.entries()) {
    direction = !direction ? -(arr[i - 1] - arr[i]) : direction;
    if (i === arr.length - 1) return !direction ? 0 : direction;
    else if ((val - arr[i + 1]) * direction > 0) return 0;
  }
};
```

<details>
<summary>Examples</summary>

```js
isSorted([0, 1, 2, 2]); // 1
isSorted([4, 3, 2]); // -1
isSorted([4, 3, 5]); // 0
```

</details>

<br>[⬆ 返回顶部](#contents)

### join

将数组的所有元素连接成一个字符串并返回该字符串。
使用分隔符和结束分隔符。

使用`Array.prototype.reduce()`将元素组合成一个字符串。
省略第二个参数`separator`，使用`'，'`的默认分隔符。
省略第三个参数`end`，默认使用与`separator`相同的值。

```js
const join = (arr, separator = ',', end = separator) =>
  arr.reduce(
    (acc, val, i) =>
      i === arr.length - 2
        ? acc + val + end
        : i === arr.length - 1
          ? acc + val
          : acc + val + separator,
    ''
  );
```

<details>
<summary>Examples</summary>

```js
join(['pen', 'pineapple', 'apple', 'pen'], ',', '&'); // "pen,pineapple,apple&pen"
join(['pen', 'pineapple', 'apple', 'pen'], ','); // "pen,pineapple,apple,pen"
join(['pen', 'pineapple', 'apple', 'pen']); // "pen,pineapple,apple,pen"
```

</details>

<br>[⬆ 返回顶部](#contents)

### JSONtoCSV ![advanced](/advanced.svg)

将对象数组转换为逗号分隔值（CSV）字符串，该字符串仅包含指定的`columns`。

使用`Array.prototype.join（delimiter）`组合`columns`中的所有名称来创建第一行。
使用`Array.prototype.map()`和`Array.prototype.reduce()`为每个对象创建一个行，用空字符串替换不存在的值，只用`columns`映射值。
使用`Array.prototype.join（'\ n'）`将所有行组合成一个字符串。
省略第三个参数`delimiter`，使用`，`的默认分隔符。

```js
const JSONtoCSV = (arr, columns, delimiter = ',') =>
  [
    columns.join(delimiter),
    ...arr.map(obj =>
      columns.reduce(
        (acc, key) => `${acc}${!acc.length ? '' : delimiter}"${!obj[key] ? '' : obj[key]}"`,
        ''
      )
    )
  ].join('\n');
```

<details>
<summary>Examples</summary>

```js
JSONtoCSV([{ a: 1, b: 2 }, { a: 3, b: 4, c: 5 }, { a: 6 }, { b: 7 }], ['a', 'b']); // 'a,b\n"1","2"\n"3","4"\n"6",""\n"","7"'
JSONtoCSV([{ a: 1, b: 2 }, { a: 3, b: 4, c: 5 }, { a: 6 }, { b: 7 }], ['a', 'b'], ';'); // 'a;b\n"1";"2"\n"3";"4"\n"6";""\n"";"7"'
```

</details>

<br>[⬆ 返回顶部](#contents)

### last

返回数组中的最后一个元素。

使用`arr.length  -  1`计算给定数组的最后一个元素的索引并返回它。

```js
const last = arr => arr[arr.length - 1];
```

<details>
<summary>Examples</summary>

```js
last([1, 2, 3]); // 3
```

</details>

<br>[⬆ 返回顶部](#contents)

### longestItem

获取具有`length`属性的任意数量的可迭代对象或对象，并返回最长的对象或对象。
如果多个对象具有相同的长度，则将返回第一个对象。
如果没有提供参数，则返回`undefined`。

使用`Array.prototype.reduce()`，比较对象的`length`以找到最长的对象。

```js
const longestItem = (...vals) => vals.reduce((a, x) => (x.length > a.length ? x : a));
```

<details>
<summary>Examples</summary>

```js
longestItem('this', 'is', 'a', 'testcase'); // 'testcase'
longestItem(...['a', 'ab', 'abc']); // 'abc'
longestItem(...['a', 'ab', 'abc'], 'abcd'); // 'abcd'
longestItem([1, 2, 3], [1, 2], [1, 2, 3, 4, 5]); // [1, 2, 3, 4, 5]
longestItem([1, 2, 3], 'foobar'); // 'foobar'
```

</details>

<br>[⬆ 返回顶部](#contents)

### mapObject ![advanced](/advanced.svg)

使用函数将数组的值映射到对象，其中键值对由作为键的字符串化值和映射值组成。

使用匿名内部函数作用域来声明未定义的内存空间，使用闭包来存储返回值。 使用一个新的`Array`来存储数组，其中包含函数的数据集，并使用逗号运算符返回第二步，而无需从一个上下文移动到另一个上下文（由于闭包和操作顺序）。

```js
const mapObject = (arr, fn) =>
  (a => (
    (a = [arr, arr.map(fn)]), a[0].reduce((acc, val, ind) => ((acc[val] = a[1][ind]), acc), {})
  ))();
```

<details>
<summary>Examples</summary>

```js
const squareIt = arr => mapObject(arr, a => a * a);
squareIt([1, 2, 3]); // { 1: 1, 2: 4, 3: 9 }
```

</details>

<br>[⬆ 返回顶部](#contents)

### maxN
返回提供的数组中的`n`最大元素。
如果`n`大于或等于提供的数组长度，则返回原始数组（按降序排序）。

使用`Array.prototype.sort()`结合扩展运算符（`...`）来创建数组的浅层克隆并按降序排序。
使用`Array.prototype.slice()`来获取指定数量的元素。
省略第二个参数`n`，得到一个单元素数组。

```js
const maxN = (arr, n = 1) => [...arr].sort((a, b) => b - a).slice(0, n);
```

<details>
<summary>Examples</summary>

```js
maxN([1, 2, 3]); // [3]
maxN([1, 2, 3], 2); // [3,2]
```

</details>

<br>[⬆ 返回顶部](#contents)

### minN

从提供的数组中返回`n`最小元素。
如果`n`大于或等于提供的数组长度，则返回原始数组（按升序排序）。

使用`Array.prototype.sort()`结合扩展运算符（`...`）来创建数组的浅层克隆并按升序对其进行排序。
使用`Array.prototype.slice()`来获取指定数量的元素。
省略第二个参数`n`，得到一个单元素数组。

```js
const minN = (arr, n = 1) => [...arr].sort((a, b) => a - b).slice(0, n);
```

<details>
<summary>Examples</summary>

```js
minN([1, 2, 3]); // [1]
minN([1, 2, 3], 2); // [1,2]
```

</details>

<br>[⬆ 返回顶部](#contents)

### none

如果对集合中所有的元素执行判定函数全部都返回`false`，则返回`true`，否则返回`false`。

使用`Array.prototype.some()`来测试集合中的任何元素是否基于`fn`返回`true`。
省略第二个参数`fn`，使用`Boolean`作为默认值。

```js
const none = (arr, fn = Boolean) => !arr.some(fn);
```

<details>
<summary>Examples</summary>

```js
none([0, 1, 3, 0], x => x == 2); // true
none([0, 0, 0]); // true
```

</details>

<br>[⬆ 返回顶部](#contents)

### nthElement

返回数组的第n个元素。

使用`Array.prototype.slice()`来获取包含第一个元素的第n个元素的数组。
如果索引超出范围，则返回“undefined”。
省略第二个参数`n`，得到数组的第一个元素。

```js
const nthElement = (arr, n = 0) => (n === -1 ? arr.slice(n) : arr.slice(n, n + 1))[0];
```

<details>
<summary>Examples</summary>

```js
nthElement(['a', 'b', 'c'], 1); // 'b'
nthElement(['a', 'b', 'b'], -3); // 'a'
```

</details>

<br>[⬆ 返回顶部](#contents)

<!-- 2019年8月11日 23:24:17 -->
### offset

将指定数量的元素移动到数组的末尾。

两次使用`Array.prototype.slice()`来获取指定索引之后的元素以及之前的元素。
使用扩展运算符（`...`）将两者合并为一个数组。
如果`offset`为负数，则元素将从end移动到start。

```js
const offset = (arr, offset) => [...arr.slice(offset), ...arr.slice(0, offset)];
```

<details>
<summary>Examples</summary>

```js
offset([1, 2, 3, 4, 5], 2); // [3, 4, 5, 1, 2]
offset([1, 2, 3, 4, 5], -2); // [4, 5, 1, 2, 3]
```

</details>

<br>[⬆ 返回顶部](#contents)

### partition

将元素分组为两个数组，具体取决于所提供的函数作用域每个元素的返回的`Boolean`。

使用`Array.prototype.reduce()`创建一个包含两个数组的数组。
使用`Array.prototype.push()`将`fn`返回'true`的元素添加到第一个数组，将`fn`返回`false`的元素添加到第二个数组。

```js
const partition = (arr, fn) =>
  arr.reduce(
    (acc, val, i, arr) => {
      acc[fn(val, i, arr) ? 0 : 1].push(val);
      return acc;
    },
    [[], []]
  );
```

<details>
<summary>Examples</summary>

```js
const users = [{ user: 'barney', age: 36, active: false }, { user: 'fred', age: 40, active: true }];
partition(users, o => o.active); // [[{ 'user': 'fred',    'age': 40, 'active': true }],[{ 'user': 'barney',  'age': 36, 'active': false }]]
```

</details>

<br>[⬆ 返回顶部](#contents)

### permutations ![advanced](/advanced.svg)

⚠️ **WARNING**: 此函数的执行时间随每个数组元素呈指数增长。 超过8到10个条目的任何内容都会导致浏览器挂起，因为它会尝试解决所有不同的组合。

生成数组元素的所有排列（包含重复项）。

使用递归。
对于给定数组中的每个元素，为其余元素创建所有部分排列。
使用`Array.prototype.map()`将元素与每个部分排列组合，然后使用`Array.prototype.reduce()`来组合一个数组中的所有排列。
基本情况是数组`length`等于'2`或`1`。

```js
const permutations = arr => {
  if (arr.length <= 2) return arr.length === 2 ? [arr, [arr[1], arr[0]]] : arr;
  return arr.reduce(
    (acc, item, i) =>
      acc.concat(
        permutations([...arr.slice(0, i), ...arr.slice(i + 1)]).map(val => [item, ...val])
      ),
    []
  );
};
```

<details>
<summary>Examples</summary>

```js
permutations([1, 33, 5]); // [ [ 1, 33, 5 ], [ 1, 5, 33 ], [ 33, 1, 5 ], [ 33, 5, 1 ], [ 5, 1, 33 ], [ 5, 33, 1 ] ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### pull

过滤掉指定的值来改变原始数组。

使用`Array.prototype.filter()`和`Array.prototype.includes()`来提取不需要的值。
使用`Array.prototype.length = 0`来改变传入的数组，方法是将它的长度重置为零，并使用`Array.prototype.push()`重新填充它，只使用过滤剩余的值。

_（对于不改变原始数组的片段，请参见[`without`](＃without)）_
```js
const pull = (arr, ...args) => {
  let argState = Array.isArray(args[0]) ? args[0] : args;
  let pulled = arr.filter((v, i) => !argState.includes(v));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
};
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'a', 'b', 'c'];
pull(myArray, 'a', 'c'); // myArray = [ 'b', 'b' ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### pullAtIndex ![advanced](/advanced.svg)

过滤掉指定索引处的值来改变原数组。

使用`Array.prototype.filter()`和`Array.prototype.includes()`来提取不需要的值。
使用`Array.prototype.length = 0`来改变传入的数组，方法是将它的长度重置为零，并使用`Array.prototype.push()`重新填充它，只使用过滤后的值。
返回一个过滤的值组成的数组。

```js
const pullAtIndex = (arr, pullArr) => {
  let removed = [];
  let pulled = arr
    .map((v, i) => (pullArr.includes(i) ? removed.push(v) : v))
    .filter((v, i) => !pullArr.includes(i));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
  return removed;
};
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtIndex(myArray, [1, 3]); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### pullAtValue ![advanced](/advanced.svg)
改变原始数组以过滤掉指定的值。 返回已删除的元素。

使用`Array.prototype.filter()`和`Array.prototype.includes()`来提取不需要的值。
使用`Array.prototype.length = 0`来改变传入的数组，方法是将它的长度重置为零，并使用`Array.prototype.push()`重新填充它，只使用过滤后的值。

```js
const pullAtValue = (arr, pullArr) => {
  let removed = [],
    pushToRemove = arr.forEach((v, i) => (pullArr.includes(v) ? removed.push(v) : v)),
    mutateTo = arr.filter((v, i) => !pullArr.includes(v));
  arr.length = 0;
  mutateTo.forEach(v => arr.push(v));
  return removed;
};
```

<details>
<summary>Examples</summary>

```js
let myArray = ['a', 'b', 'c', 'd'];
let pulled = pullAtValue(myArray, ['b', 'd']); // myArray = [ 'a', 'c' ] , pulled = [ 'b', 'd' ]
```

</details>

<br>[⬆ 返回顶部](#contents)

### pullBy ![advanced](/advanced.svg)
根据给定的迭代器函数，对原始数组进行变换以过滤掉指定的值。

检查函数中是否提供了最后一个参数。
使用`Array.prototype.map()`将迭代器函数`fn`应用于所有数组元素。
使用`Array.prototype.filter()`和`Array.prototype.includes()`来提取不需要的值。
使用`Array.prototype.length = 0`来改变传入的数组，方法是将它的长度重置为零，并使用`Array.prototype.push()`重新填充它，只使用过滤后的值。

```js
const pullBy = (arr, ...args) => {
  const length = args.length;
  let fn = length > 1 ? args[length - 1] : undefined;
  fn = typeof fn == 'function' ? (args.pop(), fn) : undefined;
  let argState = (Array.isArray(args[0]) ? args[0] : args).map(val => fn(val));
  let pulled = arr.filter((v, i) => !argState.includes(fn(v)));
  arr.length = 0;
  pulled.forEach(v => arr.push(v));
};
```

<details>
<summary>Examples</summary>

```js
var myArray = [{ x: 1 }, { x: 2 }, { x: 3 }, { x: 1 }];
pullBy(myArray, [{ x: 1 }, { x: 3 }], o => o.x); // myArray = [{ x: 2 }]
```

</details>

<br>[⬆ 返回顶部](#contents)

### reducedFilter

根据条件过滤对象数组，同时过滤掉未指定的键。

使用`Array.prototype.filter()`根据谓词`fn`过滤数组，以便返回条件返回truthy值的对象。
在过滤的数组上，使用`Array.prototype.map()`使用`Array.prototype.reduce()`返回新对象，以过滤掉未作为`keys`参数提供的键。

```js
const reducedFilter = (data, keys, fn) =>
  data.filter(fn).map(el =>
    keys.reduce((acc, key) => {
      acc[key] = el[key];
      return acc;
    }, {})
  );
```

<details>
<summary>Examples</summary>

```js
const data = [
  {
    id: 1,
    name: 'john',
    age: 24
  },
  {
    id: 2,
    name: 'mike',
    age: 50
  }
];

reducedFilter(data, ['id', 'name'], item => item.age > 24); // [{ id: 2, name: 'mike'}]
```

</details>

<br>[⬆ 返回顶部](#contents)

### reduceSuccessive

对累加器和数组中的每个元素（从左到右）应用函数，返回连续减少的值的数组。

使用`Array.prototype.reduce()`将给定函数应用于给定数组，存储每个新结果。

```js
const reduceSuccessive = (arr, fn, acc) =>
  arr.reduce((res, val, i, arr) => (res.push(fn(res.slice(-1)[0], val, i, arr)), res), [acc]);
```

<details>
<summary>Examples</summary>

```js
reduceSuccessive([1, 2, 3, 4, 5, 6], (acc, val) => acc + val, 0); // [0, 1, 3, 6, 10, 15, 21]
```

</details>

<br>[⬆ 返回顶部](#contents)

### reduceWhich

在应用提供的函数设置比较规则后，返回数组的最小/最大值。

将`Array.prototype.reduce()`与`comparator`函数结合使用，可以得到数组中的相应元素。
您可以省略第二个参数`comparator`，以使用返回数组中最小元素的默认参数。

```js
const reduceWhich = (arr, comparator = (a, b) => a - b) =>
  arr.reduce((a, b) => (comparator(a, b) >= 0 ? b : a));
```

<details>
<summary>Examples</summary>

```js
reduceWhich([1, 3, 2]); // 1
reduceWhich([1, 3, 2], (a, b) => b - a); // 3
reduceWhich(
  [{ name: 'Tom', age: 12 }, { name: 'Jack', age: 18 }, { name: 'Lucy', age: 9 }],
  (a, b) => a.age - b.age
); // {name: "Lucy", age: 9}
```

</details>

<br>[⬆ 返回顶部](#contents)

<!-- 2019年8月12日 21:44:18 -->
### reject

传入断言函数和数组，使用`Array.prototype.filter()`,如果`pred(x) === false`则保留`x`。

```js
const reject = (pred, array) => array.filter((...args) => !pred(...args));
```

<details>
<summary>Examples</summary>

```js
reject(x => x % 2 === 0, [1, 2, 3, 4, 5]); // [1, 3, 5]
reject(word => word.length > 4, ['Apple', 'Pear', 'Kiwi', 'Banana']); // ['Pear', 'Kiwi']
```

</details>

<br>[⬆ 返回顶部](#contents)

### remove

Removes elements from an array for which the given function returns `false`.

Use `Array.prototype.filter()` to find array elements that return truthy values and `Array.prototype.reduce()` to remove elements using `Array.prototype.splice()`.
The `func` is invoked with three arguments (`value, index, array`).

从数组中移除给定函数返回false的元素. 使用`Array.filter()`查找返回 `truthy` 值的数组元素和`Array.reduce()`以使用`Array.splice()`删除元素。使用三参数 `func(value, index, array)`调用函数.。

```js
const remove = (arr, func) =>
  Array.isArray(arr)
    ? arr.filter(func).reduce((acc, val) => {
      arr.splice(arr.indexOf(val), 1);
      return acc.concat(val);
    }, [])
    : [];
```

<details>
<summary>Examples</summary>

```js
remove([1, 2, 3, 4], n => n % 2 === 0); // [2, 4]
```

</details>

<br>[⬆ 返回顶部](#contents)

### sample

从数组中返回一个随机元素。

使用`Math.random()`生成一个随机数，乘以`length`并使用`Math.floor()`将其四舍五入到最接近的整数。
此方法也适用于字符串。

```js
const sample = arr => arr[Math.floor(Math.random() * arr.length)];
```

<details>
<summary>Examples</summary>

```js
sample([3, 7, 9, 11]); // 9
```

</details>

<br>[⬆ 返回顶部](#contents)

### sampleSize
从`array`获取唯一键的`n`随机元素，最大为`array`的`length`。

使用[Fisher-Yates算法](https://github.com/30-seconds/30-seconds-of-code#shuffle)对阵列进行混洗。
使用`Array.prototype.slice()`来获取第一个`n`元素。
省略第二个参数，`n`从数组中只获取一个随机元素。

```js
const sampleSize = ([...arr], n = 1) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr.slice(0, n);
};
```

<details>
<summary>Examples</summary>

```js
sampleSize([1, 2, 3], 2); // [3,1]
sampleSize([1, 2, 3], 4); // [2,3,1]
```

</details>

<br>[⬆ 返回顶部](#contents)

### shank
具有与[`Array.prototype.splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splic)相同的功能，但返回一个新的 数组而不是改变原始数组。

在删除现有元素和/或添加新元素后，使用`Array.prototype.slice（）`和`Array.prototype.concat（）`获取包含新内容的新数组。
省略第二个参数`index`，从'0'开始。
省略第三个参数`delCount`，删除`0`元素。
省略第四个参数`elements`，以便不添加任何新元素。

```js
const shank = (arr, index = 0, delCount = 0, ...elements) =>
  arr
    .slice(0, index)
    .concat(elements)
    .concat(arr.slice(index + delCount));
```

<details>
<summary>Examples</summary>

```js
const names = ['alpha', 'bravo', 'charlie'];
const namesAndDelta = shank(names, 1, 0, 'delta'); // [ 'alpha', 'delta', 'bravo', 'charlie' ]
const namesNoBravo = shank(names, 1, 1); // [ 'alpha', 'charlie' ]
console.log(names); // ['alpha', 'bravo', 'charlie']
```

</details>

<br>[⬆ 返回顶部](#contents)

### shuffle

随机化数组值的顺序，返回一个新数组。

使用[Fisher-Yates算法](https://github.com/30-seconds/30-seconds-of-code#shuffle)重新排序数组的元素。

```js
const shuffle = ([...arr]) => {
  let m = arr.length;
  while (m) {
    const i = Math.floor(Math.random() * m--);
    [arr[m], arr[i]] = [arr[i], arr[m]];
  }
  return arr;
};
```

<details>
<summary>Examples</summary>

```js
const foo = [1, 2, 3];
shuffle(foo); // [2, 3, 1], foo = [1, 2, 3]
```

</details>

<br>[⬆ 返回顶部](#contents)

### similarity

返回两个数组中出现的相同元素的数组，也可以说是两个数组的交集。

使用`Array.prototype.filter（）`删除不属于`values`的值，使用`Array.prototype.includes（）`确定。

```js
const similarity = (arr, values) => arr.filter(v => values.includes(v));
```

<details>
<summary>Examples</summary>

```js
similarity([1, 2, 3], [1, 2, 4]); // [1, 2]
```

</details>

<br>[⬆ 返回顶部](#contents)

### sortedIndex

返回应将值插入数组的最低索引，以便维护其排序顺序。

检查数组是否按降序排序（松散）。
使用`Array.prototype.findIndex（）`来查找应该插入元素的适当索引。

```js
const sortedIndex = (arr, n) => {
  const isDescending = arr[0] > arr[arr.length - 1];
  const index = arr.findIndex(el => (isDescending ? n >= el : n <= el));
  return index === -1 ? arr.length : index;
};
```

<details>
<summary>Examples</summary>

```js
sortedIndex([5, 3, 2, 1], 4); // 1
sortedIndex([30, 50], 40); // 1
```

</details>

<br>[⬆ 返回顶部](#contents)

### sortedIndexBy

返回应将值插入数组的最低索引，以便根据提供的迭代器函数维护其排序顺序。

检查数组是否按降序排序（松散）。
使用`Array.prototype.findIndex（）`根据迭代器函数`fn`找到应该插入元素的适当索引。

```js
const sortedIndexBy = (arr, n, fn) => {
  const isDescending = fn(arr[0]) > fn(arr[arr.length - 1]);
  const val = fn(n);
  const index = arr.findIndex(el => (isDescending ? val >= fn(el) : val <= fn(el)));
  return index === -1 ? arr.length : index;
};
```

<details>
<summary>Examples</summary>

```js
sortedIndexBy([{ x: 4 }, { x: 5 }], { x: 4 }, o => o.x); // 0
```

</details>

<br>[⬆ 返回顶部](#contents)

### sortedLastIndex

返回应将值插入数组的最高索引，以便维护其排序顺序。

检查数组是否按降序排序（松散）。
使用`Array.prototype.reverse（）`和`Array.prototype.findIndex（）`来查找应该插入元素的最后一个索引。

```js
const sortedLastIndex = (arr, n) => {
  const isDescending = arr[0] > arr[arr.length - 1];
  const index = arr.reverse().findIndex(el => (isDescending ? n <= el : n >= el));
  return index === -1 ? 0 : arr.length - index;
};
```

<details>
<summary>Examples</summary>

```js
sortedLastIndex([10, 20, 30, 30, 40], 30); // 4
```

</details>

<br>[⬆ 返回顶部](#contents)








