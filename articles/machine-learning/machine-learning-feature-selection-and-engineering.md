---
title: Progettazione e selezione di funzioni in Azure Machine Learning | Documentazione Microsoft
description: "Illustra le finalità della progettazione e della selezione di funzioni e fornisce esempi del relativo ruolo nel processo di miglioramento dei dati di Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: TRUE
ms.openlocfilehash: 51a5d8fed492cb9301e048c2b6a721e4573a47d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Progettazione e selezione di funzioni in Azure Machine Learning
Questo argomento illustra le finalità della progettazione e selezione di funzioni nel processo di miglioramento dei dati di Machine Learning. Descrive cosa comportano questi processi usando gli esempi forniti da Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

I dati di training usati in Machine Learning spesso possono essere migliorati con la selezione o l'estrazione di funzioni dai dati non elaborati raccolti. Un esempio di funzione progettata nel contesto dell'apprendimento della modalità di classificazione delle immagini dei caratteri scritti a mano è una mappa della densità di bit costruita dai dati di distribuzione dei bit non elaborati. La mappa può essere utile per individuare in modo più efficiente i bordi dei caratteri.

Le funzioni progettate e selezionate migliorano l'efficienza del processo di training che tenta di estrarre le informazioni essenziali contenute nei dati. Migliorano anche le potenzialità di questi modelli per la classificazione accurata dei dati di input e per la stima più affidabile dei risultati di interesse. Progettazione e selezione delle funzioni possono anche combinarsi per rendere l'apprendimento più computazionalmente trattabile. Questa operazione viene eseguita tramite il miglioramento e la successiva riduzione del numero di funzioni richieste per calibrare o eseguire il training di un modello. Da un punto di vista matematico, le funzioni selezionate per eseguire il training di un modello sono costituite da un set minimo di variabili indipendenti che spiegano i modelli nei dati e quindi stimano correttamente i risultati.

La progettazione e selezione delle funzioni fanno parte di un processo più ampio, costituito in genere da quattro passaggi:

* Raccolta dei dati
* Miglioramento dei dati
* Costruzione del modello
* Post-elaborazione

Progettazione e selezione costituiscono il passaggio di miglioramento dei dati in Machine Learning. Per le finalità di questo documento, si possono distinguere tre aspetti di questo processo:

* **Pre-elaborazione dei dati**: questo processo tenta di assicurare che i dati raccolti siano puliti e coerenti. Include attività come integrazione di più set di dati, gestione di dati mancanti, gestione di dati incoerenti e conversione di tipi di dati.
* **Progettazione di funzionalità**: questo processo tenta di creare altre funzioni rilevanti dalle funzioni non elaborate esistenti nei dati e di aumentare le potenzialità predittive dell'algoritmo di apprendimento.
* **Selezione di funzionalità**: questo processo seleziona il subset principale delle funzionalità dei dati originali per ridurre la dimensionalità del problema di training.

Questo argomento tratta solo gli aspetti relativi a progettazione e selezione di funzioni del processo di miglioramento dei dati. Per maggiori informazioni sul passaggio di pre-elaborazione dei dati, guardare il video relativo alla [pre-elaborazione dei dati in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) .

## <a name="creating-features-from-your-data--feature-engineering"></a>Creazione di funzioni dai dati: progettazione di funzioni
I dati di training sono costituiti da una matrice composta da esempi (record o osservazioni archiviate in righe), ognuno dei quali presenta un set di funzioni (variabili o campi archiviati in colonne). Le funzioni specificate nella progettazione sperimentale caratterizzeranno i modelli nei dati. Anche se molti dei campi dati non elaborati possono essere inclusi direttamente nel set di funzioni selezionate usato per il training di un modello, spesso devono essere costruite altre funzioni (progettate) dalle funzioni presenti nei dati non elaborati per generare un set di dati di training avanzato.

Il tipo di funzioni da creare per migliorare il set di dati durante il training di un modello sono le funzioni progettate che migliorano il training e forniscono informazioni che consentono di differenziare meglio i modello nei dati Le nuove funzioni dovrebbero fornire informazioni aggiuntive che non vengono chiaramente acquisite o non risultano facilmente apparenti nel set di funzioni originali o esistenti, ma questo processo è una sorta di artificio. Le decisioni valide e produttive richiedono spesso una certa esperienza specifica.

Quando si inizia a usare Azure Machine Learning, è più facile afferrare questo processo in modo concreto tramite gli esempi disponibili in Machine Learning Studio. Di seguito ne vengono presentati due:

* Un esempio di regressione basato sulla [stima del numero di noleggi di biciclette](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) in un esperimento controllato in cui sono noti i valori di destinazione.
* Un esempio di classificazione di data mining del testo tramite [Feature Hashing][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Esempio 1: Aggiunta di funzioni temporali per il modello di regressione
Per dimostrare come progettare le funzioni per un'attività di regressione, si userà l'esperimento "Demand forecasting of bikes" in Azure Machine Learning Studio. L'obiettivo di questo esperimento è stimare la domanda di biciclette, ovvero il numero di noleggi di biciclette nell'arco di un mese, un giorno o un'ora specifica. Come dati di input non elaborati si usa il set di dati **Bike Rental UCI data set**.

Questo set di dati si basa su dati reali della società Capital Bikeshare che gestisce una rete di noleggio di biciclette a Washington DC, negli Stati Uniti. Il set di dati rappresenta il numero di noleggi di biciclette in un'ora specifica del giorno dal 2011 al 2012 e include 17.379 righe e 17 colonne. Il set di funzioni non elaborate include le condizioni meteorologiche (temperatura, umidità, velocità del vento) e il tipo di giorno (festività o giorno feriale). Il campo per la stima è **cnt**, un conteggio che rappresenta i noleggi di biciclette in un'ora specifica e compreso nell'intervallo da 1 a 977.

Per costruire funzioni efficaci nei dati di training, vengono compilati quattro modelli di regressione con lo stesso algoritmo, ma con quattro diversi set di dati di training. I quattro set di dati rappresentano gli stessi dati di input non elaborati, ma con un numero crescente di set di funzioni. Queste funzioni sono raggruppate in quattro categorie:

1. A = funzioni meteo + festività + giorno feriale + fine settimana per la giornata prevista.
2. B = numero di biciclette noleggiate in ognuna delle 12 ore precedenti.
3. C = numero di biciclette noleggiate in ognuno dei 12 giorni precedenti alla stessa ora.
4. D = numero di biciclette noleggiate in ognuna delle 12 settimane precedenti nello stesso giorno e alla stessa ora.

Oltre al set di funzioni A, che esiste già nei dati non elaborati originali, gli altri tre set di funzioni vengono creati tramite il processo di progettazione delle funzioni. Il set di funzioni B acquisisce la domanda di biciclette recente. Il set di funzioni C acquisisce la domanda di biciclette in un particolare orario. Il set di funzioni D acquisisce la domanda di biciclette in un particolare orario e giorno della settimana. Ognuno dei quattro set di dati di training include rispettivamente il set di funzioni A, A+B, A+B+C e A+B+C+D.

Nell'esperimento di Azure Machine Learning questi quattro set di dati vengono creati dai quattro rami del set di dati di input pre-elaborati. Ad eccezione del ramo più a sinistra, ogni ramo contiene un modulo [Execute R Script][execute-r-script], in cui un set di funzioni derivate (set B, C e D) viene rispettivamente costruito e aggiunto al set di dati importato. La figura seguente illustra lo script R usato per creare il set di funzioni B nel secondo ramo a sinistra.

![Creazione di un set di funzioni](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

La tabella seguente riepiloga il confronto dei risultati delle prestazioni dei quattro modelli. I risultati migliori vengono forniti dalle funzioni A+B+C. Si noti che il tasso di errore diminuisce quando si include un set di funzioni aggiuntivo nei dati di training. Ciò verifica la stima secondo cui i set di funzioni B e C forniscono altre informazioni rilevanti per l'attività di regressione. L'aggiunta del set di funzioni D non sembra fornire un'altra riduzione del tasso di errore.

![Confronto dei risultati delle prestazioni](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> Esempio 2: Creazione di funzioni per il data mining del testo
La progettazione di funzioni viene ampiamente applicata nelle attività correlate al data mining del testo, ad esempio la classificazione di documenti e l'analisi del sentiment. Ad esempio, quando si vogliono classificare documenti in diverse categorie, un tipico presupposto è il fatto che le parole o le frasi incluse in una categoria di documenti sono presenti con minore probabilità in un'altra categoria di documenti. In altre parole, la frequenza di distribuzione di parole o frasi è in grado di caratterizzare diverse categorie di documenti. Nelle applicazioni di data mining del testo per creare le funzioni che comportano frequenze di parole o frasi è necessario usare il processo di progettazione delle funzioni, poiché singole parti del contenuto di testo vengono in genere usate come dati di input.

Per completare questa attività, si applica una tecnica definita *hashing di funzioni* per trasformare in modo efficiente le funzioni di testo arbitrarie in indici. Anziché associare ogni funzione di testo (parole o frasi) a un indice particolare, questo metodo applica una funzione hash alle funzioni e usa direttamente i relativi valori hash come indici.

In Azure Machine Learning è disponibile un modulo [Feature Hashing][feature-hashing] che crea queste funzioni basate su parole o frasi. La figura seguente mostra un esempio dell'uso di questo modulo. Il set di dati di input contiene due colonne: la classificazione dei libri da 1 a 5 e il contenuto effettivo della recensione. L'obiettivo del modulo [Feature Hashing][feature-hashing] è quello recuperare nuove funzioni che mostrino la frequenza di occorrenza delle parole o frasi corrispondenti nella recensione di un libro particolare. Per usare questo modulo, è necessario completare i passaggi seguenti:

1. Selezionare la colonna che contiene il testo di input (**Col2** in questo esempio).
2. Impostare *Hashing bitsize* (Dimensione bit di hashing) su 8, che equivale alla creazione di 2^8=256 funzioni. Per le parole o frasi nel testo viene generato un hash per 256 indici. Il parametro *Hashing bitsize* (Dimensione bit di hashing) è compreso nell'intervallo da 1 a 31. Se il parametro è impostato su un numero più elevato, è meno probabile che per le parole o le frasi venga generato un hash nello stesso indice.
3. Impostare il parametro *N-grams* (N-grammi) su 2. In questo modo si recupera la frequenza di occorrenze di unigrammi (una funzione per ogni singola parola) e di digrammi (una funzione per ogni coppia di valori adiacenti) dal testo di input. L'intervallo del parametro *N-grams* (N-grammi) è compreso tra 0 e 10 e indica il numero massimo di parole sequenziali da includere in una funzione.  

![Modulo Feature Hashing](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

La figura seguente mostra l'aspetto delle nuove funzioni.

![Esempio di Feature Hashing](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtro delle funzioni dai dati: selezione di funzioni
La *selezione delle funzioni* è un processo applicato comunemente alla costruzione di set di dati di training per le attività di modellazione predittive, come la classificazione o la regressione. L'obiettivo consiste nel selezionare un subset di funzioni dal set di dati originale che riduce le dimensioni usando un set minimo di funzioni per rappresentare la quantità massima di varianza nei dati. Questo subset di funzioni contiene le sole funzioni da includere per il training del modello. La selezione delle funzioni ha due scopi principali:

* La selezione di funzioni migliora spesso la precisione della classificazione eliminando le funzioni irrilevanti, ridondanti o altamente correlate.
* La selezione di funzioni riduce il numero di funzioni rendendo più efficiente il processo di training del modello. Questo aspetto è particolarmente importante per gli strumenti di apprendimento, come le macchine a vettori di supporto, il cui training risulta costoso.

Anche se la selezione delle funzioni cerca di ridurre il numero di funzioni nel set di dati usato per il training del modello, non viene in genere definita con il termine *riduzione della dimensionalità*. I metodi di selezione delle funzioni estraggono un subset delle funzioni originali presenti nei dati senza apportarvi modifiche.  I metodi di riduzione della dimensionalità usano funzioni progettate che possono trasformare le funzioni originali e quindi modificarle. Analisi in componenti principali, analisi di correlazione canonica e scomposizione di valori singolari sono esempi di metodi di riduzione della dimensionalità.

Una categoria di metodi di selezione delle funzioni ampiamente applicata in un contesto supervisionato è la selezione delle funzioni basata su filtro. Tramite la valutazione della correlazione tra ogni funzione e l'attributo di destinazione, questi metodi applicano una misura statistica per assegnare un punteggio a ogni funzione. Queste funzioni vengono quindi classificate in base al punteggio, che può essere usato per impostare la soglia per mantenere o eliminare una funzione specifica. Correlazione di Pearson, informazione mutua e test del chi quadrato sono esempi di misure statistiche usate in questi metodi.

Azure Machine Learning Studio fornisce moduli per la selezione delle funzioni. Come illustrato nella figura seguente, questi moduli includono [Filter-Based Feature Selection][filter-based-feature-selection] e [Fisher Linear Discriminant Analysis][fisher-linear-discriminant-analysis].

![Esempio di selezione delle funzioni](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Usare ad esempio il modulo [Filter-Based Feature Selection][filter-based-feature-selection] con l'esempio di data mining descritto in precedenza. Si supponga di voler compilare un modello di regressione in base a un set di 256 funzioni create con il modulo [Feature Hashing][feature-hashing] e che la variabile di risposta sia **Col1** e rappresenti le classificazioni delle recensioni di un libro in un intervallo da 1 a 5. Impostare **Feature scoring method** (Metodo di assegnazione punteggio alla funzione) su **Pearson Correlation** (Correlazione di Pearson), **Target column** (Colonna di destinazione) su **Col1** e **Number of desired features** (Numero di funzioni desiderate) su **50**. Il modulo [Filter-Based Feature Selection][filter-based-feature-selection] restituisce un set di dati contenente 50 funzioni con l'attributo di destinazione **Col1**. La figura seguente mostra il flusso dell'esperimento e i parametri di input.

![Esempio di selezione delle funzioni](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

La figura seguente mostra i set di dati risultanti. Il punteggio di ogni funzione viene calcolato in base alla correlazione di Pearson tra la funzione stessa e l'attributo di destinazione **Col1**. Vengono mantenute le funzioni con i punteggi più alti.

![Set di dati di selezione delle funzioni basata su filtro](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

La figura seguente mostra i punteggi corrispondenti delle funzioni selezionate.

![Punteggi delle funzioni selezionate](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Applicando il modulo [Filter-Based Feature Selection][filter-based-feature-selection], vengono selezionate 50 delle 256 funzioni perché presentano le funzioni maggiormente correlate alle variabile di destinazione **Col1**, sulla base del metodo di assegnazione del punteggio denominato **Pearson Correlation**.

## <a name="conclusion"></a>Conclusione
Progettazione di funzioni e selezione di funzioni sono due passaggi eseguiti comunemente per la preparazione dei dati di training durante la creazione di un modello di Machine Learning. In genere, la progettazione di funzioni viene applicata innanzitutto per generare altre funzioni e quindi viene eseguito il passaggio di selezione delle funzioni per eliminare quelle irrilevanti, ridondanti o altamente correlate.

Non sempre è necessario eseguire la progettazione o la selezione delle funzioni. La necessità di questi passaggi dipende dai dati disponibili o da raccogliere, dagli algoritmi scelti e dall'obiettivo dell'esperimento.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
