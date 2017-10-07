---
title: aaaHow tooquery dati della tabella nel database di Azure Cosmos? | Microsoft Docs
description: Ulteriori dati della tabella nel database di Azure Cosmos tooquery
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB: Come dati della tabella tooquery utilizzando hello tabella API (anteprima)?

Hello Azure Cosmos DB [tabella API](table-introduction.md) (anteprima) supporta OData e [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) query su dati chiave/valore (tabella).  

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Eseguire query sui dati con tabella API hello

le query in questo articolo Hello utilizzano seguendo l'esempio hello `People` tabella:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Poiché Azure Cosmos DB è compatibile con le API di archiviazione Azure Table hello, vedere [esecuzione di query su tabelle ed entità] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) per informazioni dettagliate su come tooquery utilizzando hello Tabella API. 

Per ulteriori informazioni sulle funzionalità premium hello che offre Azure Cosmos DB, vedere [DB Cosmos Azure: tabella API](table-introduction.md) e [sviluppare con API di tabelle in .NET hello](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Prerequisiti

Per questi toowork query, è necessario dispone di un account Azure Cosmos DB e disporre di dati di entità nel contenitore hello. Questi requisiti non sono disponibili? Hello completo [Guida introduttiva di cinque minuti](https://aka.ms/acdbtnetqs) o hello [esercitazione developer](https://aka.ms/acdbtabletut) toocreate un account e popolare il database.

## <a name="query-on-partitionkey-and-rowkey"></a>Query su PartitionKey e RowKey
Poiché le proprietà PartitionKey e RowKey hello formano la chiave primaria di un'entità, è possibile utilizzare hello seguenti entità di una sintassi speciale tooidentify hello: 

**Query**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Risultati**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

In alternativa, è possibile specificare queste proprietà come parte di hello `$filter` opzione, come illustrato nella seguente sezione hello. Si noti che i nomi di proprietà chiave hello e valori costanti tra maiuscole e minuscole. Sia hello PartitionKey e RowKey proprietà sono di tipo stringa. 

## <a name="query-by-using-an-odata-filter"></a>Eseguire una query usando un filtro OData
Quando si crea una stringa di filtro, tenere presente queste regole: 

* Usare hello operatori logici definiti dalla specifica del protocollo OData toocompare un valore della proprietà tooa hello. Si noti che non è possibile confrontare un valore di proprietà tooa dinamico. Un lato dell'espressione hello deve essere una costante. 
* valore costante, operatore e il nome di proprietà Hello devono essere separati da spazi con codifica URL. Uno spazio con codifica URL è come `%20`. 
* Tutte le parti della stringa di filtro hello maiuscole e minuscole. 
* valore costante Hello deve essere di hello del tipo di dati stesso come proprietà hello affinché hello filtro tooreturn valido risultati. Per ulteriori informazioni sui tipi di proprietà supportati, vedere [hello comprensione modello di dati del servizio tabelle](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Ecco una query di esempio che illustra come toofilter da hello PartitionKey e le proprietà di posta elettronica utilizzando un OData `$filter`.

**Query**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Per ulteriori informazioni su come tooconstruct espressioni per vari tipi di dati di filtro, vedere [query su tabelle ed entità](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Risultati**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Eseguire una query utilizzando LINQ 
È anche possibile eseguire una query utilizzando LINQ, che converte le espressioni di query OData corrispondente toohello. Di seguito è riportato un esempio di come query toobuild utilizzando hello .NET SDK:

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Appreso come tooquery utilizzando hello tabella API (anteprima) 

È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.

> [!div class="nextstepaction"]
> [Distribuire i dati a livello globale](tutorial-global-distribution-documentdb.md)
