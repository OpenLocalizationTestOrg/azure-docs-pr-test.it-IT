---
title: un database di graph di Azure Cosmos DB con Java aaaCreate | Documenti Microsoft
description: "Visualizza un linguaggio del codice è possibile utilizzare i dati del grafico tooconnect tooand query nel database di Azure Cosmos utilizzando Gremlin di esempio."
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
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>DB Cosmos Azure: Creare un database di graph tramite Java e hello portale di Azure

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida rapida viene creato un grafico utilizzando database hello gli strumenti del portale di Azure per Azure Cosmos DB. Questa Guida rapida illustra anche come tooquickly creare un'applicazione console Java utilizzando un database di grafico con i sistemi operativi hello [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver. istruzioni di Hello in questa Guida rapida possono essere seguite in qualsiasi sistema operativo che è in grado di eseguire Java. Questa Guida rapida consente di acquisire familiarità con la creazione e la modifica delle risorse di grafico in hello dell'interfaccia utente o a livello di codice, a seconda del valore è la preferenza. 

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

Prima di creare un database di grafico, è necessario un account di database Gremlin (grafico) con Azure Cosmos DB toocreate.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Aggiungere un grafo

A questo punto, è possibile utilizzare strumento di esplorazione dei dati hello in hello toocreate portale Azure un database di grafico. 

1. Nel portale di Azure, nel menu di navigazione sinistro hello, hello fare clic su **Esplora dati (anteprima)**. 
2. In hello **Esplora dati (anteprima)** pannello, fare clic su **nuovo grafico**, quindi immettere nella pagina di hello mediante hello le seguenti informazioni:

    ![Esplora dati in hello portale di Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    Impostazione|Valore consigliato|Descrizione
    ---|---|---
    ID database|sample-database|Hello ID per il nuovo database. I nomi dei database devono avere una lunghezza compresa tra 1 e 255 caratteri e non possono contenere `/ \ # ?` o spazi finali.
    ID grafo|sample-graph|Hello ID per il nuovo grafico. I nomi dei grafici sono hello stesso carattere requisiti come ID di database.
    Capacità di archiviazione| 10 GB|Lasciare il valore di predefinito hello. Questa è la capacità di archiviazione hello del database hello.
    Velocità effettiva|400 UR/s|Lasciare il valore di predefinito hello. È possibile scalare in verticale della velocità effettiva hello in un secondo momento se si desidera tooreduce latenza.
    Chiave di partizione|Lasciare vuoto|A scopo di hello di questa Guida rapida, lasciare vuota la chiave di partizione hello.

3. Una volta compilato il modulo di hello, fare clic su **OK**.

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si clonare un'app di grafico da github, impostare la stringa di connessione hello ed eseguirlo. Viene visualizzato quanto sia facile toowork con i dati a livello di codice. 

1. Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Esaminare il codice hello

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. Aprire hello `Program.java` file dalla cartella \src\GetStarted hello e trovare le righe di codice. 

* Hello Gremlin `Client` viene inizializzato dalla configurazione hello in `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Una serie di passaggi Gremlin vengono eseguite utilizzando hello `client.submit` metodo.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

1. File src/remote.yaml hello aperto. 

3. Compilare il *host*, *username*, e *password* valori nel file src/remote.yaml hello. altre Hello hello impostazioni non è necessario toobe modificato.

    Impostazione|Valore consigliato|Descrizione
    ---|---|---
    Hosts|[***.graphs.azure.com]|Vedere la figura hello segue questa tabella. Questo valore è hello Gremlin URI nella pagina di panoramica hello del portale di Azure, tra parentesi quadre, hello finali hello: 443 / rimosso.<br><br>Questo valore può anche essere recuperato dalla scheda chiavi hello, usando il valore URI hello rimozione https://, la modifica di documenti toographs, nonché hello finali: 443 /.
    Username|/dbs/sample-database/colls/sample-graph|risorse del form hello Hello `/dbs/<db>/colls/<coll>` in `<db>` è il nome del database esistente e `<coll>` è il nome della raccolta esistente.
    Password|*Chiave master primaria*|Vedere hello seconda figura è presente nella tabella seguente. Questo valore è la chiave primaria, che è possibile recuperare dalla pagina chiavi hello del portale di Azure, nella casella di chiave primaria hello hello. Copiare il valore di hello utilizzando il pulsante di copia hello hello destra della casella hello.

    Per il valore di host hello, copiare hello **Gremlin URI** valore hello **Panoramica** pagina. Se è vuota, vedere le istruzioni di hello nella riga hello host hello tabella sulla creazione di hello Gremlin URI dal pannello chiavi hello precedente.
![Visualizzare e copiare valore URI Gremlin hello nella pagina di panoramica hello in hello portale di Azure](./media/create-graph-java/gremlin-uri.png)

    Per il valore di Password hello, copiare hello **chiave primaria** da hello **chiavi** pannello: ![visualizzare e copiare la chiave primaria nel portale di Azure hello chiavi pagina](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Eseguire app console hello

1. Nella finestra terminale git hello, `cd` toohello azure-cosmos-db-graph-java-getting-started cartella.

2. Nella finestra terminal git hello, digitare `mvn package` tooinstall hello necessari pacchetti Java.

3. Nella finestra terminale di hello git, eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` hello finestra terminale toostart l'applicazione Java.

finestra terminale Hello Visualizza vertici hello aggiunti toohello grafico. Al termine del programma hello, passa indietro toohello portale di Azure nel browser internet. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Verificare e aggiungere dati di esempio

È possibile tornare indietro tooData Explorer e vedere i vertici hello aggiunto toohello grafico e aggiungere ulteriori punti dati.

1. In Esplora dati espandere hello **database di esempio**/**grafico di esempio**, fare clic su **grafico**, quindi fare clic su **Applica filtro**. 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure hello](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. In hello **risultati** elenco, l'aggiunta di nuovi utenti hello toohello grafico. Selezionare **ben** e notare che si è connesso toorobin. È possibile spostarsi vertici hello in Esplora grafico hello, ingrandire e ridurre ed espandere hello dimensioni dell'area di Esplora grafico hello. 

   ![Nuovo vertici nel grafico hello in Esplora dati nel portale di Azure hello](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Aggiungere alcuni nuovo grafico toohello di utenti con hello Esplora dati. Fare clic su hello **nuovi Vertex** grafico tooyour dati tooadd di pulsante.

   ![Creare nuovi documenti in Esplora dati nel portale di Azure hello](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Immettere un'etichetta di *persona* quindi immettere hello seguenti chiavi e valori primo vertice hello toocreate nel grafico hello. Si noti che è possibile creare proprietà univoche per ogni persona del grafo. È necessaria solo hello id chiave.

    key|value|Note
    ----|----|----
    id|ashley|Identificatore univoco di Hello per vertice hello. Se non si specifica alcun ID, ne verrà generato automaticamente uno.
    gender|female| 
    tech | java | 

    > [!NOTE]
    > In questa esercitazione introduttiva viene creata una raccolta non partizionata. Tuttavia, se si crea una raccolta partizionata specificando una chiave di partizione durante la creazione dell'insieme di hello, è necessario chiave di partizione hello tooinclude come chiave in ogni nuovo vertice. 

5. Fare clic su **OK**. Potrebbe essere necessario tooexpand toosee la schermata **OK** nella parte inferiore di hello della schermata di hello.

6. Fare di nuovo clic su **New Vertex** (Nuovo vertice) e aggiungere un altro nuovo utente. Immettere un'etichetta di *persona* quindi immettere il seguente hello chiavi e valori:

    key|value|Note
    ----|----|----
    id|rakesh|Identificatore univoco di Hello per vertice hello. Se non si specifica alcun ID, ne verrà generato automaticamente uno.
    gender|male| 
    school|MIT| 

7. Fare clic su **OK**. 

8. Fare clic su **Applica filtro** predefinito hello `g.V()` filtro. Tutti gli utenti di hello ora Mostra in hello **risultati** elenco. Quando si aggiungono più dati, è possibile utilizzare i filtri toolimit i risultati. Per impostazione predefinita, si utilizza Esplora dati `g.V()` tooretrieve tutti i vertici in un grafico, ma è possono modificare tale tooa diversi [query graph](tutorial-query-graph.md), ad esempio `g.V().count()`, tooreturn un conteggio di tutti i vertici hello nel grafico hello in formato JSON.

9. È ora possibile connettere rakesh e ashley. Verificare **Alice** in selezionata nel hello **risultati** elenco, quindi fare clic su pulsante Modifica hello Avanti troppo**destinazioni** nel lato inferiore destro. Potrebbe essere necessario toowiden il hello toosee finestra **proprietà** area.

   ![Modificare la destinazione di hello di un vertice in un grafico](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. In hello **destinazione** digitare *rakesh*e in hello **etichetta Edge** nella casella *sa*e quindi fare clic sulla casella di controllo hello.

   ![Aggiungere una connessione tra ashley e rakesh in Esplora dati](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. A questo punto selezionare **rakesh** dall'elenco dei risultati hello e vedere che Alice e rakesh siano connessi. 

   ![Due vertici connessi in Esplora dati](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    È inoltre possibile utilizzare Esplora dati toocreate stored procedure, funzioni definite dall'utente e anche logica di business sul lato server tooperform trigger come velocità effettiva di scala. Esplora dati espone tutti hello predefinite a livello di codice l'accesso ai dati disponibile in hello API, ma fornisce un accesso semplice tooyour dati hello portale di Azure.



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

