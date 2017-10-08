---
title: aaaGetting avviato con l'archiviazione di Azure e servizi di Visual Studio connesso (processo Web progetti)
description: "La modalità di avvio tooget utilizzando l'archiviazione tabelle di Azure in un progetto processi Web di Azure in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Introduzione all'Archiviazione di Azure (progetti Azure WebJob)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Panoramica
Questo articolo fornisce esempi di codice c# che mostrano mostrano come toouse hello Azure WebJobs SDK versione 1. x con il servizio di archiviazione tabelle di Azure hello. esempi di codice Hello utilizzano hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versione 1. x.

servizio di archiviazione tabelle Azure Hello consente toostore grandi quantità di dati strutturati. servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure. Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.  Per altre informazioni, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) .

Alcuni dei frammenti di codice hello mostrano hello **tabella** attributo utilizzato nelle funzioni che vengono chiamate manualmente, vale a dire non utilizzando uno degli attributi di hello trigger.

## <a name="how-tooadd-entities-tooa-table"></a>La tabella di tooa tooadd entità
tabella tooa tooadd entità utilizzare hello **tabella** attributo con un **ICollector<T>**  o **IAsyncCollector<T>**  parametro dove **T** specifica dello schema hello di entità hello desiderato tooadd. costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello della tabella di hello.

Hello nell'esempio di codice seguente consente di aggiungere **persona** tabella tooa entità denominata *in ingresso*.

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

In genere hello tipo da utilizzare con **ICollector** deriva da **TableEntity** o implementa **ITableEntity**, ma non è necessario. Uno dei seguenti hello **persona** le classi di lavoro con codice di hello di hello precedente **in ingresso** metodo.

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

Se si desidera toowork direttamente con hello API di archiviazione di Azure, è possibile aggiungere un **CloudStorageAccount** firma del metodo toohello parametro.

## <a name="real-time-monitoring"></a>Monitoraggio in tempo reale
Poiché le funzioni in ingresso dei dati spesso elaborano grandi volumi di dati, hello dashboard WebJobs SDK fornisce i dati di monitoraggio in tempo reale. Hello **chiamata Log** sezione viene indicato se la funzione hello è ancora in esecuzione.

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hello **chiamata dettagli** pagina report hello lo stato di avanzamento della funzione (numero di entità scritta) durante l'esecuzione e offre un tooabort opportunità è.

![Funzione Ingress in esecuzione](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Quando la funzione hello viene completata, hello **chiamata dettagli** pagina viene indicato il numero di hello di righe scritte.

![Funzione Ingress completata](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Come tooread più entità da una tabella
tooread una tabella, utilizzare hello **tabella** attributo con un **IQueryable<T>**  parametro in cui digitare **T** deriva da **TableEntity**o implementa **ITableEntity**.

legge Hello nell'esempio di codice seguente e i log di tutte le righe da hello **in ingresso** tabella:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Come tooread una singola entità da una tabella
È presente un **tabella** costruttore di attributo con due parametri aggiuntivi che consentono di specificare la chiave di partizione hello e chiave di riga quando si desidera toobind tooa tabella singola entità.

esempio di codice seguente Hello legge una riga della tabella per un **persona** entità in base a partizione chiave e riga di valori di chiave ricevuti in un messaggio nella coda:  

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


Hello **persona** classe in questo esempio non dispone di tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Come toouse hello API di archiviazione .NET direttamente toowork con una tabella
È inoltre possibile utilizzare hello **tabella** attributo con un **CloudTable** oggetto per una maggiore flessibilità durante l'utilizzo di una tabella.

codice Hello seguente viene utilizzata una **CloudTable** tooadd toohello una singola entità dell'oggetto *in ingresso* tabella.

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

Per ulteriori informazioni su come hello toouse **CloudTable** , vedere [Introduzione all'archiviazione tabelle di Azure usando .NET](../storage/storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Argomenti correlati coperti da hello code come-tooarticle
Per informazioni su come l'elaborazione tabella toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non è l'elaborazione, vedere specifiche tootable [Guida introduttiva a Visual Studio e l'archiviazione delle code di Azure connessa servizi (processo Web progetti) ](../storage/vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di tabelle di Azure. Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse della documentazione di processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

