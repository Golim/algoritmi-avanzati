# Lazy Learning

## Apprendimento Supervisionato
Nell'apprendimento supervisionato un sistema è allenato da un supervisore (insegnante) che fornisce esempi classificati. Ogni esempio è un vettore di parametri di input *x*, chiamati **features**, associati al una classificazione di output *y*.

## Nearest Neighbors
Il metodo dei nearest neighbors che funziona come segue:
1. Gli esempi classificati sono salvati senza che nessuna azione sia effettuata fino a che un nuovo modello di input richiede un valore di output. Quando arriva un nuovo modello di input, il sistema cerca in memoria l'esempio più *vicino* al nuovo modello e l'output è determinato ritornando l'output memorizzato per il modello più vicino.

## K Nearest Neighbors
E' una tecnica più flessibile e robusta, che considera un set di *k* vicini invece che uno solo.

La flessibilità è data dalla possibilità di avere tecniche di classificazione differenti:
- **Maggioranza**: l'output è quello della maggioranza dei vicini.
- **Unanimità**: l'output viene ritornato solo se tutti gli output dei k vicini sono uguali, altrimenti è sconosciuto.
- **Regressione**: serve a predire un numero reale. L'output è ottenuto come semplice media degli output dei k vicini.

## Weighted K Nearest Neighbors
L'output viene calcolato come media degli output dei k vicini, pesata con l'inverso della distanza dal nuovo input e il valore memorizzato.

Questa tecnica è semplice da implementare e spesso raggiunge bassi livelli di errore. Di contro, necessita di molta memoria e computazioni nella fase predittiva.

### Dal Brute-Force a ricerche più intelligenti
Per trovare l'esempio più vicino si può utilizzare la tecnica del *brute-force*: calcolare tutte le distanze per identificare la più piccola, in tempo O(l*d), dove *l* è l'insieme degli esempi memorizzati e *d* la dimensione dell'input.

E' possibile sviluppare metodi più veloci nei casi medi e, a volte, anche nei peggiori, investendo in *strutture dati* o accontentandosi di *risultati approssimati*.

#### Ordinare gli esempi memorizzati
Ordinando gli esempi memorizzati (alfabeticamente, per esempio) significa avere più lavoro da fare all'inizio, ma avere ricerche più velocit. Si può ad esempio usare la *ricerca binaria*.

#### Hashing
Utilizzando l'hashing è possibile ottenere un elemento memorizzato in tempo costante. L'idea è quella di prendere una chiave *k* e "tagliarla" in maniera brutale, ma **deterministica**, per ottenere un numero intero.

##### Local-Sensitive Hashing
L'hashing standard mira a randomizzare le cose, quindi l'hash di due vicini sarà molto diverso e lontano senza alcuna relazione apparente.

Il LSH è una versione specializzata di hashing, che mira a mappare elementi vicini nello stesso *bucket* con una probabilità maggiore per punti vicini rispetto a quelli lontani.

#### Alberi k-d
E' una struttura dati di space-partitioning, proposta per organizzare dei punti in uno spazio *d*-dimensionale. La radice dell'albero corrisponde all'intero spazio. Ad ogni nodo viene definito un sottoalbero destro e un sottoalbero sinistro da un test su una singola coordinata. E' molto utile per la tecnica dei nearest-neighbors.

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.