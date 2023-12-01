<!--

@license Apache-2.0

Copyright (c) 2018 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# isPrototypeOf

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Test if an object's prototype chain contains a provided prototype.

<section class="intro">

</section>

<!-- /.intro -->

<section class="installation">

## Installation

```bash
npm install @stdlib/assert-is-prototype-of
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm` branch][esm-url].
-   If you are using Deno, visit the [`deno` branch][deno-url].
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd` branch][umd-url].

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

</section>

<section class="usage">

## Usage

<!-- eslint-disable stdlib/no-redeclare -->

```javascript
var isPrototypeOf = require( '@stdlib/assert-is-prototype-of' );
```

#### isPrototypeOf( obj, prototype )

Tests if an `object`'s prototype chain contains a provided `prototype`.

<!-- eslint-disable stdlib/no-redeclare -->

```javascript
var inherit = require( '@stdlib/utils-inherit' );

function Foo() {
    return this;
}

function Bar() {
    return this;
}
inherit( Bar, Foo );

var bar = new Bar();

var bool = isPrototypeOf( bar, Foo.prototype );
// returns true
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The function returns `false` if provided a primitive value.

    <!-- eslint-disable stdlib/no-redeclare -->

    ```javascript
    var Number = require( '@stdlib/number-ctor' );

    var bool = isPrototypeOf( 5, Number.prototype );
    // returns false

    bool = isPrototypeOf( 'beep', String.prototype );
    // returns false

    bool = isPrototypeOf( true, Boolean.prototype );
    // returns false
    ```

-   The function throws a `TypeError` if provided a `prototype` value which is neither an `object` (except `null`) or a `function`.

    <!-- eslint-disable stdlib/no-redeclare -->

    ```javascript
    var bool = isPrototypeOf( Object.create( null ), null );
    // throws <TypeError>
    ```

-   `isPrototypeOf()` is generally more robust than the `instanceof` operator. Consider the following example which does not use constructors:

    <!-- eslint-disable stdlib/no-redeclare -->

    ```javascript
    // Functionally similar to `Object.create()`...
    function createObject( proto ) {
        function Ctor() {
            // Empty constructor...
        }
        Ctor.prototype = proto;
        return new Ctor();
    }
    var superProto = {
        'beep': 'beep'
    };

    var subProto = createObject( superProto );
    subProto.boop = 'boop';

    var v = createObject( subProto );

    var bool;
    try {
        bool = ( v instanceof superProto );
    } catch ( error ) {
        // Encountered a type error...
        console.error( error.message );
    }

    bool = isPrototypeOf( v, superProto );
    // returns true
    ```

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint-disable stdlib/no-redeclare -->

<!-- eslint no-undef: "error" -->

```javascript
var inherit = require( '@stdlib/utils-inherit' );
var isPrototypeOf = require( '@stdlib/assert-is-prototype-of' );

function A() {
    return this;
}

function B() {
    return this;
}
inherit( B, A );

function C() {
    return this;
}
inherit( C, B );

function D() {
    return this;
}
inherit( D, C );

var a = new A();
var b = new B();
var c = new C();
var d = new D();

var bool = isPrototypeOf( d, C.prototype );
// returns true

bool = isPrototypeOf( d, B.prototype );
// returns true

bool = isPrototypeOf( d, A.prototype );
// returns true

bool = isPrototypeOf( c, B.prototype );
// returns true

bool = isPrototypeOf( c, A.prototype );
// returns true

bool = isPrototypeOf( c, D.prototype );
// returns false

bool = isPrototypeOf( b, A.prototype );
// returns true

bool = isPrototypeOf( b, C.prototype );
// returns false

bool = isPrototypeOf( b, D.prototype );
// returns false

bool = isPrototypeOf( a, B.prototype );
// returns false

bool = isPrototypeOf( a, C.prototype );
// returns false

bool = isPrototypeOf( a, D.prototype );
// returns false
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/utils-get-prototype-of`][@stdlib/utils/get-prototype-of]</span><span class="delimiter">: </span><span class="description">return the prototype of a provided object.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2023. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/assert-is-prototype-of.svg
[npm-url]: https://npmjs.org/package/@stdlib/assert-is-prototype-of

[test-image]: https://github.com/stdlib-js/assert-is-prototype-of/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/assert-is-prototype-of/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/assert-is-prototype-of/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/assert-is-prototype-of?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/assert-is-prototype-of.svg
[dependencies-url]: https://david-dm.org/stdlib-js/assert-is-prototype-of/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/assert-is-prototype-of/tree/deno
[umd-url]: https://github.com/stdlib-js/assert-is-prototype-of/tree/umd
[esm-url]: https://github.com/stdlib-js/assert-is-prototype-of/tree/esm
[branches-url]: https://github.com/stdlib-js/assert-is-prototype-of/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/assert-is-prototype-of/main/LICENSE

<!-- <related-links> -->

[@stdlib/utils/get-prototype-of]: https://github.com/stdlib-js/utils-get-prototype-of

<!-- </related-links> -->

</section>

<!-- /.links -->
