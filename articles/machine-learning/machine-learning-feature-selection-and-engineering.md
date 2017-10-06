---
title: aaaFeature team di progettazione e la selezione in Azure Machine Learning | Documenti Microsoft
description: "Vengono illustrati a scopo di hello di progettazione di funzionalità e funzionalità di selezione e vengono forniti esempi del proprio ruolo nel processo di miglioramento dei dati hello di machine learning."
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
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Progettazione e selezione di funzioni in Azure Machine Learning
Questo argomento illustra a scopo di hello del team di progettazione di funzionalità e la selezione di funzionalità nel processo di miglioramento dei dati hello di machine learning. Descrive cosa comportano questi processi usando gli esempi forniti da Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

spesso è possibile migliorare i dati di training Hello usati in machine learning dalla selezione hello o l'estrazione di funzionalità da dati non elaborati di hello raccolti. Un esempio di una funzionalità decodificata nel contesto di hello di apprendimento come immagini hello tooclassify di caratteri scritti a mano è una mappa di bit densità costruito dai dati di distribuzione di hello bit non elaborati. Questa mappa consente di individuare in modo più efficiente di distribuzione non elaborato hello bordi hello di caratteri hello.

Le funzionalità selezionate e ingegneria aumentare l'efficienza di hello del processo di training hello, che tenta di informazioni chiave hello tooextract contenute nei dati hello. Sono anche migliorare power hello questi modelli tooclassify hello di dati di input in modo accurato e risultati toopredict di interessano più in modo affidabile. Progettazione di funzionalità e la selezione anche possibile combinare learning hello toomake gestibile calcoli più complessi. Ciò avviene tramite ottimizzazione e quindi riducendo il numero di hello delle funzionalità necessarie toocalibrate o un modello di training. Matematicamente generale, il modello di hello di hello funzionalità tootrain selezionato sono un set minimo di variabili indipendenti che descrivono i modelli di hello nei dati hello e quindi una stima dei risultati correttamente.

progettazione di Hello e selezione di funzionalità fa parte di un processo più ampio, in genere costituito da quattro passaggi:

* Raccolta dei dati
* Miglioramento dei dati
* Costruzione del modello
* Post-elaborazione

Progettazione e la selezione costituiscono fase di miglioramento dei dati hello di machine learning. Per le finalità di questo documento, si possono distinguere tre aspetti di questo processo:

* **Pre-elaborazione di dati**: questo processo Cerca tooensure che hello i dati raccolti sia pulito e coerente. Include attività come integrazione di più set di dati, gestione di dati mancanti, gestione di dati incoerenti e conversione di tipi di dati.
* **Funzionalità di progettazione**: il processo tenta toocreate funzionalità aggiuntive di rilevanti da funzionalità non elaborato esistente di hello in hello dati e tooincrease predittiva toohello algoritmo di apprendimento.
* **Selezione delle caratteristiche**: questo processo consente di selezionare hello chiave sottoinsieme dati funzionalità tooreduce hello dimensionalità originale dei problemi di training hello.

In questo argomento descrive solo hello funzionalità ingegneria e funzionalità di selezione gli aspetti del processo di miglioramento dei dati hello. Per ulteriori informazioni sulla fase di pre-elaborazione dei dati hello, vedere [pre-elaborazione dati in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Creazione di funzioni dai dati: progettazione di funzioni
dati di training Hello è costituito da una matrice composta da esempi, record o osservazioni archiviate nelle righe, ognuna delle quali include un set di funzionalità (le variabili o campi archiviati nelle colonne). funzionalità Hello specificate nella progettazione sperimentale hello sono modelli di hello toocharacterize previsto nei dati di hello. Sebbene molti dei dati non elaborati di hello campi possono essere inclusi direttamente in hello tootrain set utilizzato funzionalità selezionato un modello, le funzionalità aggiuntive di ingegneria è spesso necessario toobe costruito dalla funzionalità di hello hello dati non elaborati toogenerate un set di dati di training avanzata.

Il tipo di funzionalità deve essere creato il set di dati di tooenhance hello durante il training di un modello? Ingegneria funzionalità che migliorano la formazione di hello forniscono informazioni che consentono di distinguere più modelli di hello nei dati hello. Si prevedono di hello nuova funzionalità tooprovide informazioni aggiuntive che non sono chiaramente acquisita o rendere chiaramente evidente in hello originale o set di funzionalità esistente, ma questo processo è un elemento di un'immagine. Le decisioni valide e produttive richiedono spesso una certa esperienza specifica.

A partire da Azure Machine Learning, è più semplice toograsp questo processo concretamente utilizzando gli esempi fornito in Machine Learning Studio. Di seguito ne vengono presentati due:

* Un esempio di regressione ([stima del numero di hello di noleggio di biciclette](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) in un esperimento di supervisione in cui sono noti i valori di destinazione hello
* Un esempio di classificazione di data mining del testo tramite [Feature Hashing][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Esempio 1: Aggiunta di funzioni temporali per il modello di regressione
toodemonstrate come tooengineer funzionalità per un'attività di regressione, utilizziamo hello esperimento "Demand forecasting di biciclette" in Azure Machine Learning Studio. obiettivo di Hello di questo esperimento è richiesta hello toopredict per bikes hello, ovvero hello numero dei noleggi bike all'interno di un determinato mese, giorno o un'ora. set di dati Hello **set di dati UCI noleggio Bike** viene utilizzato come dati di input non elaborato hello.

Questo set di dati è basato su dati reali di hello capitale Bikeshare società che gestisce una rete di noleggio di biciclette in Washington DC in hello Stati Uniti. Hello set di dati rappresenta il numero di hello di noleggio di bicicletta all'interno di un'ora specifica di un giorno, too2012 2011 e contiene 17379 righe e 17 colonne. set di funzionalità non elaborato di Hello contiene condizioni climatiche (temperatura, umidità, velocità del vento) e il tipo di hello di hello giorno (giorno festivo o giorno della settimana). Hello campo toopredict è **cnt**, un numero che rappresenta il noleggio di biciclette hello all'interno di un'ora specifica e che è compreso tra 1 too977.

tooconstruct funzionalità valide nei dati di training hello, quattro modelli di regressione compilati utilizzando hello stesso algoritmo, ma con dati di training diversi quattro imposta. Hello quattro set di dati rappresentano hello stessi dati di input non elaborati, ma impostando un numero crescente di funzionalità. Queste funzioni sono raggruppate in quattro categorie:

1. A = weather + giorno della settimana e giorno festivo + nel fine settimana funzionalità per giorno stimato hello
2. B = numero di biciclette che sono stati affittati in ognuna delle hello ultime 12 ore
3. C = numero di biciclette che sono stati affittati in ognuna delle hello precedente 12 giorni hello stesso ora
4. D = numero di biciclette che sono stati affittati in ognuna delle hello precedente 12 settimane hello stessa ora e hello stesso giorno

Oltre A set di funzionalità che contiene già dati non elaborati originale hello, hello altri tre set di funzionalità vengono creati tramite funzionalità hello processo di progettazione. Funzionalità set B acquisisce hello recente richiesta per bikes hello. Impostare funzionalità C acquisizioni richiesta hello di biciclette in un'ora specifica. Funzionalità impostare D acquisizioni richiesta per bikes particolare ora e giorno specifico della settimana hello. Ognuno dei set di dati di training hello quattro include set di funzionalità A, A + B, A + B + C e A + B + C + D, rispettivamente.

In hello esperimento di Azure Machine Learning, questi quattro set di dati di training sono formati mediante quattro rami hello pre-elaborato input set di dati. Ad eccezione di ramo all'estrema sinistra hello, ognuno di questi branch contiene un [Execute R Script] [ execute-r-script] rispettivamente costruito e aggiunto modulo in cui un set di derivato funzionalità (set di funzionalità B, C e D) toohello importati set di dati. Hello seguente illustrazione viene script hello R set di funzionalità toocreate B in hello secondo ramo sinistro.

![Creazione di un set di funzioni](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Hello nella tabella seguente sono riepilogate confronto hello dei risultati delle prestazioni di quattro modelli hello hello. ottenere risultati ottimali Hello vengono visualizzati per le funzionalità A + B + C. Si noti che la frequenza degli errori di hello diminuisce quando set di funzionalità aggiuntive sono incluse nei dati di training hello. In questo modo si verifica il nostro presume che il set di funzionalità B e C forniscono altre informazioni rilevanti per attività di regressione hello hello. Aggiunta di set di funzionalità hello D non sembra tooprovide qualsiasi ulteriore riduzione della percentuale di errore hello.

![Confronto dei risultati delle prestazioni](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> Esempio 2: Creazione di funzioni per il data mining del testo
Progettazione di funzionalità ampiamente verrà applicati in tootext correlati di attività di data mining, ad esempio di analisi di classificazione e la valutazione di documento. Ad esempio, quando si desidera tooclassify documenti in diverse categorie, un presupposto tipico è hello analitico incluso nella categoria di un documento siano toooccur meno probabile che in un'altra categoria di documento. In altre parole, frequenza di hello della distribuzione di parole o frasi hello è in grado di toocharacterize categorie di documento diverso. Nelle applicazioni di data mining di testo, funzionalità di hello processo di produzione è necessario toocreate hello le funzioni frequenze parola o frase perché singole parti del contenuto di testo, in genere utilizzati come dati di input hello.

tooachieve questa attività, una tecnica denominata *feature hashing* è applicato tooefficiently attivare le funzionalità di testo arbitrario in indici. Anziché associare ogni testo funzionalità (parole o frasi) tooa indice specifico, questo metodo funziona tramite l'applicazione di una funzionalità di toohello funzione hash e utilizzando i valori hash come indici direttamente.

In Azure Machine Learning è disponibile un modulo [Feature Hashing][feature-hashing] che crea queste funzioni basate su parole o frasi. Hello figura riportata di seguito viene illustrato un esempio dell'utilizzo di questo modulo. set di dati di input Hello contiene due colonne: classificazione libro hello compreso fra 1 too5 hello effettiva revisione e contenuta. obiettivo di Hello di questo [Feature Hashing] [ feature-hashing] modulo è tooretrieve nuove funzionalità che mostra la frequenza di occorrenza hello di hello corrispondente parole all'interno di revisione particolare libro hello. toouse questo modulo, è necessario hello toocomplete alla procedura seguente:

1. Colonna hello SELECT che contiene il testo di input hello (**Col2** in questo esempio).
2. Impostare *Hashing bitsize* too8, ovvero 2 ^ 8 = 256 funzionalità vengono create. Hello parola o frase nel testo hello viene quindi eseguito l'hashing too256 indici. parametro Hello *Hashing bitsize* compreso tra 1 too31. Se il parametro hello è impostato tooa maggiore numero, hello di parole o frasi sono meno probabile toobe l'hashing in hello stesso indice.
3. Impostare il parametro hello *N-grammi* too2. Consente di recuperare la frequenza di occorrenza hello gli unigrammi che i (una funzionalità per ogni singola parola) e bigrammi (una funzionalità per ogni coppia di parole adiacenti) dal testo di input hello. parametro Hello *N-grammi* compreso tra 0 too10, che indica il numero massimo di hello di parole sequenziale toobe inclusi in una funzionalità.  

![Modulo Feature Hashing](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Hello figura seguente illustra queste nuove funzionalità di aspetto.

![Esempio di Feature Hashing](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtro delle funzioni dai dati: selezione di funzioni
*Selezione delle caratteristiche* è un processo che viene in genere applicato toohello costruzione del set di dati di training per la modellazione predittiva di attività, ad esempio attività di classificazione o regressione. obiettivo di Hello è un subset delle funzionalità di hello dal set di dati originale hello che riduce le dimensioni utilizzando un set minimo di funzionalità toorepresent hello massimo della varianza nei dati hello tooselect. Questo subset di funzionalità contiene hello solo funzionalità toobe inclusi tootrain hello modello. La selezione delle funzioni ha due scopi principali:

* La selezione di funzioni migliora spesso la precisione della classificazione eliminando le funzioni irrilevanti, ridondanti o altamente correlate.
* Funzionalità selezione diminuisce hello numerose funzionalità, che rende più efficiente processo di training del modello hello. Ciò è particolarmente importante per strumenti di apprendimento che sono costosi tootrain, ad esempio macchine a vettori di supporto.

Sebbene Selezione funzionalità ricerche numero hello tooreduce funzionalità hello set di dati utilizzato tootrain hello modello, non è in genere definite termine hello tooby *la riduzione della dimensionalità.* Metodi di selezione delle funzioni di estrarre un subset delle funzionalità originale in dati hello senza modificarli.  Metodi di riduzione della dimensionalità utilizzano ingegneria funzionalità che è possibile trasformare le funzionalità originali di hello e quindi modificarli. Analisi in componenti principali, analisi di correlazione canonica e scomposizione di valori singolari sono esempi di metodi di riduzione della dimensionalità.

Una categoria di metodi di selezione delle funzioni ampiamente applicata in un contesto supervisionato è la selezione delle funzioni basata su filtro. Per la valutazione di correlazione hello tra ogni attributo di destinazione di funzionalità e hello, questi metodi si applicano tooassign una misura statistica una funzionalità tooeach punteggio. Hello funzionalità vengono quindi classificate in base al punteggio di hello, che è possibile utilizzare soglia hello tooset per mantenere o eliminare una funzionalità specifica. Esempi di misure statistiche di hello usate in questi metodi includono la correlazione di Pearson, basato sull'informazione mutua e test del chi quadrato hello.

Azure Machine Learning Studio fornisce moduli per la selezione delle funzioni. Come illustrato nella seguente illustrazione hello, questi moduli includono [Filter-Based Feature Selection] [ filter-based-feature-selection] e [Fisher Linear Discriminant Analysis] [ fisher-linear-discriminant-analysis].

![Esempio di selezione delle funzioni](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Ad esempio, utilizzare hello [Filter-Based Feature Selection] [ filter-based-feature-selection] modulo con un esempio di data mining testo hello descritta in precedenza. Si supponga di voler toobuild un modello di regressione dopo la creazione di un set di 256 funzionalità tramite hello [Feature Hashing] [ feature-hashing] modulo e la variabile di risposta hello è **Col1**e rappresenta un libro esaminare classificazione compreso fra 1 too5. Impostare **funzionalità metodo valutazione** troppo**la correlazione di Pearson**, **colonna di destinazione** troppo**Col1**, e **svariate desiderato funzionalità** troppo**50**. modulo Hello [Filter-Based Feature Selection] [ filter-based-feature-selection] produce quindi un set di dati contenente le funzionalità di 50 con attributo di destinazione hello **Col1**. di seguito Hello figura mostra il flusso di hello di questa sperimentazione e hello parametri di input.

![Esempio di selezione delle funzioni](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Hello figura riportata di seguito viene illustrato il set di dati risultante hello. Ogni funzionalità viene calcolato il punteggio in base su hello correlazione di Pearson tra l'elemento e hello attributo di destinazione **Col1**. funzionalità di Hello con i punteggi migliori vengono mantenute.

![Set di dati di selezione delle funzioni basata su filtro](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Hello illustrata nella figura seguente hello corrispondenti punteggi delle funzionalità di hello selezionato.

![Punteggi delle funzioni selezionate](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Applicando questo [Filter-Based Feature Selection] [ filter-based-feature-selection] modulo, 50 da 256 le funzionalità sono selezionate perché hanno la maggior parte delle funzionalità correlate con la variabile di destinazione hello hello **Col1** basato sul punteggio metodo hello **la correlazione di Pearson**.

## <a name="conclusion"></a>Conclusioni
Progettazione di funzionalità e funzionalità di selezione sono i dati di training hello tooprepare due passaggi in genere eseguiti durante la compilazione di un modello di machine learning. In genere, progettazione di funzionalità viene applicata prima toogenerate le funzionalità aggiuntive e quindi passaggio di selezione delle funzionalità hello è eseguita tooeliminate irrilevanti e ridondante o funzioni altamente correlate.

Non è sempre necessariamente tooperform di funzionalità engineering o funzionalità di selezione. Se è necessario dipende dai dati hello aver o raccogliere, si sceglie, algoritmo di hello e hello obiettivo dell'esperimento hello.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
