# Modelli basati sulla fattorizzazione della matrice

**Nota**: questo intero capitolo **non** sarà richiesto all'esame.

## Filtraggio e raccomandazione collaborativa
E' un metodo per predire gli interessi di una persona raccogliendo informazioni riguardanti il gusto da molte altre persone che collaborano. L'assuzione di base è che che coloro che hanno concordato su qualcosa in passato, tenderanno a concordare di nuovo in futuro.

Ad esempio, si può considerare una matrice *R* utenti-elementi, dove ogni entry alla posizione *ui* è il voto di un utente *u* per un elemento *i*. Il voto deve essere compreso tra un valore minimo ed uno massimo. Un voto è predetto utilizzando una media pesata dei voti degli altri utenti, dove i pesi sono dati dalla somiglianza. La motivazione per questa tecnica è che utenti simili tendono a dare voti simili. La **somiglianza** tra due utenti è calcolata misurando la somiglianza tra due vettori, che sono le righe della matrice *R* corrispondenti ai due utenti.

Va tenuto conto però che le persone hanno modi di esprimere le opinioni molto differenti: dai più critici ai più esagerati positivamente. Per questo, può essere utile tarare le valutazioni individuali prima di usarle per misurare la somiglianza ed ottenere predizioni.

Dato che i voti non sono centrati in zero, il sistema potrebbe avere difficoltà nel riprodurre i voti. Per aiutare il sistema, può essere utile *centrare* i dati sottraendo il valore della media.

## Fattorizzazione della matrice
La sparsità della matrice utente-elemento grezzia può essere un problema, dato che ogni utente valuterà solo un piccolo sottoinsieme di elementi e la maggior parte delle entry risulteranno sconosciute. Comprimendo e riassumento le caratteristiche di un utente in un vettore più piccolo, si spera di ottenere dei risultati più generalizzati e, possibilmente, una migliore comprensione del modello.

Un possibile metodo per determinare l'interesse o il voto di un utente perun elemento è di associare un piccolo *vettore di caratteristiche* con con ognin utente e con ogni elemento e derivando i voti osservando la somiglianza tra l'utente e i vettori delle caratteristiche dell'elemento.

### Aggiungere i bias
Alcuni utenti tendono a dare voti più alti ed alcuni elementi ricevono spesso voti più alti di altri. Si può quindi stimare un valore di bias sia per l'elemento stesso che per l'utente. Ad esempio, Titanic tende ad essere votato *0.5* sopra la media e Joe, un utente molto critico, tende a votare *0.3* sotto la media. Se il voto medio per tutti i film è *3.7*, la stima di base del voto di Joe per Titanic sarà *3.7 + 0.5 - 0.3 = 3.9*.

Per essere più precisi, un voto può essere spezzato in quattro componenti:
- Media globale.
- Bias dell'elemento.
- Bias dell'utente.
- Interazione utente-elemento.

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.