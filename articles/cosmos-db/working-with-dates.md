---
title: aaaWorking con date nel database di Azure Cosmos | Documenti Microsoft
description: Informazioni su come toowork con le date nel database di Azure Cosmos.
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a>Uso delle date in Azure Cosmos DB
Azure Cosmos DB offre flessibilità dello schema e un'indicizzazione avanzata tramite un modello di dati [JSON](http://www.json.org) nativo. Tutte le risorse di Azure Cosmos DB, inclusi database, raccolte, documenti e procedure archiviate, sono modellate e archiviate come documenti JSON. Come requisito per essere portatile, JSON, insieme a Azure Cosmos DB, supporta solo un piccolo set di tipi di base: String, Number, Boolean, Array, Object e Null. Tuttavia, JSON è flessibile e consente agli sviluppatori e Framework toorepresent tipi più complessi utilizzando queste primitive e componendoli come oggetti o matrici. 

In tipi di base toohello inoltre, molte applicazioni necessario hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) digitare le date toorepresent e timestamp. In questo articolo viene descritto come gli sviluppatori possono archiviare, recuperare e date nel database di Azure Cosmos utilizzando hello SDK .NET di query.

## <a name="storing-datetimes"></a>Archiviazione di valori DateTime
Per impostazione predefinita, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializza i valori DateTime come [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) stringhe. La maggior parte delle applicazioni è possono utilizzare rappresentazione di stringa hello predefinito per DateTime per hello seguenti motivi:

* Per confrontare stringhe e hello relativo ordinamento dei valori DateTime hello verrà mantenuto quando sono toostrings trasformato. 
* Questo approccio non richiede codici o attributi personalizzati per la conversione JSON.
* le date di Hello archiviata in JSON sono risorse umane leggibile.
* Questo approccio può sfruttare l'indicizzazione di Azure Cosmos DB per query più veloci.

Ad esempio, hello seguenti archivi di frammento di codice un `Order` oggetto che contiene due proprietà DateTime - `ShipDate` e `OrderDate` come un documento utilizzando hello .NET SDK:

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

Il documento viene archiviato in Azure Cosmos DB come illustrato di seguito:

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

In alternativa, è possibile archiviare valori DateTime come timestamp Unix, vale a dire, come un numero che rappresenta il numero di hello di secondi trascorsi dal 1 gennaio 1970. La proprietà Timestamp interna di Azure Cosmos DB (`_ts`) segue questo approccio. È possibile utilizzare hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) classe tooserialize date e ore come numeri. 

## <a name="indexing-datetimes-for-range-queries"></a>Indicizzazione dei valori DateTime per le query di intervallo
Le query di intervallo sono comuni con i valori DateTime. Ad esempio, se è necessario toofind tutti gli ordini creati da ieri o trovare tutti gli ordini spediti in hello ultimi 5 minuti, è necessario tooperform le query di intervallo. tooexecute queste query in modo efficiente, è necessario configurare la raccolta per l'indicizzazione intervallo sulle stringhe.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Ulteriori informazioni su tooconfigure criteri di indicizzazione [criteri di indicizzazione Azure Cosmos DB](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Esecuzione di query per i valori DateTime in LINQ
Hello, DocumentDB .NET SDK supporta automaticamente l'esecuzione di query su dati archiviati nel database di Azure Cosmos tramite LINQ. Ad esempio, hello frammento di codice seguente mostra una query LINQ che ordini i filtri che sono stati spediti in hello ultimi tre giorni.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Maggiori informazioni su Azure Cosmos DB SQL query language e hello provider LINQ in [l'esecuzione di query Cosmos DB](documentdb-sql-query.md).

In questo articolo è stato esaminato come toostore, indice e query date e ore in Azure Cosmos DB.

## <a name="next-steps"></a>Passaggi successivi
* Scaricare ed eseguire hello [esempi su GitHub di codice](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* Altre informazioni sulle [query dell'API di DocumentDB](documentdb-sql-query.md)
* Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)
