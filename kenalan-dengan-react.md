# Kenalan dengan React JS

## Disclaimer

Note ini memang jauh dari sempurna dari segi banyak kontennya, tetapi secara
berkala(per hari) akan selalu diupdate.

## Intro

Seperti yang kita tahu [React](https://github.com/facebook/react) adalah library
untuk view dalam pembuatan aplikasi Front End. Nah seiring berjalannya update
terkini, pada note ini akan membahas perintah react dasar. Sangat
direkomendasikan untuk memahami `JS ES6` terlebih dahulu. Salah satu note nya
[disini](https://github.com/randyviandaputra/my-notes/blob/master/kenalan-dengan-react.md).

## Daftar Isi

- [Komponen Fungsi](#komponen-fungsi)
- Akan diupdate/ bertambah ASAP^^

## Komponen Fungsi

<a name="komponen-fungsi"></a> Pada saat note ini dibuat, versi terakhir react
yang digunakan adalah 16.8.6. The newest update nya komponen sekarang
menggunakan fungsi tidak menggunakan class lagi.

<div class="class">Contoh Komponen</div>

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

  return <footer style={style}>Copyright 2019</footer>
}

export default CustomFooter
```

Jika ini bermanfaat, silahkan share 😃
