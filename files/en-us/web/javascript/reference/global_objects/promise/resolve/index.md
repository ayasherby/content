---
title: Promise.resolve()
slug: Web/JavaScript/Reference/Global_Objects/Promise/resolve
tags:
  - ECMAScript 2015
  - JavaScript
  - Method
  - Promise
  - Reference
browser-compat: javascript.builtins.Promise.resolve
---
{{JSRef}}

The **`Promise.resolve()`** method returns a
{{jsxref("Promise")}} object that is resolved with a given value. If the value is a
promise, that promise is returned; if the value is a thenable (i.e. has a
{{jsxref("Promise.then", "\"then\" method")}}), the returned promise will "follow" that
thenable, adopting its eventual state; otherwise the returned promise will be fulfilled
with the value. This function flattens nested layers of promise-like objects (e.g. a
promise that resolves to a promise that resolves to something) into a single layer.

## Syntax

```js
Promise.resolve(value);
```

### Parameters

- `value`
  - : Argument to be resolved by this `Promise`. Can also be a
    `Promise` or a thenable to resolve.

### Return value

A {{jsxref("Promise")}} that is resolved with the given value, or the promise passed as
value, if the value was a promise object.

## Description

The static `Promise.resolve` function returns a `Promise` that is
resolved.

## Examples

### Using the static Promise.resolve method

```js
Promise.resolve('Success').then(function(value) {
  console.log(value); // "Success"
}, function(value) {
  // not called
});
```

### Resolving an array

```js
const p = Promise.resolve([1,2,3]);
p.then(function(v) {
  console.log(v[0]); // 1
});
```

### Resolving another Promise

```js
const original = Promise.resolve(33);
const cast = Promise.resolve(original);
cast.then(function(value) {
  console.log('value: ' + value);
});
console.log('original === cast ? ' + (original === cast));

// logs, in order:
// original === cast ? true
// value: 33
```

The inverted order of the logs is due to the fact that the `then` handlers
are called asynchronously. See how `then` works [here](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then#return_value).

### Resolving thenables and throwing Errors

```js
// Resolving a thenable object
const p1 = Promise.resolve({
  then: function(onFulfill, onReject) { onFulfill('fulfilled!'); }
});
console.log(p1 instanceof Promise) // true, object casted to a Promise

p1.then(function(v) {
    console.log(v); // "fulfilled!"
  }, function(e) {
    // not called
});

// Thenable throws before callback
// Promise rejects
const thenable = { then: function(resolve) {
  throw new TypeError('Throwing');
  resolve('Resolving');
}};

const p2 = Promise.resolve(thenable);
p2.then(function(v) {
  // not called
}, function(e) {
  console.error(e); // TypeError: Throwing
});

// Thenable throws after callback
// Promise resolves
const thenable = { then: function(resolve) {
  resolve('Resolving');
  throw new TypeError('Throwing');
}};

const p3 = Promise.resolve(thenable);
p3.then(function(v) {
  console.log(v); // "Resolving"
}, function(e) {
  // not called
});
```

> **Warning:** Do not call `Promise.resolve()` on a thenable that resolves to itself. That leads to infinite recursion, because it attempts to flatten an infinitely-nested promise.

```js example-bad
let thenable = {
  then: (resolve, reject) => {
    resolve(thenable)
  }
}

Promise.resolve(thenable)  // Will lead to infinite recursion.
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Promise")}}
