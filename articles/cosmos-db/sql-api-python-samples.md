---
title: Esempi di Python API SQL per Azure Cosmos DB | Documenti Microsoft
description: "Esempi Python in GitHub per attività comuni in Azure Cosmos DB, tra cui operazioni CRUD."
keywords: Esempi di Python
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: 7f6300b5105b6b54cc27cde4cb95234d7dbf6a98
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Esempi Python per Azure Cosmos DB
> [!div class="op_single_selector"]
> * [Esempi di .NET](sql-api-dotnet-samples.md)
> * [Esempi di Node.js](sql-api-nodejs-samples.md)
> * [Esempi di Python](sql-api-python-samples.md)
> * [Raccolta di esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?sort=0&service=cosmos-db)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Il repository [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) di GitHub include soluzioni di esempio che eseguono operazioni CRUD e altre operazioni comuni su risorse di Azure Cosmos DB. Questo articolo include:

* Collegamenti alle attività in ogni file di progetto Python di esempio. 
* Collegamenti al contenuto di riferimento sulle API correlato.

**Prerequisiti**

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

- È possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio): con la sottoscrizione Visual Studio ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.

[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

È anche necessario [Python SDK](sql-api-sdk-python.md). 
   
   > [!NOTE]
   > Ogni esempio è indipendente e le operazioni di installazione e pulizia sono eseguite automaticamente. Di conseguenza, gli esempi effettuano più chiamate a [document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Ogni volta che questa operazione viene eseguita la sottoscrizione viene fatturato per un'ora di utilizzo per il livello di prestazioni della raccolta da creare. 
   > 
   > 

## <a name="database-examples"></a>Esempi di database
Il [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file il [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) progetto viene illustrato come eseguire le attività seguenti:

| Attività | Informazioni di riferimento sulle API |
| --- | --- |
| [Creare un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Eseguire query in un account per un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Lettura di un database in base all'ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Elencare database per un account](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Eliminare un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Esempi di raccolta
Il [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file il [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) progetto viene illustrato come eseguire le attività seguenti:

| Attività | Informazioni di riferimento sulle API |
| --- | --- |
| [Creare una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Leggere un elenco di raccolte in un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Ottenere una raccolta in base all'ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Ottenere il livello di prestazioni di una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Cambiare il livello di prestazioni di una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Eliminare una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

