---
title: 'Connessione dati: input di flussi di dati da un flusso di eventi | Microsoft Docs'
description: Informazioni sulla configurazione di un tooStream di connessione dati Analitica chiamato 'input'. Gli input includono un flusso di dati dagli eventi, oltre a dati di riferimento.
keywords: flusso di dati, connessione dati, flusso di eventi
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Connessione dati: informazioni sui dati di input flusso di eventi tooStream Analitica
processo di flusso Analitica tooa connessione dati Hello è un flusso di eventi da un'origine dati, ovvero del processo di cui viene fatto riferimento tooas hello *input*. Analisi di flusso si integra perfettamente con le origini del flusso dei dati di Azure, come [Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/), [Hub IoT di Azure](https://azure.microsoft.com/services/iot-hub/) e [Archiviazione BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/). Questi input origini possono provenire da hello stessa sottoscrizione di Azure come il processo analitica o da un'altra sottoscrizione.

## <a name="data-input-types-data-stream-and-reference-data"></a>Tipi di input di dati: flusso dei dati e dati di riferimento
Come origine dati tooa i dati vengono spostati, ha utilizzato dal processo di flusso Analitica hello ed elaborati in tempo reale. Gli input si dividono in due tipi: input del flusso dei dati e input dei dati di riferimento.

### <a name="data-stream-inputs"></a>Input del flusso dei dati
Un flusso dei dati è una sequenza non associata di eventi che accadono nel tempo. I processi di Analisi di flusso devono includere almeno un input del flusso dei dati. Gli hub eventi, l'hub IoT e l'archiviazione BLOB sono supportati come origini di input del flusso dei dati. Gli hub eventi sono flussi di eventi toocollect utilizzato da più dispositivi e servizi. ad esempio i feed attività dei social media, le informazioni sulle quotazioni azionarie o i dati di sensori. Hub IoT sono ottimizzati toocollect dati dai dispositivi connessi in scenari Internet delle cose (IoT).  L'archiviazione BLOB può essere usata come origine di input per l'inserimento di dati in blocco come flusso, ad esempio i file di log.  

### <a name="reference-data"></a>Dati di riferimento
Analisi di flusso supporta anche l'input noto come *dati di riferimento*. Si tratta di dati ausiliari che sono statici o cambiano lentamente e che di solito sono usati per eseguire correlazioni e ricerche. Ad esempio, è possibile unire dati in hello toodata input flusso dati nei dati di riferimento hello, quanto sarà necessario eseguire un toolook join SQL valori statici. Archiviazione Blob di Azure è attualmente origine di input hello è supportato solo per i dati di riferimento. BLOB di origine dati di riferimento sono limitati too100 MB di dimensioni.

toolearn toocreate input di dati di riferimento, vedere [Use Reference Data](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Creare un input del flusso dei dati dagli hub eventi

Hub eventi di Azure offre una tecnologia di inserimento altamente scalabile per eventi di pubblicazione-sottoscrizione. Un hub eventi è possibile raccogliere milioni di eventi al secondo, in modo che sia possibile elaborare e analizzare hello enormi quantità di dati prodotti da applicazioni e dispositivi connessi. Hub eventi e Analisi di flusso offrono una soluzione end-to-end per l'analisi in tempo reale. Gli hub eventi consentono di inserire gli eventi in Azure tramite feed e i processi di Analisi di flusso sono in grado di elaborare tali eventi. Entrambe le operazioni vengono eseguite in tempo reale. Ad esempio, è possibile inviare selezioni nel web, letture dei sensori o in linea registro eventi tooEvent hub. È quindi possibile creare i processi di flusso Analitica toouse hub eventi come flussi di dati di input hello per in tempo reale il filtro, l'aggregazione e la correlazione.

Hello predefinito timestamp di eventi provenienti dall'hub di eventi nel flusso Analitica è timestamp hello che hello eventi arrivati in hub eventi hello, ovvero `EventEnqueuedUtcTime`. tooprocess hello dati come flusso usando un timestamp nel payload dell'evento hello, è necessario utilizzare hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (parola chiave).

### <a name="consumer-groups"></a>Gruppi di utenti
È necessario configurare ogni toohave di input hub di eventi flusso Analitica il proprio gruppo di consumer. Quando un processo contiene un self-join o ha più input, è possibile che qualche input venga letto da più lettori downstream. Questa situazione ha un impatto hello numero di lettori in un gruppo singolo consumer. tooavoid superiore hello hub eventi limite di cinque lettori per ogni gruppo di consumer per partizione, è una migliore toodesignate pratica un consumer di gruppo per ogni processo di flusso Analitica. È definito anche un limite di 20 gruppi di consumer per ogni hub eventi. Per altre informazioni, vedere [Guida alla programmazione di Hub eventi](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Configurare un hub eventi come input del flusso dei dati
Hello nella tabella seguente viene illustrato ogni proprietà nell'hello **nuovo input** pannello in hello portale di Azure quando si configura un hub eventi come input.

| Proprietà | Descrizione |
| --- | --- |
| **Alias di input** |Un nome descrittivo utilizzato in tooreference di query del processo di hello questo input. |
| **Spazio dei nomi del bus di servizio** |Spazio dei nomi del bus di servizio di Azure che viene usato come contenitore per un set di entità di messaggistica. Quando si crea un nuovo hub eventi, viene creato anche uno spazio dei nomi del bus di servizio. |
| **Nome hub eventi** |nome Hello di hello evento hub toouse come input. |
| **Nome criteri hub eventi** |Hello criteri di accesso condiviso che fornisce l'hub di eventi di accesso toohello. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. |
| **Gruppo di consumer dell'hub eventi** (facoltativa) |dati di tooingest toouse per gruppo di consumer Hello da hub di eventi hello. Se viene specificato alcun gruppo di consumer, il processo di flusso Analitica hello utilizza il gruppo di consumer predefinito hello. È consigliabile usare un gruppo di consumer distinto per ogni processo di Analisi di flusso. |
| **Formato di serializzazione eventi** |Hello formato di serializzazione (JSON, CSV o Avro) hello in arrivo del flusso di dati. |
| **Codifica** | UTF-8 è attualmente supportata solo hello formato di codifica. |

Quando i dati provengono da un hub eventi, è necessario toohello di accesso seguente i campi di metadati nella query Analitica di flusso:

| Proprietà | Descrizione |
| --- | --- |
| **EventProcessedUtcTime** |hello data e ora dell'evento hello è stato elaborato dal flusso Analitica. |
| **EventEnqueuedUtcTime** |hello data e ora dell'evento hello ha ricevuto gli hub di eventi. |
| **PartitionId** |ID di partizione in base zero di Hello per adattatore di input hello. |

Ad esempio, tramite questi campi, è possibile scrivere una query come hello di esempio seguente:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Creare un input del flusso dei dati dall'hub IoT
Hub IoT di Azure è un servizio di inserimento di eventi di pubblicazione-sottoscrizione altamente scalabile ottimizzato per scenari IoT.

Hello predefinito timestamp di eventi provenienti da un hub IoT in flusso Analitica è timestamp hello che hello eventi arrivati in hub IoT hello, ovvero `EventEnqueuedUtcTime`. tooprocess hello dati come flusso usando un timestamp nel payload dell'evento hello, è necessario utilizzare hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (parola chiave).

> [!NOTE]
> Solo i messaggi inviati con una proprietà `DeviceClient` possono essere elaborati.
> 
> 

### <a name="consumer-groups"></a>Gruppi di utenti
È necessario configurare ogni toohave di input hub IoT Analitica flusso il proprio gruppo di consumer. Quando un processo contiene un self-join o ha più input, è possibile che qualche input venga letto da più lettori downstream. Questa situazione ha un impatto hello numero di lettori in un gruppo singolo consumer. tooavoid superiore hello Azure IoT Hub limite di cinque lettori per ogni gruppo di consumer per partizione, è una migliore toodesignate pratica un consumer di gruppo per ogni processo di flusso Analitica.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Configurare un hub IoT come input del flusso dei dati
Hello nella tabella seguente viene illustrato ogni proprietà nell'hello **nuovo input** pannello in hello portale di Azure quando si configura un hub IoT come input.

| Proprietà | Descrizione |
| --- | --- |
| **Alias di input** |Un nome descrittivo utilizzato in tooreference di query del processo di hello questo input.|
| **Hub IoT** |nome Hello di hello IoT hub toouse come input. |
| **Endpoint** |Hello endpoint per l'hub IoT hello.|
| **Nome criteri di accesso condiviso** |criteri di accesso condiviso Hello che fornisce l'hub IoT toohello di accesso. Tutti i criteri di accesso condiviso dispongono di un nome e di autorizzazioni impostati, nonché di chiavi di accesso. |
| **Chiave criteri di accesso condiviso** |chiave di accesso condiviso Hello utilizzato tooauthorize l'hub IoT toohello accesso. |
| **Gruppo di consumer** (facoltativa) |dati di tooingest toouse per gruppo di consumer Hello dall'hub IoT hello. Se viene specificato alcun gruppo di consumer, un processo di flusso Analitica utilizza il gruppo di consumer predefinito hello. È consigliabile usare un gruppo di consumer diverso per ogni processo di Analisi di flusso. |
| **Formato di serializzazione eventi** |Hello formato di serializzazione (JSON, CSV o Avro) hello in arrivo del flusso di dati. |
| **Codifica** |UTF-8 è attualmente supportata solo hello formato di codifica. |

Quando i dati provengono da un hub IoT, si dispone di accesso toohello seguenti campi di metadati nella query Analitica di flusso:

| Proprietà | Descrizione |
| --- | --- |
| **EventProcessedUtcTime** |hello data e ora dell'evento hello è stato elaborato. |
| **EventEnqueuedUtcTime** |hello data e ora dell'evento hello è stato ricevuto dall'hub IoT hello. |
| **PartitionId** |ID di partizione in base zero di Hello per adattatore di input hello. |
| **IoTHub.MessageId** | Un ID che ha utilizzato la comunicazione bidirezionale toocorrelate hub IoT. |
| **IoTHub.CorrelationId** |ID usato nelle risposte dei messaggi e nei feedback nell'hub IoT. |
| **IoTHub.ConnectionDeviceId** |ID per l'autenticazione Hello utilizzato toosend questo messaggio. Questo valore viene indicato il servicebound messaggi dall'hub IoT hello. |
| **IoTHub.ConnectionDeviceGenerationId** |ID di generazione Hello di hello autenticato dispositivo che è stato utilizzato toosend questo messaggio. Questo valore viene indicato il servicebound messaggi dall'hub IoT hello. |
| **IoTHub.EnqueuedTime** |ora di Hello ricezione messaggio hello dall'hub IoT hello. |
| **IoTHub.StreamId** |Una proprietà di evento personalizzato aggiunta dal dispositivo mittente hello. |


## <a name="create-data-stream-input-from-blob-storage"></a>Creare un input del flusso dei dati dall'archiviazione BLOB
Per gli scenari con grandi quantità di dati non strutturati toostore nel cloud hello, archiviazione Blob di Azure offre una soluzione economica e scalabile. I dati nell'archiviazione BLOB sono in genere considerati dati inattivi, ma possono essere elaborati come flusso dei dati da Analisi di flusso. Uno scenario tipico per gli input di archiviazione BLOB con Analisi di flusso consiste nell'elaborazione dei log. In questo scenario, i dati di telemetria acquisiti da un sistema e toobe esigenze analizzati ed elaborati dati significativi tooextract.

Hello predefinito timestamp degli eventi di archiviazione Blob nel flusso Analitica è timestamp hello che hello blob dell'ultima modifica, ovvero `BlobLastModifiedUtcTime`. tooprocess hello dati come flusso usando un timestamp nel payload dell'evento hello, è necessario utilizzare hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) (parola chiave).

Gli input in formato CSV *richiedono* campi un toodefine riga di intestazione per il set di dati di hello. Inoltre, tutti i campi delle righe di intestazione devono essere univoci.

> [!NOTE]
> Analitica flusso non supporta l'aggiunta di blob esistente tooan contenuto. Flusso Analitica visualizzeranno un blob in una sola volta e non vengono elaborate tutte le modifiche che si verificano nel blob hello dopo che il processo di hello ha letto dati hello. Una procedura consigliata non tooupload tutti i dati di hello una sola volta e quindi archivio blob toothat di eventi.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Configurare l'archiviazione BLOB come input del flusso dei dati

Hello nella tabella seguente viene illustrato ogni proprietà nell'hello **nuovo input** pannello in hello portale di Azure quando si configura l'archiviazione Blob come input.

| Proprietà | Descrizione |
| --- | --- |
| **Alias di input** | Un nome descrittivo utilizzato in tooreference di query del processo di hello questo input. |
| **Account di archiviazione** | nome Hello hello dell'account di archiviazione in cui si trovano i file blob hello. |
| **Chiave dell'account di archiviazione** | chiave segreta Hello associata con l'account di archiviazione hello. |
| **Contenitore** | contenitore di Hello per input blob hello. I contenitori forniscono un raggruppamento logico dei blob archiviati nel servizio Blob di Microsoft Azure hello. Quando si carica un toohello blob del servizio di archiviazione Blob di Azure, è necessario specificare un contenitore per il blob. |
| **Modello percorso** (facoltativa) | percorso del file Hello utilizzato BLOB hello toolocate all'interno del contenitore specificato hello. Nel percorso di hello, è possibile specificare uno o più istanze di segue tre variabili hello: `{date}`, `{time}`, o`{partition}`<br/><br/>Esempio 1: `cluster1/logs/{date}/{time}/{partition}`<br/><br/>Esempio 2: `cluster1/logs/{date}`<br/><br/>Hello `*` carattere non è un valore consentito per il prefisso di percorso hello. Sono consentiti solo <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">Caratteri BLOB di Azure</a> validi. |
| **Formato data** (facoltativa) | Se si utilizza una variabile di tipo date hello nel percorso di hello, hello in cui hello sono organizzati i file di formato di Data. Esempio: `YYYY/MM/DD` |
| **Formato ora** (facoltativa) |  Se si utilizza la variabile di time hello nel percorso di hello, hello quali hello sono organizzati i file di formato di ora. Il valore di hello solo supportato attualmente è `HH`. |
| **Formato di serializzazione eventi** | Hello formato di serializzazione (JSON, CSV o Avro) per i flussi di dati in entrata. |
| **Codifica** | Per CSV e JSON, UTF-8 è attualmente supportata solo hello formato di codifica. |

Quando i dati provengono da un'origine di archiviazione Blob, è necessario toohello di accesso seguente i campi di metadati nella query Analitica di flusso:

| Proprietà | Descrizione |
| --- | --- |
| **BlobName** |da cui proviene il nome di Hello del blob di input hello che hello evento. |
| **EventProcessedUtcTime** |hello data e ora dell'evento hello è stato elaborato dal flusso Analitica. |
| **BlobLastModifiedUtcTime** |hello data e ora ultima modifica del blob che hello. |
| **PartitionId** |ID di partizione in base zero di Hello per adattatore di input hello. |

Ad esempio, tramite questi campi, è possibile scrivere una query come hello di esempio seguente:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Ottenere aiuto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
Sono state apprese le opzioni di connessione dei dati in Azure per i processi di Analisi di flusso. toolearn ulteriori informazioni su Analitica di flusso, vedere:

* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
