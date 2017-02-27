---
title: Guide
type: v0.2.2
order: 1
---

About
-----

This module provides a simple and flexible way to create [data-driven tests](https://booker.codes/data-driven-tests-in-javascript-using-mocha/) in JavaScript. It works with [mocha](https://mochajs.org/), [jasmine](https://jasmine.github.io/), and [jest](https://facebook.github.io/jest/).

Check out [sazerac-example](http://github.com/mikec/sazerac-example) or read on.


Getting Started
---------------

Install Sazerac as an npm module and save it to your `package.json` file as a development dependency:

```js
npm install sazerac --save-dev
```

Import the `test` and `given` helper functions into your project:

```js
import { test, given } from 'sazerac'
```


Why Use This?
-------------

Let's say you have a function `isPrime()`. When given a number, it returns `true` or `false` depending on whether the number is a prime number.

```js
function isPrime(num) {
  for(var i = 2; i < num; i++) {
    if(num % i === 0) return false;
  }
  return num > 1;
}
```

If you're using a framework like [jasmine](https://jasmine.github.io/), your tests might look something like this:

```js
describe('isPrime()', () => {

  describe('when given 2', () => {
    it('should return true', () => {
      assert.isTrue(isPrime(2))
    })
  })

  describe('when given 3', () => {
    it('should return true', () => {
      assert.isTrue(isPrime(3))
    })
  })

  describe('when given 4', () => {
    it('should return false', () => {
      assert.isFalse(isPrime(4))
    })
  })

  // and more ...

})
```

It's a lot of code to write for only 3 test cases and such a basic function!

The same tests can be defined with Sazerac as follows:

```js
test(isPrime, () => {
  given(2).expect(true)
  given(3).expect(true)
  given(4).expect(false)
})
```

Sazerac runs the `describe` and `it` functions needed for these test cases. It adds reporting messages in a consistent format based on the input and output parameters. For this example, the test report ends up looking like this:

```
isPrime()
  when given 2
    ✓ should return true
  when given 3
    ✓ should return true
  when given 4
    ✓ should return false
```
