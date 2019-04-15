# Regole, alberi decisionali e foreste

## Regole
Le regole sono metodi per condensare pepite di conoscenza in un modo comprensibile per l'uomo.

Se il set di regole diventa grande, può comparire della complessità, come regole che portano a classificazioni contraddittorie. I metodi che estraggono le regole non contraddittorie sono preziosi. Invece che avere regole con precondizioni lunghe e molti test, è meglio spezzare le regole in catene di semplici domande. E' meglio posizionare le domande più informative all'inizio della sequenza, portando ad una gerarchia di domande dalla più informativa, alla meno informativa. Questo porta ad un **albero decisionale**: un arrangiamento senza contraddizioni di regole decisionali organizzato gerarchicamente. Molti alberi decisionali possono essere uniti in una **foresta decisionale** per ottenere un classificatore robusto.

### Costruire un albero decisionale
Per costruire un albero decisionale, si mette la domanda più informativa per prima e, ricorsivamente, si costruisce l'intera gerarchia di domande seguendo la stessa regola: ad ogni step si sceglie la domanda che conduce ai sottoinsiemi più puri. In generale le domande dovrebbero avere un output binario.

E' necessario avere un metodo per misurare quantitativamente la purezza, i metodi più utilizzati sono: information gain e gini impurity.

#### Information gain
L'information gain è la media della riduzione nell'entropia dopo che si conosce la risposta.

#### Gini impurity
La gini impurity misura quanto spesso un elemento scelto randomicamente dall'insieme sarebbe non correttamente classificato se fosse classificatoo randomicamente in accordo con la distribuzione delle classificazioni nel sottoinsieme. Questo metodo produce zero errori se l'insieme è puro, e un piccolo tasso d'errore se una singola classe ha la quota maggiore dell'insieme.

#### Valori mancanti
Quando si ha a che fare con dati reali, sono frequenti le mancanze di valori. Se un'istanza raggiunge un nodo e la domanda non può essere risposta perchè manca il dato, si divide l'istanza in due e si mandano le due parti nei due rami. Quando i vari pezzi dell'istanza raggiungono le foglie, si fa la media tra gli output, o si utilizzano altre tecniche decisionali.

### Costruire una foresta decisionale
L'idea di base è di usare un insieme di alberi per prendere decisioni in modo democratico. Per costruire alberi diversi si possono usare differenti set di esempi. Ogni albero isolato sarà piuttosto debole, ma la regola della maggioranza (o una media pesata) fornirà una risposta ragionevole.

#### **Bibliografia**
- Roberto Battiti, Mauro Brunato

    [The LION way. Machine Learning plus Intelligent Optimization. Version 3.0.](https://intelligent-optimization.org/LIONbook/)
    
    LIONlab, University of Trento, Italy, 2017.
