# Soluzioni domande aperte esercitazione 02

## Esercizio 1

A) Domanda: Quali sono il maximum branching factor e la profondità della soluzione? Calcolare le risultanti complessità di spazio e tempo (worst case) di breadth-first search

Risposta: il branching factor è b = 4, la profondità della soluzione è
d = (|x0 - xg| + |y0 - yg|), mentre le complessità di spazio e tempo sono
entrambe O(b^d).

B) La soluzione trovata da breadth-first search è sempre ottima per ogni configurazione di start, goal e celle grigie (assumendo che la soluzione esista)? Motivare la risposta

Risposta: sì, è ottima. Infatti, breadth-first search trova sempre una
soluzione ottima quando tutte le azioni hanno lo stesso costo.

C) Se si aggiungessero le azioni diagonali, ognuna di costo c > 2, sarebbe ancora garantita l’ottimalità della soluzione ritornata da breadth-first search? Motivare la risposta, e in caso negativo, fornire un algoritmo di ricerca non informata che garantisca l’ottimalità della soluzione trovata.

Risposta: No, non sarebbe ottima. Infatti, per ogni coppia di azioni
sequenziali non diagonali che agiscano su coordinate diverse, vi sarebbe un'azione
diagonale equivalente con costo maggiore. Dato che breadth-first search
non tiene conto del costo delle azioni nello scegliere il prossimo nodo
da espandere dalla frontiera, potrebbe quindi ritornare soluzioni di
profondità minima contententi azioni diagonali ma di costo non ottimale.

## Esercizio 2

A) Domanda: Qual è il limite inferiore al costo di ogni azione e il costo della soluzione ottima per la configurazione data? Calcolare le risultanti complessità di spazio e tempo (worst case) di uniform cost search

Risposta: eps = 1, C* = 6 --> O(b^(1 + floor(C*/eps)))

B) Domanda: La completezza di uniform cost search su alberi è garantita per ogni configurazione di start, goal e celle grigie (assumendo esista una soluzione)? Motivare

Risposta: sì, è garantita. Infatti uniform-cost search è completa in tutti i casi in cui non vi sono azioni a costo nullo.

C) Domanda: Se si aggiungesse l’azione None (nessun movimento, costo 0), sarebbe ancora garantita la completezza di uniform-cost search su alberi? Motivare

Risposta: no, non sarebbe più garantita in quanto vi sarebbe un'azione a costo 0.
Si noti come invece, in questo caso particolare, la versione di uniform-cost search
su grafi non soffra di questo problema: l'azione None infatti non aggiungerebbe
mai nodi alla frontiera perché già esplorati, e rimarrebbe quindi garantita
la completezza, nonostante esista l'azione None a costo 0.

## Esercizio 3

B) Domanda: Nel caso in cui la griglia non abbia confini, è ancora garantita la completezza con depth-first search? In caso negativo, fornire un algoritmo di ricerca alternativo che sia completo e non abbia complessità di spazio esponenziale (rispetto alla profondità)

Risposta: no, non è garantita: depth-first search non è completo quando gli stati possibili sono infiniti. Un'alternativa con le proprietà richieste è iterative deepening search.

# Esercizio 4

A) L'evoluzione della open list per IDS è:
```
# depth 1

# root
open = {0: [Home:0]}
# expand Home
open = {1: [Library, Market]}
# expand Library
open = {1: [Market]}
# expand Market
open = {}
# STOP: no solution, empty fringe

# depth 2

# root
open = {0: [Home]}
# expand Home
open = {1: [Library, Market]}
# expand Library
open = {1: [Market], 2: [Market, Station]}
# expand Market (depth 2)
open = {1: [Market], 2: [Station]}
# expand Station, STOP: solution found
open = {1: [Market]}
```

B) L'evoluzione delle open list e closed list per UCS è:
```
# root
open = {0: Home}
closed = {}
# expand Home
open = {2: [Library, Market]}
closed = {0: [Home]}
# expand Library
open = {2: [Market], 3: [Market], 5: [Station]}
closed = {0: [Home], 2: [Library]}
# expand Market (2)
open = {3: [Market, Bar, Library], 5: [Station]}
closed = {0: [Home], 2: [Library, Market]}
# expand Market (3): already closed
open = {3: [Bar, Library], 5: [Station]}
closed = {0: [Home], 2: [Library, Market]}
# expand Bar
open = {3: [Library], 4: [Station, Market], 5: [Station]}
closed = {Home, Library, Market, Bar}
# expand Library: already closed
open = {4: [Station, Market], 5: [Station]}
closed = {Home, Library, Market, Bar}
# expand Station, STOP: solution found
```
