---
title: 'Esercitazione su NoSQL: API di DocumentDB per Azure Cosmos DB Java SDK | Microsoft Docs'
description: "In questa esercitazione NoSQL che crea un database online e l'applicazione console Java utilizzando l'API DocumentDB hello per Azure Cosmos DB. Azure DocumentDB è un database NoSQL per JSON."
keywords: esercitazione su nosql, database online, applicazione console java
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Esercitazione su NoSQL: Compilare un'applicazione console Java con l'API di DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js per MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Introduzione toohello NoSQL esercitazione per l'API DocumentDB hello Azure SDK per Java DB Cosmos. Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.

Argomenti trattati:

* Creazione e connessione account Azure Cosmos DB tooan
* Configurare una soluzione Visual Studio
* Creazione di un database online
* Creare una raccolta
* Creazione di documenti JSON
* Esecuzione di query hello raccolta
* Creazione di documenti JSON
* Esecuzione di query hello raccolta
* Sostituzione di un documento
* Eliminazione di un documento
* L'eliminazione di database hello

Ecco come procedere.

## <a name="prerequisites"></a>Prerequisiti
Verificare di che aver seguito hello:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.
* [Git](https://git-scm.com/downloads)
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Passaggio 1: Creare un account di Azure Cosmos DB
Creare prima di tutto un account Azure Cosmos DB. Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[progetto GitHub di Clone hello](#GitClone). Se si utilizza l'emulatore di Azure Cosmos DB hello, seguire i passaggi di hello in [emulatore di Azure Cosmos DB](local-emulator.md) tooset backup emulatore hello e andare troppo[progetto GitHub di Clone hello](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Passaggio 2: Clonare progetto GitHub hello
È possibile iniziare duplicando il repository GitHub hello per [Introduzione a Azure Cosmos DB e Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Ad esempio, eseguire hello seguente tooretrieve hello del progetto di esempio in locale da una directory locale.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Hello directory contiene un `pom.xml` per progetto hello e una `src` cartella che contiene codice di origine Java inclusi `Program.java` che mostra come esegue semplici operazioni con Azure Cosmos DB come la creazione di documenti e query sui dati all'interno di un raccolta. Hello `pom.xml` include una dipendenza hello [DocumentDB SDK per Java su Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Passaggio 3: Connettere l'account di Azure Cosmos DB tooan
Successivamente, head nuovamente toohello [portale Azure](https://portal.azure.com) tooretrieve l'endpoint e la chiave master primaria. Hello Azure Cosmos DB endpoint e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.

In hello portale di Azure, passare tooyour Azure Cosmos DB account e quindi fare clic su **chiavi**. Copiare hello URI dal portale di hello e incollarlo in `https://FILLME.documents.azure.com` nel file Program.java hello. Quindi copia hello chiave primaria dal portale hello e incollarlo in `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Cattura di schermata del portale di Azure utilizzato da hello NoSQL esercitazione toocreate un'applicazione console Java hello. Viene illustrato un database di Azure Cosmos account, con l'hub attivo hello evidenziato, hello pulsante CHIAVI evidenziato nel Pannello di account Azure Cosmos DB hello e valori URI, la chiave primaria e SECONDARIA hello evidenziato nella hello pannello chiavi][keys]

## <a name="step-4-create-a-database"></a>Passaggio 4: Creare un database
Il database di Azure Cosmos [database](documentdb-resources.md#databases) possono essere create usando hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) metodo hello **DocumentClient** classe. Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Passaggio 5: Creare una raccolta
> [!WARNING]
> **createCollection** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) metodo hello **DocumentClient** classe. Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON
Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) metodo hello **DocumentClient** classe. I documenti sono contenuto JSON definito dall'utente (arbitrario). Ora è possibile inserire uno o più documenti. Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) dati hello tooimport in un database.

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagramma che illustra relazione gerarchica di hello tra account hello, database online hello, raccolta hello e documenti hello utilizzato dai hello NoSQL esercitazione toocreate un'applicazione console Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB
Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.  Hello codice di esempio seguente viene illustrato come tooquery dei documenti in Azure Cosmos DB utilizzando la sintassi SQL con hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) metodo.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON
Azure Cosmos DB supporta l'aggiornamento di documenti JSON tramite hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) metodo.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON
Analogamente, Azure Cosmos DB supporta l'eliminazione di documenti JSON tramite hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) metodo.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Passaggio 10: Eliminare database hello
L'eliminazione database hello creato rimuove database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console Java
un'applicazione hello toorun dalla console di hello passare toohello cartella del progetto e compilazione Maven utilizzando:
    
    mvn package

Esecuzione `mvn package` Scarica libreria Azure Cosmos DB più recente di hello Maven e produce `GetStarted-0.0.1-SNAPSHOT.jar`. Eseguire quindi l'applicazione hello eseguendo:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Congratulazioni. L'esercitazione su NoSQL è stata completata ed è stata creata un'applicazione console Java funzionante.

## <a name="next-steps"></a>Passaggi successivi
* Per un'esercitazione su app Web Java, vedere [Creazione di un'applicazione Web Java con Azure Cosmos DB](documentdb-java-application.md).
* Informazioni su come troppo[monitorare un account Azure Cosmos DB](monitor-accounts.md).
* Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).
* Ulteriori informazioni sul modello di programmazione hello nella sezione sviluppo di hello hello [pagina della documentazione di Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
