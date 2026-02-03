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

`$ go test nomeEseguibile.go TestNome.go`


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

---
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

---
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

---

## Conversioni di tipo

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
var r rune = []rune(stringa)[0]
```

---
## Formattazione (fmt)

```go
import "fmt"

fmt.Print("Testo senza a capo")
fmt.Println("Testo con a capo finale")

// Printf: Stampa formattata (NON va a capo da solo, serve \n)
fmt.Printf("Il valore è %d\n", x)

// Sprintf: Non stampa, ma crea una stringa formattata
s := fmt.Sprintf("Risultato: %.2f", 10.555)
```

### Verbi principali per Printf

|Simbolo|Descrizione|Esempio Input|Output|
|---|---|---|---|
|**Generici**||||
|`%v`|Valore generico (ottimo se non ricordi il tipo)|`10` o `"ciao"`|`10`|
|`%+v`|**Struct con nomi campi** (Salva-vita per il debug!)|`{X:1 Y:2}`|`{X:1 Y:2}`|
|`%T`|Mostra il **Tipo** della variabile|`10`|`int`|
|**Numeri**||||
|`%d`|Intero (Base 10)|`123`|`123`|
|`%f`|Float standard (6 decimali)|`10.5`|`10.500000`|
|`%.2f`|Float arrotondato a 2 decimali|`10.567`|`10.57`|
|`%t`|Booleano|`true`|`true`|
|**Testo**||||
|`%s`|Stringa semplice|`"ciao"`|`ciao`|
|`%q`|Stringa "quotata" (con virgolette)|`"ciao"`|`"ciao"`|
|`%c`|Rune (stampa il carattere dal codice numerico)|`65`|`A`|
|`%p`|Puntatore (indirizzo di memoria)|`&x`|`0xc00...`|

---
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

### **Append**

> **Attenzione:** `append` può cambiare l'indirizzo di memoria dello slice se supera la capacità. Bisogna sempre riassegnarlo alla variabile originale.

```go
s = append(s, nuovoElemento) // Corretto
// append(s, nuovoElemento)  // SBAGLIATO (il risultato va perso)
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

### Iterazione

> **Attenzione:** Quando usi `range` su una mappa, l'ordine è **casuale**. Non dare per scontato che stampi le chiavi in ordine alfabetico o di inserimento!

```go
for k, v := range mappa {
    fmt.Println(k, v) // Ordine random
}
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


## Ricorsione

Una funzione che chiama se stessa. **Importante:** Ricordarsi sempre il _caso base_ (condizione di uscita) altrimenti il programma va in loop infinito (stack overflow).

```go
// Esempio: Fattoriale (n!)
// 5! = 5 * 4 * 3 * 2 * 1
func Fattoriale(n int) int {
    // 1. Caso Base: quando fermarsi
    if n == 0 {
        return 1
    }
    // 2. Passo Ricorsivo: chiamata a se stessa
    return n * Fattoriale(n-1)
}

func main() {
    fmt.Println(Fattoriale(5)) // Stampa 120
}
```

### Fibonacci (Ricorsivo)

La logica è:

1. **Caso Base:** Se `n` è 0 o 1, restituisci `n`.
    
2. **Passo Ricorsivo:** Altrimenti, restituisci la somma di `Fib(n-1)` e `Fib(n-2)`.
    

```go
package main

import "fmt"

// Funzione ricorsiva
func Fibonacci(n int) int {
    // Caso Base: condizione di arresto
    if n <= 1 {
        return n
    }
    // Passo Ricorsivo: chiamata a se stessa
    return Fibonacci(n-1) + Fibonacci(n-2)
}

func main() {
    // Esempio: stampiamo i primi 10 numeri della sequenza
    for i := 0; i < 10; i++ {
        fmt.Printf("%d ", Fibonacci(i))
    }
    // Output: 0 1 1 2 3 5 8 13 21 34 
}
```

---
# Struct

```go
type Vertex struct {
    X, Y float64
}
```

## Metodi (Funzioni legate alle Struct)

A differenza delle funzioni normali, il metodo ha un "ricevitore" (receiver) tra `func` e il nome.

```go
type Rettangolo struct {
    Base, Altezza float64
}

// Metodo "Area" legato alla struct Rettangolo
// (r Rettangolo) è il ricevitore. Qui è per VALORE (copia)
func (r Rettangolo) Area() float64 {
    return r.Base * r.Altezza
}

// Metodo che MODIFICA la struct
// Qui serve il PUNTATORE (*Rettangolo) altrimenti modificherei solo una copia
func (r *Rettangolo) RaddoppiaDimensioni() {
    r.Base = r.Base * 2
    r.Altezza = r.Altezza * 2
}

// Utilizzo
r := Rettangolo{10, 5}
fmt.Println(r.Area()) // 50
r.RaddoppiaDimensioni() // Ora r è {20, 10}
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
strings.TrimSpace(<variabile string>) //toglie gli spazi vuoti alla fine e all'inizio di una stringa
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
func IsPrimo(n int) bool {
    if n < 2 {
        return false
    }
    for i := 2; i*i <= n; i++ { // Ottimizzazione radice quadrata
        if n%i == 0 {
            return false
        }
    }
    return true
}
```

## Ordinamento rune
```go
func SortRunes(a []rune) {
    for i:=0;i<len(a)-1;i++{
        indiceMin := i
        for j := i + 1; j<len(a); j++ {
            if a[indiceMin] > a[j] {
            indiceMin = j
            }
        }
        a[i], a[indiceMin] = a[indiceMin], a[i]
    }
}
```

---
## Lettura da un file di testo contenuto nella stessa cartella dell'eseguibile
```go
contenuto, err := os.ReadFile("dati.txt")
if err != nil {
    fmt.Println("Errore:", err)
    return
}
// contenuto è []byte → lo trasformiamo in string
testo := string(contenuto)
fmt.Println("Contenuto del file:")
fmt.Println(testo)
```

### Defer

> Usalo subito dopo aver aperto un file per non dimenticarti di chiuderlo.

```go
f, err := os.Open("file.txt")
if err != nil { return }
defer f.Close() // Si chiuderà da solo alla fine della funzione
```

---
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

## MCD (Massimo Comune Divisore)

Algoritmo di Euclide: il più efficiente.
```go
func MCD(a, b int) int {
    for b != 0 {
        a, b = b, a%b
    }
    return a
}
```

## mcm (Minimo Comune Multiplo)

Si calcola usando la formula: `(a * b) / MCD(a, b)`.
```go
func MCM(a, b int) int {
    if a == 0 || b == 0 {
        return 0
    }
    // MCD è la funzione definita sopra
    return (a * b) / MCD(a, b)
}
```

#### Fibonacci Iterativo

Più efficiente di quello ricorsivo (O(n) invece di O(2n)), spesso richiesto per evitare stack overflow.
```go
func FibonacciIter(n int) int {
    if n <= 1 {
        return n
    }
    a, b := 0, 1
    for i := 2; i <= n; i++ {
        a, b = b, a+b
    }
    return b
}
```

## Somma delle cifre di un numero

Esempio: Input `123` -> Output `6` (1+2+3).
```go
func SumDigits(n int) int {
    sum := 0
    // Usiamo il valore assoluto se n può essere negativo
    if n < 0 { n = -n }
    
    for n > 0 {
        resto := n % 10 // Prende l'ultima cifra
        sum += resto
        n = n / 10      // Toglie l'ultima cifra
    }
    return sum
}
```

#### Palindromo (Stringhe)

Verifica se una stringa si legge uguale al contrario (es. "anna").
```go
func IsPalindrome(s string) bool {
    // Convertiamo in rune per gestire caratteri speciali/accentati
    runes := []rune(s) 
    n := len(runes)
    for i := 0; i < n/2; i++ {
        if runes[i] != runes[n-1-i] {
            return false
        }
    }
    return true
}
```

#### Minimo e Massimo in uno Slice

Trovare min e max con un solo passaggio.
```go
func MinMax(arr []int) (int, int) {
    if len(arr) == 0 {
        return 0, 0 // Gestire caso vuoto come serve
    }
    min := arr[0]
    max := arr[0]
    
    for _, v := range arr {
        if v < min {
            min = v
        }
        if v > max {
            max = v
        }
    }
    return min, max
}
```

## Eliminare l'elemento all'indice `i` (Mantenendo l'ordine)

```go
func RemoveIndex(s []int, index int) []int {
    // Prende tutto fino a i (escluso) e appende tutto da i+1 in poi
    return append(s[:index], s[index+1:]...)
}
```

## Eliminare l'elemento all'indice `i` (Veloce, senza ordine)

```go
func RemoveFast(s []int, i int) []int {
    s[i] = s[len(s)-1] // Copia l'ultimo elemento al posto di quello da eliminare
    return s[:len(s)-1] // Riduci la lunghezza di 1
}
```

## Filtrare (Es. tenere solo i pari)

```go
func FilterEven(s []int) []int {
    var result []int // Slice vuoto (nil)
    // Oppure: result := make([]int, 0, len(s)) per efficienza
    for _, v := range s {
        if v%2 == 0 {
            result = append(result, v)
        }
    }
    return result
}
```

## Ordinamento Personalizzato (Struct)

```go
import "sort"

type Studente struct {
    Nome string
    Voto int
}

func main() {
    classe := []Studente{
        {"Mario", 24}, {"Luigi", 30}, {"Anna", 18},
    }

    // Ordina per Voto CRESCENTE
    sort.Slice(classe, func(i, j int) bool {
        return classe[i].Voto < classe[j].Voto
    })

    // Ordina per Voto DECRESCENTE
    sort.Slice(classe, func(i, j int) bool {
        return classe[i].Voto > classe[j].Voto
    })
}
```

## Matrici (Operazioni classiche)

Le matrici (slice di slice) sono un classico.
```go
func SommaDiagonale(m [][]int) int {
    sum := 0
    // Assumiamo matrice quadrata N x N
    for i := 0; i < len(m); i++ {
        sum += m[i][i]
    }
    return sum
}
```

## Somma Diagonale Secondaria

La diagonale secondaria è dove riga + colonna == len-1.
```go
func SommaDiagonaleSec(m [][]int) int {
    sum := 0
    n := len(m)
    for i := 0; i < n; i++ {
        sum += m[i][n-1-i]
    }
    return sum
}
```

## Conteggio frequenza caratteri (Istogramma)

Fondamentale per verificare anagrammi o trovare la lettera più frequente.
```go
func ContaCaratteri(s string) map[rune]int {
    conteggio := make(map[rune]int)
    for _, char := range s {
        conteggio[char]++
    }
    return conteggio
}
// Esempio uso: "banana" -> {'b':1, 'a':3, 'n':2}
```

## Cifrario di Cesare (Shift di lettere)

Spesso chiedono di "spostare le lettere di k posizioni".
```go
func CaesarCipher(s string, k int) string {
    runes := []rune(s)
    for i, r := range runes {
        if r >= 'a' && r <= 'z' {
            // Logica: portiamo a base 0, shiftiamo, modulo 26, riportiamo a base 'a'
            runes[i] = 'a' + (r-'a'+rune(k))%26
        } else if r >= 'A' && r <= 'Z' {
            runes[i] = 'A' + (r-'A'+rune(k))%26
        }
    }
    return string(runes)
}
```

## Anagramma

Due stringhe sono anagrammi se hanno gli stessi caratteri nelle stesse quantità.
```go
func IsAnagram(s1, s2 string) bool {
    if len(s1) != len(s2) { return false }
    m1 := ContaCaratteri(s1) // Vedi funzione sopra
    m2 := ContaCaratteri(s2)
    
    // reflect.DeepEqual(m1, m2) è lento, meglio il controllo manuale in esame:
    for k, v := range m1 {
        if m2[k] != v {
            return false
        }
    }
    return true
}
```