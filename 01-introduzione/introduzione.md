# Introduzione

## Ottimizzazione intelligente
L'ottimizzazione è un processo per migliorare continuamente processi, decisioni, prodotti e servizi. E' correlato al processo decisionale, ma va oltre: il processo decisionale prende la miglior soluzione da un'insieme di soluzioni date, l'ottimizzazione **crea** attivamente nuove soluzioni.

Quasi tutti i problemi di business possono essere formulati come trovare la decisione ottimale *x*, massimizzando una misura *goodness(x)* (bontà). Formalizzare un problema in questo modo incoraggia ad utilizzare obiettivi quantificabili, a capire gli intenti in modo misurabile e a focalizzarsi sulle policies, piuttosto che sui dettagli implementativi.

L'automazione è la chiave: una volta che è stato formulato il problema, si manda il modello di bontà ad un computer, che creerà e cercherà una o più scelte ottimali.

L'esistenza di una funzione matematica da ottimizzare è, però, anche un limite che blocca l'adozione globale di questa tecnica.

### Machine Learning
Il Machine Learning obbliga a rinunciare ad un obiettivo *goodness(x)* chiaramente specificato: il modello di bontà può essere costruito dal Machine Learning da **dati abbondanti**.

I **dati** possono essere creati dalla storia passata dell'ottimizzazione o da feedback dei decision makers.

#### Kriging
E' una tecnica basata sull'idea che il valore di output di un punto sconosciuto debba essere la **media** dei valori vicini conosciuti, pesati in base alla loro distanza dal punto sconosciuto.

## Analisi Descrittiva
L'analisi descrittiva è utile per registrare e visualizzare le performance storiche.

Risponde alla domanda: *Cos'è successo?*

## Analisi Predittiva
L'analisi predittiva è utile per cercare di anticipare l'effetto di una decisione.

Risponde alla domanda: *Cosa potrebbe succedere?*

## Analisi Prescrittiva
L'analisi prescrittiva conduce dai dati direttamente al miglior piano di miglioramento, dai dati, alle informazioni utili, alle azioni.

Risponde alla domanda: *Cosa dovremmo fare?*

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.