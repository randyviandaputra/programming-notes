# Menggunakan Eslint dan Git-Hook

Eslint merupakan linter pada javascript yang melakukan pengencekan agar kita dapat meminimalisir kemungkinan bug dan menjaga kekonsistensian pada kode kita. 

Berikut adalah cara untuk meng-integrasikan eslint dengan git-hooks sehingga eslint akan menolak commit kita jika tidak sesuai dengan "rule"-nya

# [ESLint](https://eslint.org/)

ESLint adalah sebuah alat yang bertujuan untuk membuat kode lebih konsisten dan menghindari kemungkinan bugs.

Untuk menginstall ESLint pada project, cukup lakukan instalasi menggunakan npm seperti pada contoh.

```
$ npm install --save-dev eslint
```
Kemudian untuk menjalankan konfigurasinya bisa jalankan perintah:
```
$ npx eslint --init
```
selanjutnya kita tinggal menjawab pertanyaan seputar code style yang akan dipakai.

# [Husky](https://www.npmjs.com/package/husky)

Sekarang setelah kita memiliki alat untuk melakukan cek terhadap code berdasarkan peraturan yang dibuat. Hal selanjutnya adalah kita perlu "memaksa" peraturan yang kita buat untuk ditaati. Disinilah Husky berperan.
Husky berfungsi untuk menjalankan suatu perintah tertentu saat kita memasukan perintah git, atau dalam kasus ini ESLint kita jalankan saat kita memasukan perintah `git commit`. Jika ESLint mendeteksi ada kesalahan, maka commit akan gagal. 

Untuk meng-install husky pada project kita, kita cukup jalankan perintah:
```
$ npm i --save-dev husky
```
lalu pada file package.json tambahkan baris code berikut:
```
{
  …
    “scripts”: {
      …
      “pretest”: “./node_modules/.bin/eslint --ignore-path .gitignore . --fix”
      },
    … 
  “husky”: {
     “hooks”: {
       “pre-commit”: “npm run pretest”
     }
  }
}
```
Namun sekarang permasalahan lainnya muncul. Perintah tersebut memerintahkan ESLint untuk mengecek semua file pada project kita, termasuk yang tidak akan kita push. Untuk menanggulangi hal tersebut kita membutuhkan satu alat lagi.

# [Lint-staged](https://www.npmjs.com/package/lint-staged)

Lint staged memungkinkan ESLint untuk hanya memeriksa dan melakukan perbaikan pada file yang akan kita commit. Cara menginstallnya dengan mengetikan perintah:
```
$ npm install --save-dev lint-staged
```
Lalu rubah baris perintah yang tadi dimasukan pada package.json dengan baris perintah berikut:
```
{
  ...
  “husky”: {
    “hooks”: {
      “pre-commit”: “lint-staged”
    }
  },
  “lint-staged”: {
    “*.js”: [“./node_modules/.bin/eslint — fix”, “git add”]
  }
}
```
Dengan ini maka ESLint akan melakukan perbaikan pada file yang akan dicommit, atau jika ESLint tidak bisa memperbaiki, maka error akan muncul sehingga commit tidak dapat dilakukan sampai error diperbaiki.

Cara ini diharapkan dapat menjaga konsistensi code pada repository dan meminimalisir kemungkinan munculnya bugs pada program