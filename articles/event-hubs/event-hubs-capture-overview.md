---
title: aaaOverview di hub di eventi di Azure Capture | Documenti Microsoft
description: Acquisire i dati di telemetria con Acquisizione di Hub eventi
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Acquisizione di Hub eventi di Azure

Acquisizione di hub eventi Azure consente tooautomatically recapito hello flusso di dati in hub eventi tooan [archiviazione Blob di Azure](https://azure.microsoft.com/services/storage/blobs/) o [archivio Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) account desiderato, con hello una maggiore flessibilità specificare un intervallo di tempo o dimensione. Impostazione di acquisizione è veloce, non esistono toorun i costi amministrativi e viene ridimensionato automaticamente con gli hub di eventi [unità di velocità effettiva](event-hubs-features.md#capacity). Acquisire gli hub eventi è tooload modo più semplice hello flusso di dati in Azure e consente toofocus sull'elaborazione dei dati anziché sull'acquisizione di dati.

Acquisire gli hub eventi permette tooprocess in tempo reale e basata su batch pipeline sul hello stesso flusso. Ciò significa che è possibile compilare soluzioni che si adattano alle esigenze nel corso del tempo. Se si sta creando sistemi basati su batch corrente con un occhio verso futura elaborazione in tempo reale, o si desidera tooadd una soluzione di percorso freddo efficiente tooan esistente in tempo reale, acquisire gli hub eventi rende l'uso con il flusso di dati più semplici.

## <a name="how-event-hubs-capture-works"></a>Come funziona Acquisizione di Hub eventi

Hub eventi è un buffer di durevole tempo conservazione per l'ingresso di telemetria, log distribuite a tooa simile. Hello tooscaling chiave in hub eventi è hello [modello consumer partizionato](event-hubs-features.md#partitions). Ogni partizione è un segmento di dati indipendente e viene utilizzata in modo indipendente. Nel tempo che all'età di dati esterno, in base al periodo di memorizzazione configurabile hello. Di conseguenza, un determinato hub eventi non sarà mai "troppo pieno".

Acquisizione di hub eventi consente si toospecify proprio account di archiviazione Blob di Azure e un contenitore o un account archivio Azure Data Lake, che vengono utilizzati toostore hello acquisito dati. Questi account possono essere in hello stessa regione dell'hub eventi o in un'altra area, aggiungendo flessibilità toohello della funzionalità di acquisizione di hub eventi hello.

I dati acquisiti vengono scritti in formato [Apache Avro][Apache Avro], un formato compatto, rapido, binario che offre strutture di dati avanzate con lo schema inline. Questo formato è ampiamente utilizzato ecosistema Hadoop hello flusso Analitica e Data Factory di Azure. Altre informazioni sull'uso di Avro sono disponibili più avanti in questo articolo.

### <a name="capture-windowing"></a>Acquisire windowing

Acquisizione di hub eventi consente tooset di acquisizione di toocontrol una finestra. Questa finestra è una dimensione minima e la configurazione di tempo con un "primo wins criteri," vale a dire che hello eseguita trigger durante un'operazione di acquisizione. Se si dispone di quindici minuti, 100 MB finestra di acquisizione e inviare 1 MB al secondo, i trigger di hello dimensioni finestra prima dell'intervallo di tempo hello. Ogni partizione acquisisce in modo indipendente e scrive un blob in blocchi completato al momento di hello dell'acquisizione, denominato per volta hello in cui hello è stata rilevata l'intervallo di acquisizione. convenzione di denominazione archiviazione Hello è come segue:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Unità di scala toothroughput

Il traffico di Hub eventi è controllato dalle [unità elaborate](event-hubs-features.md#capacity). Una singola unità elaborata consente 1 MB al secondo o 1000 eventi al secondo in ingresso e il doppio in uscita. Hub eventi Standard può essere configurato con 1-20 unità elaborate e altre possono essere acquistate con una [richiesta di supporto][support request] per l'aumento della quota. L'uso superiore rispetto alle unità elaborate acquistate è limitato. Acquisizione di hub eventi copia i dati direttamente da archiviazione di hub eventi interno hello, ignorando le quote in uscita di unità di velocità effettiva e salvando il traffico in uscita per altri lettori di elaborazione, ad esempio flusso Analitica o Spark.

Acquisizione di Hub eventi, dopo essere stata configurata, viene eseguita automaticamente quando si invia il primo evento e continua l'esecuzione. toomake più semplice per tooknow l'elaborazione downstream che sia in esecuzione il processo di hello, hub eventi scrive file vuoti quando non sono presenti dati. Questo processo ottiene una cadenza prevedibile e un marcatore che possono alimentare i processori batch.

## <a name="setting-up-event-hubs-capture"></a>Configurazione di Acquisizione di Hub eventi

È possibile configurare l'acquisizione al momento della creazione di hello evento hub utilizzando hello [portale di Azure](https://portal.azure.com), o utilizzando i modelli di gestione risorse di Azure. Per ulteriori informazioni, vedere hello seguenti articoli:

- [Abilitare gli hub di eventi Capture utilizzando hello portale di Azure](event-hubs-capture-enable-through-portal.md)
- [Creare uno spazio dei nomi di Hub eventi con un hub eventi e abilitare l'acquisizione con un modello di Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Esplorazione file hello acquisito e l'utilizzo di Avro

Acquisire gli hub di eventi crea un file in formato Avro, come specificato nella finestra temporale hello configurato. È possibile visualizzare questi file con qualsiasi strumento, ad esempio [Azure Storage Explorer][Azure Storage Explorer]. È possibile scaricare hello file localmente toowork su di essi.

file Hello generati da acquisire gli hub eventi sono hello seguente schema Avro:

![][3]

I file Avro tooexplore un modo semplice consiste nell'utilizzare hello [Avro strumenti] [ Avro Tools] file jar di Apache. Dopo aver scaricato il file jar, è possibile visualizzare schema hello di un file Avro specifico eseguendo hello comando seguente:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Questo comando restituisce

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

È inoltre possibile utilizzare strumenti Avro tooconvert hello formato tooJSON ed eseguire altre elaborazioni.

tooperform avanzati di elaborazione, scaricare e installare Avro per la scelta della piattaforma. In fase di hello della redazione del presente documento, sono disponibili le implementazioni per C, C++ e C\#, Java, NodeJS, Perl, PHP, Python e Ruby.

In Apache Avro sono disponibili guide introduttive complete per [Java][Java] e [Python][Python]. È inoltre possibile leggere hello [introduzione acquisire gli hub di eventi](event-hubs-capture-python.md) articolo.

## <a name="how-event-hubs-capture-is-charged"></a>Come viene addebitato l'uso di Acquisizione di Hub eventi

Acquisizione di hub eventi è a consumo Analogamente toothroughput unità: come tariffa oraria. addebito Hello è direttamente proporzionale toohello numero di unità di velocità effettiva acquistate per spazio dei nomi hello. Come unità di velocità effettiva vengono aumentate e ridotte, acquisire gli hub eventi metri aumentare e diminuire tooprovide prestazioni corrispondenti. metri Hello si verificano in parallelo. Per i dettagli sui prezzi, vedere [Prezzi di Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Passaggi successivi

Acquisire gli hub eventi è più semplice modo tooget dati hello in Azure. Con Azure Data Lake, Azure Data Factory e Azure HDInsight, è possibile eseguire l'elaborazione batch e altre analisi usando strumenti e piattaforme familiari a scelta con la scalabilità necessaria.

Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Introduzione all'invio e alla ricezione di eventi](event-hubs-dotnet-framework-getstarted-send.md)
* Un'[applicazione di esempio completa che usa Hub eventi][sample application that uses Event Hubs]
* [Panoramica di Hub eventi][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
