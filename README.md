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
    var num float64 = 4.6789531
    fmt.Printf("%.2f",num) //stampa il numero float con solo due valori dopo il punto
    fmt.Printf("%T",num) //stampa il tipo di dato di num
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

## Matrice
```go
M = make([][]int, nRighe) //alloca prima le righe
for i := 0; i < nRighe; i++ {
    M[i] = make([]int, nColonne) //e poi le colonne
}
M[riga][colonna] = valore //assegna un valore
```

## Mappe
```go
Var m map[string]int //dichiarazione
m := make(map[string]int)
m["key"] = 42
v,ok = m["key"] //nella variabile v viene memorizzato il valore e la variabile ok è vera se all'interno di m["key"] c'è un valore, false altrimenti
delete(m, “key”) //elimina il valore associato a key
```

## Struct
```go
Var <nome struct> struct{
	<nome variabile1> <tipo>
	<nome variabile2><tipo>
}
<nome struct>.<nome variabile1> = <valore> //per assegnare alla variabile un valore o per accedere alla variabile
```

## Type
```go
Type celsius = int32 //crea un alias di un tipo
var x celsius
```

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
```go
scanner := bufio.NewScanner(os.Stdin)
for scanner.Scan() { //finisce di ciclare quando arriva a EOF
	scanner.Text() //restituisce la stringa letta 
}
```
---
# Librerie

## Math
```go
math.Abs(<numero reale>) //arrotonda il numero
math.Trunc(<numero reale>) //ritorna il valore intero del numero reale 
math.Round(<numero reale>) //ritorna l’intero arrotondato (sopra il 0.5 è il numero successivo, sotto è quello scritto)
math.Floor(<numero reale>) //arrotonda per difetto
math.Ceil(<numero reale>) //arrotonda per eccesso
math.Pow(n1, n2) //calcola la potenza con n1 alla base e n2 come esponente (entrambi float64)
math.Sqrt(<variabile>) //calcola la radice quadrata della variabile
```

## Math/Rand
```go
rand.Seed(int64(time.Now().Nanosecond())) //questa funzione fa partire il random da un seme, noi in questo caso usiamo il tempo perché cambia ogni volta che lancio il programma  
Rand.Intn(N) //genera un numero casuale da 0 a N (escluso) 
Rand.Float64() //genera un numero random float
Limite1 + rand.Float64()*(limite2-limite1) // genera un numero random con dei limiti specifici
```

## time
```go
Time.now().UnixNano() //è l’ora in cui si lancia il programma
```
## unicode
```go
unicode.IsLetter() //restituisce vero se la rune in input è una lettera
unicode.IsDigit() //restituisce vero se la rune in input è un numero
unicode.IsSpace() //restituisce vero se la rune in input è uno spazio vuoto
```
## strings
```go
S = strings.ToUpper(S) //rende la stringa tutta maiuscola
Slice := strings.Split(s, “;”) //divide una stringa in slice ogni volta che c’è un ;
strings.Contains(s, “;”) //restituisce vero se la stringa s contiene il carattere ;
string.Repeat(<variabile string>, <variabile int>) //restituisce una nuova stringa composta da un numero di coppie della variabile string (esempio se c’è a e 3 restituirà aaa)
```
## strconv
```go
strconv.Atoi(stringa) //prende in input una stringa e restituisce un valore intero e un valore di controllo, se la conversione è andata a buon fine è nil
strconv.ParseFloat(stringa, precisione del float (32 o 64)) //trasforma una stringa in un valore float
strconv.Itoa(intero) //prende in input un intero e restituisce una stringa
```
## sort
```go
sort.Strings(s) //prende in input una slice di stringhe e la restituisce ordinata
sort.Integer(i) //prende in input una slice di interi e la restituisce ordinata
```




---
# Cose Avanzate
## Puntatori

```go
var p *int //dichiarazione
p = &x //referenziazione
x = *p //deferenziazione
```
