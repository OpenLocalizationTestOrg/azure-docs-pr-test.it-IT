---
title: un'applicazione Azure Cosmos DB .NET utilizzando aaaBuild hello API Graph | Documenti Microsoft
description: "Visualizza un esempio di codice .NET è possibile utilizzare tooconnect tooand query Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: Compilare un'applicazione .NET usando hello API Graph

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database e l'utilizzo di graph (contenitore) hello portale di Azure. Quindi compilazione e l'esecuzione di un'applicazione console basata su hello [API Graph](graph-sdk-dotnet.md) (anteprima).  

## <a name="prerequisites"></a>Prerequisiti

Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Aggiungere un grafo

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si app clone un'API Graph da github, impostare la stringa di connessione hello ed eseguirlo. Si noterà quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Aprire Visual Studio e i file di soluzione hello aperto. 

## <a name="review-hello-code"></a>Esaminare il codice hello

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. File Program.cs aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB. 

* Hello DocumentClient viene inizializzato. Nell'anteprima hello, abbiamo aggiunto un'estensione di graph API client di Azure Cosmos DB hello. Stiamo lavorando in un client di graph autonoma scollegato dal client di Azure Cosmos DB hello e risorse.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Viene creato un nuovo database.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Viene creato un nuovo grafo.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Una serie di passaggi Gremlin vengono eseguite utilizzando hello `CreateGremlinQuery` metodo.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.

1. In Visual Studio 2017, aprire il file app. config hello. 

2. Nel portale di Azure nell'account di Azure Cosmos DB, hello fare clic su **chiavi** nel riquadro di spostamento sinistro hello. 

    ![Visualizzare e copiare una chiave primaria nel portale di Azure, nella pagina chiavi hello hello](./media/create-graph-dotnet/keys.png)

3. Copia il **URI** valore dal portale hello e renderlo hello valore della chiave di Endpoint hello in App. config. È possibile utilizzare il pulsante di copia hello come mostrato nella precedente schermata valore di hello toocopy hello.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Copia il **chiave primaria** valore dal portale hello e renderlo hello valore della chiave AuthKey hello in App. config, quindi salvare le modifiche. 

    `<add key="AuthKey" value="FILLME" />`

È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB. 

## <a name="run-hello-console-app"></a>Eseguire app console hello

1. In Visual Studio, fare clic su hello **GraphGetStarted** nel progetto **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**. 

2. In hello NuGet **Sfoglia** digitare *Microsoft.Azure.Graphs* e controllare hello **include una versione provvisoria** casella. 

3. Dai risultati di hello, installare hello **Microsoft.Azure.Graphs** libreria. Questo Installa pacchetto di hello Azure Cosmos DB grafico estensione della libreria e tutte le dipendenze.

    Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**. Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.

4. Premere CTRL + F5 applicazione hello toorun.

   finestra della console Hello Visualizza vertici hello e bordi aggiunti toohello grafico. Quando hello completamento dello script, premere INVIO due volte finestra della console hello tooclose. 

## <a name="browse-using-hello-data-explorer"></a>Sfogliare il modello utilizzando hello Esplora dati

È possibile tornare indietro tooData Explorer nel portale di Azure hello e Sfoglia e query nei nuovi dati grafico.

1. In Esplora dati hello nuovo database verrà visualizzato nel riquadro di grafici di hello. Espandere **graphdb** e **graphcollz** e quindi fare clic su **Grafico**.

2. Fare clic su hello **Applica filtro** predefinito di hello toouse pulsante query tooview tutti i vertici hello nel grafico hello. dati Hello generati dall'applicazione di esempio hello viene visualizzati nel riquadro di grafici di hello.

    È possibile ingrandire o ridurre il grafico di hello, è possibile espandere lo spazio di visualizzazione grafico hello, aggiungere ulteriori vertici e spostare vertici su hello dell'area di visualizzazione.

    ![Visualizza un grafico di hello in Esplora dati nel portale di Azure hello](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente: 

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come creare un grafico utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app. È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin. 

> [!div class="nextstepaction"]
> [Eseguire query con Gremlin](tutorial-query-graph.md)

