# Pengertian OOP

OOP atau **Object Oriented Programming** adalah metode atau model pemograman yang berorientasi dengan object, berbeda dengan model pemograman lain seperti **Functional Programming** dan **Procedural Programming** yang berorientasi fungsi.

Berikut adalah beberapa konsep yang dimiliki oleh OOP

- **Object**: Hasil instansiasi dari class
- **Class**: Bersifat seperti ***blueprint*** seperti cetakan yang digunakan untuk meng-instansiasikan object-object
- **Methods & Properties**: Variable dan function yang berada di dalam sebuah object
- **Data Abstraction & Encapsulation**: Penyembunyian data dalam suatu object sehingga tidak semua bagian dari kode dapat mengakses property/method dari object
- **Polymorphism**: Banyak class menggunakan [***interface***](#interface) dan atau [***abstract class***](#abstract-class) yang sama tapi memiliki fungsi yang berbeda-beda
- [**Visibility**](#visibility): Tingkat ***visibilitas*** dari sebuah object & method (**private**, **protected**, **public**)
- [**Inheritence**](#inheritance): Pewarisan dari sebuah class sehingga class yang diwarisi mewariskan semua property & method dari bapaknya kecuali yang private
- [**Constructor**](#__construct): Sebuah method didalam class yang akan langsung dijalankan ketika class tersebut di instansiasikan menjadi object
- [**Destructor**](#__destruct): Hampir sama dengan construct hanya saja dijalankan paling terakhir
 
 Berikut contoh penulisan syntax OOP sederhana dalam PHP:

 ``` php
 <?php
 class IniClass{ // huruf awal dari class wajib huruf kapital
	public $iniProperty;

	public function iniMethod(){
		// do something
	}
 }
 ```

dan cara untuk penginstansiannya:

``` php
<?php
$iniObject = new iniClass(); // instansiasikan object baru dari class 'iniClass'
$iniObject2 = new iniClass; // Tanpa buka tutup kurung '()' juga bisa

$iniObject->iniMethod() // jalankan method 'iniMethod' dari object yang dibuat dari class 'iniClass'
```

## Visibility


Tingkatan atau level dalam hal pengaksesan untuk sebuah property & method, **3 tingkat** visibility dalam OOP menentukan dimana saja property/method tersebut bisa diakses

- **Public**: Bisa diakses dimana saja termasuk diluar dari Class
- **Protected**: Hanya bisa diakses didalam class nya dan turunan dari classnya (melalui extends)
- **Private**: Hanya bisa diakses didalam class yang mendefinisikannya saja

Contoh:
``` php
<?php
class IniClass{
	public $iniPublic = 'Bisa dipanggil dimana saja';
	protected $iniProtected = 'Dipanggil di class ini dan turunannya';
	private $iniPrivate = 'Hanya bisa dipanggil di class ini';
}

$tes = new IniClass();

echo $tes->iniPublic; // Bisa dipanggil dimana saja
echo $tes->iniProtected; // Error: Cannot access protected property
echo $tes->iniPrivate; // Error: Cannot access private property
```
Property yang bisa diakses dari luar class hanyalah **Public** sedangkan **Protected** dan **Private** akan menghasilkan error jika dipanggil dari luar class

Secara default jika kita tidak menyebutkan tingkat visibility apa yang digunakan saat pendeklarasian propert atau method, maka property atau method tersebut akan menjadi **Public**

## Inheritance

Proses pewarisan untuk class. Class diwarisi akan mewariskan atau mendapatkan semua propery & method dari class yang mewarisinya, kecuali kalau sifat visibility dari property/method tersebut adalah **Private**
``` php
<?php
class Parent{
	protected $fromParent = 'berasal dari bapak';
}

class Child extends Parent{
	public function getFromParent(){
		echo $this->fromParent; // berasal dari bapak
	}
}
```
class `Child` akan dapat mengakses property `$fromParent` yang di deklarasi oleh class bapaknya berkat **Inheritance** atau pewarisan. 

**Compiler PHP pertama akan mencari property/method yang dipanggil di dalam class nya dahulu, kalau tidak ketemu makan pencarian akan naik ke class bapak nya dari yang di `extends`**

# Magic Method

Magic Method adalah method-method yang digunakan didalam OOP yang digunakan untuk menghandle suatu keadaan tertentu atau request tertentu yang diberikan, contohnya saat kita  akan menginstansiasikan object, men-set atau get value dari property dan menangani lemparan data dari post, ada magic method yang akan menanganinya. 

Semua magic method diawali dengan `__` (2 underscore) seperti yang dimiliki oleh magic method `__construct` dan `__destruct`, berikut adalah beberapa contoh magic method dan keadaan atau request terentu yang ditanganinya:

- `__construct`: Menangani keadaan saat sebuah object di instansiasikan
- `__destruct`: Menangani keadaan saat semua method atau property dalam object yang di instansiasi sudah dijalankan
- [`__set`](#__set): Menhandle suatu saat dimana dilakukannya perubahan atau set nilai property dari sebuah object, property yang di set tidak harus benar-benar ada
- `__get`; Mirip sepeti `__set` hanya saja dijalankan saat sebuah property dari sebuah object diakses
- `__isset`: Menangani saat ada keyword `isset()` atau `empty()` dipanggil terhadap suatu property dari object
- `__toString`: Dijalankan saat sebuah object di salah artikan sebagai sebuah string

Semua magic method harus di deklarasikan sebagai tipe visibility **Public**

## `__construct`

Sering juga dibilang dengan sebutan **Constructor** Sebuah magic method dalam sebuah class yang dijalankan paling awal atau yang akan langsung dijalankan ketika sebuah class di instansiasikan

``` php
<?php
class User{
	public function __construct(){
		echo 'Selamat datang di class User!';
		echo '<br>';
}

public function register(){
	echo 'user ter-register';
	}
}

$john = new User();

$john->register();
/*
Output:
Selamat datang di class User!
'user ter-register'
*/
```
method `__construct` akan otomatis dijalankan ketika ada method dari class tersebut yang dipanggil, sehingga menggunakan `__construct` cocok untuk menegeset property2 dari class di awal saat class di instansiasikan, men-load library, dll

Contoh construct yang menerima parameter:
``` php
<?php
class User{
public $Fname;
public $Lname;

// Menerima parameter saat di-instansiasikan dan menset ke property
public function __construct($fnam, $lname){
	$this->Fname = $fname;
	$this->Lname = $lname;
}

public function greetUser(){
	echo 'Selamat datang ' . $this->Fname . ' ' $this->Lname;
	}
}

$john = new User('John', 'Smith');

$john->greetUser(); // Selamat datang John Smith
```
keyword `$this->` digunakan untuk mengakses atau memanggil property/method yang berada di dalam satu class atau class yang mewariskannya

## `__destruct`

**Destructor** hampir sama dengan `__construct` hanya saja `__destruct` dijalankan di paling akhir, setelah semua method & property yang dipanggil dijalankan
``` php
<?php
class User{
	public function __construct(){
		echo 'Selamat datang di class User!';
		echo '<br>';
}

public function register(){
	echo 'user ter-register';
}

public function __destruct(){
	echo '<br>';
	echo 'Goodbye user!';
	}
}

$john = new User();

$john->register();
/*
Output:
Selamat datang di class User!
user ter-register
Goodbye user!
*/
```
Setelah semua method selesai dipanggil maka `__destruct` akan dijalankan, sehingga `__destruct` berguna untuk hal-hal seperti menutup koneksi database, dan hal lain yang perlu dilakukan diakhir

## `__set`

Sebuah magic method yang akan otomatis dijalankan **saat ada yang merubah nilai atau men-set nilai dari sebuah property dalam object**, meskipun property tersebut tidak ada yang penting ada sebuah permintaan untuk men-set nilai property.

`__set` menerima 2 parameter yaitu parameter untuk property dan value, yang akan menjadi nama variablenya dan nilai dari variablenya
``` php
<?php
class Test{
	public function __set($property, $value){
		echo 'ada yang lagi men-set nilai ' . $property . ' menjadi ' . $value;
}

$test = new Test()
$test->PropertyYangTidakAda = 'Bambang';
/*
Output:
ada yang lagi men-set nilai PropertyYangTidakAda menjadi Bambang
*/
```
`__set` berguna untuk menghandle hal-hal pengesetan nilai property, berikut contoh `__set` dalam men-set property **Private**
``` php
<?php
class Test{
	private $iniPrivate;

	 // handle yg akan dilakukanjika ada yang berusaha menset property apapun di class ini
	public function __set($property, $value){
		$this->iniPrivate = $value;
	}

	public function getPrivate(){
		echo $this->iniPrivate;
	}

}

$test = new Test();
$test->iniPrivate = 'Udah gak private lagi dong'; // Seharusnya error karena propertynya private

$test->getPrivate(); // Udah gak private lagi dong
```
## `__get`

Hampir mirip dengan `__set` hanya saja `__get` akan otomatis dijalankan **saat ada yang mengakses sebuah property dari luar class** atau dari sebuah object yang sudah di instansiasikan. Variable yang diakses juga tidak harus benar-benar ada di dalam objectnya, sama seperti `__set` yang penting adanya suatu tindakan memanggil property maka magic method `__get` akan dijalankan

`__get` hanya meneriman 1 parameter yaitu parameter nama property yang diakses atau di **get**
``` php
<?php
class Test{
	public function __get($property){
		echo 'property '. $property . ' tidak ada';
	}
}

$test = new Test();

// untuk memicu __get bisa dilakukan apa saja, yang penting ada pengaksesan property dari suatu object

$test->propertyNgasal; // property propertyNgasal tidak ada
echo $test->propertyNgasalPakeEcho; // property propertyNgasalPakeEcho tidak ada
someFunc($test->propertyNgasalJadiParameter); // property propertyNgasalJadiParameter tidak ada lalu jalankan functionnya
```
## `__isset`

Dijalankan saat ada panggilan `isset()` atau `empty()` yang dilakukan terhadap sebuah property dari sebuah object, sehingga **`__isset()` berguna untuk mengubah sifat `isset()` atau `empty()` yang digunakan terhadap property suatu object**
``` php
<?php
class Test{
	public function __isset($property){
	// Cek apakah property sudah di-set atau tidak
		if(isset($this->$property)){
			echo $property . ' sudah di set';
		}
		else{
			echo 'Maaf! property tersebut belum di set';
		}
	}
}

$test = new Test();
isset($test->gakMungkinAda) // Maaf! property tersebut belum di set
```
Yang seharusnya `isset()` hanya mengembalikan nilai boolean true atau false namun sifatnya diubah menjadi men-output pesan yang sudah dibuat di dalam magic method `__isset`

## `__toString`

Hanya akan dijalankan jika ada object instansiasi dari class yang diperlakukan seperti sebuah string artinya jika object tersebut di `echo`, di concanate dengan string lain, dsb

Sehingga magic method ini berguna untuk sebagai handling error
``` php
<?php
class Test{
	public function __toString(){
		echo 'ini bukan string woi!';
	}
}

$test = new Test();

echo $test; // ini bukan string woi!
```

# Static Property & Method

`static` adalah sebuah keyword yang diberikan pada saat pendeklarasian property atau method **sehingga property atau method tersebut bisa diakses di luar class TANPA HARUS DI INSTANSIASIKAN DAHULU**

Untuk pengaksesan property atau method static di dalam sebuah class maupun di luar class perlu digunakan **Scope Resolution Operator** (`::`)  titik dua dobel, bukan menggunakan keyword `$this->`, karena **`$this->`  berlaku untuk object yang sudah di instansiasi** sementara property dan method yang static tidak perlu di instansiasi untuk pengaksesannya

Sintaksnya adalah `<class>::<property/method>`
``` php
<?php
class User{
	public static $minimumLength = 5;

	public static function authPassword($password){
	// Cek panjang karakter password melebihi batas minimum atau tidak
		if(strlen($password) >= self::$minimumLength){
			echo 'Ukuran password diterima';
		} else{
			echo 'Ukuran password terlalu pendek!';
		}
	}
}

User::authPassword('abcd'); // Ukuran password terlalu pendek!
echo User::$minimumLength // 5
```

Selain itu yang membedakan property dan method yang static dengan property dan method biasa, **property/method static terikat dengan class nya, bukan dengan object hasil instansiasinya.**
Sehingga nilai dari sebuah property/method static akan selalu tetap, meskiupun object di instansiasikan berulang kali.

Contoh perbedaan dengan instansiasi object biasa:
``` php
<?php
// contoh biasa tanpa static
class Test{
	public $counter = 1;

	public function incCounter(){
		echo $this->counter++;
		echo <br>;
	}
}

$obj = new Test();
$obj->incCounter(); // 1
$obj->incCounter(); // 2
$obj->incCounter(); // 3

$obj2 = new Test();
$obj2->incCounter(); // 1
$obj2->incCounter(); // 2
$obj2->incCounter(); // 3

// contoh dengan static
class TestStatic{
	public static $counter = 1;

	public static function incCounter(){
		echo self::$counter++;
		echo <br>;
	}
}

$obj = new TestStatic();
$obj->incCounter(); // 1
$obj->incCounter(); // 2
$obj->incCounter(); // 3

$obj2 = new TestStatic();
$obj2->incCounter(); // 4
$obj2->incCounter(); // 5
$obj2->incCounter(); // 6
```

Nilai dari variable `$counter` akan direset kembali ketika class yang memiliki property tersebut di instansiasikan dengan object baru yang berbeda, sedangkan property `$counter` yang bersifat `static` akan selalu memiliki nilai yang tetap karena **sifat static yang terikat kepada class nya bukan objectnya**

### Scope Resolution Operator (`::`)

Operator ini bisa digunakan di dalam sebuah class dan juga di luar class sama-sama untuk mengakses property/method static.

Untuk penggunaan di luar class, `::` digunakan untuk mengakses atau menjalankan property/method static sebuah class tanpa harus menginstansiasikannya menjadi sebuah object.

Untuk penggunaan di dalam class, nama dari class yang property/method static nya ingin kita akses kita ganti dengan `self` atau `parent`
- `self::<property/method>`: Akses property/method static yang di definisikan di class yang sama
- `parent::<property/method>`: Akses property/method static yang di definisikan di class atasannya

Yang terakhir **Scope Resolution Operator** juga bisa digunakan untuk mengakses **Constant**

# Abstract Class

Berbeda dengan class biasa **Class Abstract tidak bisa di instansiasikan langsung**, class abstract harus di extends terlebih dahulu sehingga hanya class-class turunannya yang bisa di instansiasikan menjad sebuah object. Jika class abstract mendefinisikan method yang abstract maka class turunannya harus dan wajib memiliki class tersebut

**Class Abstract lebih berguna seperti sebuah *base class* atau sebuah template dan aturan-aturan untuk semua class yang mewarisinya**

Method yang di definisikan sebagai abstract dalam class abstract tidak boleh dituliskan isi nya (***body function***), isinya harus di isikan oleh class turunannya
``` php
 <?php
abstract class Animal{
	public $name;
	public $color;

	public function describe(){
		return $this->name . ' berwarna ' . $this->color;
	}

 	abstract public function sound(); // di definisikan dulu, harus ada di semua turunannya
 }

class Bebek{
 	public function describe(){
 		return parent::describe(); // Mengembalikan method 'describe' yang dimiliki atasannya
 	}

	public function sound(){ // Wajib ada karena sudah di deklarasikan di abstract classnya
		return 'kwek kwek';
	}
 }

$binatang = new Animal(); // Error!
$bebek = new Bebek();

$bebek->name = 'Donald';
$bebek->color = 'Kuning';

$bebek->describe(); // Donald berwarna Kuning
$bebek->sound(); // Kwek Kwek
 ```
Kalau ada sebuah method yang `abstract` maka class nya juga harus `abstract`

# Interface

**Interface** bersifat sedikit mirip dengan [abstract](#abstract-class) yakni tidak bisa di instansiasikan dan hanya digunakan sebagai sebuah template untuk class turunannya, yang membedakan adalah <u>**interface murni merupakan sebuah template**</u> kalau kelas abstract bisa memiliki property/method yang bukan abstract dan hanya memperlukan satu method/property yang abstract yang wajib digunakan class turunannya. **semua method yang di deklarasikan di interface wajib ada di class turunannya**

**interface juga hanya boleh berisikan deklarasi method (tidak dengan isi methodnya) dan hanya bisa bersifat public, interface juga tidak boleh memiliki property** sehingga nantinya semua class turunan dari interface harus mempunyai isi method (*body function*) yang di deklarasikan di interface 
``` php
<?php
interface Buah { // Tidak perlu menulis 'class'
	public function makan(); // hanya deklarasi saja
	public function setWarna($warna); // method yg menerima parameter
}

class Apel implements Buah { // keyword 'implements' menggantikan 'extends' untuk interface
	private $warna;

	public function makan(){
		echo 'nyamm nyam...'; // isi dari method yang di deklarasikan pada interface
	}

	public function setWarna($warna){
		$this->warna = $warna;
	}
}
```
Sifat dari interface sedikit berbeda dari class, sehingga interface tidak bisa disamakan dengan class, `extends` dan `implements` adalah 2 keyword yang bebeda, maksud dari ini adalah **sebuah class dapat mewarisi dari class lain (`extends`) dan juga mengimplementasikan (`implements`) dari sebuah interface <u>secara bersamaan</u>**. sebuah class juga bisa mengimplementasikan lebih dari 1 interface
``` php
<?php
abstract class Buah{
	protected $nama;
	protected $rasa;
	protected $warna;

	public abstract function setNama($nama);
	public abstract function setRasa($rasa);
	public abstract function setWarna($rasa);
}

interface SifatBuah{
	public function deskripsi();
}

interface InstruksiBuah{
	public function caraMakan();
}

// Pisahkan interface dengan koma (,) jika lebih dari satu
class Apel extends Buah implements SifatBuah, InstruksiBuah{
	public function setNama($nama){
		$this->nama = $nama;
	}

	public function setRasa($nama){
		$this->nama = $nama;
	}

	public function setWarna($warna){
		$this->warna = $warna;
	}
	// method yang di definisikan di interface
	public function deskripsi(){
		echo $this->nama . ' adalah buah berwarna ' $this.>warna;
	}

	public function caraMakan(){
		echo $this->nama . ' harus dikupas dahulu agar ' $this.>rasa;
	}
}

$apel = new Apel();
$apel->setNama('Apel');
$apel->setRasa('gurih');
$apel->setWarna('Merah');

$apel->deskripsi(); // apel adalah buah berwarna merah
$apel->caraMakan(); // apel harus dikupas dahulu agar gurih
```



# Final Keyword

Keyword `final` digunakan untuk melindungi sebuah class atau method agar **tidak bisa diubah oleh class pewarisnya atau anakannya yang memiliki nama method yang sama.**

Karena sifat dasarnya OOP pada PHP yang jika ada sebuah class yang di extends dan kedua class tersebut mempunyai method dengan nama yang sama, maka saat di akses dengan `$this->` PHP akan menggunakan method yang terdekat sebelum menggunakan method atasannya, tetapi tidak dengan keyword `final`
``` php
<?php
class Kucing{
	final public function suara(){
		echo 'meongg..';
	}
}

class KucingGalak extends Kucing{
	public function suara(){
		echo 'RRRAAHHSSS';
	}	
}

$joni = new KucingGalak();
$joni->suara(); // error: cannot override final method
```

Yang seharusnya `$joni->suara()` akan meng-output suara RRRAAHHSSS, tetapi karena ada method yang memiliki nama suara yang bersifat `final` php akan melemparkan error.

keyword `final` juga bisa digunakan di sebuah class untuk melindungi class tersebut agar tidak bisa di `extends`
``` php
<?php
final class Kucing{
	public function suara(){
		echo 'meong...';
	}
}

class KucingGalak extends Kucing{ // error: KucingGalak may not inherit from final class
}
```

# Type Hinting

Bisa juga disebut **Type Declaration** adalah suatu cara untuk memastikan argumen atau parameter yang diberikan ke dalam sebuah function atau method merupakan tipe data yang tepat
``` php
<?php
declare(strict_types = 1); // Men-set strict mode agar tipe data string bisa dibedakan dengan integer

function pangkat(int $nomor){
	return $nomor * $nomor;
}

$a = pangkat('bukanNomor');
echo $a; // TypeError: Argument bukanNomor passed to pangkat() must be of the type int, string given
```
Biasanya type hinting digunakan untuk memberikan argumen sebuah object atau class. Tipe-tipe data yang bisa digunakan dalam type hinting adalah:
- **array**: Harus array
- **callabe**: Harus sebuah fungsi yang **callable**
- **bool**: Harus sebuah niali boolean (true/false)
- **float**: Harus sebuah nilai float atau pecahan
- **int**: Harus sebuah nilai integer
- **string**: Harus sebuah nilai string
- **iterable**: Harus sebuah array atau **instanceOf Traversable**
- **object** / <i>\<**nama object**></i>: Harus sebuah object atau sebuah object yang spesifik
- class/interface / <i>\<**nama class**></i>: Harus instansiasi dari sebuah class atau instansiasi dari class yang spesifik
- **self**: Harus sebuah instansiasi dari class method nya dibuat. Hanya bisa digunakan di dalam method sebua class

Contoh penggunaan type hinting pada object:
``` php
<?php
class Orang{
	public $nama = 'John';
	Public $umur = 17;
}

function deskripsi(Orang $orang){ // Hanya menerima parameter object instansiasi dari class 'Orang'
	echo $orang->nama . ' berumur ' . $orang->umur . ' tahun';
}

$seseorang = new Orang();

deskripsi($seseorang); // John berumur 17 tahun
```

# Load Class

Dalam kasus nyata pembuatan aplikasi OOP dengan PHP, biasanya satu class akan dibuat di satu file lalu di instansiasikan menjadi object di file yang berbeda pula, oleh karena itu ada beberapa cara untuk men-load file yang memiliki class di dalamnya kedalam file code php lain di tempat kita akan meng-instansiasikannya

## Include & Require

Dengan menggunakan `include` atau `require` diikuti dengan file atau path file yang ingin di load oleh php, kita bisa mengakses class yang berada di file tersebut
``` php
<?php
include 'user.php' // load file users.php di directory yang sama dengan file ini
require 'auth.php' // menggunakan auth

$user = new User();
$auth = new Auth();
```

perbedaan `include` dengan `require` adalah jika file yang di load dengan `requre` tidak ditemukan, maka akan terjadi **fatal error** bahwa dan proses eksekusi kode akan berhenti sedangkan file yang tidak ditemukan dengan `include` akan tetap berjalan dan hanya akan menimbulkan **warning**

## Include once & Require once

Hampir sama dengan include & require biasa, hanya saja jika code dari file yang di load sudah pernah di load atau digunakan sebelumnya php akan menimbulkan fatal error untuk require once dan menimbulkan warning untuk include once

Hal ini berguna ketika ada file yang akan di load berulang kali dalam pengeksekusian kode, agar tidak terjadinya pendefinisian ulang variable-variable dan function
``` php
<?php
include_once 'user.php'
require_once 'auth.php'
```
## spl_autoload_register

Jika file yang perlu di load berjumlah banyak, tentu akan kurang efektif dan efisien jika kita harus menulis `require` atau `include` berulang kali, function `spl_autoload_register()` adalah sebuah function yang menerima function lain sebagai parameternya yang digunakan untuk men-load secara otomatis file-file class yang diperlukan
``` php
<?php
// load semua file di directory ini
spl_autoload_register(function ($class_name) {
    include $class_name . '.php';
});

// instansiasikan semua
$obj  = new MyClass1();
$obj2 = new MyClass2(); 
```

# Namespace

**Namespace** adalah suatu cara untuk mengelompokkan program ke dalam package tersendiri atau bisa juga dibilang **enkapsulasi** (***encapsulation***). namespace biasa digunakan oleh package-package atau library buatan orang untuk mengenkapsulasi kodenya, atau bisa juga digunakan untuk menghindari pendefinisian nama variable atau nama class yang sama.

Contoh penggunaan keyword `namespace`;
``` php
<?php
namespace App\Helpers;

class Auth{}
```
class `Auth` yang di definisikan di dalam namespace `App\Helpers` sekarang harus di instansiasikan secara lengkap menggunakan nama namespacenya
``` php
<?php
$auth = new App\Helpers\Auth;
```
Penulisan nama namespace dipisahkan oleh ***backslash*** (\) dan biasanya memiliki format *Vendor*\\*Namespace*\\*SubNamespace* (jika ada). atau bisa berupa nama directoryna

## `use` Operator

Untuk mempersingkat atau penggunaan kode atau class yang ada di dalam sebuah namespace agar tidak dilakukannya penulisan namespace yang panjang berulang-ulang, bisa digunakan keyword `use`. Contoh dengan class Auth diatas:
``` php
<?php
use App\Helpers\Auth; // nama namespace ditambah nama class dari namespace itu 

$auth = new Auth();
```
`use` juga bisa digunakan dengan sebuah alias menggunakan `as` untuk mengubah nama class yang di-`use` atau digunakan. Berikut contoh penggunaan `use` dengan penggunaan alias untuk menginstansiasi object dengan nama class yang sama:
``` php
<?php
use App\Helpers\Auth as AuthRegister;
use App\Lib\Auth as AuthSignIn; // class auth dalam namespace berbeda

$authReg = new AuthRegister();
$authSign = new AuthSignIn();
```


















  

