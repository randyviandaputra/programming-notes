# Penulisan Kode ES6 & Pengenalan Fitur

ECMAScript 2015, atau dikenal sebagai ES6, memperkenalkan banyak perubahan pada
JavaScript. Berikut adalah gambaran dari beberapa fitur yang paling umum dan
perbedaan pada penulisannya dengan membandingkan dengan penulisan ES5.

## Daftar Isi

- [Deklarasi Variabel](#variabel)
- [Deklarasi Konstanta](#konstanta)
- [Penulisan Arrow function](#arrow-function)
- [Template literals](#template-literal)
- [Penulisan singkat Key/property](#key-property)
- [Penulisan singkat definisi Method](#method-definition)
- [Destructuring (object matching)](#destructuring)
- [Array iteration (looping)](#iteration)
- [Paramenter Default](#parameter-default)
- [Penulisan Spread](#spread)
- [Classes/constructor functions](#class)
- [Inheritance](#inheritance)
- [Modules - export/import](#modules)
- [Promises/callbacks](#promise-callback)

## Variables dan constant perbandingan fitur

Saya menjelaskan konsep, ruang lingkup dan perbedaan antara `let`,`var`, dan
`const` dari artikel
[Understanding Variables, Scope, and Hoisting in JavaScript](https://www.digitalocean.com/community/tutorials/understanding-variables-scope-hoisting-in-javascript)
sumber dari DigitalOcean

| Keyword                                                                                       | Scope          | Hoisting | Can Be Reassigned | Can Be Redeclared |
| --------------------------------------------------------------------------------------------- | -------------- | -------- | ----------------- | ----------------- |
| [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)     | Function scope | Yes      | Yes               | Yes               |
| [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)     | Block scope    | No       | Yes               | No                |
| [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) | Block scope    | No       | No                | No                |

<a name="variabel"></a>

## Deklarasi Variabel

ES6 memperkenalkan `let`, yang memungkinkan untuk variabel `block-scoped` yang
tidak dapat dideklarasikan ulang.

<div class="class">ES5</div>

```js
var x = 0
```

<div class="class">ES6</div>

```js
let x = 0
```

- [MDN Referensi: let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

<a name="konstanta"></a>

## Deklarasi Konstanta

ES6 memperkenalkan `const`, yang tidak dapat dideklarasikan ulang atau `assign`
ulang.

<div class="class">ES6</div>

```js
const CONST_IDENTIFIER = 0
```

- [MDN Referensi: const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

<a name="arrow-function"></a>

## Arrow functions

Penulisan pada Arrow Function adalah cara yang lebih pendek untuk membuat fungsi
`expression`. Arrow Function tidak memiliki `this`, tidak memiliki `prototypes`,
tidak dapat digunakan untuk konstruktor, dan tidak boleh digunakan sebagai
metode objek.

<div class="class">ES5</div>

```js
function func(a, b, c) {} // function declaration
var func = function(a, b, c) {} // function expression
```

<div class="class">ES6</div>

```js
let func = a => {}
let func = (a, b, c) => {}
```

- [MDN Referensi: Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

<a name="template-literal"></a>

## Template literals

### Concatenation/string interpolation

Ekspresi dapat tambahkan dalam string template literal.

<div class="class">ES5</div>

```js
var str = 'Tanggal: ' + date
```

<div class="class">ES6</div>

```js
let str = `Tanggal: ${date}`
```

- [MDN Referensi: Expression interpolation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Expression_interpolation)

### Multi-line strings

Menggunakan template literal, string pada JavaScript dapat menjangkau beberapa
baris kode tanpa perlu penggabungan.

<div class="class">ES5</div>

```js
var str = 'ini text ' + 'dalam ' + 'multiple line'
```

<div class="class">ES6</div>

```js
let str = `ini text
            dalam
            multiple line`
```

- [MDN Referensi: Multi-line strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Multi-line_strings)

<a name="key-property"></a>

## Penulisan singkat Key/property

ES6 memperkenalkan notasi yang lebih pendek untuk menempatkan properti ke
variabel nama yang sama.

<div class="class">ES5</div>

```js
var obj = {
  a: a,
  b: b,
}
```

<div class="class">ES6</div>

```js
let obj = {
  a,
  b,
}
```

- [MDN Referensi: Property definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Property_definitions)

<a name="method-definition"></a>

## Penulisan singkat definisi Method

Keyword `function` dapat dihilangkan saat menulis method pada suatu object.

<div class="class">ES5</div>

```js
var obj = {
  a: function(c, d) {},
  b: function(e, f) {},
}
```

<div class="class">ES6</div>

```js
let obj = {
  a(c, d) {},
  b(e, f) {},
}
```

```js
obj.a() // call method a
```

- [MDN Referensi: Method definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)

<a name="destructuring"></a>

## Destructuring (object matching)

Gunakan curly bracket untuk menulis properti suatu object ke variabel itu
sendiri.

```js
var obj = {a: 1, b: 2, c: 3}
```

<div class="class">ES5</div>

```js
var a = obj.a
var b = obj.b
var c = obj.c
```

<div class="class">ES6</div>

```js
let {a, b, c} = obj
```

- [MDN Referensi: Object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)

<a name="iteration"></a>

## Array iteration (looping)

Penulisan yang lebih singkat telah kenalkan untuk iterasi melalui array.

```js
var arr = ['a', 'b', 'c']
```

<div class="class">ES5</div>

```js
for (var i = 0; i < arr.length; i++) {
  console.log(arr[i])
}
```

<div class="class">ES6</div>

```js
for (let i of arr) {
  console.log(i)
}
```

- [MDN Referensi: for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

<a name="parameter-default"></a>

## Paramenter Default

Function dapat diinisialisasi dengan parameter default, yang hanya akan
digunakan jika argumen tidak dipanggil melalui function.

<div class="class">ES5</div>

```js
var func = function(a, b) {
  b = b === undefined ? 2 : b
  return a + b
}
```

<div class="class">ES6</div>

```js
let func = (a, b = 2) => {
  return a + b
}
```

```js
func(10) // return 12
func(10, 5) // return 15
```

- [MDN Referensi: Default paramters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

<a name="spread"></a>

## Penulisan Spread

Penulisan spread dapat digunakan untuk memperluas/pengembangkan array.

<div class="class">ES6</div>

```js
let arr1 = [1, 2, 3]
let arr2 = ['a', 'b', 'c']
let arr3 = [...arr1, ...arr2]

console.log(arr3) // [1, 2, 3, "a", "b", "c"]
```

Penulisan spread dapat digunakan untuk fungsi argumen.

<div class="class">ES6</div>

```js
let arr1 = [1, 2, 3]
let func = (a, b, c) => a + b + c

console.log(func(...arr1)) // 6
```

- [MDN Referensi: Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

<a name="class"></a>

## Classes/constructor functions

ES6 memperkenalkan penulisan `class` di atas konstruktor berbasis prototype
fungsi.

<div class="class">ES5</div>

```js
function Func(a, b) {
  this.a = a
  this.b = b
}

Func.prototype.getSum = function() {
  return this.a + this.b
}

var x = new Func(3, 4)
```

<div class="class">ES6</div>

```js
class Func {
  constructor(a, b) {
    this.a = a
    this.b = b
  }

  getSum() {
    return this.a + this.b
  }
}

let x = new Func(3, 4)
```

```js
x.getSum() // return 7
```

- [MDN Referensi: Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

<a name="inheritance"></a>

## Inheritance

Keyword `extends` dapat membuat subclass.

<div class="class">ES5</div>

```js
function Inheritance(a, b, c) {
  Func.call(this, a, b)

  this.c = c
}

Inheritance.prototype = Object.create(Func.prototype)
Inheritance.prototype.getProduct = function() {
  return this.a * this.b * this.c
}

var y = new Inheritance(3, 4, 5)
```

<div class="class">ES6</div>

```js
class Inheritance extends Func {
  constructor(a, b, c) {
    super(a, b)

    this.c = c
  }

  getProduct() {
    return this.a * this.b * this.c
  }
}

let y = new Inheritance(3, 4, 5)
```

```js
y.getProduct() // 60
```

- [MDN Referensi: Subclassing with extends](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Sub_classing_with_extends)
-

<a name="modules"></a>

## Modules - export/import

Modules dapat dibuat untuk mengekspor dan mengimpor kode antar file.

<div class="class">index.html</div>

```html
<script src="export.js"></script>
<script type="module" src="import.js"></script>
```

export.js

```js
let func = a => a + a
let obj = {}
let x = 0

export {func, obj, x}
```

<div class="class">import.js</div>

```js
import {func, obj, x} from './export.js'

console.log(func(3), obj, x)
```

- [MDN Referensi: export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [MDN Referensi: import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

<a name="promise-callback"></a>

## Promises/Callbacks

Promise mewakili penyelesaian fungsi asynchronous. Bisa juga digunakan sebagai
alternatif fungsi chaining.

<div class="class">ES5 callback</div>

```js
function doSecond() {
  console.log('Do second.')
}

function doFirst(callback) {
  setTimeout(function() {
    console.log('Do first.')

    callback()
  }, 500)
}

doFirst(doSecond)
```

<div class="class">ES6 Promise</div>

```js
let doSecond = () => {
  console.log('Do second.')
}

let doFirst = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('Do first.')

    resolve()
  }, 500)
})

doFirst.then(doSecond)
```

Contoh di bawah ini menggunakan `XMLHttpRequest`, hanya untuk demo
([Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)).

<div class="class">ES5 callback</div>

```js
function makeRequest(method, url, callback) {
  var request = new XMLHttpRequest()

  request.open(method, url)
  request.onload = function() {
    callback(null, request.response)
  }
  request.onerror = function() {
    callback(request.response)
  }
  request.send()
}

makeRequest('GET', 'https://url.json', function(err, data) {
  if (err) {
    throw new Error(err)
  } else {
    console.log(data)
  }
})
```

<div class="class">ES6 Promise</div>

```js
function makeRequest(method, url) {
  return new Promise((resolve, reject) => {
    let request = new XMLHttpRequest()

    request.open(method, url)
    request.onload = resolve
    request.onerror = reject
    request.send()
  })
}

makeRequest('GET', 'https://url.json')
  .then(event => {
    console.log(event.target.response)
  })
  .catch(err => {
    throw new Error(err)
  })
```

- [MDN Referensi](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

Jika ini bermanfaat, silahkan share 😃
