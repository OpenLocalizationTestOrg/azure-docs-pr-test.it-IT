---
title: un database di documenti DB Cosmos Azure con Java aaaCreate | Documenti Microsoft | Microsoft documenti
description: "Visualizza un esempio di codice Java è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>DB Cosmos Azure: Creare un database di documenti tramite Java e hello portale di Azure

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida rapida viene creato un documento utilizzando database hello gli strumenti del portale di Azure per Azure Cosmos DB. Questa Guida rapida illustra anche come tooquickly creare un'applicazione console Java utilizzando hello [API Java di DocumentDB](documentdb-sdk-java.md). istruzioni di Hello in questa Guida rapida possono essere seguite in qualsiasi sistema operativo che è in grado di eseguire Java. Completando questa Guida rapida sarà familiarità con la creazione e la modifica delle risorse di database di documenti in hello dell'interfaccia utente o a livello di codice, a seconda del valore è la preferenza.

## <a name="prerequisites"></a>Prerequisiti

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * In Ubuntu, eseguire `apt-get install default-jdk` tooinstall hello JDK.
    * Essere tooset che hello JAVA_HOME ambiente variabile toopoint toohello cartella in cui è installato hello JDK.
* [Scaricare](http://maven.apache.org/download.cgi) e [installare](http://maven.apache.org/install.html) un archivio binario [Maven](http://maven.apache.org/)
    * In Ubuntu, è possibile eseguire `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * In Ubuntu, è possibile eseguire `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

Prima di creare un database di documenti, è necessario un account di database SQL (DocumentDB) con Azure Cosmos DB toocreate.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Aggiungere una raccolta

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Aggiungere dati di esempio

È ora possibile aggiungere una nuova raccolta utilizzando Esplora dati tooyour dati.

1. In Esplora dati hello nuovo database verrà visualizzato nel riquadro raccolte hello. Espandere hello **attività** del database, espandere hello **elementi** raccolta, fare clic su **documenti**, quindi fare clic su **nuovi documenti**. 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Ora è possibile aggiungere una raccolta di documenti toohello con hello seguente struttura.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Dopo aver aggiunto hello json toohello **documenti** scheda, fare clic su **salvare**.

    ![Copiare i dati json e fare clic su Salva in Esplora dati nel portale di Azure hello](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Creare e salvare un documento più in cui si inserisce un valore univoco per hello `id` proprietà e modificare hello altre proprietà nel modo desiderato. I nuovi documenti possono avere la struttura desiderata, perché Azure Cosmos DB non impone alcuno schema per i dati.

     È possibile utilizzare le query in Esplora dati tooretrieve i dati facendo clic su hello **Modifica filtro** e **Applica filtro** pulsanti. Per impostazione predefinita, si utilizza Esplora dati `SELECT * FROM c` tooretrieve tutti i documenti nella raccolta di hello, ma è possibile modificare tale tooa diversi [query SQL](documentdb-sql-query.md), ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tutti i documenti hello in ordine decrescente in base a al relativo timestamp. 
 
     È inoltre possibile utilizzare Esplora dati toocreate stored procedure, funzioni definite dall'utente e anche logica di business sul lato server tooperform trigger come velocità effettiva di scala. Esplora dati espone tutti hello predefinite a livello di codice l'accesso ai dati disponibile in hello API, ma fornisce un accesso semplice tooyour dati hello portale di Azure.

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si passa tooworking con il codice. Si clona una app per le API DocumentDB da GitHub, impostare la stringa di connessione hello ed eseguirlo. Viene visualizzato quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `CD` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Esaminare il codice hello

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. Aprire hello `Program.java` file dalla cartella \src\GetStarted hello e trovare le righe di codice che creano hello risorse Azure Cosmos DB. 

* Hello `DocumentClient` viene inizializzato.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Viene creato un nuovo database.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Viene creata una nuova raccolta.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Vengono creati alcuni documenti.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Viene eseguita una query SQL su JSON.

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello. In questo modo il toocommunicate app con il database di hosting.

1. In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**. È possibile usare i pulsanti copia hello per il lato destro hello di hello toocopy di hello schermata URI e chiave primaria in hello `Program.java` file nel passaggio successivo hello.

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. In aprire hello `Program.java` file, copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderla hello valore hello endpoint toohello DocumentClient costruttore `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Quindi copiare il valore di chiave primaria dal portale di hello e incollarla su "FILLME", rendendo hello secondo parametro nel costruttore DocumentClient hello. È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB. 
    
## <a name="run-hello-app"></a>Eseguire app hello

1. Nella finestra terminale git hello, `cd` toohello azure-cosmos-db-documentdb-java-getting-started cartella.

2. Nella finestra terminal git hello, digitare `mvn package` tooinstall hello necessari pacchetti Java.

3. Nella finestra terminale di hello git, eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` hello finestra terminale toostart l'applicazione Java.

    Nella finestra terminal hello, si riceverà la notifica che hello FamilyDB database è stato creato e toopress toocontinue una chiave. Premere un database di hello toocreate chiave, quindi passare toohello Esplora dati e si noterà che ora contiene un database FamilyDB. Continuare toopress chiavi toocreate hello hello e raccolta documenti e quindi eseguire una query. Al termine del progetto hello, vengono eliminate le risorse di hello dal tuo account. 

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come toocreate un account Azure Cosmos DB, database di documenti e raccolta utilizzando Esplora dati hello ed eseguire un toodo app hello stessa operazione a livello di codice. È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi. 

> [!div class="nextstepaction"]
> [Importare dati in Azure Cosmos DB](import-data.md)


