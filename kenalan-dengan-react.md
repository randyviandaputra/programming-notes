# Kenalan dengan React JS

## Disclaimer

Note ini memang jauh dari sempurna dari segi banyak kontennya, tetapi secara
berkala(per hari) akan selalu diupdate.

## Intro

Seperti yang kita tahu [React](https://github.com/facebook/react) adalah library
untuk view dalam pembuatan aplikasi Front End. Nah seiring berjalannya update
terkini, pada note ini akan membahas perintah react dasar. Sangat
direkomendasikan untuk memahami `JS ES6` terlebih dahulu. Salah satu note nya
[disini](https://github.com/randyviandaputra/my-notes/blob/master/penulisan-es6-dan-pengenalan-fitur.md).

## Daftar Isi

- [Komponen Fungsi](#komponen-fungsi)
- [Bermain dengan Props](#bermain-props)
- [Stateful dan Stateless](#state)
- Akan diupdate/ bertambah ASAP^^

## Komponen Fungsi

<a name="komponen-fungsi"></a> Pada saat note ini dibuat, versi terakhir react
yang digunakan adalah 16.8.6. The newest update nya komponen sekarang
menggunakan fungsi tidak menggunakan class lagi.

<div class="class">Contoh Komponen, contoh di <a href = "https://codesandbox.io/embed/programming-notes-komponen-fungsi-1knl3?fontsize=14" target="_blank">sandbox.io</a></div>

```js
function CustomFooter() {
  return <footer>Copyright 2019</footer>
}

export default CustomFooter
```

Kalau ingin ngasih styling pada komponennya menggunakan CSS tinggal ditambahin
sebelum return.

<div class="class">Styling Komponen</div>

```js
function CustomFooter() {
  const customStyle = {
    color: 'red',
  }

  return <footer style={customStyle}>Copyright 2019</footer>
}

export default CustomFooter
```

## Bermain dengan Props

<a name="bermain-props"></a> Komponen dalam aplikasi web maupun native React
seringkali terdari dari lebih dari 1 komponen. Props adalah teknik untuk
mengirim data antar komponen tersebut.

<div class="class">Contoh Props</div>

```js
//CustomFooter.js
function CustomFooter(copyrightYear = "defaultTahun") {
  return <footer>Copyright {copyrightYear}</footer>
}

export default CustomFooter

//App.js
import CustomFooter from './components/CustomFooter.js'

function App(){
  return(<div>
    <header>Aku tag native header</header>
    <section>Aku tag native section</section>
    <CustomFooter copyrightYear = "2019"/>
  </div>)
}

export default App
```

Gimana kalau mau passing props lain selain `copyrightYear` dengan ringkas?
solusi menggunakan spread atribute.

```js
//CustomFooter.js
function CustomFooter({copyrightYear = "defaultTahun", ...props}) {
  return <footer {...props}>Copyright {copyrightYear}</footer>
}

export default CustomFooter

//App.js
import CustomFooter from './components/CustomFooter.js'

function App(){
  return(<div>
    <header>Aku tag native header</header>
    <section>Aku tag native section</section>
    <CustomFooter className = "custom-footer" copyrightYear = "2019"/>
  </div>)
}

export default App
```

Snippet code diatas memberikan props `className` pada elemen `<footer>` yang
berada pada fungsi `CustomFooter`.

## Stateful dan Stateless

<a name="state"></a> Kalau bagian sebelumnya membahas bagaimana mengirim data
antar komponen, kali ini bagaimana mengubah/ memutasi data dalam satu komponen.
Dikatakan stateful ketika ada state didalam komponen nya, cirinya menggunakan
`useState`. Sedangkan stateless sebaliknya.

<div class="class">Stateful dan Stateless</div>

```js
//Components.js
import React, {useState} from 'react'

//Component Stateful
export default function ComponentStateful() {
  const [name, setName] = useState('Budi')

  return (
    <div>
      <ComponentStateless nama={name} />
      <input type="text" value={name} onKeyDown={setName(e.target.value)} />
    </div>
  )
}

//Component Stateless
function ComponentStateless(nama = 'defaultNama') {
  return (
    <div>
      <section>Hi nama ku {nama}</section>
    </div>
  )
}
```

Jika ini bermanfaat, silahkan share 😃
