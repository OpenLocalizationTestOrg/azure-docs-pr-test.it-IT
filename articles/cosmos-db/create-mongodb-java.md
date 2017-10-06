---
title: 'Azure Cosmos DB: Compilare un''applicazione console con Java e hello MongoDB API | Documenti Microsoft'
description: "Visualizza un esempio di codice Java è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure DB Cosmos: Compilare un'applicazione console API MongoDB con Java e hello portale di Azure

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure. Verrà quindi compilare e distribuire un'applicazione console basata su hello [driver MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Prerequisiti

* Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:
   * JDK 1.7+ (eseguire `apt-get install default-jdk` se JDK non è disponibile)
   * Maven (eseguire `apt-get install maven` se Maven non è disponibile)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Aggiungere una raccolta

Assegnare un nome al nuovo database, **db**, e alla nuova raccolta, **coll**.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si app clone un'API di MongoDB da github, impostare la stringa di connessione hello ed eseguirlo. Si noterà quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Aprire quindi il file di soluzione hello in Visual Studio. 

## <a name="review-hello-code"></a>Esaminare il codice hello

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. Aprire hello `Program.cs` file e trovare le righe di codice creano hello risorse Azure Cosmos DB. 

* Hello DocumentClient viene inizializzato.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Vengono creati un nuovo database e una nuova raccolta.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Vengono inseriti alcuni documenti usando `MongoCollection.insertOne`

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Vengono eseguite alcune query usando `MongoCollection.find`

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.

1. Hello Account, selezionare **avvio rapido**selezionare Java, quindi copiare negli Appunti tooyour stringa di connessione hello

2. Aprire hello `Program.java` file, sostituire hello argomento toohello MongoClientURI costruttore con la stringa di connessione hello. È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB. 
    
## <a name="run-hello-console-app"></a>Eseguire app console hello

1. Eseguire `mvn package` in un terminal tooinstall necessari moduli npm

2. Eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` in un terminal toostart l'applicazione Java.

È ora possibile usare [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificare e utilizzare questi nuovi dati.

## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'applicazione console. È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi. 

> [!div class="nextstepaction"]
> [Importare i dati di MongoDB in Azure Cosmos DB](mongodb-migrate.md)


