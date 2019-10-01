# NodeJS Crash Course

Untuk memulai belajar NodeJS pertama-tama install terlebih dahulu NodeJS nya. NodeJS bisa didownload di link berikut: <https://nodejs.org/en/>. Download versi yang terbaru.

Apabila instalasi telah selesai, ketikkan `node --v` untuk memastikan bahwa NodeJS telah berhasil terinstall.

Pada terminal kamu juga bisa secara langsung mencoba menuliskan kode melalui _REPL_ singkatan dari _Read Eval Print Loop_, mudahnya memungkinkan kita menulis kode JavaScript di console.

![1556978502785](https://i.ibb.co/KWD66t3/1556978502785.png)

Untuk keluar dari REPL, tekan `CTRL + C`. Meski kita bisa menuliskan kode JavaScript di terminal, kita tentu tidak akan menuliskannya disana, disini saya akan menggunakan Visual Studio Code sebagai kode editor.

Disini saya bekerja di Visual Studio Code pada folder `NODE_CRASH_COURSE`.

## Membuat Package.json

Biasanya yang pertama kali kita lakukan ketika membuat project node adalah membuat `package.json`. Kita tidak perlu membuat file ini secara manual, kita akan menggenerate file nya dengan cara mengetikkan di terminal `npm init`. Kemudian isilah beberapa pertanyaan yang diajukan.

`package.json` sendiri tujuan utamanya adalah menyimpan daftar _dependency-dependency_ yang aplikasi kita gunakan. Sehingga, ketika kita berganti komputer kita bisa langsung menginstall _dependency_ yang ada di daftar `package.json` akan diinstall semuanya dengan cara mengetikkan `npm install` di terminal.

Maksud dari _dependency_ diatas adalah misalnya kita menginstall suatu _package atau module_ di aplikasi kita dengan cara `npm install nama_package`.

### Contoh Instalasi Package

Disini kita akan coba menginstall sebuah package bernama `uuid`. Package ini berfungsi untuk menggenerate id secara random.

Ketikkan di terminal `npm install uuid`. Setelah berhasil, maka akan terbuat folder `node_modules` yang mana di dalamnya ada modul `uuid`. Dan pada `package.json` juga akan terupdate bahwa terdapat _dependency_. **Package yang kita install akan diletakkan di dalam folder `node_modules`**.

### Dev Dependency

Ada juga yang dinamakan _dev dependency_ dimana hanya diperlukan sewaktu _development_ atau pengembangan saja, tidak ketika aplikasi kita _deploy_ ke internet.

Sekarang kita akan menginstall `nodemon` dimana package ini berguna untuk ketika kita ada perubahan pada kode, kita tidak perlu me-restart ulang server nya. `nodemon` akan kita install saat development saja.

Ketikkan perintah berikut: `npm install --save-dev nodemon` atau lebih singkatnya `npm install -D nodemon`.

### NPM Install

Misalnya kita ingin mengupload file aplikasi kita dan menggunakannya di komputer lain. Kita tidak meng-upload folder `node_modules`. Folder tersebut berisikan banyak sekali file dari _dependency_ yang aplikasi kita gunakan. Olehkarenanya, cobalah hapus folder `node_modules`, kemudian ketikkan di terminal `npm install`. Maka npm akan menginstall modul-modul yang diperlukan aplikasi kita.

## Hello World

Selanjutnya, buatlah file `index.js` di folder utama, kemudian ketikkanlah kode berikut:

```javascript
console.log('Hello from NodeJS...');
```

Untuk menjalankan file ini, ketikkan di terminal `node index` atau `node index.js`.

Berikut screenshot hasil nya:

![1556980124756](https://i.ibb.co/zhbH6VR/1556980124756.png)

Pada kenyataannya nanti, ketika mengembangkan aplikasi kita akan memiliki banyak file. Tidak hanya satu file. File itu bisa berisi suatu _class, function_ dan lain-lain yang nantinya akan di-_export_ sehingga dapat kita gunakan.

## Membuat Module

Buatlah sebuah file bernama `person.js`, lalu ketikkan kode berikut:

```java
const person = {
  name: 'Fadli Hidayatullah',
  age: 22
};

module.exports = person;
```

`module.exports = person` berfungsi untuk meng-ekspor `person` sehingga bisa digunakan di tempat lain. Jadi ketika modul ini di-_require_ di tempat lain, `person` inilah yang akan dikembalikan. Untuk dapat menggunakannya pada tempat lain misalnya di `index.js`. Kita gunakan fungsi `require(lokasi_file)`.

Selanjutnya, pada `index.js` ketikkan kode berikut:

```javascript
// ...
const person = require('./person');

console.log(person);
console.log(person.name);
```

Berikut hasilnya:

![1556980644672](https://i.ibb.co/qWQzs5R/1556980644672.png)

Biasanya suatu modul tidak hanya suatu objek yang di ekspor tetapi, biasanya function atau class. Olehkarenanya, ubahlah kode yang ada di `person.js` menjadi sebuah class.

```javascript
console.log('person.js');
console.log(__dirname, __filename);

class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greeting() {
    console.log(`Hi. My name is ${this.name} and I am ${this.age}.`);
  }
}

module.exports = Person;
```

Dan file `index.js` menjadi berikut:

```javascript
const Person = require('./person');

const person1 = new Person('Fadli', 22);

person1.greeting();
```

Ketika file `index.js` dijalankan maka berikut hasilnya:

![1556981230630](https://i.ibb.co/y6pd3KW/1556981230630.png)

Ketika kita me-_require_ suatu modul, file yang di-_require_ kode nya juga akan dijalankan. Oleh sebab itulah mengapa `person.js` dan informasi `__dirname` dan `__filename` tampil pada terminal.

## Node Core Modules

Sekarang, kita akan mencoba menggunakan modul-modul yang sudah disediakan oleh NodeJS.

### Modul Path

Pada NodeJS terdapat package `path` yang bisa digunakan untuk bekerja dengan file dan direktori path. Disini kita akan melihat sekilas beberapa method yang nantinya akan kita gunakan.

Buatlah sebuah folder baru bernama `reference`, kemudian buat file `path_demo.js`. Tulislah kode berikut ini:

```javascript
const path = require('path');

// File name
console.log(path.basename(__filename));

// Directory name
console.log(path.dirname(__filename));

// Create path object
console.log(path.parse(__filename).dir);

// Concatenate paths
console.log(path.join(__dirname, 'test', 'hello.html'));
```

### Modul FS

Disini kita akan mencoba bekerja dengan file sistem, diantaranya adalah:

- Membuat folder
- Membuat sekaligus menulis file
- Meng-append file
- Membaca file

Buatlah sebuah file baru bernama `fs_demo.js` pada folder `reference`, kemudian tuliskan kode berikut:

```javascript
const fs = require('fs');
const path = require('path');

// Create folder
fs.mkdir(path.join(__dirname, '/test'), (err) => {
  // if (err) throw err;

  console.log('Folder created ...');
});

// Create and write to file
fs.writeFile(
  path.join(__dirname, '/test', 'hello.txt'),
  'Hello world!',
  (err) => {
    if (err) throw err;

    console.log('File written to ...');

    // Append file
    fs.appendFile(
      path.join(__dirname, '/test', 'hello.txt'),
      'Welcome Ramadhan Mubarrak',
      (err) => {
        if (err) throw err;

        console.log('File appended to ...');
      },
    );
  },
);

// Read file
fs.readFile(path.join(__dirname, '/test', 'hello.txt'), 'utf8', (err, data) => {
  if (err) throw err;

  console.log('Read data: ');
  console.log(data);
});
```

Terdapat metode _Synchronous_ dan _Asynchronous_. Ketika kita menggunakan Asynchronous maka kita harus menuliskan _function callback_-nya.

### Module OS

Modul selanjutnya adalah modul `os`, memungkinkan kita untuk mengetahui informasi tentang Sistem Operasi dari platform yang sedang digunakan.

Buatlah sebuah file baru bernama `os_demo.js` pada folder `reference`. Tulislah kode berikut ini:

```javascript
const os = require('os');

// Platform
console.log(os.platform());

// CPU Arch
console.log(os.arch());

// CPU Core Info
console.log(os.cpus());

// Free memory
console.log(os.freemem());

// Total memory
console.log(os.totalmem());

// Home directory
console.log(os.homedir());

// OS Type
console.log(os.type());

// Uptime
console.log(os.uptime());
```

### Module URL

Selanjutnya adalah modul `url` yang memungkinkan kita untuk bekerja dengan URL.

Buatlah file baru bernama `url_demo.js` pada folder `reference`. Tuliskan kode berikut ini:

```javascript
const url = require('url');

const myUrl = new URL(
  'http://fadlihdytullah.id/hello.html?id=10&status=active',
);

// Serialize URL
console.log(myUrl.href);
console.log(myUrl.toString());

// Host (root domain)
console.log(myUrl.host);
// Host (does not get port)
console.log(myUrl.hostname);

// Path name
console.log(myUrl.pathname);

// Serialize query
console.log(myUrl.search);
// Params object
console.log(myUrl.searchParams);

// Add param
console.log(myUrl.searchParams.append('abc', '123'));

// Loop through params
myUrl.searchParams.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});
```

## EventEmitter

Terkadang adakalanya lebih baik kita mengganti _callbacks_ dan _promises_ dengan _EventEmitter_. Mungkin untuk awal-awal agak sulit untuk dimengerti, namun mudahnya, kita bisa membuat _events listener_ dari suatu object dan mengaktifkannya.

Untuk dapat menggunakan EventEmitter kita menggunakan modul `events`. Kita bisa men-_extend_ EventEmitter pada suatu class ataupun mewarisi sifat dari EventEmitter dengan modul `util`.

Buatlah file baru bernama `event_demo.js` pada folder `reference`, kemudian tuliskan kode berikut:

```javascript
const EventEmitter = require('events').EventEmitter;
const util = require('util');

const myObject = function(thing) {
  EventEmitter.call(this);
};

util.inherits(myObject, EventEmitter);

myObject.prototype.doSomething = function(thing) {
  this.emit('something', thing);

  return this; // make it chainable method, for ease of use
};

const obj = new myObject();
obj.on('something', (thing) => console.log(thing));

obj
  .doSomething('Ohayou!')
  .doSomething('Nan da yo')
  .doSomething('Yare yare na kimi wa...');
```

Kemudian jalankan file tersebut, maka hasilnya adalah sebagai berikut:

![1557099198368](https://i.ibb.co/C8WPNhg/1557099198368.png)

Selanjutnya buatlah file `logger.js` pada project folder, kemudian tuliskan kode berikut:

```javascript
const EventEmitter = require('events');
const uuid = require('uuid');

module.exports = class Logger extends EventEmitter {
  log(msg) {
    this.emit('message', { id: uuid.v4(), msg });
    return this;
  }
};
```

Pada `index.js`, kita akan menggunakan kelas `Logger`.

```javascript
// ... kode sebelumnya
const Logger = require('./logger');

const loggerObj = new Logger();
loggerObj.on('message', (data) => console.log(data));

loggerObj
  .log('Yare2 na')
  .log('Nan da yo')
  .log('Wakatta yo!');
```

Ketika `index.js` dijalankan maka berikut hasilnya:

![1557099523275](https://i.ibb.co/6tVt3rh/1557099523275.png)

> Referensi lebih lanjut:
> <https://scotch.io/@thelettere/nodejs-event-emitter> > <https://nodejs.org/api/events.html>

## Membuat Server

Untuk membuat server kita membutuhkan modul `http`. Berikut contoh sederhana dalam membuat server.

Buatlah sebuah file baru bernama `http_demo.js` pada folder `reference`. Tulislah kode berikut:

```javascript
const http = require('http');

http
  .createServer((req, res) => {
    res.end('Yosh! Sugoi desu.');
  })
  .listen(5000, () => console.log('Server running ...'));
```

Method `createServer()` membutuhkan function callback yang memiliki dua parameter, yakni `req` sebagai _request_ dan `res` sebagai _response_.

Agar si server dapat bekerja maka kita harus membuat si server _listen_ terhadap suatu port tertentu, misalnya 5000.

Maka ketika kita menjalankan file tersebut, server berhasil dibuat.

![1557102194790](https://i.ibb.co/Qcy0m0h/1557102194790.png)

### Merender File HTML

Sejatinya, server nantinya akan menyajikan file HTML untuk ditampilkan pada user. Misalnya user melakukan request pada halaman utama, halaman about, halaman contact.

Hapuslah semua kode pada `index.js`, kemudian tuliskan kode berikut:

```javascript
const http = require('http');
const path = require('path');
const fs = require('fs');

const PORT = process.env.PORT || 5000;
const server = http.createServer((req, res) => {
  res.end('<h1>Home</h1>');
});

server.listen(PORT, () => console.log(`Server is running on port ${PORT}`));
```

Kita menggunakan `process.env.PORT` disini karena nantinya kita akan menyesuaikan port dari _environment_ yang kita gunakan, jika tidak ditemukan maka gunakan port 5000.

Untuk mengetahui URL apa yang sedang diakses oleh user, kita gunakan `req.url`. Sehingga, kita bisa membuat rute atau _routing_ mengenai file mana yang nantinya kita akan render.

Kita jug bisa menuliskan kode HTML pada `res.end()`.

Jalankan lah file tersebut, akses `localhost:5000` atau sesuaikan port nya. Tapi, ketika kita mengubah file `index.js` , misalnya dari `res.end('<h1>Home</h1>')` menjadi `res.end('<h1>Homepage</h1>');` kita diharuskan me-restart server agar terjadi perubahan.

Maka dari itulah sebelumnya kita install package `nodemon`, sehingga jika terjadi perubahan maka akan ter-restart otomatis.

Untuk dapat melakukannya, buka file `package.json`. Ubahlah kode:

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

Menjadi,

```json
{
  "scripts": {
    "start": "node index",
    "dev": "nodemon index"
  }
}
```

Kode `"start": "node index"` tidak akan melakukan update perubahan, tetapi ini merupakan skrip standar yang akan dijalankan ketika kita men-_deploy_ aplikasi kita.

Kode yang membuat update perubahan secara otomatis yang akan kita lakukan saat _dev_ adalah `"dev" : "nodemon index"`. Untuk dapat menjalankan skrip ini, pada terminal ketikkan `npm run dev`. Maka apapun yang kamu ubah pada file `index.js` akan ter-update.

### Menambahkan Content-type

Jika diperhatikan kita hanya menggunakan `res.end('<h1>Homepage</h1>')` maka ketika lihat `view page source` halaman utama nya dan _network_ nya tidaka akan kita temukan _template_ html serta _content-type_ bahwa file tersebut adalah HTML.

Untuk itu tambahkan kode sebelum `res.end(<h1>Homepage</h1>)` dengan kode berikut:

```javascript
res.writeHead(200, { 'Content-type': 'text/html' });
```

Maka disini kita menulis _header_ nya 200 yang artinya OK, kemudian content type nya HTML.

### Merender File HTML

Untuk melakukannya kita akan menggunakan modul `fs` untuk membaca file HTML nya, dan `path` untuk lokasi filenya.

Buatlah folder baru pada root folder, berilah nama `public`. Pada folder inilah kita akan meletakkan file-file HTML dan CSS kita nantinya.

Buatlah 2 file, yakni `index.html` dan `about.html`. Masing-masing kode nya dibawah ini:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Welcome</title>
  </head>
  <body>
    <h1>Welcome to the homepage</h1>
  </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>About</title>
  </head>
  <body>
    <h1>About</h1>
  </body>
</html>
```

Selanjutnya, kembalilah ke `index.html`. Ubahlah kode berikut ini,

```javascript
if (req.url === '/') {
  res.writeHead(200, { 'Content-type': 'text/html' });
  res.end('<h1>Homepage</h1>');
}
```

Menjadi,

```javascript
if (req.url === '/') {
  fs.readFile(path.join(__dirname, 'public', 'index.html'), (err, content) => {
    if (err) throw err;

    res.writeHead(200, { 'Content-type': 'text/html' });
    res.end(content);
  });
}

if (req.url === '/about') {
  fs.readFile(path.join(__dirname, 'public', 'about.html'), (err, content) => {
    if (err) throw err;

    res.writeHead(200, { 'Content-type': 'text/html' });
    res.end(content);
  });
}
```

#### RESTApi & Microservices

Adakalanya nanti kamu akan mengembangkan suatu RESTApi atau microservices, yang biasanya data yang dikirim dalam bentuk JSON. Meskipun biasanya kita melakukannya menggunakan _express_, berikut cara melakukannya pada NodeJS.

Tambahkan kode berikut ini setelah penutup _if_ untu route `/about`.

```javascript
if (req.url === '/api/user') {
  const users = [
    { id: 1, name: 'fadlihdytullah', age: 22 },
    { id: 2, name: 'yusriron', age: 20 },
  ];

  res.writeHead(200, { 'Content-type': 'application/json' });
  res.end(JSON.stringify(users));
}
```
