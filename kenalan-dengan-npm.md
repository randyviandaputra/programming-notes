# NPM Crash Course

Adakalanya kamu ingin menginstall suatu library, dengan NPM kita bisa melakukannya dengan mudah.

## Pengenalan Apa Itu NPM

**Node Package Manager**

Jika kamu pernah bekerja dengan teknologi lain, pada Ruby ada _Ruby Gems_, pada Python ada _Pip_, mudahnya NPM adalah _JavaScript Package Manager_ memudahkan kamu untuk menginstall modul/package/library dengan mudah, misalnya menginstall _Bootstrap, JQuery, Express_.

**Pre-Installed with Node.js**

**Instalasi modul/package di sistem kita dengan mudah**

Modul ataupun package mudahnya library JavaScript.

**Membuat developer mudah untuk berbagi _reuse_ kode**

## Apa yang Akan Kamu Pelajari

- Install, remove, update, & list package
- Berkenalan dengan _package.json_
- Local & global package
- Dependency & dev-dependency
- Commands & Shortcuts
- Versioning
- NPM Scripts

## Menggunakan NPM

Untuk dapat menggunakan NPM, kamu harus menginstall Node.js terlebih dahulu. Node.js bisa di download di link berikut: <https://nodejs.org/en/>

Untuk melihat-lihat package yang ada di NPM, kamu bisa mengunjungi situs <https://www.npmjs.com/>.

Kita akan bermain-main dengan command NPM di terminal, olehkarena, buatlah project baru bernama `npm-app`, buka folder tersebut di teks editor kamu, kemudian bukalah terminal, pastikan terminal path nya ada di project folder tersebut. Disarankan menggunakan _git bash_ untuk terminal nya, jika kamu menggunakan windows.

- `npm -v` atau `npm --version`, melihat versi NPM
- `npm` melihat seluruh daftar command pada NPM

## Package.json File

File `package.json` merupakan file yang sangat penting dalam dunia JavaScript, file ini berisi _manifest_ dan informasi mengenai app kita.

Tapi, yang paling penting adalah di dalam file ini terdapat daftar _dependency_ yang digunakan aplikasi kita, _nama dan versi_ dari package yang digunakan. Sehingga, ketika kita deploy aplikasi kita ke internet, maka NPM dapat menginstall semua dependency yang ada.

Kita juga bisa membuat _NPM Scripts_ untuk melakukan suatu _task_.

Kita bisa membuat file ini secara manual, tetapi kita bisa dengan mudah membuat file `package.json` dengan perintah `npm init`.

### Membuat File Package.json

Buka kembali terminal kamu dan ketikkan `npm init`, kamu akan dipaparkan beberapa pertanyaan informasi mengenai app yang akan dibuat.

Berikut pertanyaan yang diajukan:

- `npm init`, membuat file `package.json`
- `package name`, nama package yang diinginkan
- `version`, versi dari package nya
- `description`, deskripsi package
- `entry point`, file utama JavaScript nya, terkadang `app.js`, adajuga `server.js`
- `test command`, dikosongkan saja
- `git repository` git repository nya
- `keywords` kata kunci dari package nya
- `author`, author dari package
- `licence`, defaultnya ISC, tetapi terkadang MIT

Jika kamu ingin menggunakan jawaban default nya, ketikkan perintah `npm init -y` atau `npm init --yes`. Informasi tadi bisa dirubah pada file `package.json`.

### Konfigurasi Nilai Default NPM Init

Untuk **mengubah** nilai default dari `package.json` ketika di `npm init`, gunakan perintah berikut

```bash
npm config set init-author-name "Fadli Hidayatullah"
# atau
npm set init-licence "MIT"
```

Untuk **mengetahui** nilai default dari `package.json` ketika di `npm init`, gunakan perintah berikut

```bash
npm config get init-author-name
# atau
npm get init-licence
```

Untuk **menghapus** nilai yang kita ubah dari `package.json` ketika di `npm init` sehingga kembali ke pengaturan default, gunakan perintah berikut

```bash
npm config delete init-author-name
```

## Menginstall Package

Untuk menginstall suatu package atau modul, kita gunakan perintah,

```bash
npm install package_name --save
```

Flag atau opsi `--save` berguna untuk menyimpan informasi package yang diinstall, kemudian didaftarkan pada object `dependency` di `package.json`.

Sebagai contoh, kita akan menginstall package `lodash`.

```bash
npm install lodash --save
```

Setelah berhasil diinstall maka,

- Terdapat object dependecy pada `package.json`
- Terdapat folder `node_modules` yang didalamnya terdapat `lodash`

Mengapa flag atau opsi `--save` sangat penting? Ketika kita mem-push project kita ke github atau misalnya memindahkan project kita ke komputer lain, kita tidak mengikutsertakan `node_modules`. Hal ini dikarenakan folder tersebut nantinya berisikan banyak sekali modul-modul yang digunakan aplikasi kita, sehingga membuat project kita ukuran nya semakin besar jika kita upload.

Jadinya, dengan menggunakan `--save` ketika menginstall suatu package, kita bisa dengan mudah menginstall kembali package tersebut di tempat lain.

Sebagai contoh, seseorang mengkloning project kamu yang di upload di github. Tentu, kamu tidak mengikutsertakan folder `node_modules`, semua dependecy aplikasi kamu berada di `package.json`.

Gunakan perintah,

```bash
npm install
```

Untuk menginstall seluruh modul-modul yang diperlukan aplikasi tersebut.

Setelah berhasil menginstall package di atas, maka isi dari `package.json`, kurang lebih seperti berikut,

```json
{
  "name": "npm-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lodash": "^4.17.11"
  }
}
```

Buatlah sebuah file baru di _project folder_, ketikkan kode berikut,

```javascript
const _ = require('lodash');

const numbers = [22, 43, 23, 93, 55, 87, 1];

console.table(numbers);

_.each(numbers, function(number, i) {
  console.log(i, number);
});
```

[![Image from Gyazo](https://i.gyazo.com/9c1595bd375c855772d569b542980a4c.png)](https://gyazo.com/9c1595bd375c855772d569b542980a4c)

## Dev Dependency

Ada juga yang dinamakan _dev-dependency_ dimana dependency ini hanya kamu gunakan saat _development_ bukan pada production.

Sebagai contoh yang biasa kita gunakan saat development, salah satunya `gulp` salah satu tugasnya me-_minify_ file CSS kamu.

```bash
npm install gulp gulp-sass --save-dev
# atau
npm install gulp gulp-sass -D
```

Setelah berhasil diinstall maka pada `package.json` akan ditambahkan object `devDependencies`.

```json
{
  "name": "npm-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "lodash": "^4.17.11"
  },
  "devDependencies": {
    "gulp": "^4.0.2",
    "gulp-sass": "^4.0.2"
  }
}
```

Perintah `npm install` akan menginstall dependency dan juga dev-dependency. Jika kamu ingin menginstall regular dependency nya saja, maka gunakan perintah `npm install --production`.

## Menghapus Package

Untuk menghapus package dapat dilakukan beberapa cara, berikut diantaranya,

```bash
npm uninstall gulp gulp-sass --save-dev
npm un stylus --save
# atau
npm remove lodash --save
npm rm nodemon --save-dev
```

## Install Versi Tertentu & Update

```bash
npm install lodash@4.17.4 --save

npm update lodash
```

## Global Package

Ketika kita menginstall package secara global, maka file nya tidak akan disimpan di `node_modules` dan didaftarkan di `package.json`.

Package yang biasa kita install secara global adalah `nodemon` atau `live-server`. Package `nodemon` sangat berguna ketika kamu mengembangkan aplikasi menggunakan _express_ dimana `nodemon` akan nge-_watch_ perubahan yang kamu lakukan, sehingga tidak perlu me-restart server melihat perubahannya.

```bash
npm install nodemon -g
npm remove nodemon -g
```

Lantas, berada dimana package ini?

```bash
npm root -g
```

## Melihat Daftar Package

```bash
npm list
```

Perintah `npm list` akan menampilkan semua dependency di semua modul.

```bash
npm list --depth 0
npm list --depth 1
```

## Scripts

Pada file `package.json` terdapat skrip, dimana dengan skrip ini, kita bisa menjalankan suatu _testing_ dengan _mocha_, atau menjalankan aplikasi yang awalnya `node index.js` menjadi `node start`, karena bisajadi ada orang lain yang mengkloning aplikasi kita dan ingin langsung menjalankan aplikasi.

Bukalah file `package.json`, ubahlah kode berikut,

```json
"test": "echo \"Error: no test specified\" && exit 1"
```

Menjadi,

```json
"start": "node index.js",
"dev": "nodemon index"
```

Untuk menjalankan skrip ini, pada terminal,

```bash
npm start
```

Akan tetapi, untuk menjalankan skrip yang `dev`, terdapat sedikit perbedaan,

```bash
npm run dev
```

## Mengupload ke Github

Jika kamu ingin mengupload project kamu ke Github dan tidak ingin mengikutsertakan suatu file atau folder, misalnya folder `node_modules`, buatlah file `.gitignore` pada root folder.

Kemudian, tulislah daftar yang tidak ingin kamu sertakan ketika ingin di _push_.
