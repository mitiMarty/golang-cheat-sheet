# Go Cheat Sheet

# Indice

1. [Sintassi di base](#sintassi-di-base)
2. [Operatori](#operatori)

   * [Aritmetici](#aritmetici)
   * [Di confronto](#di-confronto)
   * [Logici](#logici)
   * [Altri](#altri)
3. [Dichiarazioni](#dichiarazioni)
4. [Funzioni](#funzioni)

   * [Funzioni come valori e closure](#funzioni-come-valori-e-closure)
   * [Funzioni variadiche](#funzioni-variadiche)
5. [Tipi built-in](#tipi-built-in)
6. [Conversioni di tipo](#conversioni-di-tipo)
7. [Package](#package)
8. [Strutture di controllo](#strutture-di-controllo)

   * [If](#if)
   * [Cicli](#cicli)
   * [Switch](#switch)
9. [Array, Slice, Range](#array-slice-range)

   * [Array](#array)
   * [Slice](#slice)
   * [Operazioni su array e slice](#operazioni-su-array-e-slice)
10. [Mappe](#mappe)
11. [Struct](#struct)
12. [Puntatori](#puntatori)
13. [Interfacce](#interfacce)
14. [Embedding](#embedding)
15. [Errori](#errori)
16. [Concorrenza](#concorrenza)

    * [Goroutine](#goroutine)
    * [Canali](#canali)
    * [Assiomi dei canali](#assiomi-dei-canali)
17. [Stampa](#stampa)
18. [Reflection](#reflection)

    * [Type Switch](#type-switch)
    * [Esempi](https://github.com/a8m/reflect-examples)
19. [Snippet](#snippet)

    * [Embedding di file](#embedding-di-file)
    * [Server HTTP](#server-http)

## Crediti

La maggior parte degli esempi di codice è tratta da [A Tour of Go](http://tour.golang.org/), che è un’eccellente introduzione a Go.
Se sei nuovo in Go, segui quel tour. Seriamente.

## Go in breve

* Linguaggio imperativo
* Tipizzazione statica
* Sintassi simile a C (ma con meno parentesi e senza punto e virgola) e struttura ispirata a Oberon-2
* Compila in codice nativo (nessuna JVM)
* Nessuna classe, ma struct con metodi
* Interfacce
* Nessuna ereditarietà di implementazione. Esiste però il [type embedding](http://golang.org/doc/effective%5Fgo.html#embedding)
* Le funzioni sono cittadini di prima classe
* Le funzioni possono restituire valori multipli
* Supporto alle closure
* Puntatori, ma senza aritmetica sui puntatori
* Primitive di concorrenza integrate: Goroutine e Canali

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

`$ go run hello.go`

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

// iota può essere usato per numeri incrementali, a partire da 0
const (
    _ = iota
    a
    b
    c = 1 << iota
    d
)
fmt.Println(a, b) // 1 2
fmt.Println(c, d) // 8 16
```

## Funzioni

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

### Funzioni come valori e closure

```go
add := func(a, b int) int {
    return a + b
}
```

Le closure sono lessicalmente scoping: possono accedere a variabili definite nello scope esterno.

### Funzioni variadiche

```go
func adder(args ...int) int {
    total := 0
    for _, v := range args {
        total += v
    }
    return total
}
```

## Tipi built-in

```go
bool
string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte   // alias di uint8
rune   // alias di int32 ≈ carattere Unicode

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

## Package

* Dichiarazione del package in cima a ogni file
* Gli eseguibili sono nel package `main`
* Convenzione: nome del package = ultimo elemento del path di import
* Identificatori con iniziale maiuscola: esportati
* Identificatori minuscoli: privati

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
```

### Switch

```go
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("Mac OS")
case "linux":
    fmt.Println("Linux")
default:
    fmt.Println("Altro")
}
```

## Array, Slice, Range

### Array

```go
var a [10]int
a := [...]int{1, 2}
```

### Slice

```go
a := []int{1, 2, 3}
a = append(a, 4)
```

### Operazioni

```go
for i, e := range a {}
```

## Mappe

```go
m := make(map[string]int)
m["key"] = 42
```

## Struct

```go
type Vertex struct {
    X, Y float64
}
```

## Puntatori

```go
p := &Vertex{1, 2}
```

## Interfacce

```go
type Awesomizer interface {
    Awesomize() string
}
```

## Embedding

Go non supporta l’ereditarietà, ma l’embedding di struct e interfacce.

## Errori

Niente eccezioni: gli errori sono valori restituiti.

## Concorrenza

### Goroutine

```go
go doStuff()
```

### Canali

```go
ch := make(chan int)
ch <- 42
v := <-ch
```

### Assiomi dei canali

* Invio o ricezione su un canale `nil` blocca per sempre
* Invio su canale chiuso causa panic
* Ricezione da canale chiuso restituisce il valore zero

## Stampa

```go
fmt.Println("Hello")
fmt.Printf("%d %f", 17, 17.0)
```

## Reflection

### Type Switch

```go
switch v := i.(type) {
case int:
    fmt.Println(v)
}
```

