---
title: aaaHow toouse archiviazione tabelle di Azure con hello WebJobs SDK
description: "Informazioni su come toouse Azure tabella archiviazione con hello WebJobs SDK. Creare tabelle, aggiungere entità tootables e leggere le tabelle esistenti."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>La modalità di archiviazione con tabelle di Azure toouse hello WebJobs SDK
## <a name="overview"></a>Panoramica
Questa guida fornisce esempi di codice c# che mostrano come tooread e scrittura di archiviazione Azure tabelle utilizzando [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.

Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o troppo[più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Alcuni dei frammenti di codice hello mostrano hello `Table` attributo utilizzato nelle funzioni che sono [chiamato manualmente](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), vale a dire, non tramite uno degli attributi di hello trigger. 

## <a id="ingress"></a>La tabella di tooa tooadd entità
tabella tooa tooadd entità hello utilizzare `Table` attributo con un `ICollector<T>` o `IAsyncCollector<T>` parametro dove `T` specifica dello schema di hello di entità hello desiderato tooadd. costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello della tabella di hello. 

Hello nell'esempio di codice seguente consente di aggiungere `Person` tabella tooa entità denominata *in ingresso*.

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

In genere hello tipo da utilizzare con `ICollector` deriva da `TableEntity` o implementa `ITableEntity`, ma non è necessario. Uno dei seguenti hello `Person` le classi di lavoro con codice di hello di hello precedente `Ingress` metodo.

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

Se si desidera toowork direttamente con hello API di archiviazione di Azure, è possibile aggiungere un `CloudStorageAccount` firma del metodo toohello parametro.

## <a id="monitor"></a> Monitoraggio in tempo reale
Poiché le funzioni in ingresso dei dati spesso elaborano grandi volumi di dati, hello dashboard WebJobs SDK fornisce i dati di monitoraggio in tempo reale. Hello **chiamata Log** sezione viene indicato se la funzione hello è ancora in esecuzione.

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hello **chiamata dettagli** pagina report hello lo stato di avanzamento della funzione (numero di entità scritta) durante l'esecuzione e offre un tooabort opportunità è. 

![Funzione Ingress in esecuzione](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Quando la funzione hello viene completata, hello **chiamata dettagli** pagina viene indicato il numero di hello di righe scritte.

![Funzione Ingress completata](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Come tooread più entità da una tabella
tooread una tabella, utilizzare hello `Table` attributo con un `IQueryable<T>` parametro in cui digitare `T` deriva da `TableEntity` o implementa `ITableEntity`.

legge Hello nell'esempio di codice seguente e i log di tutte le righe da hello `Ingress` tabella:

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a id="readone"></a>Come tooread una singola entità da una tabella
È presente un `Table` costruttore di attributo con due parametri aggiuntivi che consentono di specificare la chiave di partizione hello e chiave di riga quando si desidera toobind tooa tabella singola entità.

esempio di codice seguente Hello legge una riga della tabella per un `Person` entità in base a partizione chiave e riga di valori di chiave ricevuti in un messaggio nella coda:  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


Hello `Person` classe in questo esempio non dispone di tooimplement `ITableEntity`.

## <a id="storageapi"></a>Come toouse hello API di archiviazione .NET direttamente toowork con una tabella
È inoltre possibile utilizzare hello `Table` attributo con un `CloudTable` oggetto per una maggiore flessibilità durante l'utilizzo di una tabella.

codice Hello seguente viene utilizzata una `CloudTable` tooadd toohello una singola entità dell'oggetto *in ingresso* tabella. 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

Per ulteriori informazioni su come hello toouse `CloudTable` , vedere [come toouse archiviazione tabelle da .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Argomenti correlati coperti da hello code come-tooarticle
Per informazioni su come l'elaborazione tabella toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non è l'elaborazione, vedere specifiche tootable [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Gli argomenti trattati in tale articolo includono hello informazioni seguenti:

* Funzioni asincrone
* Più istanze
* Arresto normale
* Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione
* Impostare le stringhe di connessione SDK hello nel codice
* Impostare i valori per i parametri del costruttore WebJobs SDK nel codice
* Attivare manualmente una funzione
* Scrivere i log

## <a id="nextsteps"></a> Passaggi successivi
Questa guida è fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di tabelle di Azure. Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

