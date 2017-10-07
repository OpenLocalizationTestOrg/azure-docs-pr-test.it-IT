---
title: ingegneria aaaFeature scienza dei dati | Documenti Microsoft
description: Vengono illustrati a scopo di hello di progettazione delle funzioni e vengono forniti esempi del relativo ruolo nel processo di miglioramento dei dati hello di machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Progettazione di funzionalità nell'analisi scientifica dei dati
In questo argomento vengono illustrati a scopo di hello di progettazione delle funzioni e vengono forniti esempi del relativo ruolo nel processo di miglioramento dei dati hello di machine learning. esempi di Hello usati tooillustrate questo processo vengono disegnate da Azure Machine Learning Studio. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Questo **menu** collegamenti tootopics che descrivono come toocreate funzionalità per i dati in vari ambienti. Questa attività è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Funzionalità di progettazione tentativi tooincrease hello predittiva di algoritmi di apprendimento mediante la creazione di funzionalità da dati non elaborati che contribuiscono a semplificare hello processo di apprendimento. Hello engineering e selezione di funzionalità fa parte di hello TDSP descritte nella hello [novità hello ciclo di vita del processo di analisi scientifica dei dati del Team?](data-science-process-overview.md) Progettazione di funzionalità e di selezione sono parti di hello **sviluppare funzionalità** passaggio di hello TDSP. 

* **funzionalità di progettazione**: il processo tenta toocreate funzionalità aggiuntive di rilevanti da funzionalità non elaborato hello esistenti nei dati hello e tooincrease hello predittiva dell'algoritmo di apprendimento hello.
* **selezione delle caratteristiche**: questo processo consente di selezionare sottoinsieme di chiave hello delle funzionalità di dati originale della dimensionalità di hello tooreduce tentativo di problema training hello.

In genere **funzionalità engineering** verrà applicato prima toogenerate le funzionalità aggiuntive, quindi hello **selezione delle caratteristiche** passaggio viene eseguito tooeliminate irrilevanti, ridondanti o altamente correlate funzionalità.

spesso è possibile migliorare i dati di training Hello usati in machine learning per l'estrazione delle funzionalità da dati non elaborati di hello raccolti. Un esempio di una funzionalità decodificata nel contesto di hello di apprendimento come immagini hello tooclassify di caratteri scritti a mano è la creazione di un bit della mappa densità costruita dai dati di distribuzione di hello bit non elaborati. Questa mappa consente di individuare i bordi di hello dei caratteri hello in modo più efficiente rispetto all'uso distribuzione raw hello direttamente.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Creazione di funzioni dai dati: progettazione di funzioni
dati di training Hello è costituito da una matrice composta da esempi, record o osservazioni archiviate nelle righe, ognuna delle quali include un set di funzionalità (le variabili o campi archiviati nelle colonne). funzionalità Hello specificate nella progettazione sperimentale hello sono modelli di hello toocharacterize previsto nei dati di hello. Sebbene molti dei dati non elaborati di hello campi possono essere inclusi direttamente in hello tootrain set utilizzato funzionalità selezionato un modello, è spesso il caso hello che necessitano di ulteriori funzionalità (ingegneria) toobe costruito dalla funzionalità di hello hello dati non elaborati toogenerate un'avanzata set di dati di training.

Il tipo di funzionalità deve essere creato tooenhance hello set di dati durante il training di un modello? Ingegneria funzionalità che migliorano la formazione di hello forniscono informazioni che consentono di distinguere più modelli di hello nei dati hello. Prevediamo hello nuova funzionalità tooprovide informazioni aggiuntive che non sono hello chiaramente acquisita o rendere chiaramente evidente nel set di funzionalità originale o esistente. Questo processo è tuttavia una sorta di artificio. Le decisioni valide e produttive richiedono spesso una certa esperienza specifica.

A partire da Azure Machine Learning, è più semplice toograsp questo processo concretamente utilizzando gli esempi fornito in hello Studio. Di seguito ne vengono presentati due:

* Un esempio di regressione [stima del numero di hello di noleggio di biciclette](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) in un esperimento di supervisione in cui sono noti i valori di destinazione hello
* Un esempio di classificazione di data mining del testo tramite [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Esempio 1: Aggiunta di funzioni temporali per il modello di regressione
Utilizziamo hello esperimento "Demand forecasting di biciclette" in Azure Machine Learning Studio toodemonstrate come tooengineer funzionalità per un'attività di regressione. obiettivo di Hello di questo esperimento è richiesta hello toopredict per bikes hello, ovvero hello numero dei noleggi bike all'interno di una mese/giorno/ora specifica. Hello set di dati "Bike noleggio UCI dataset" viene utilizzato come dati di input non elaborato hello. Questo set di dati è basato su dati reali di hello capitale Bikeshare società che gestisce una rete di noleggio di biciclette in Washington DC in hello Stati Uniti. set di dati Hello rappresenta il numero di hello di noleggio di bicicletta all'interno di un'ora specifica di un giorno in anni di hello 2011 e l'anno 2012 e contiene 17379 righe e 17 colonne. set di funzionalità non elaborato di Hello contiene condizioni climatiche (velocità temperatura/umidità/del vento) e il tipo di hello del giorno hello (giorno festivo o giorno della settimana). Hello campo toopredict è "cnt", un numero che rappresenta il noleggio di biciclette hello all'interno di un'ora specifica e che gli intervalli è compreso tra 1 too977.

Con l'obiettivo di hello di creazione di funzioni valide nei dati di training di hello, quattro modelli di regressione vengono compilati mediante hello stesso algoritmo, ma con quattro set di dati di training diversi. Hello quattro set di dati rappresentano hello stessi dati di input non elaborati, ma impostando un numero crescente di funzionalità. Queste funzioni sono raggruppate in quattro categorie:

1. A = weather + giorno della settimana e giorno festivo + nel fine settimana funzionalità per giorno stimato hello
2. B = numero di biciclette che sono stati affittati in ognuna delle hello ultime 12 ore
3. C = numero di biciclette che sono stati affittati in ognuna delle hello precedente 12 giorni hello stesso ora
4. D = numero di biciclette che sono stati affittati in ognuna delle hello precedente 12 settimane hello stessa ora e hello stesso giorno

Oltre A set di funzionalità che già esiste nei dati non elaborati originali hello, hello altri tre set di funzionalità vengono creati tramite funzionalità hello processo di progettazione. Impostare funzionalità B acquisisce molto recente richiesta per bikes hello. Impostare funzionalità C acquisizioni richiesta hello di biciclette in un'ora specifica. Funzionalità impostare D acquisizioni richiesta per bikes particolare ora e giorno specifico della settimana hello. Hello quattro training set di dati ogni include un set di funzionalità, A + B, A + B + C e A + B + C + D, rispettivamente.

In hello esperimento di Azure Machine Learning, questi quattro set di dati di training sono formate mediante quattro rami da hello pre-elaborato input set di dati. Ad eccezione del fatto hello sinistra la maggior parte dei branch, ognuno di questi branch contiene un [Execute R Script](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) modulo, in cui un set di funzionalità derivata (funzionalità set B, C e D) sono rispettivamente costruiti e aggiunti toohello importato set di dati. Hello seguente illustrazione viene script hello R set di funzionalità toocreate B in hello secondo ramo sinistro.

![creare funzioni](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

confronto dei risultati delle prestazioni hello di hello in hello nella tabella seguente sono riepilogati quattro modelli di Hello. ottenere risultati ottimali Hello vengono visualizzati per le funzionalità A + B + C. Si noti che hello diminuisce tasso di errore quando il set di funzionalità aggiuntive sono incluse nei dati di training hello. Consente di verificare il nostro presume che set di funzionalità hello B, C forniscono altre informazioni rilevanti per attività di regressione hello. Ma aggiunta funzionalità hello D non sembra tooprovide qualsiasi ulteriore riduzione della percentuale di errore hello.

![confronto dei risultati](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> Esempio 2: Creazione di funzionalità per il data mining del testo
Progettazione di funzionalità ampiamente verrà applicati in tootext correlati di attività di data mining, ad esempio di analisi di classificazione e la valutazione di documento. Ad esempio, quando si desidera che i documenti tooclassify in diverse categorie, un tipico presupposto è che hello/frasi incluse nella categoria di un documento sono toooccur meno probabile che in un'altra categoria di documento. In altre parole, frequenza di hello di hello parole o frasi distribuzione è in grado di toocharacterize categorie di documento diverso. Nelle applicazioni di data mining di testo, poiché singole parti del contenuto di testo in genere utilizzati come dati di input hello, funzionalità hello processo di produzione è necessario toocreate hello funzionalità che coinvolgono le frequenze di parola o frase.

tooachieve questa attività, una tecnica denominata **feature hashing** è applicato tooefficiently attivare le funzionalità di testo arbitrario in indici. Anziché associare ogni testo funzionalità (parole o frasi) tooa indice specifico, questo metodo funziona applicando una funzionalità di toohello funzione hash e utilizzando i valori hash come indici direttamente.

In Azure Machine Learning è disponibile un modulo [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) che crea in modo pratico queste funzioni basate su parole/frasi. La figura seguente mostra un esempio dell'uso di questo modulo. set di dati input Hello contiene due colonne: hello classificazione libro compreso fra 1 too5 e hello contenuto effettivo di revisione. obiettivo di Hello di questo [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) modulo è una serie di nuove funzionalità che mostra la frequenza di occorrenza hello di hello corrispondente parole tooretrieve / adeguata all'interno di revisione particolare libro hello. toouse questo modulo, è necessario hello toocomplete alla procedura seguente:

* Selezionare innanzitutto colonna hello che contiene il testo di input hello ("Col2" in questo esempio).
* In secondo luogo, impostare hello too8 "Hashing bitsize", ovvero 2 ^ 8 = 256 funzionalità verranno create. Hello word fase o in tutto il testo hello sarà indici too256 con hash. il parametro Hello "Hashing bitsize" varia da 1 too31. Hello parole o frasi toobe meno probabile che l'hashing in hello stesso indice se l'impostazione di un numero maggiore di toobe.
* In terzo luogo, impostare too2 parametro "N-grammi" hello. Ottiene la frequenza di occorrenza hello gli unigrammi che i (una funzionalità per ogni singola parola) e bigrammi (una funzionalità per ogni coppia di parole adiacenti) hello testo di input. Hello parametro "N-grammi" è compreso tra 0 too10, che indica il numero massimo di hello di parole sequenziale toobe inclusi in una funzionalità.  

![Modulo "Feature Hashing"](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Hello figura seguente viene illustrato cosa hello queste nuove funzionalità è simile.

![Esempio di "Feature Hashing"](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Conclusioni
Le funzionalità selezionate e ingegneria aumentare l'efficienza di hello del processo di training hello che tenta di informazioni chiave hello tooextract contenute nei dati hello. Sono anche migliorare power hello questi modelli tooclassify hello di dati di input in modo accurato e risultati toopredict di interessano più in modo affidabile. Progettazione di funzionalità e la selezione anche possibile combinare learning hello toomake gestibile calcoli più complessi. Ciò avviene tramite ottimizzazione e quindi riducendo il numero di hello delle funzionalità necessarie toocalibrate o un modello di training. Matematicamente generale, il modello di hello di hello funzionalità tootrain selezionato sono un set minimo di variabili indipendenti che descrivono i modelli di hello nei dati hello e quindi una stima dei risultati correttamente.

Si noti che non è sempre necessariamente tooperform di funzionalità engineering o funzionalità di selezione. Se è necessario o non dipende dai dati hello è o raccogliere, algoritmo hello che viene selezionato, e hello obiettivo dell'esperimento hello.

