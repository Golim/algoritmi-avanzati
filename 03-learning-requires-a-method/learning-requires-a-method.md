# Learning Requires a Method
Il vero apprendimento è associato a:
- Estrarre le relazioni profonde e fondamentali in un fenomeno.
- Riassumere una vasta gamma di eventi attraverso modelli compatti.
- Unificare diversi casi, scoprendo le leggi esplicative sottostanti.

L'apprendimento per esempi è un mezzo per raggiungere l'obiettivo della **generalizzazione**: la capacità di spiegare nuovi casi non incontrati durante la fase di apprendimento, predicendo nuovi output, nella stessa area di applicazione. Se l'obiettivo è la generalizzazione, è necessario stimare le performance in maniera molto accurata. Osservare il comportamento del modello sugli esempi di apprendimento non garantisce una corretta generalizzazione e può condurre ad un ottimismo ingiustificato.

Le **feature** sono proprietà misurabili individualmente di un fenomeno osservato, hanno informazioni utili a derivare il valore di output.

### Classificazione
Nella **classificazione**, l'output è un codice adatto per la classe. L'output *y* appartiene ad un insieme finito di possibili output.

### Regressione
Nella **regressione**, l'output è un numero reale e l'obiettivo è quello di modellare una relazione tra una variabile dipendente (l'output *y*) e una o più variabili indipendenti (le feature di input *x*). Questo porta ad una maggiore **flessibilità**  per l'utilizzo pratico di sistemi di classificazione.

## Apprendimento da esempi classificati
L'apprendimento supervisionato utilizza gli esempi per costruire un'associazione (una funzione) *y = f(x)* tra l'input *x* e l'output *y*. L'associazione è selezionata all'interno di un modello flessibile *f(x, w)*, dove la flessibilità è data da qualche parametro impostabile *w*. La forza del Machine Learning è la capacità di impostare automaticamente i migliori parametri interni tramite l'ottimizzazione, ricevendo una serie di coppie input-output di esempio corrette.

Nel processo di ottimizzazione, viene definita una misura di errore che deve essere minimizzata. Una misura di errore adatta è la somma degli errori tra la risposta corretta (data dagli esempi classificati) e l'output previsto dal modello. Gli errori possono essere considerati come valori assoluti, oppure essere elevati al quadrato. La somma degli errori al quadrato è la misura di errore più utilizzata nel Machine Learning. Se l'errore è *zero*, il modello lavora correttamente sugli esempi dati. Più piccolo è l'errore, migliore è il comportamento medio sugli esempi. L'apprendimento supervisionato diventa quindi un problema di minimizzazione di una specifica funzione d'errore, dipendente su dei parametri *w*.

Se la funzione da ottimizzare è *differenziabile*, un semplice approccio può essere l'utilizzo della *discesa del gradiente*. Consiste nell'iterare calcolando il gradiente della funzione rispetto ai pesi e prendendo piccoli passi in direzione del gradiente negativo.


- Una funzione è **differenziabile** in un punto se può essere approssimata, cioè tutte le derivate parziali calcolate nel punto devono esistere.
- Il **gradiente** di una funzione è il vettore che ha come componenti le derivate parziali della funzione.

### Bias-variance dilemma
Il bias-variance dilemma può essere descritto come segue:
- I modelli con troppo pochi parametri sono inaccurati a causa di grandi bias: non sono flessibili.
- I modelli con troppi parametri sono inaccurati a causa della grande varianza: sono troppo sensibili ai dettagli degli esempi, variazioni nei dettagli degli esempi portano a grandi variazioni.
- Identificare il modello migliore necessita di controllare la complessità del modello: identificare la giusta architettura e il giusto numero di parametri, per raggiungere il giusto compromesso tra bias e varianza.

## Apprendere, validare, testare
Quando si apprende per esempi classificati è necessario seguire procedure sperimentali accurate per misurare l'efficacia del processo di apprendimento. E' un errore imperdonabile valutare le performance di un sistema di apprendimento sugli stessi esempi usati per il training. L'obiettivo è quello di produrre un sistema capace di **generalizzare** su nuovi dati mai visti prima, altrimenti il sistema non sta apprendendo, ma sta memorizzando un insieme di pattern conosciuti.

E' quindi necessario avere un grande numero di esempi per allenare il sistema, ma un ancora più grande numero di nuovi dati da usare per il testing.

Se il numero di esempi classificati forniti è troppo piccolo, è necessario trovare un buon modo per partizionarli in due sottoinsiemi: uno per il training e uno per il testing.

### Cross-validation
E' un metodo generalmente applicabile per prevedere le performance di di un modello su un set di convalida utilizzando esperimenti ripetuti, anzichè analisi matematiche. L'idea è quella di ripetere molti esperimenti di allenamento e testing, utilizzando diverse partizioni del set di esempi originale in due sottoinsiemi, uno per il training ed uno per il testing, e calcolando la media dei risultati.

#### K-fold cross-validation
E' un implementazione della cross-validation, che prevede il partizionamento del set di esempi originale in *K* partizioni:
- *K - 1* utilizzate per il training.
- *1* utilizzata per la convalida.

Il processo è poi ripetuto K volte, utilizzando per la convalida ognuno dei K sottoinsiemi una sola volta.

#### Cross-validation stratificata
E' un miglioramento che permette di evitare di avere difersi equilibri di una classe nel set di training rispetto al set di convalida.

## Errori
Quando si misurano le performance di un modello, si possono incontrare diversi tipi di errore. Dipendentemente dal problema, i criteri per decidere la miglior classificazione possono cambiare. Se la classificazione è binaria, si possono utilizzare come criteri l'accuratezza, la precisione e il recupero.

### Accuratezza
E' la proporzione tra i risultati veri forniti dal classificatore (veri positivi e veri negativi) e il numero di elementi appartenenti alla classe positiva.

### Precisione
Il numero di elementi correttamente classificati con la classe corretta (veri positivi) diviso per il numero di elementi classificati come positivi (veri positivi e falsi positivi).

`precisione = veri positivi / (veri positivi + falsi positivi)`

### Recupero
Il numero di veri positivi diviso per il numero di elementi che che appartengono effettivamente alla classe positiva.

`precisione = veri positivi / (veri positivi + falsi negativi)`

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.
