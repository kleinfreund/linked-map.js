# reverse-iterable-map

The `ReverseIterableMap` object is a reverse-iterable map implementation based on the built-in [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) object.

It implements a linked list meaning that each element in the internal data structure (a `Map` object) knows about its previous and next element; thus, allowing iteration in both directions *at the same time*. This implies added memory usage because in addition to its key and value, an element also needs to store the two references for the previous and next elements.

Links:

- [**npmjs.com**/package/reverse-iterable-map](https://www.npmjs.com/package/reverse-iterable-map)
- [**github.com**/kleinfreund/reverse-iterable-map](https://github.com/kleinfreund/reverse-iterable-map)

See also:

- `ReverseIterableArray`: [reverse-iterable-array](https://www.npmjs.com/package/reverse-iterable-array)
- `ReverseIterableSet`: [reverse-iterable-set](https://www.npmjs.com/package/reverse-iterable-set)



## Table of Contents

* [Install](#install)
  * [ES Module](#es-module)
  * [Node.js package](#nodejs-package)
* [Usage](#usage)
* [Tests](#tests)
* [Documentation](#documentation)
  * [Constructor](#constructor)
  * [`size`](#size)
  * [`clear()`](#clear)
  * [`delete()`](#delete)
  * [`entries()`](#entries)
  * [`forEach()`](#foreach)
  * [`forEachReverse()`](#foreachreverse)
  * [`get()`](#get)
  * [`has()`](#has)
  * [`iteratorFor()`](#iteratorfor)
  * [`keys()`](#keys)
  * [`reverseIterator()`](#reverseiterator)
  * [`set()`](#set)
  * [`setFirst()`](#setfirst)
  * [`[Symbol.iterator]()`](#symboliterator)
  * [`values()`](#values)
* [Why this was implemented](#why-this-was-implemented)
* [How to update this package](#how-to-update-this-package)



## Install

### ES Module

Download only the ES module file:

```shell
curl -O https://raw.githubusercontent.com/kleinfreund/reverse-iterable-map/main/src/reverse-iterable-map.mjs
```

### Node.js package

*(Requires Node version 8.5 or higher for ES module support)*

Installs the node package as a dependency. It doesn’t have any dependencies itself.

```shell
npm install --save reverse-iterable-map
```

Note, that Node.js version 8.5 or higher is required, as it comes with experimental support for ES modules. If you don’t want to use it as an ES module, you will need to transpile the package yourself.

## Usage

```js
import { ReverseIterableMap } from './src/reverse-iterable-map.mjs';

const map = new ReverseIterableMap();
```

For more usage examples, clone the repository and run:

```shell
npm install && npm run examples
```

Then, open `http://127.0.0.1:8080/examples` in your browser.



## Tests

**… with Node’s experimental ES module feature**:

```shell
npm test
```



## Documentation

**Disclaimer**: The documentation section copies a lot of content from the [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) documentation on the Mozilla Developer Network.

A `ReverseIterableMap` object iterates its elements in insertion or reverse-insertion order — a [`for...of`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) loop returns an array of `[key, value]` for each iteration.



### Constructor

#### Syntax

```
new ReverseIterableMap([iterable])
```

**Parameters**:

* `iterable`: An [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) object whose elements are key-value pairs.

  In order to construct a `ReverseIterableMap` object from an array, it can be passed by calling the [`Array.prototype.entries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries) method.

  ```js
  const map = new ReverseIterableMap([1, 2, 3].entries());
  ```

#### Usage

```js
const map = new ReverseIterableMap();
```

##### `Array`

```js
const map = new ReverseIterableMap([1, 2, 3].entries());
```

##### `Array` of `Array`s

```js
const map = new ReverseIterableMap([[0, 1], [1, 2], [2, 3]]);
```

##### `Map`

```js
const builtInMap = new Map([['key1', 1], ['key2', 2], ['key3', 3]]);
const map = new ReverseIterableMap(builtInMap);
```

##### `NodeList`

```js
const nodeList = document.querySelectorAll('a');
const map = new ReverseIterableMap(nodeList.entries());
```



### `size`

The `size` accessor property returns the number of elements in a `ReverseIterableMap` object.

#### Syntax

```
map.size
```

#### Usage

```js
const map = new ReverseIterableMap();

map
  .set('one', 'I')
  .set('two', 'lack')
  .set('three', 'creativity');

map.size
//> 3
```




### `clear()`

#### Syntax

```
map.clear();
```

**Return value**:

[`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined).

#### Usage

```js
// Clears the underlying Map object
// Sets the first and last node references to null
map.clear();
```



### `delete()`

#### Syntax

```
map.delete(key);
```

**Parameters**:

* **key**: Required. The key of the element to remove from the `ReverseIterableMap` object.

**Return value**:

* **Boolean**: Returns `true` if an element in the `ReverseIterableMap` object existed and has been removed, or `false` if the element does not exist.

#### Usage

```js
const map = new ReverseIterableMap(['hey', 'beauty'].entries());

map.delete(0);
//> true (deletes the key value pair [0, 'hey'])

map.delete(1);
//> true (deletes the key value pair [1, 'beauty'])

map.delete(2);
//> false (key 2 does not exist in map)
```



### `entries()`

Returns an iterator containing the `[key, value]` pairs for each element in the `ReverseIterableMap` object in insertion order.

An iterator containing the same pairs in reverse-insertion order can be obtained with `entries().reverseIterator()`.

#### Syntax

```
map.entries();
```

**Return value**:

A new `ReverseIterableMap` iterator object.



### `forEach()`

The `forEach()` method executes a provided function once per each `[key, value]` pair in the `ReverseIterableMap` object, in insertion order.

#### Syntax

```
map.forEach(callback[, thisArg]);
```

**Parameters**:

* **callback**: Function to execute for each element.
* **thisArg**: Value to use as `this` when executing `callback`.

**Return value**:

[`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined).



### `forEachReverse()`

The `forEachReverse()` method executes a provided function once per each `[key, value]` pair in the `ReverseIterableMap` object, in reverse-insertion order.

#### Syntax

```
map.forEachReverse(callback[, thisArg]);
```

**Parameters**:

* **callback**: Function to execute for each element.
* **thisArg**: Value to use as `this` when executing `callback`.

**Return value**:

[`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined).



### `get()`

#### Syntax

```
map.get(key);
```

**Parameters**:

* **key**: Required. The key of the element to return from the `ReverseIterableMap` object.

**Return value**:

* Returns the element associated with the specified key or `undefined` if the key can't be found in the `ReverseIterableMap` object.

#### Usage

```js
const map = new ReverseIterableMap(['hey', 'beauty'].entries());

map.get(0);
//> 'hey'

map.get(1);
//> 'beauty'

map.get(2);
//> undefined
```



### `has()`

#### Syntax

```
map.has(key);
```

**Parameters**:

* **key**: Required. The key of the element to test for presence in the `ReverseIterableMap` object.

**Return value**:

* **Boolean**: Returns `true` if an element with the specified key exists in the `ReverseIterableMap` object; otherwise `false`.

#### Usage

```js
const map = new ReverseIterableMap(['hey', 'beauty'].entries());

map.has(0);
//> true

map.has(1);
//> true

map.has(2);
//> false
```



### `iteratorFor()`

Returns an iterator containing the `[key, value]` pairs for each element in the `ReverseIterableMap` object in insertion order **starting with the pair specified by the `key` parameter**.

This allows starting iteration at a specific element in the map.

An iterator containing the same pairs in reverse-insertion order can be obtained with `iteratorFor().reverseIterator()`.

#### Syntax

```
map.iteratorFor(key);
```

**Parameters**:

* **key**: Required. The key of the element to start iterating from.

**Return value**:

A new `ReverseIterableMap` iterator object.

#### Usage

```js
const map = new ReverseIterableMap([1, 2, 4].entries());

// Iterator, starting at the element with key 1.
const iterator = map.iteratorFor(1);

iterator.next().value;
//> [1, 2]

iterator.next().value;
//> [2, 4]

iterator.next().value;
//> undefined

// Reverse-iterator, starting at the element with key 1.
const reverseIterator = map.iteratorFor(1).reverseIterator();

reverseIterator.next().value;
//> [1, 2]

reverseIterator.next().value;
//> [0, 1]

reverseIterator.next().value;
//> undefined
```



### `keys()`

Returns an iterator containing the keys for each element in the `ReverseIterableMap` object in insertion order.

An iterator containing the same keys in reverse-insertion order can be obtained with `keys().reverseIterator()`.

#### Syntax

```
map.keys();
```

**Return value**:

A new `ReverseIterableMap` iterator object.



### `reverseIterator()`

In theory, following the semantics of `[Symbol.iterator]()`, this should be `[Symbol.reverseIterator]()`. However, as a developer, I cannot define a well-known symbol myself and make use of it. In the future, the a proposal like [The ReverseIterable Interface, by Lee Byron](https://github.com/leebyron/ecmascript-reverse-iterable) might make it’s way into the specification. For the time being, the `reverseIterator()` function serves the same purpose.

#### Syntax

```
map.reverseIterator();
```

**Return value**:

The map **reverse-iterator** function, which is the `entries().reverseIterator()` function by default.

#### Usage

```js
const map = new ReverseIterableMap([1, 2, 4].entries());

const reverseIterator = map.reverseIterator();

reverseIterator.next().value;
//> [2, 4]

reverseIterator.next().value;
//> [1, 2]

reverseIterator.next().value;
//> [0, 1]

reverseIterator.next().value;
//> undefined
```



### `set()`

#### Syntax

```
map.set(key, value);
```

**Parameters**:

* **key**: Required. The key of the element to add to the `ReverseIterableMap` object.
* **value**: Required. The value of the element to add to the `ReverseIterableMap` object.

**Return value**:

* The `ReverseIterableMap` object.

#### Usage

```js
const map = new ReverseIterableMap();

map.set('you', 'beauty');
//> map

map.set('the-magic-key', 'hey');
//> map
```

The `set()` method returns a reference to the map object. This makes the set operation chainable.

```js
const map = new ReverseIterableMap()
  .set('key', '… is spelled like tea')
  .set('hey', '… somehow ney');
```



### `setFirst()`

The `setFirst()` method functions like `set()` but uses reverse-insertion order.

#### Syntax

```
map.set(key, value);
```

**Parameters**:

* **key**: Required. The key of the element to add to the `ReverseIterableMap` object.
* **value**: Required. The value of the element to add to the `ReverseIterableMap` object.

**Return value**:

* The `ReverseIterableMap` object.

#### Usage

```js
const map = new ReverseIterableMap()
  .setFirst('key1', 'was inserted first')
  .setFirst('key2', 'was inserted last');

map.values().next().value;
//> 'was inserted last'

map.values().reverseIterator().next().value;
//> 'was inserted first'
```



### `[Symbol.iterator]()`

Returns the map iterator function. By default, this is the `entries()` function.

#### Syntax

```
map[Symbol.iterator]();
```

**Return value**:

The map **iterator** function, which is the `entries()` function by default.

#### Usage

```js
const map = new ReverseIterableMap([1, 2, 4].entries());

const iterator = map[Symbol.iterator]();

iterator.next().value;
//> [0, 1]

iterator.next().value;
//> [1, 2]

iterator.next().value;
//> [2, 4]

iterator.next().value;
//> undefined
```



### `values()`

Returns an iterator containing the values for each element in the `ReverseIterableMap` object in insertion order.

An iterator containing the same values in reverse-insertion order can be obtained with `values().reverseIterator()`.

#### Syntax

```
map.values();
```

**Return value**:

A new `ReverseIterableMap` iterator object.



## Why this was implemented

Part of the additions to ECMAScript 2015 are the [iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols): [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) and [iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol). The former allows arbitrary objects to become iterable. Following the rules of the protocol gives one iteration capabilities via the following techniques:

* [`for...of` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
* [`Array.from()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
* [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

**However**, only the iteration in one direction is considered by the [specification](https://www.ecma-international.org/ecma-262/6.0/#sec-iteration) at the time. This means that we only get forward-iteration by default. There is a draft for a proposal to add a `ReverseIterable` interface to the specification: [“The ReverseIterable Interface” by Lee Byron](https://github.com/leebyron/ecmascript-reverse-iterable).

Now, with the iteration protocols, we could redefine the iteration behavior for our purpose and make an object backwards-iterable. At the same time, this means losing the ability to iterate forwards.

**If you need both a forwards- and backwards-iterable object, this implementation might be for you.**

**But why a map?**

That’s what I needed. To be precise, I needed to access an iterator _at a specific location_ in my data structure and be able to _iterate in both directions_.

I tried to stick to the [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) interface as close as possible.

Implementing a reverse-iterable array, for example, can be accomplished by using the same techniques of this implementation.

## How to update this package

… because I keep forgetting that.

Let’s assume a *minor* update was made. First of all, the working directory needs to cleaned up; all changes need to be comitted and pushed.

```shell
git add .
git commit -m "Implemented extremely nice feature"
git push
```

Next, make sure you have a valid NPM authentication token set up:

```shell
npm whoami
```

If not, do that with `npm login` and continue. We now create a new commit with the next *minor* version tag and update the package.json. Actually, the following command will do that:

```shell
npm version minor # See `npm version --help` for more options
```

This creates a new git tag that we need to publish as well. With that, we can now publish the new version.

```shell
git push --tags
npm publish
```

That’s it.
