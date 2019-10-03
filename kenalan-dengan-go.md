# Kenalan dengan Go

## Daftar Isi

- [Hello World](#hello-world)
- [Variable](#variable)
- [Function](#function)
- [Pointer](#pointer)

<a name="hello-world"></a>

## Hello World
Program dalam Go terbuat dari paket - paket (`package`). Dan program mulai berjalan dalam `package` bernama `main`

```
package main

import (
  "fmt"
)

func main() {
  fmt.Println("Hello World") // Hello World
}
```

<a name="variable"></a>

## Variable
Variable dalam Go dapat dideklarasikan dengan perintah `var` diikuti nama variable dan tipe data di akhir

```
package main

import (
  "fmt"
)

var name string = "John Doe"
var age int = 19

func main() {
  fmt.Println(name) // John Doe
  fmt.Println(age) // 19
}
```

Adapun cara singkat dalam medeklarasikan variabel yakni dengan statement `:=`. Dengan cara ini variabel akan secara terdeteksi tipe datanya. Namun cara ini hanya bisa dilakukan dalam fungsi

```
package main

import (
  "fmt"
)

func main() {
  name := "John Doe"
  age := 19
  
  fmt.Println(name) // John Doe
  fmt.Println(age) // 19
}
```

Dalam Go, dapat juga mendeklarasikan varible konstanta (varible yang nilainya tidak dapat diubah) dengan perintah `const`. Konstanta tidak dapat dideklarasikan dengan cara singkat seperti di atas

```
package main

import "fmt"

func main() {
	const name string = "John Doe"
  
	fmt.Println("Hello my name is", name) // Hello my name is John Doe
}
```

<a name="function"></a>

## Function
Hampir sama dengan variable. Function dalam Go dapat dideklarasikan dengan perintah `func` diikuti nama function, tanda kurung dan tipe data di akhir. Tipe data tersebut merupakan tipe data dari nilai yang di-return oleh function tersebut (jika ada nilai yang di-return)

```
package main

import (
  "fmt"
)

func greet() string {
  return "Hello world, this is my Go demo";
}

func main() {
  fmt.Println(greet()) // Hello world, this is my Go demo
}
```

Argumen juga dapat ditambahkan ke function dengan mendeklarasikan nama variable argumen diikuti tipe data dalam tanda kurung function

```
package main

import (
  "fmt"
)

func greet() string {
  return "Hello world, this is my Go demo";
}

func addAge(a int, b int) int {
  return a + b
}

func main() {
  age := 19
  
  fmt.Println(greet()) // Hello world, this is my Go demo
  fmt.Println("My age is ", addAge(age, 5)) // My age is 24
}
```

<a name="pointer"></a>

## Pointer
Go memiliki pointer. Sebuah pointer menyimpan alamat memori dari sebuah nilai. Jika di-print, alamat memori akan berbentuk hexadesimal dengan awalan 0x. Untuk menggunakan pointer diperlukan operator `*` dan `&`

Operator `&` mengambil alamat memori dari sebuah variable
```
i := 42
p = &i

fmt.Println(p) // 0x******
```

Operator `*` mengambail nilai dari alamat memori 
```
fmt.Println(*p) // 42

*p = 21         
```

```
package main

import "fmt"

func main() {
  i := 42
  p := &i         
  
  fmt.Println(p) // 0x******
  fmt.Println(*p) // 42
  
  *p = 21         
  
  fmt.Println(i)  // 21
}
```
