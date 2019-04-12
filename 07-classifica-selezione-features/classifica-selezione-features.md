# Classifica e selezione delle feature
Prima di iniziare ad apprendere un modello dagli esempi è necessario assicurarsi che i dati in input (**feature** o **attributi**) abbiano sufficienti informazioni per predire gli output. Inoltre, dopo che il modello è stato costruito, si potrebbe voler avere una vista approfondita per identificare gli attributi che influenzano l'output in modo significativo.

## Selezione delle feature
E' il processo di selezione di un sottoinsieme di feature rilevanti utilizzato nella costruzione del modello. Questo processo è piuttosto complesso. Se il modello è lineare, è possibile ottenere alcune informazioni *normalizzando* gli input, cioè moltiplicando gli input per dei fattori costanti in modo che il range dei valori tipici sia lo stesso (tra 0 ed 1, per esempio). Per i modelli non lineari questo processo è ancora più complicato.

E' necessario scegliere un sottoinsieme di features da utilizzare per la costruzione del modello a causa della **maledizione della dimensionalità**: se la dimensione dell'input è troppo alto, il processo di apprendimento diventa ingestibile.

Euristicamente, l'obiettivo è quello di ottenere un piccolo sottoinsieme, possibilmente vicino al più piccolo possibile, che contenga abbastanza informazioni per predire l'output, eliminando però la ridondanza. Questo permette di ridurre l'utilizzo di memoria e di migliorare la generalizzazione, inoltre permette una miglior comprensione del modello da parte di un umano.

In primo luogo, è necessario applicare le intuizioni e le conoscenze pregresse del designer. In secondo luogo, è necessario trovare un modo per stimare la rilevanza p il potere discriminatorio delle singole feature per poi proseguire con un approccio bottom-up o top-down. Il valore di una feature è relazionato ad un metodo di costruzione di un modello ed alcune tecniche di valutazione dipendono dal metodo. Esistono tre classi di metodi:
- **Wrapper methods**: sono metodi costruiti attorno ad uno specifico modello predittivo. Ogni sottoinsieme di feature viene utilizzato per allenare un modello. Le performance di generalizzazione di un modello danno un punteggio al sottoinsieme con cui è stato allenato. Questo metodo è particolarmente intenso computazionalmente, ma generalmente fornisce il miglior sottoinsieme per uno specifico modello.
- **Filter methods**: usano una misura sostitutiva al posto del tasso d'errore per dare un punteggio ad un sottoinsieme di feature. Le misurazioni utilizzate comunemente includono le informazioni reciproche e il **coefficiente di correlazione**. Molti filtri forniscono una classifica delle feature, piuttosto che un sottoinsieme esplicito di feature.
- **Embedded methods**: effettuano la selezione delle feature come parte del processo di costruzione del modello. Un esempio di questo approccio è il metodo **LASSO** per la costruzione di un modello lineare, che penalizza il coefficiente di regressione, riducendone molti a zero, di modo che la feature corrispondente possa essere eliminata. Un altro approccio è l'**eliminazione ricorsiva di feature**, usato comunemente con macchine a vettori di supporto per costruire modelli ripetutamente e rimuovere le feature con pesi bassi.

La combinazione del filtraggio e del metodo wrapper permette di procedere in maniera top-down o bottom-up:
- **Bottom-up**: si inseriscono gradualmente le feature classificate nell'ordine del loro potere discriminatorio individuale e si controlla l'effetto sulla riduzione dell'errore di output mediante un set di validazione. Il numero ottimale di feature viene determinato quando l'errore misurato sul set di validazione smette di diminuire.
- **Top-down**: si inizia con l'intero insieme di feature e si eliminano progressivamente le feature ricercando il punto con le performance ottimali, di nuovo controllando l'errore mediante un set di valutazione.

### Coefficiente di correlazione
E' un indice che esprime che esprime un'eventuale relazione di linearità tra due variabili statistiche. Il metodo più utilizzato per misurare questo coefficiente è l'indice di correlazione di *Pearson*, definito come la covarianza delle variabili divisa per il prodotto delle loro deviazioni standard.
Il coefficiente di correlazione assume che l'output sia numerico, non è quindi applicabile quando il risultato è categorico (binario).

### Tasso di correlazione
Il tasso di correlazione misura una relazione tra un input numerico ed un output categorico. L'idea di base è di dividere il vettore delle feature in classi, in accordo con l'output osservato. Se una feature è significativa, dovrebbe essere possibile identificare almeno una classe di esito in cui il valore medio della funzione è significativamente diverso dalla media di tutte le classi, altrimenti quel componente non sarebbe utile per discriminare un qualsiasi risultato.

### Test Chi Quadrato
Permette di valutare la correlazione tra due feature categoriche. Consiste nel mantenere dei contatori, contando in quanti casi si verifica (o non si verifica) un determinato evento e, dividendo questi contatori per il numero totale dei casi, si può stimare la probabilità. Se il conteggio si discosta da quello atteso per due eventi indipendenti, allora si può concludere che i due eventi sono *dipendenti* e quindi la feature è significativa per predire l'output. Si deve comunque controllare che la deviazione sia sufficientemente alta da non poter capitare per caso. Un metodo statisticamente valido per effettuare questo controllo è il *test delle ipotesi statistiche*.

#### Test delle ipotesi statistiche
E' un metodo che permette di fare delle decisioni statistiche utilizzando dati sperimentali. In statistica, un risultato è considerato *statisticamente significativo* se è improbabile che sia accaduto per caso. Le decisioni sono prese quasi sempre utilizzando il *test dell'ipotesi nulla*, che risponde alla domanda: "Assumendo che l'ipotesi nulla sia vera, qual è la probabilità di osservare un valore per la statistica del test che sia almeno estremo quanto il valore effettivamente osservato?". Se la probabilitàè troppo bassa, l'ipotesi viene rifiutata.

## Rilevanza euristica basata sui nearest neighbors
Esistono molti criteri per classificare feature individuali in accordo con la loro rilevanza in contesto con altre feature. L'algoritmo di rilevanza deriva un indice di classificazione per i problemi basato sull'algoritmo dei k-nearest neighbors. Per valutare l'indice, si identificano come prima cosa i K esempi più vicini della stessa classe (**nearest hits**) e i K esempi più vicini di una classe diversa (**nearest misses**) per ogni esempio nello spazio originale delle feature.
Poi, in proiezione sulla caratteristica *j*, viene confrontata la somma delle distanze tra gli esempi e i loro *nearest misses* con la somma delle distanze tra gli esempi e i loro *nearest hits*. L'dea è che una feature sia buona se i vicini (nello stazio originale delle feature) della stessa classe tendono ad avere valori vicini a quello della feature, mentre i vicini di una classe differente tendono ad avere valori differenti. L'approssimazione è causata dal considerare solo un determinato numero di vicini, invece che l'intero insieme.

## Entropia ed informazioni reciproche
E' possibile rendere preciso in modo statistico il criterio della *feature informativa* mediante la nozione di informazione reciproca. Una distribuzione dell'output può essere caratterizzata da un'incertezza, che può essere misurata dalla distribuzione di probabilità dell'output. Il metodo teoricamente corretto per misurare l'incertezza è l'**entropia**. Conoscendo un valore in input specifico *x*, l'incertezza nell'output può diminuire. La quantità di cui diminuisce l'incertezza nell'output quando l'input è noto è detta **informazione reciproca**. Se l'informazione reciproca è zero, conoscere l'input non fa diminuire l'incertezza nell'output e quindi la feature selezionata non può essere utilizzata da sola per predire l'output, qualsiasi sia il modello. La misura dell'informazione reciproca è molto utile per identificare le feature più promettenti, può quindi essere utilizzata nel processo di selezione delle feature.

Nella classificazione, l'informazione reciproca è relazionata ad un limite superiore e ad un limite inferiore con il **tasso d'errore di Bayes** ottimale. Questo tasso descrive il più basso tasso d'errore possibile che un classificatore può raggiungere.

L'informazione reciproca è qualitativamente differente dalla correlazione lineare: una feature può essere informativa anche senza essere correlata linearmente con l'output. Va comunque tenuto presente che avere informazioni è necessario per predire l'output, ma non è sufficiente: l'informazione deve essere estratta da tecniche di apprendimento.

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.