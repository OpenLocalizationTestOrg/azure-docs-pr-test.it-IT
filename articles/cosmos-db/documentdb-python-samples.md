---
title: esempi di Python aaaDocumentDB API per Azure Cosmos DB | Documenti Microsoft
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
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Esempi Python per Azure Cosmos DB
> [!div class="op_single_selector"]
> * [Esempi di .NET](documentdb-dotnet-samples.md)
> * [Esempi di Node.js](documentdb-nodejs-samples.md)
> * [Esempi di Python](documentdb-python-samples.md)
> * [Raccolta di esempi di codice di Azure](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

Esempi di soluzioni che eseguono operazioni CRUD e altre operazioni sulle risorse di Azure Cosmos DB comuni sono inclusi in hello [python di azure documentdb](https://github.com/Azure/azure-documentdb-python/tree/master/samples) repository GitHub. Questo articolo include:

* Attività toohello di collegamenti in ognuno dei file di progetto di esempio Python hello. 
* Toohello collegamenti correlati di contenuti di riferimento API.

**Prerequisiti**

1. È necessario un account di Azure di toouse questi esempi di Python:
   * È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/): si ottiene crediti è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che vengono utilizzati fino è possibile tenere conto di hello e liberare di utilizzare servizi di Azure, ad esempio siti Web. Carta di credito non verranno mai addebitata, a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.
     * È possibile [attivare i benefici della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): con la sottoscrizione Visual Studio ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.
2. È inoltre necessario hello [Python SDK](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Ogni esempio è indipendente e le operazioni di installazione e pulizia sono eseguite automaticamente. Di conseguenza, gli esempi di hello eseguire più chiamate troppo[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Ogni volta che questa operazione viene eseguita la sottoscrizione verrà addebitata per un'ora di utilizzo per ogni livello di prestazioni hello dell'insieme di hello viene creato. 
   > 
   > 

## <a name="database-examples"></a>Esempi di database
Hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) file hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) progetto Mostra come hello tooperform seguenti attività.

| Attività | Informazioni di riferimento sulle API |
| --- | --- |
| [Creare un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Eseguire query in un account per un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Leggere un database in base all'ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Elencare database per un account](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Eliminare un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Esempi di raccolta
Hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) file hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) progetto Mostra come hello tooperform seguenti attività.

| Attività | Informazioni di riferimento sulle API |
| --- | --- |
| [Creare una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Leggere un elenco di raccolte in un database](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Ottenere una raccolta in base all'ID](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Ottenere il livello di prestazioni di una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Cambiare il livello di prestazioni di una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Eliminare una raccolta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

