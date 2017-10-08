---
title: aaaIntroduction tooStream Analitica | Documenti Microsoft
description: Informazioni sul flusso Analitica, un servizio che consente di analizzare i dati di streaming di hello Internet delle cose (IoT) in tempo reale.
keywords: "analisi come servizio, servizi gestiti, elaborazione dei flussi, analisi di flusso, che cos'è Analisi di flusso"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Che cos'è Analisi di flusso?

Analisi di flusso di Azure è un motore di elaborazione di eventi completamente gestito che consente di configurare calcoli di analisi in tempo reale sui dati di streaming. Hello dati possono provenire da dispositivi, sensori, siti web, feed di social networking, applicazioni, sistemi di infrastruttura e altro ancora. 

## <a name="what-can-i-do-with-stream-analytics"></a>Cosa si può fare con Analisi di flusso?

Utilizzare volumi elevati di tooexamine Analitica di flusso di dati da dispositivi o i processi, estrarre informazioni dal flusso di dati hello e cercare modelli, tendenze e relazioni. In base che cos'è nei dati di hello, è quindi possibile eseguire attività di applicazione. Ad esempio, è possibile generare degli avvisi, avviano i flussi di lavoro di automazione, feed tooa informazioni strumento quali Power BI reporting o archiviare i dati per analisi successive. 

Esempi:

* Analisi e avvisi del mercato azionario, in tempo reale e personalizzati, offerti da aziende di servizi finanziari.
* Rilevamento delle frodi in tempo reale in base alle analisi dei dati delle transazioni. 
* Servizi di protezione di dati e identità.
* Analisi dei dati generati da sensori e attuatori incorporati in oggetti fisici (Internet delle cose o IoT).
* Analisi clickstream Web.
* Applicazioni CRM (Customer Relationship Management), ad esempio emissione di avvisi quando l'esperienza del cliente risulta compromessa in un determinato intervallo di tempo.

## <a name="how-does-stream-analytics-work"></a>Funzionamento di Analisi di flusso

Questo diagramma illustra hello flusso Analitica pipeline, che mostra la modalità di caricamento e analizzati e quindi inviati per la presentazione o azione dati. 

![Pipeline di Analisi di flusso](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Analisi di flusso inizia con un'origine di dati in streaming. dati Hello possono essere acquisiti in Azure da un dispositivo tramite un hub di eventi di Azure o hub IoT. dati Hello possono anche effettuare il pull da un archivio dati come archiviazione Blob di Azure. 

flusso hello tooexamine, si crea un flusso di Analitica *processo* che specifica la provenienza dei dati di hello. processo Hello specifica inoltre un *trasformazione*&mdash;come toolook di dati, modelli o relazioni. Per questa attività, Analisi di flusso supporta un linguaggio di query simile a SQL che consente di filtrare, ordinare, aggregare e unire dati di streaming in un periodo di tempo.

Infine, il processo di hello specifica un output toosend hello trasformato dati. Ciò consente di controllare quali toodo nelle informazioni di risposta toohello aver analizzato. Ad esempio, in risposta tooanalysis, è possibile:

* Inviare un comando toochange le impostazioni del dispositivo. 
* Dati tooa coda che viene monitorata da un processo che esegue un'operazione in base a quanto rilevato di invio. 
* Dashboard di Power BI tooa dati per la segnalazione di trasmissione.
* Inviare dati toostorage come archivio Data Lake, database di SQL Server o l'archiviazione Blob di Azure o di tabella.

È possibile monitorare un processo e modificare il numero di eventi elaborati al secondo mentre è in esecuzione. È anche possibile far sì che i processi generino log di diagnostica per la risoluzione dei problemi.

## <a name="key-capabilities-and-benefits"></a>Funzionalità e vantaggi principali

Flusso Analitica è progettato toobe facile toouse, flessibile e scalabile tooany processo dimensione ed economico.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Connettività toomany input e output

Flusso Analitica connessa direttamente troppo[hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) e [IoT Hub Azure](https://azure.microsoft.com/services/iot-hub/) per l'inserimento di flusso e hello [servizio di archiviazione Blob di Azure](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest i dati cronologici. Se si ottengono dati dagli hub eventi, è possibile combinare Analisi di flusso con altre origini dati e motori di elaborazione.

L'input del processo può anche includere dati di riferimento statici o a modifica lenta. È possibile partecipare streaming dati toothis riferimento dati tooperform ricerca operazioni hello esattamente come si farebbe con le query di database.

Indirizzare l'output del processo di Analisi di flusso in più direzioni. È possibile scrivere toostorage, come BLOB di archiviazione di Azure o tabelle, database SQL di Azure, Azure Data Lake archivi o Azure Cosmos DB. Da qui, dati hello potrebbero passare per analitica batch tramite Azure HDInsight. È possibile inviare hello output tooanother servizio per l'utilizzo da un altro processo, ad esempio code, argomenti del Bus di servizio di Azure o hub eventi. È possibile inviare l'output di hello tooPower Business Intelligence per la visualizzazione.

### <a name="ease-of-use"></a>Semplicità d'uso

le trasformazioni toodefine, utilizzare una semplice dichiarativa [Analitica flusso il linguaggio di query](https://msdn.microsoft.com/library/azure/dn834998.aspx) che consente di creare analisi sofisticate con alcuna programmazione. il linguaggio di query Hello accetta flusso di dati come input. È possibile filtrare e ordinare dati hello, aggregare valori, eseguire i calcoli, unire i dati (all'interno di un flusso o tooreference di dati), e utilizzare funzioni geospaziali. È possibile modificare le query nel portale di hello, tramite IntelliSense e la verifica della sintassi e per verificare le query che utilizzano dati di esempio che è possibile estrarre dal flusso in tempo reale hello.

### <a name="extensible-query-language"></a>Linguaggio di query estendibile

È possibile estendere le funzionalità di hello del linguaggio di query hello definendo e richiamare funzioni aggiuntive. È possibile definire le chiamate di funzione in hello Azure Machine Learning servizio tootake sfruttare le soluzioni di Azure Machine Learning. È inoltre possibile integrare le funzioni definite dall'utente JavaScript (UDF) i calcoli complessi tooperform di ordine come parte di una query di flusso Analitica.

### <a name="scalability"></a>Scalabilità

Flusso Analitica può gestire too1 GB di dati in ingresso al secondo. Integrazione con [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) e [IoT Hub Azure](https://azure.microsoft.com/services/iot-hub/) consente di alcuni processi tooingest milioni di eventi al secondo provenienti da dispositivi connessi, clickstreams e file di log, tooname. Funzione partizione hello degli hub di eventi, è possibile partizionare i calcoli in passaggi logici, ognuno con toobe possibilità di hello ulteriormente partizionati tooincrease scalabilità.

### <a name="low-cost"></a>Basso costo

Come un servizio cloud, flusso Analitica è toolet ottimizzato iniziare a basso costo. Si paga man mano in base alla quantità di informazioni sull'utilizzo e hello unità di streaming di dati elaborati dal sistema hello. Utilizzo viene derivato dal volume hello di eventi elaborati e quantità hello di potenza di calcolo eseguito il provisioning all'interno di hello cluster toohandle i processi di flusso Analitica.

### <a name="reliability-quick-recovery-and-repeatability"></a>Affidabilità, ripristino rapido e ripetibilità

Come servizio gestito nel cloud hello, Analitica di flusso consente di evitare la perdita di dati e fornisce la continuità aziendale. Se si verificano errori, il servizio di hello offre funzionalità di ripristino predefinite. Possibilità di hello toointernally mantengono lo stato, servizio hello fornisce risultati ripetibili garantire è tooarchive possibili eventi e riapplicare l'elaborazione in futuro hello, recupero sempre hello stessi risultati. Questo permette toogo indietro nel tempo e analizzare i calcoli quando si esegue l'analisi della causa radice, l'analisi di simulazione e così via.

## <a name="next-steps"></a>Passaggi successivi

* Per iniziare, [provare a usare l'input e le query provenienti da dispositivi IoT](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Compilare un [soluzione Analitica flusso end-to-end](stream-analytics-real-time-fraud-detection.md) che esamina toolook metadati telefonico per chiamate fraudolente.
* Informazioni sul linguaggio di query simile a SQL per flusso Analitica hello e sulle concetti univoci come [funzioni finestra](stream-analytics-window-functions.md).
* Informazioni su come troppo[ridimensionare i processi di flusso Analitica](stream-analytics-scale-jobs.md). 
* Informazioni su come troppo[integrare flusso Analitica e Azure Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).
* Trovare le risposte alle domande di flusso Analitica tooyour in hello [forum di Azure flusso Analitica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

