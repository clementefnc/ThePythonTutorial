# The Python Tutorial

## 0. Prefazione e Licenza

Questo lavoro di [Francesco Clemente](https://clementefnc.github.io) è rilasciato sotto licenza [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

![CC-BY-NC-SA](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)

## 1. Introduzione

Python è un linguaggio ad oggetti, **interpretato**, ideale sia per *scripting* sia per sviluppo di applicazioni.

Ha una libreria standard davvero enorme e può essere esteso con ulteriori moduli gratuitamente reperibili.

È estensibile con funzioni e tipi di dato scritti in C o C++.

Utile per automatizzare compiti, creare un piccolo DB, fare applicazioni grafiche (Tk) o giochi.

Permette di suddividere il programma in moduli che possono essere facilmente **riutilizzati** in altri programmi.

Essendo interpretato non necessita di compilazione o linking; si può utilizzare l'interprete interattivamente per testare pezzi di codice.



## 2. L'interprete Python

### Invocare l'interprete

Lanciando in una shell il comando `python` è possibile lanciare la shell interattiva di python.

Per uscire basta digitare `quit()`.

L'interprete opera in modo simile alla shell Unix: legge ed esegue i comandi interattivamente.

Un ulteriore modo di lanciare l'interprete è attraverso la sintassi `python -c comando [arg] ...` che esegue le istruzioni del *comando*.

Alcuni moduli sono utilizzati come fossero script. Possono essere invocati con `python -m module [arg] ...` che esegue il codice sorgente per il *module*.

Quando è utilizzato un file di script è a volte utile utilizzarlo in modo interattivo; ciò è possibile utilizzando il parametro `-i`.

### Passaggio di parametri

Quando viene lanciato uno script, il suo nome e gli argomenti addizionali vengono trasformati in una **lista di stringhe** ed assegnato alla variabile `argv` nel modulo `sys`. È possibile accedervi eseguendo `import sys`. La lunghezza della lista è di almeno 1 elemento; se non vengono passati nè script né parametri, `sys.argv[0]` è una stringa vuota; se viene passato il nome dello script in `sys.argv[0]` vi si troverà quest'ultimo; se si utilizza l'opzione `-c` troveremo `-c`; nel caso di `-m` ytoveremo invece il nome del modulo.



### Modalità interattiva

Nella modalità interattiva ci viene presentato un prompt primario (`>>>`) dopo il quale è possibile inserire i comandi che vogliamo python interpreti per noi. 

Se un comando si deve esprimere su più righe, quando si andrà a capo ci verrà presentato un prompt secondario (`...`).

```python
>>> terra_piatta = True
>>> if terra_piatta:
...		print("Attento a non cadere.")
Attento a non cadere.
```



### L'interprete ed il suo Environment

Di default, il codice sorgente di Python è trattato come se fosse codificato **UTF-8**.

Per dichiarare una codifica differente da quella standard è necessario inserire una prima riga speciale con la seguente sintassi:

```python
# -*- coding: encoding -*-
```

dove al posto di encoding va inserito uno dei vari *codec* supportati da Python.

Unica eccezione alla regola della prima regola è nel caso in cui il sorgente inizi con una riga *UNIX she-bang*, come nell'esempio:

```python
#!/usr/bin/env python3
# -*- coding: encoding -*-
```



## 3. Una introduzione informale a Python

I commenti in python iniziano con cancelletto `#` e comprendono tutto ciò che lo segue; un cancelletto in un literal è solo un carattere cancelletto.



### Numeri

L'interprete si comporta come una semplice calcolatrice: è possibile scrivere una espressione e lui la valuterà per noi.

Gli operatori sono gli stessi della stragrande maggioranza dei linguaggi (`+`, `-`, `*`, `/`) e si possono usare le parentesi per definire la precedenza delle operazioni.

```python
>>> 2 + 2
4
>>> 50 - 5 * 6
20
>>> (50 - 5 * 6) / 4
5.0
>>> 8 / 5 # le divisioni restituiscono sempre float
1.6
```

I numeri interi sono di tipo `int`, quelli con parte frazionaria sono di tipo `float`.

La divisione restituisce sempre un float.

Per effettuare la divisione intera (*floor division*) ed ottenere un risultato intero (troncando la parte decimale) si usa `//`; per calcolare il resto si usa `%`.

```python
>>> 17 / 3
5.666666666666667
>>> 17 // 3
5
>>> 17 % 3
2
```

È possibile utilizzare `**` per calcolare le potenze:

```python
>>> 5 ** 2
25
```

L'uguale è utilizzato per assegnare un valore ad una variabile; in tal caso nessun risultato è mostrato dopo il prompt interattivo:

```python
>>> larghezza = 20
>>> altezza = 5 * 9
>>> larghezza * altezza
900
```

Se una variabile non è "definita", provare ad utilizzarla genererà un errore:

```python
>>> n
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'n' is not defined
```

Vi è supporto completo per i numeri decimali; gli operatori con operandi di tipi diversi convertono gli interi in float:

```python
>>> 4 * 3.75 - 1
14.0
```

Nella modalità interattiva, il risultato della ultima espressione è assegnato alla variabile `_` come si può vedere nell'esempio:

```python
>>> tasse = 12.5 / 100
>>> prezzo = 100.50
>>> prezzo * tasse
12.5625
>>> prezzo + _
113.0625
>>> round(_,2)
113.06
```

La variabile `_` dovrebbe essere trattata come *read-only* dall'utente in quanto qualora le si assegnasse esplicitamente un valore si creerebbe una variabile locale con lo stesso nome mascherando quella *built-in*.

Oltre `int` e `float`, python supporta altri tipi numerici come ad esempio `Decimal` e `Fraction`. Inoltre supporta numeri complessi e l'uso del suffisso `j` o `J` per indicare la parte immaginaria (e.g. `3+5j`).



### Stringhe

Oltre ai numeri, python può manipolare le stringhe che possono essere espresse in vari modi: racchiuse in singoli apici (`'...'`) o in doppi apici (`"..."`). Il backslash `\` può essere utilizzato per fare l'escape degli apici

```python
>>> 'bella frase' # singoli apici
'bella frase'
>>> 'usare l\'apostrofo con i singoli apici' # backslash per fare l'escape dell'apice
"usare l'apostrodo con i singoli apici"
>>> "usare i doppi apici per gestire l'apostrofo"
"usare i doppi apici per gestire l'apostrofo"
```

In questo modo si può vedere che le stringhe vengono presentate con gli apici.

Per evitare questo è possibile fare stampe a schermo con la funzione `print()`.

```python
>>> "Ciao caro"
"Ciao caro"
>>> print("Ciao caro")
Ciao caro
>>> s = "Come stai?"
>>> s
"Come stai?"
>>> print(s)
Come stai?
```

Alcuni caratteri preceduti dal backslash sono interpretati come caratteri speciali, come ad esempio `\n` inserisce un carattere di *a capo*. È possibile utilizzare stringhe *grezze* inserendo una `r` prima del literal.

```python
>>> print("C:\some\name") #interpreterà la 'n' come a capo
C:\some
ame
>>> print(r"C:\some\name")
C:\some\name
```

I literal delle strinche possono essere espressi su più linee usando i *tripli-apici* o i *tripli-doppi-apici* (suona decisamente meglio in inglese); gli *a capo* sono inclusi in automatico, ma è possibile evitarlo inserendo dei backslash.

```python
print("""\
Utilizzo: qualcosa [OPZIONI]
	-a		Attiva una opzione a-osa
	-h		Mostra questo help
""")
Utilizzo: qualcosa [OPZIONI]
	-a		Attiva una opzione a-osa
	-h		Mostra questo help
```

Le stringhe possono essere concatenate con l'operatore `+` o ripetute con l'operatore `*`.

```python
>>> 2 * 'tar' + ' di tonno'
'tartar di tonno'
```

Due o più literal di stringhe giustapposte sono concatenate in automatico.

```python
>>> 'Nel mezzo' ' del cammin di nostra vita'
'Nel mezzo del cammin di nostra vita'
```

Questa funzione funziona solo con literals, non con variabili o espressioni, nel qual caso la concatenazione va fatta con il `+`.

Le stringhe si possono vedere come array di caratteri a cui si può fare accesso con indice, anche negativi per contare da destra (nota che il carattere in posizione 0 è il primo da sinistra, in posizione -1 è il primo da destra).

```python
>>> parola = 'domodossola'
>>> parola[2]
'm'
>>> parola[-1]
'a'
>>> parola [-2]
'l'
```

Oltre all'accesso indicizzato è possibile effettuare lo slicing ovvero è possibile estrarne una sottostringa.

```python
>>> parola[0:2] #dal carattere in posizione 0 a quello in posizione 2 (escluso)
'do'
>>> parola[2:5]
'mod'
>>> parola[:3] #dall'inizio fino alla pos 3 esclusa
'dom'
>>> parola[3:] #dalla pos 3 fino alla fine
'odossola'
```

Tentare di accedere ad un indice troppo grande genererà un errore, ma lo slicing funzionerà senza problemi.

```python
>>> parola[3:1241452]
'odossola'
```

Attenzione: **le stringhe sono oggetti immutabili** per cui non sarà possibile effettuare un assegnazioni per *cambiare una delle sue lettere*.

Nel caso in cui si necessiti modificare una stringa è necessario crearne una nuova.

La funzione *built-in* `len()` restituisce la lunghezza di una stringa:

```
>>> s = 'Supercalifragilistichespiralidoso'
33
```



### Liste

Python ha un numero ragguardevole di tipi di dato aggregati, utilizzati per raggruppare insieme più valori. Il più versatile è la lista che può essere rappresentata da una lista di valori separati da virgola (*elementi* o *items*) racchiusi in parentesi quadre. Le liste possono contenere dati di diverso tipo ma usualmente le si usano per dati omogenei.

```python
>>> laMiaLista = [1, 2, 3, 45, 12, 0, 3]
>>> laMiaLista
[1, 2, 3, 45, 12, 0, 3]
```

Come le stringhe e tutte i tipi *sequenza built-in*, si può accedere alle liste attraverso indici oppure ne si può effettuare lo slicing.

```python
>>> laMiaLista[1]
2
>>> laMiaLista[1:3]
[2, 3]
```

Lo slicing restituisce una nuova lista contenente gli elementi richiesti.

Questo significa che l'esempio seguente restituisce una copia della lista.

```python
>>> laMiaLista[:]
[1, 2, 3, 45, 12, 0, 3]
```

Le liste supportano inoltre la concatenazione

```python
>>> laMiaLista + [15, 62, 632]
[1, 2, 3, 45, 12, 0, 3, 15, 62, 632]
```

A differenza delle stringhe che sono immutabili, le liste sono **modificabili**.

```python
>>> cubi = [1, 8, 27, 65, 125]  # c'è un errore
>>> 4 ** 3  # il cubo di 4 è 64, non 65!
64
>>> cubi[3] = 64  # sostituiamo il valore
>>> cubi
[1, 8, 27, 64, 125]
```

È possibile anche aggiungere elementi in coda ad una lista utilizzando il *metodo* `append()`:

```python
>>> cubi.append(216)
>>> cubi.append(7 ** 3)
>>> cubi
[1, 8, 27, 65, 125, 216, 343]
```

È possibile fare assegnamenti agli *slices* e questo può persino cambiare le dimensioni della lista o cancellarla del tutto:

```python
>>> lettere = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
>>> lettere[2:5] = ['C', 'D', 'E']
>>> lettere
['a', 'b', 'C', 'D', 'E', 'f', 'g']
>>> lettere[2:5] = []
>>> lettere
['a', 'b', 'f', 'g']
>>> lettere[:] = []
>>> lettere
[]
```

La funzione *built-in* `len()` funziona anche sulle liste.

```python
>>> lettere = ['a', 'b', 'c', 'd']
>>> len(lettere)
4
```

È possibile anche innestare le liste (usare una lista come elemento di una lista):

```python
>>> a = ['a', 'b', 'c']
>>> n = [1, 2, 3]
>>> x = [a, n]
>>> x
[['a', 'b', 'c'], [1, 2, 3]]
>>> x[0]
['a', 'b', 'c']
>>> x[0][1]
'b'
```



## Controllo del flusso

Ovviamente è possibile utilizzare python per svolgere compiti molto più complessi.

### `while`

Ad esempio possiamo iniziare a scrivere una sotto-sequenza della serie di Fibonacci come segue:

```python
>>> # Serie di Fibonacci:
... # la somma di due elementi definisce il successivo
... a, b = 0, 1
>>> while a < 10:
...     print(a)
...     a, b = b, a+b
...
0
1
1
2
3
5
8
```

Questo esempio introduce svariate nuove feature:

- la prima riga contiene una *assegnazione multipla*: le variabili `a` e `b` ottengono simultaneamente i nuovi valori 0 e 1. È usato nuovamente nell'ultima riga dimostrando che l'espressione sulla destra è valutata prima di effettuare l'assegnazione; l'espressione sulla destra è valutata da sinistra a destra

- il ciclo `while` ripete il suo *corpo* fintanto che la condizione resta vera. In python, così come in C, qualsiasi valore diverso da 0 è vero; 0 è falso. La condizione può essere anche una stringa o una lista, in tal caso qualsiasi variabile aggregata è vera se contiene almento un valore, falsa se è vuota (la sua `len()` è 0). Gli operatori di confronto standard sono:

  - `<` minore di
  - `>` maggiore di
  - `==` uguale a
  - `<=` minore o uguale di
  - `>=` maggiore o uguale di
  - `!=` non uguale

- il *corpo* del ciclo è **indentato**: l'indentazione è il modo con cui python raggruppa le espressioni (*statements*). Nella shell interattiva bisogna usare o la tabulazion o spazi per ogni riga indentata; per far capire alla shell interattiva che la parte indentata è terminata, è necessario lasciare una linea bianca. È fondamentale che **ogni linea dello stesso blocco deve essere indentata dello stesso numero di spazi**.

-  la funzione `print()` scrive il valore degli argomenti che gli vengono passati come parametro; è diverso scrivere l'espressione che si vuole che stampi dal passare argomenti multipli; le stringhe sono stampate senza apici e gli spazi vengono automaticamente inseriti tra gli elementi passati come parametro, è possibile per cui scrivere cose del genere

  ```python
  >>> i = 256*256
  >>> print('Il valore di i è', i)
  Il valore di i è 65536
  ```

  Un ulteriore modo è utilizzare l'argomento *con parola chiave* `end` per evitare che venga aggiungo un *a capo* dopo ogni stampa

  ```python
  >>> a, b = 0, 1
  >>> while a < 1000:
  ...     print(a, end=',')
  ...     a, b = b, a+b
  ...
  0,1,1,2,3,5,8,13,21,34,55,89,144,233,377,610,987,
  ```