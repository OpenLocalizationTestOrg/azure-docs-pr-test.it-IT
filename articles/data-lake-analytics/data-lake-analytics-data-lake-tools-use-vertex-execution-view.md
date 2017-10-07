---
title: hello aaaUse visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio | Documenti Microsoft
description: Informazioni su come toouse hello i processi di Data Lake Analitica tooexam visualizzazione esecuzione vertice.
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Utilizzare Visualizzazione esecuzione vertice hello in Data Lake Tools per Visual Studio
Informazioni su come toouse hello i processi di Data Lake Analitica tooexam visualizzazione esecuzione vertice.

## <a name="prerequisites"></a>Prerequisiti

Occorre una conoscenza di base dell'utilizzo di Data Lake strumenti per lo script U-SQL toodevelop di Visual Studio.  Vedere [Esercitazione: Sviluppare script U-SQL tramite Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Aprire visualizzazione esecuzione vertice hello
Aprire un processo U-SQL in Strumenti Data Lake per Visual Studio. Fare clic su **visualizzazione esecuzione vertice** nell'angolo inferiore sinistro di hello. È possibile profili tooload richiesta innanzitutto e può richiedere alcuni minuti in base la connettività di rete.

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Informazioni sulla visualizzazione esecuzioni vertici
Visualizzazione esecuzione vertice Hello include tre parti:

![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Hello **selettore vertice** sulla sinistra consente di hello selezionate vertici dalle funzionalità (ad esempio le prime 10 dati di lettura o scegliere dalla fase). Uno dei filtri di uso frequente hello è hello toosee **vertici sul percorso critico**. Hello **percorso critico** hello catena più lungo di vertici di un processo U-SQL. Percorso critico di conoscenza hello è utile per ottimizzare i processi controllando il vertice richiede tempo più lungo di hello.
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

riquadro superiore centrale Hello Mostra hello **allo stato di tutti i vertici hello in esecuzione**.
  
![Visualizzazione esecuzioni vertici di Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

riquadro centrale inferiore di Hello Mostra informazioni su ogni vertice:
* Nome processo: hello Nome istanza vertice hello. costituito da parti differenti in NomeFase | NomeVertice | IstanzaEsecuzioneVertice. Ad esempio, vertice .v1 [62] hello SV7_Split è l'acronimo di hello seconda istanza in esecuzione (.v1, indice, a partire da 0) del numero di vertici 62 nella fase SV7_Split.
* Totale dei dati in lettura/scrittura: hello dati sono stati letti/scritti da questo vertice.
* Stato e lo stato di uscita: hello stato finale quando vertice hello viene terminata.
* Tipo di errori o codice di uscita: hello quando vertice hello non riuscita.
* Motivo di creazione: Perché vertice hello è stato creato.
* Risorsa o il processo latenza latenza/PN coda latenza: hello durata toowait vertice hello per le risorse e dati tooprocess toostay nella coda di hello.
* GUID processo/creatore: GUID per vertice di esecuzione corrente di hello o il relativo autore.
* Versione: istanza hello ennesima hello in esecuzione vertice (sistema hello possibile pianificare nuove istanze di un vertice per diversi motivi, ad esempio il failover, calcolano la ridondanza, ecc.)
* Version Created Time (Data e ora creazione versione).
* Elaborare crea inizio ora o il processo in coda o il processo ora inizio ora/processo completa tempo: quando il processo di vertex hello avvii la creazione; Quando il processo di vertex hello avvia tooqueue; hello quando l'inizio del processo determinati vertice. Quando hello determinati vertice viene completata.

## <a name="next-steps"></a>Passaggi successivi
* informazioni di diagnostica toolog, vedere [accesso ai log di diagnostica per Azure Data Lake Analitica](data-lake-analytics-diagnostic-logs.md)
* toosee una query più complessa, vedere [sito Web di analizzare i log di Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).
* vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md)
