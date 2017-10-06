---
title: selezione aaaFeature nel processo di analisi scientifica dei dati di Team hello | Documenti Microsoft
description: "Viene spiegato hello scopo della funzionalità di selezione e vengono forniti esempi del proprio ruolo nel processo di miglioramento dei dati hello di machine learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Selezione di funzionalità in hello Team Data Science processo (TDSP)
In questo articolo illustra a scopo di hello di selezione delle funzionalità e fornisce esempi del relativo ruolo nel processo di miglioramento dei dati hello di machine learning. Questi esempi sono tratti da Azure Machine Learning Studio. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Hello engineering e selezione di funzionalità fa parte di hello indicati in Team dati scienza processo (TDSP) [novità hello processo di analisi scientifica dei dati del Team?](data-science-process-overview.md). Progettazione di funzionalità e di selezione sono parti di hello **sviluppare funzionalità** passaggio di hello TDSP.

* **funzionalità di progettazione**: il processo tenta toocreate funzionalità rilevanti aggiuntive dalle funzionalità non elaborato esistente di hello hello di dati e l'algoritmo di apprendimento toohello tooincrease capacità predittiva.
* **selezione delle caratteristiche**: questo processo consente di selezionare sottoinsieme di chiave hello delle funzionalità di dati originale della dimensionalità di hello tooreduce tentativo di problema training hello.

In genere **funzionalità engineering** verrà applicato prima toogenerate le funzionalità aggiuntive, quindi hello **selezione delle caratteristiche** passaggio viene eseguito tooeliminate irrilevanti, ridondanti o altamente correlate funzionalità.

## <a name="filtering-features-from-your-data---feature-selection"></a>Filtro delle funzioni dai dati: selezione di funzioni
Funzionalità di selezione è un processo che viene in genere applicato per la costruzione di hello del set di dati di training per la modellazione predittiva di attività, ad esempio attività di classificazione o regressione. obiettivo di Hello è un subset delle funzionalità di hello dal set di dati originale hello che consentono di ridurre le dimensioni utilizzando un set minimo di funzionalità toorepresent hello massimo della varianza nei dati hello tooselect. Questo sottoinsieme di funzionalità, quindi, hello solo funzionalità toobe inclusi modello hello tootrain. La selezione delle funzioni ha due scopi principali.

* La selezione di funzioni migliora spesso la  precisione della classificazione eliminando le funzioni irrilevanti, ridondanti o altamente correlate.
* In secondo luogo, tale operazione riduce hello numerose funzionalità che rende più efficiente il processo di training del modello. Ciò è particolarmente importante per strumenti di apprendimento che sono costosi tootrain, ad esempio macchine a vettori di supporto.

Sebbene Selezione funzionalità seek numero hello tooreduce funzionalità hello set di dati utilizzato tootrain hello modello, non è in genere tooby cui hello termine "riduzione della dimensionalità". Metodi di selezione delle funzioni di estrarre un subset delle funzionalità originale in dati hello senza modificarli.  Metodi di riduzione della dimensionalità utilizzano ingegneria funzionalità che è possibile trasformare le funzionalità originali di hello e quindi modificarli. Analisi in componenti principali, analisi di correlazione canonica e scomposizione di valori singolari sono esempi di metodi di riduzione della dimensionalità.

Tra le altre, una categoria di funzioni ampiamente applicata in un contesto supervisionato è detta "Selezione delle funzioni basata su filtro". Per la valutazione di correlazione hello tra ogni attributo di destinazione di funzionalità e hello, questi metodi si applicano tooassign una misura statistica una funzionalità tooeach punteggio. funzionalità di Hello vengono quindi classificate in base punteggio hello, che può essere utilizzato toohelp set hello soglia per il mantenimento o l'eliminazione di una funzionalità specifica. Esempi di misure statistiche di hello usate in questi metodi includono correlazione persona, basato sull'informazione mutua e test di hello Chi quadrato.

In Azure Machine Learning Studio sono disponibili moduli per la selezione delle funzioni. Come illustrato nella seguente illustrazione hello, questi moduli includono [Filter-Based Feature Selection] [ filter-based-feature-selection] e [Fisher Linear Discriminant Analysis] [ fisher-linear-discriminant-analysis].

![Esempio di selezione delle funzioni](./media/machine-learning-data-science-select-features/feature-Selection.png)

Si consideri, ad esempio, usare hello di hello [Filter-Based Feature Selection] [ filter-based-feature-selection] modulo. Ai fini di hello della praticità, continuiamo toouse hello text mining riportato di seguito viene illustrato in precedenza. Si supponga che un modello di regressione dopo un set di 256 funzionalità vengono creati tramite hello toobuild [Feature Hashing] [ feature-hashing] modulo e la variabile di risposta hello hello "Col1" e rappresenta un libro Esaminare le classificazioni comprese tra 1 too5. Tramite l'impostazione "Funzionalità di assegnazione dei punteggi metodo" toobe "Correlazione di Pearson", hello "Colonna di destinazione" toobe "Col1" e too50 "Numero di funzioni desiderate" hello. Quindi hello modulo [Filter-Based Feature Selection] [ filter-based-feature-selection] produrrà un set di dati contenente le funzionalità di 50 con attributo di destinazione hello "Col1". di seguito Hello figura mostra il flusso di hello di questa sperimentazione e hello parametri di input che appena descritti.

![Esempio di selezione delle funzioni](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Hello nella figura seguente mostra i set di dati risultante hello. Ogni funzionalità viene calcolato il punteggio in base su hello correlazione di Pearson tra stesso e attributo di destinazione "Col1" hello. funzionalità di Hello con i punteggi migliori vengono mantenute.

![Esempio di selezione delle funzioni](./media/machine-learning-data-science-select-features/feature-Selection2.png)

Hello corrispondente moltissimi funzionalità hello selezionato vengono visualizzati nella seguente illustrazione hello.

![Esempio di selezione delle funzioni](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Applicando questo [Filter-Based Feature Selection] [ filter-based-feature-selection] modulo, 50 da 256 funzionalità selezionate sono in quanto essi hanno hello più funzioni correlate con la variabile di destinazione hello "Col1", in base a hello punteggio metodo "Correlazione di Pearson".

## <a name="conclusion"></a>Conclusioni
Progettazione di funzionalità e funzionalità di selezione sono due comunemente progettata e funzionalità selezionate e aumentare l'efficienza di hello di formazione di processo che tenta di informazioni chiave hello tooextract contenute nei dati hello hello. Sono anche migliorare power hello questi modelli tooclassify hello di dati di input in modo accurato e risultati toopredict di interessano più in modo affidabile. Progettazione di funzionalità e la selezione anche possibile combinare learning hello toomake gestibile calcoli più complessi. Ciò avviene tramite ottimizzazione e quindi riducendo il numero di hello delle funzionalità necessarie toocalibrate o un modello di training. Matematicamente generale, il modello di hello di hello funzionalità tootrain selezionato sono un set minimo di variabili indipendenti che descrivono i modelli di hello nei dati hello e quindi una stima dei risultati correttamente.

Si noti che non è sempre necessariamente tooperform di funzionalità engineering o funzionalità di selezione. Se è necessario o non dipende dai dati hello è o raccogliere, algoritmo hello che viene selezionato, e hello obiettivo dell'esperimento hello.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

