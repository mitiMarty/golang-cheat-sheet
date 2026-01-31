# Go Cheat Sheet

# Indice

1. [Sintassi di base](#sintassi-di-base)
2. [Operatori](#operatori)

   * [Aritmetici](#aritmetici)
   * [Di confronto](#di-confronto)
   * [Logici](#logici)
   * [Altri](#altri)
3. Todo...

# Crediti

- [A Tour of Go](http://tour.golang.org/).
- [a8m/golang-cheat-sheet](https://github.com/a8m/golang-cheat-sheet)
- Il minimo necessario per il corso di Programmazione I.


----
# Comandi da Terminale


Creare l'eseguibile
`$ go build nomeprogetto.go `

Esecuzione
`$ go run nomeprogetto.go`

Documentazione
`$ go doc nomecomando`

`$ go test -run TestNome`


---
# Sintassi di base

## Hello World

File `hello.go`:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello Go")
}
```



## Operatori

### Aritmetici

| Operatore | Descrizione         |
| --------- | ------------------- |
| `+`       | addizione           |
| `-`       | sottrazione         |
| `*`       | moltiplicazione     |
| `/`       | divisione           |
| `%`       | resto               |
| `&`       | and bit a bit       |
| `\|`      | or bit a bit        |
| `^`       | xor bit a bit       |
| `&^`      | bit clear (and not) |
| `<<`      | shift a sinistra    |
| `>>`      | shift a destra      |

### Di confronto

| Operatore | Descrizione       |
| --------- | ----------------- |
| `==`      | uguale            |
| `!=`      | diverso           |
| `<`       | minore            |
| `<=`      | minore o uguale   |
| `>`       | maggiore          |
| `>=`      | maggiore o uguale |

### Logici

| Operatore | Descrizione |
| --------- | ----------- |
| `&&`      | and logico  |
| `\|\|`    | or logico   |
| `!`       | not logico  |

### Altri

| Operatore | Descrizione                                  |
| --------- | -------------------------------------------- |
| `&`       | indirizzo / crea un puntatore                |
| `*`       | dereferenzia un puntatore                    |
| `<-`      | operatore di invio / ricezione (vedi Canali) |

## Dichiarazioni

Il tipo viene dopo l’identificatore.

```go
var foo int                  // dichiarazione senza inizializzazione
var foo int = 42             // dichiarazione con inizializzazione
var foo, bar int = 42, 1302  // dichiarazione e init multipla
var foo = 42                 // tipo omesso, inferito
foo := 42                    // shorthand, solo nei corpi delle funzioni
const constant = "This is a constant"

```

## Tipi built-in

```go
bool
string
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr
byte 
rune   
float32 float64
complex64 complex128
```

Tutti gli identificatori predefiniti sono definiti nel package [builtin](https://golang.org/pkg/builtin/).



## Conversioni di tipo

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```



## Strutture di controllo

### If

```go
if a := b + c; a < 42 {
    return a
}
```

### Cicli

In Go esiste solo `for`.

```go
for i := 0; i < 10; i++ {}
for i < 10 {}
for {}
for i,c := range s {} // i prende in input la posizione e c il carattere (della stringa o array)
```

### Switch

```go
switch os {
case "darwin":
    fmt.Println("Mac OS")
case "linux":
    fmt.Println("Linux")
default:
    fmt.Println("Altro")
}
```

---

# Array, Slice, Range

## Array

```go
var a [10]int
a := [...]int{1, 2}
```

## Slice

```go
a := []int
a = make([]int, 4)
a = append(a, 4)
s = a[2:4]//diventa una sottostringa di a che parte dalla posizione 2 alla posizione 4-1

```

## Operazioni

```go
for i, e := range a {}
```

## Mappe

```go
m := make(map[string]int)
m["key"] = 42
```


## Libreria: sort


---

# Funzioni

```go
func functionName() {}

func functionName(param1 string, param2 int) {}

func functionName(param1, param2 int) {}

func functionName() int {
    return 42
}

func returnMulti() (int, string) {
    return 42, "foobar"
}
var x, str = returnMulti()

func returnMulti2() (n int, s string) {
    n = 42
    s = "foobar"
    return
}
var x, str = returnMulti2()
```

## Funzioni come valori e closure

```go
add := func(a, b int) int {
    return a + b
}
```

Le closure sono lessicalmente scoping: possono accedere a variabili definite nello scope esterno.

## Funzioni variadiche

```go
func adder(args ...int) int {
    total := 0
    for _, v := range args {
        total += v
    }
    return total
}
```

---
# Struct

```go
type Vertex struct {
    X, Y float64
}
```

---
# Organizzazione Codice (main e packages)

## Package

* Dichiarazione del package in cima a ogni file
* Gli eseguibili sono nel package `main`
* Convenzione: nome del package = ultimo elemento del path di import
* Identificatori con iniziale maiuscola: esportati
* Identificatori minuscoli: privati

---
# Gestione stringhe

## Libreria: strconv

## Libreria: strings


---
# Gestione I/O Command Line

## os
```go
args = os.Args //args è una slice di valori di tipo strnga lette dalla barra dei comandi
```
## bufio

---
# Librerie

## Math

## Math/Rand

## time

## unicode

## strconv





---
# Cose Avanzate
## Puntatori

```go
var p *int //dichiarazione
p = &x //referenziazione
x = *p //deferenziazione
```
