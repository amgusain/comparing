
# comparing  <a href="https://www.github.com/JanMalch/comparing"><img src="https://user-images.githubusercontent.com/25508038/63974103-75242700-caac-11e9-8ca4-71cc5b905e90.png" width="90" height="90" align="right"></a>  
  
[![Docs](https://img.shields.io/badge/completed--docs-true-brightgreen)][docs-url] [![npm](https://badge.fury.io/js/comparing.svg)][npm-url] [![Travis-CI](https://travis-ci.org/JanMalch/comparing.svg?branch=master)][build-url] 
[![codecov](https://codecov.io/gh/JanMalch/comparing/branch/master/graph/badge.svg)][codecov-url]
  
<i>Easily create descriptive comparators.</i>    
  
## Features  
  
- predefined Comparators for common use-cases  
- easily sort arrays of objects via [`Comparators.with`](http://janmalch.github.io/comparing/classes/comparators.html#with)  
- easily combine predefined and custom Comparators  
- chain or reverse your own custom Comparators  
- single [`Comparators` class](http://janmalch.github.io/comparing/classes/comparators.html#bylength) as a common namespace  
- lightweight, only ~500 bytes gzipped  
- ...  
  
Make sure to checkout the [complete docs][docs-url].   
  
[![Docs](https://img.shields.io/badge/docs%20coverage-100%25-brightgreen)][docs-url]  
  
## Installation & Usage  
  
```bash  
npm i comparing  
```  
  
Core functionality is contained in the [`Comparators` class](http://janmalch.github.io/comparing/classes/comparators.html#bylength).  
  
```typescript  
import { Comparators, CompareFunction, Comparator } from 'comparing';  
  
// chose from various available Comparators  
const simple = [4, 1, 3, 5].sort(Comparators.naturalOrder);
expect(simple).toEqual([1, 3, 4, 5]);  
  
// start with your own simple function  
const myCompareFn: CompareFunction<string> = (a, b) => a.charCodeAt(0) - b.charCodeAt(0);  
// add `reversed` and `then` to any function with Comparators.of  
const complex: Comparator<string> = Comparators.of(myCompareFn)  
  .reversed() // reverse any Comparator 
  .then( // compare by a certain field or other values via `Comparators.with` 
    Comparators.with(x => x.charAt(1), Comparators.ignoreCase)
  );
const result = ['aB', 'bB', 'aa'].sort(complex);  
expect(result).toEqual(['bB', 'aa', 'aB']);  
```  
  
[docs-url]: https://janmalch.github.io/comparing/  
[npm-url]: https://www.npmjs.com/package/comparing  
[build-url]: https://travis-ci.org/JanMalch/comparing  
[codecov-url]:https://codecov.io/gh/JanMalch/comparing
