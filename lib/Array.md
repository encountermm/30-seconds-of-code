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

使用`Array.prototype.reduce（）`和`Array.prototype.push（）`根据`fn`为每个元素返回的值向组添加元素。

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

使用`Array.prototype.slice（）`从左侧删除指定数量的元素。

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

使用`Array.prototype.slice（）`从右侧删除指定数量的元素。

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

循环遍历数组，使用`Array.prototype.slice（）`删除数组的最后一个元素，直到函数返回的值为`true`,返回剩余的元素。

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

循环遍历数组，使用`Array.prototype.slice（）`删除数组的第一个元素，直到函数返回的值为`true`，返回剩余的元素。

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


使用`Array.prototype.filter（）`创建一个包含给定数组中序号为n的倍数的所有元素的新数组。

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

使用`Array.prototype.filter（）`创建一个只包含真值`true`的新数组。

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

使用`Array.prototype.filter（）`创建一个只包含唯一值的新数组。

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

使用`Array.prototype.filter（）`和`Array.prototype.every（）`基于比较器函数`fn`创建一个只包含唯一值的数组。

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

使用`Array.prototype.filter（）`删除`fn`返回falsy值的元素，'Array.prototype.pop（）`来获取最后一个元素。

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

使用`Array.prototype.map（）`将每个元素映射到具有索引和值的数组。

使用`Array.prototype.filter（）`删除`fn`返回falsy值的元素，'Array.prototype.pop（）`来获取最后一个。

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

使用递归，每个深度级别将“深度”递减1。使用`Array.prototype.reduce（）`和`Array.prototype.concat（）`来合并元素或数组。

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

使用`Array.prototype.slice（0）`来克隆给定的数组，使用`Array.prototype.reverse（）`来反转它，使用`Array.prototype.forEach（）`迭代反转的数组。

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

使用`Array.prototype.map（）`将数组的值映射到函数或属性名称。
使用`Array.prototype.reduce（）`创建一个对象，其中的键是从映射的结果中生成的。

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

