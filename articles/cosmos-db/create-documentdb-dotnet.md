---
title: 'Azure Cosmos DB: Creare un''app web con .NET e hello API DocumentDB | Documenti Microsoft'
description: "Visualizza un esempio di codice .NET è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>DB Cosmos Azure: Creare un'app di web API DocumentDB con .NET e hello portale di Azure

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure. Verrà quindi compilare e distribuire un'app web di elenco todo basata su hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md), come illustrato nella seguente schermata hello. 

![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Prerequisiti

Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     È ora possibile utilizzare le query in Esplora dati tooretrieve i dati. Per impostazione predefinita, si utilizza Esplora dati `SELECT * FROM c` tooretrieve tutti i documenti nella raccolta di hello, ma è possibile modificare tale tooa diversi [query SQL](documentdb-sql-query.md), ad esempio `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn tutti i documenti hello in ordine decrescente in base a al relativo timestamp.
 
     È inoltre possibile utilizzare Esplora dati toocreate stored procedure, funzioni definite dall'utente e anche logica di business sul lato server tooperform trigger come velocità effettiva di scala. Esplora dati espone tutti hello predefinite a livello di codice l'accesso ai dati disponibile in hello API, ma fornisce un accesso semplice tooyour dati hello portale di Azure.

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si passa tooworking con il codice. Si clona una app per le API DocumentDB da GitHub, impostare la stringa di connessione hello ed eseguirlo. Si noterà quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `CD` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Aprire file di soluzione todo hello in Visual Studio. 

## <a name="review-hello-code"></a>Esaminare il codice hello

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. File DocumentDBRepository.cs aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB. 

* Hello DocumentClient viene inizializzato su riga 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Viene creato un nuovo database alla riga 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Viene creata una nuova raccolta alla riga 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.

1. In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**. Utilizzare i pulsanti di hello copia sul lato destro hello di hello toocopy di hello schermata URI e chiave primaria nel file Web. config hello nel passaggio successivo hello.

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. In Visual Studio 2017, aprire il file Web. config hello. 

3. Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave di endpoint hello in Web. config. 

    `<add key="endpoint" value="FILLME" />`

4. Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore authKey hello in Web. config. È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Eseguire app web hello
1. In Visual Studio, fare clic su progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**. 

2. In hello NuGet **Sfoglia** digitare *DocumentDB*.

3. Dai risultati di hello, installare hello **Microsoft.Azure.DocumentDB** libreria. Consente di installare il pacchetto di Microsoft.Azure.DocumentDB hello, nonché tutte le dipendenze.

4. Premere CTRL + F5 applicazione hello toorun. L'app viene visualizzata nel browser. 

5. Fare clic su **Crea nuovo** in hello browser e creare nuove attività alcuni nell'app attività da eseguire.

   ![App elenco attività con dati di esempio](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

È ora possibile tornare indietro tooData Esplora e vedere query, modificare e funzionare con questi nuovi dati. 

## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app web. È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi. 

> [!div class="nextstepaction"]
> [Importare dati in Azure Cosmos DB](import-data.md)


