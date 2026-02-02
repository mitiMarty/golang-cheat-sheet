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
for i := 0; i < 10; i++ {} // for solito
for ; i < 10 {} // while
for i < 10 {} // si può omettere ; se c'è una sola condizione
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

# Array, Slice, Matrici, Mappe

## Array

```go
var a [10]int // array di lunghezza 10
a[3] = 42 // setta l'elemento di indice 3 al valore 42
i := a[3] // legge l'elemento di indice 3

// dichiara e inizializza
var a = [2]int{1, 2} // array di due elementi inizializzato a (1,2)
a := [2]int{1, 2} // come prima ma abbreviato
a := [...]int{1, 2} // ... il compilatore si rende conto della lunghezza
```

## Slice
Uno slice è come un array ma la lunghezza non è specificata

```go
a := []int // dichiaro uno slice di interi
var a = []int{1,2,3,4} // dichiaro e inizializzo uno slice
a := []int{1,2,3,4} // versione abbreviata
chars := []string{ 0:"a", 2:"c", 1:"b"} // ["a","b","c"]

s = a[2:4]//diventa una sottostringa di a che parte dalla posizione 2 alla posizione 4-1
s = a[:3] // se non dichiaro l'indice a sinistra parte da 0
s = a[2:] // se non indico l'indice a destra va fino a len(a)-1

// Creare un array con il make
a = make([]int, 4) // il numero è la lunghezza
a = append(a, 4)

// Creare uno slice partendo da un array
x := [3]string{"uno","due","tre"}
s := x[:] // copia il contenuto di x in uno slice

```

## Matrici
```go
M = make([][]int, nRighe) //alloca prima le righe
for i := 0; i < nRighe; i++ {
    M[i] = make([]int, nColonne) //e poi le colonne
}
M[riga][colonna] = valore //assegna un valore
var a [3][2]int = [3][2]int{{1, 2}, {10, 20}, {100, 200}} //viene creata e vengono assegnati i valori

```

## Mappe
```go
Var m map[string]int //dichiarazione
m := make(map[string]int) //allocazione
m["key"] = 42 //assegnazione di un valore
v, ok = m[“key”] //leggo il valore nella variabile v, e la variabile di controllo ok è vera se quella chiave è stata associata ad un valore, falsa altrimenti
delete(m, “key”) //elimina il valore contrassegnato dal nome key
```

---

# Funzioni

```go
// no argomenti
func functionName() {}

// due argomenti 
func functionName(param1 string, param2 int) {}

// argomenti multipli dello stesso tipo int
func functionName(param1, param2 int) {}

// no argomenti e dichiarazione del return type
func functionName() int {
    return 42
}

// no argomenti, return type può essere più di un valore
func returnMulti() (int, string) {
    return 42, "foobar"
}
var x, str = returnMulti()

// le variabili di return possono essere nominate nella dichiarazione
func returnMulti2() (n int, s string) {
    n = 42
    s = "foobar"
    return
}
var x, str = returnMulti2()
```

## Funzioni come valori e closure
Una funzione può essere anche definita come una variabile di tipo func
```go
func main() {
    // add è una variabile di tipo funzione
    add := func(a, b int) int {
        return a + b
    }
    // basta usare il nome per chiamare la funzione
    fmt.Println(add(3, 4))
}

```

Le closure sono lessicalmente scoping: possono accedere a variabili definite nello scope esterno.



Closures, lexically scoped: 
le funzioni possono accedere a valori che erano nello scope quando si stava definendo la funzionen

```go
func scope() func() int{
    outer_var := 2
    foo := func() int { return outer_var}
    return foo
}

func another_scope() func() int{
    // ERRORE: non compila perchè outer_var e foo non sono definite in questo scope
    outer_var = 444
    return foo
}
```

Closures: non mutare le outer_var, è meglio ridefinire le variabili esterne 
```go
func outer() (func() int, int) {
    outer_var := 2       // NOTE outer_var è fuori dallo scope interno
    inner := func() int {
        outer_var += 99  // prova a mutare outer_var
        return outer_var // => 101 (ma outer_var è nuovamente ridefinita come una variabile visibile solo nello scope interno
    }
    return inner, outer_var // => 101, 2 (invariato!)
}
```

## Funzioni variadiche
usando  ... prima del type name dell'ultimo paramento significa che può prendere un numero variabile (anche zero) di input di quel tipo.


```go
func adder(args ...int) int {
    total := 0
    for _, v := range args {
        total += v
    }
    return total
}
```
 
La funzione è invocata sempre nello stesso modo solo che ora puoi passare il numero di argomenti che vuoi.



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
```go
strconv.Atoi(stringa) //prende in input una stringa e restituisce un valore intero e un valore di controllo, se la conversione è andata a buon fine è nil
strconv.ParseFloat(stringa, precisione del float (32 o 64)) //trasforma una stringa in un valore float
strconv.Itoa(intero) //prende in input un intero e restituisce una stringa
```
## Libreria: strings
```go
S = strings.ToUpper(S) //rende la stringa tutta maiuscola
Slice := strings.Split(s, “;”) //divide una stringa in slice ogni volta che c’è un ;
strings.Contains(s, “;”) //restituisce vero se la stringa s contiene il carattere ;
string.Repeat(<variabile string>, <variabile int>) //restituisce una nuova stringa composta da un numero di coppie della variabile string (esempio se c’è a e 3 restituirà aaa)
strings.Fields(<variabile string>) //elimina automaticamente gli spazi vuoti
```

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
## sort
```go
sort.Strings(s) //prende in input una slice di stringhe e la restituisce ordinata
sort.Ints(i) //prende in input una slice di interi e la restituisce ordinata
sort.Sort(sort.Reverse(sort.IntSlice(numeri))) //restituisce una slice in ordine decrescente
```
## reflect
```go
reflect.DeepEqual(a, b) //restituisce true se la slice a è uguale alla slice b
```


---
# Cose Avanzate
## Puntatori

```go
var p *int //dichiarazione
p = &x //referenziazione
x = *p //deferenziazione
```
---
# Pezzi di codice che possono tornare utili 
## Numeri primi
```go
func ÈPrimo(n int) bool {
	for i:=2;i*i<=n;i++ {
		if n%i==0{
			return false
		}
	}
	return true
}
```

## Selezione di più stringhe da riga di comando
```go
func main() {
	parole := os.Args[1:]	// Creo una slice di stringhe: parto da 1, args[0] è il nome del programma

	if len(parole) == 0 {
		return	// Se ci son 0 stringhe, return
	}

	for i, parola := range parole {    // i = indice stringa (Es: 1), parola = valore stringa ("Es: ciao")
		// Codice richiesto...
	}
	fmt.Println()
}
```

## Iterazione su chars (da stringa)
```go
chars := []rune(parola)

for i := range chars {
	if i%2 == 1 {	// Converte caratteri alternati
		chars[i] = unicode.ToUpper(chars[i])	// a -> A
	}
}
```


	
