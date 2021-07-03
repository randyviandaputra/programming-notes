#**Apa Sih Itu Vuejs?**

Vue.js adalah sebuah framework untuk membangun antarmuka web yang interaktif.

##**Installasi VueJs**

Untuk instalasi vue.js sendiri ada beberapa alternatif bisa menggunakan nya secara langsung dengan mendownload file vue.js nya , menggunakan CDN, NPM, dan Vue-cli, tapi pada kesempatan kali ini kita akan belajar dengan menggunakan cara yg pertama dengan mendownload filenya secara langsung ke komputer kita, cara inilah cara yg paling mudah untuk digunakan dalam tahap awal belajar vue.js itu sendiri, ok untuk mendownload file vue.js nya anda bisa menuju link berikut https://vuejs.org/v2/guide/installation.html dan pilih yg Direct Script Include kemudian pilih yg development version setelah itu letakan filenya di dalam directory untuk belajar vue.js nya.

###**Membuat Hello World**

Salah satu kelebihan dari Vue.js adalah flexibilitas dimana kita dapat membuat sebuah aplikasi web dengan berbagai cara tergantung pada kebutuhan dan skala dari aplikasi web kita.

Kita akan memulai belajarnya dengan membuat sebuah aplikasi “Hello World!” sederhana. Untuk memulai buatlah sebuah file html dengan code sebagai berikut :

<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <title>Belajar vue.js dasar</title>
</head>
<body><div id="app">
  <p> {{ pesan }} </p>
</div><script src="vue.js"></script>
 <script>
  new Vue({
   el:"#app",
   data: {
    pesan:"Hello World!"
   }
  });
 </script>
</body>
</html>
