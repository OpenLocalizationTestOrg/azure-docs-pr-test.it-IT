---
title: Creare un database a grafo di Azure Cosmos DB con Java | Microsoft Docs
description: Presenta un esempio di codice Java che permette di connettersi ai dati di un grafo ed eseguire query su di essi in Azure Cosmos DB tramite Gremlin.
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
ms.openlocfilehash: 0273072c7c10e219ab8d6c85eb252badafc17147
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-the-azure-portal"></a><span data-ttu-id="a1cad-103">Azure Cosmos DB: Creare un database a grafo con Java e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a1cad-103">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>

<span data-ttu-id="a1cad-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a1cad-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a1cad-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a1cad-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a1cad-106">Questa esercitazione introduttiva illustra come creare un database a grafo con gli strumenti del portale di Azure per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a1cad-106">This quickstart creates a graph database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="a1cad-107">Illustra anche come creare rapidamente un'app console Java usando un database a grafo con il driver OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver).</span><span class="sxs-lookup"><span data-stu-id="a1cad-107">This quickstart also shows you how to quickly create a Java console app using a graph database using the OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="a1cad-108">Le istruzioni di questa guida introduttiva possono essere eseguite in qualsiasi sistema operativo in grado di eseguire Java.</span><span class="sxs-lookup"><span data-stu-id="a1cad-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="a1cad-109">Questa guida introduttiva consente di acquisire familiarità con la creazione e la modifica di risorse di tipo grafo nell'interfaccia utente o a livello di codice, in base alle proprie preferenze.</span><span class="sxs-lookup"><span data-stu-id="a1cad-109">This quickstart familiarizes you with creating and modifying graph resources in either the UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1cad-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a1cad-110">Prerequisites</span></span>

* [<span data-ttu-id="a1cad-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="a1cad-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="a1cad-112">In Ubuntu eseguire `apt-get install default-jdk` per installare JDK.</span><span class="sxs-lookup"><span data-stu-id="a1cad-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="a1cad-113">Assicurarsi di impostare la variabile di ambiente JAVA_HOME in modo che faccia riferimento alla cartella di installazione di JDK.</span><span class="sxs-lookup"><span data-stu-id="a1cad-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="a1cad-114">[Scaricare](http://maven.apache.org/download.cgi) e [installare](http://maven.apache.org/install.html) un archivio binario [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="a1cad-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="a1cad-115">In Ubuntu è possibile eseguire `apt-get install maven` per installare Maven.</span><span class="sxs-lookup"><span data-stu-id="a1cad-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="a1cad-116">Git</span><span class="sxs-lookup"><span data-stu-id="a1cad-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="a1cad-117">In Ubuntu è possibile eseguire `sudo apt-get install git` per installare Git.</span><span class="sxs-lookup"><span data-stu-id="a1cad-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="a1cad-118">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="a1cad-118">Create a database account</span></span>

<span data-ttu-id="a1cad-119">Prima di potere creare un database a grafo, è necessario creare un account database Gremlin (grafo) con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a1cad-119">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="a1cad-120">Aggiungere un grafo</span><span class="sxs-lookup"><span data-stu-id="a1cad-120">Add a graph</span></span>

<span data-ttu-id="a1cad-121">È ora possibile usare lo strumento Esplora dati nel portale di Azure per creare un database a grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-121">You can now use the Data Explorer tool in the Azure portal to create a graph database.</span></span> 

1. <span data-ttu-id="a1cad-122">Nel menu di navigazione a sinistra del portale di Azure fare clic su **Esplora dati (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-122">In the Azure portal, in the left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="a1cad-123">Nel pannello **Esplora dati (anteprima)** fare clic su **New Graph** (Nuovo grafo) e quindi compilare i campi della pagina con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1cad-123">In the **Data Explorer (Preview)** blade, click **New Graph**, then fill in the page using the following information:</span></span>

    ![Esplora dati nel portale di Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="a1cad-125">Impostazione</span><span class="sxs-lookup"><span data-stu-id="a1cad-125">Setting</span></span>|<span data-ttu-id="a1cad-126">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="a1cad-126">Suggested value</span></span>|<span data-ttu-id="a1cad-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a1cad-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="a1cad-128">ID database</span><span class="sxs-lookup"><span data-stu-id="a1cad-128">Database ID</span></span>|<span data-ttu-id="a1cad-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="a1cad-129">sample-database</span></span>|<span data-ttu-id="a1cad-130">ID del nuovo database.</span><span class="sxs-lookup"><span data-stu-id="a1cad-130">The ID for your new database.</span></span> <span data-ttu-id="a1cad-131">I nomi dei database devono avere una lunghezza compresa tra 1 e 255 caratteri e non possono contenere `/ \ # ?` o spazi finali.</span><span class="sxs-lookup"><span data-stu-id="a1cad-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="a1cad-132">ID grafo</span><span class="sxs-lookup"><span data-stu-id="a1cad-132">Graph ID</span></span>|<span data-ttu-id="a1cad-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="a1cad-133">sample-graph</span></span>|<span data-ttu-id="a1cad-134">ID del nuovo grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-134">The ID for your new graph.</span></span> <span data-ttu-id="a1cad-135">I nomi dei grafi presentano gli stessi requisiti relativi ai caratteri degli ID di database.</span><span class="sxs-lookup"><span data-stu-id="a1cad-135">Graph names have the same character requirements as database ids.</span></span>
    <span data-ttu-id="a1cad-136">Capacità di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a1cad-136">Storage Capacity</span></span>| <span data-ttu-id="a1cad-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="a1cad-137">10 GB</span></span>|<span data-ttu-id="a1cad-138">Lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="a1cad-138">Leave the default value.</span></span> <span data-ttu-id="a1cad-139">Indica la capacità di archiviazione del database.</span><span class="sxs-lookup"><span data-stu-id="a1cad-139">This is the storage capacity of the database.</span></span>
    <span data-ttu-id="a1cad-140">Velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="a1cad-140">Throughput</span></span>|<span data-ttu-id="a1cad-141">400 UR/s</span><span class="sxs-lookup"><span data-stu-id="a1cad-141">400 RUs</span></span>|<span data-ttu-id="a1cad-142">Lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="a1cad-142">Leave the default value.</span></span> <span data-ttu-id="a1cad-143">È possibile aumentare la velocità effettiva in un secondo momento se si desidera ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="a1cad-143">You can scale up the throughput later if you want to reduce latency.</span></span>
    <span data-ttu-id="a1cad-144">Chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="a1cad-144">Partition key</span></span>|<span data-ttu-id="a1cad-145">Lasciare vuoto</span><span class="sxs-lookup"><span data-stu-id="a1cad-145">Leave blank</span></span>|<span data-ttu-id="a1cad-146">Per le finalità di questa esercitazione introduttiva, lasciare vuoto il valore relativo alla chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="a1cad-146">For the purpose of this quickstart, leave the partition key blank.</span></span>

3. <span data-ttu-id="a1cad-147">Dopo aver compilato il modulo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-147">Once the form is filled out, click **OK**.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="a1cad-148">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a1cad-148">Clone the sample application</span></span>

<span data-ttu-id="a1cad-149">Clonare ora un'app Graph da GitHub, impostare la stringa di connessione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="a1cad-149">Now let's clone a graph app from github, set the connection string, and run it.</span></span> <span data-ttu-id="a1cad-150">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="a1cad-150">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a1cad-151">Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a1cad-151">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="a1cad-152">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="a1cad-152">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="a1cad-153">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="a1cad-153">Review the code</span></span>

<span data-ttu-id="a1cad-154">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="a1cad-154">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="a1cad-155">Aprire il file `Program.java` dalla cartella \src\GetStarted e trovare queste righe di codice.</span><span class="sxs-lookup"><span data-stu-id="a1cad-155">Open the `Program.java` file from the \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="a1cad-156">Viene inizializzato `Client` di Gremlin dalla configurazione in `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a1cad-156">The Gremlin `Client` is initialized from the configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="a1cad-157">Viene eseguita una serie di passaggi di Gremlin tramite il metodo `client.submit`.</span><span class="sxs-lookup"><span data-stu-id="a1cad-157">A series of Gremlin steps are executed using the `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="a1cad-158">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="a1cad-158">Update your connection string</span></span>

1. <span data-ttu-id="a1cad-159">Aprire il file src/remote.yaml.</span><span class="sxs-lookup"><span data-stu-id="a1cad-159">Open the src/remote.yaml file.</span></span> 

3. <span data-ttu-id="a1cad-160">Inserire i valori relativi a *hosts*, *username* e *password* nel file src/remote.yaml.</span><span class="sxs-lookup"><span data-stu-id="a1cad-160">Fill in your *hosts*, *username*, and *password* values in the src/remote.yaml file.</span></span> <span data-ttu-id="a1cad-161">Non è necessario modificare le impostazioni rimanenti.</span><span class="sxs-lookup"><span data-stu-id="a1cad-161">The rest of the settings do not need to be changed.</span></span>

    <span data-ttu-id="a1cad-162">Impostazione</span><span class="sxs-lookup"><span data-stu-id="a1cad-162">Setting</span></span>|<span data-ttu-id="a1cad-163">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="a1cad-163">Suggested value</span></span>|<span data-ttu-id="a1cad-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a1cad-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="a1cad-165">Hosts</span><span class="sxs-lookup"><span data-stu-id="a1cad-165">Hosts</span></span>|<span data-ttu-id="a1cad-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="a1cad-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="a1cad-167">Vedere la schermata che segue questa tabella.</span><span class="sxs-lookup"><span data-stu-id="a1cad-167">See the screenshot following this table.</span></span> <span data-ttu-id="a1cad-168">Si tratta del valore URI Gremlin disponibile nella pagina Panoramica del portale di Azure, tra parentesi quadre, senza la parte finale :443/.</span><span class="sxs-lookup"><span data-stu-id="a1cad-168">This value is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="a1cad-169">Questo valore può anche essere recuperato dalla scheda Chiavi, usando il valore dell'URI senza https://, sostituendo documents con graphs e rimuovendo la parte :443/ finale.</span><span class="sxs-lookup"><span data-stu-id="a1cad-169">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="a1cad-170">Username</span><span class="sxs-lookup"><span data-stu-id="a1cad-170">Username</span></span>|<span data-ttu-id="a1cad-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="a1cad-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="a1cad-172">Risorsa nel formato `/dbs/<db>/colls/<coll>` dove `<db>` è il nome del database esistente e `<coll>` è il nome della raccolta esistente.</span><span class="sxs-lookup"><span data-stu-id="a1cad-172">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="a1cad-173">Password</span><span class="sxs-lookup"><span data-stu-id="a1cad-173">Password</span></span>|<span data-ttu-id="a1cad-174">*Chiave master primaria*</span><span class="sxs-lookup"><span data-stu-id="a1cad-174">*Your primary master key*</span></span>|<span data-ttu-id="a1cad-175">Vedere la seconda schermata che segue questa tabella.</span><span class="sxs-lookup"><span data-stu-id="a1cad-175">See the second screenshot following this table.</span></span> <span data-ttu-id="a1cad-176">Si tratta della chiave primaria, che può essere recuperata dalla pagina Chiavi del portale di Azure nella casella Chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="a1cad-176">This value is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="a1cad-177">Copiare il valore usando il pulsante di copia a destra della casella.</span><span class="sxs-lookup"><span data-stu-id="a1cad-177">Copy the value using the copy button on the right side of the box.</span></span>

    <span data-ttu-id="a1cad-178">Per il valore Hosts copiare il valore **URI Gremlin** dalla pagina **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-178">For the Hosts value, copy the **Gremlin URI** value from the **Overview** page.</span></span> <span data-ttu-id="a1cad-179">Se la casella è vuota, vedere le istruzioni relative alla riga Hosts nella tabella precedente per la creazione dell'URI Gremlin dal pannello Chiavi.</span><span class="sxs-lookup"><span data-stu-id="a1cad-179">If it's empty, see the instructions in the Hosts row in the preceding table about creating the Gremlin URI from the Keys blade.</span></span>
<span data-ttu-id="a1cad-180">![Visualizzare e copiare il valore dell'URI Gremlin nella pagina Panoramica del portale di Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="a1cad-180">![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="a1cad-181">Per il valore Password, copiare la **Chiave primaria** dal pannello **Chiavi**: ![Visualizzare e copiare la chiave primaria nella pagina Chiavi del portale di Azure](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="a1cad-181">For the Password value, copy the **Primary key** from the **Keys** blade: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="a1cad-182">Eseguire l'app console</span><span class="sxs-lookup"><span data-stu-id="a1cad-182">Run the console app</span></span>

1. <span data-ttu-id="a1cad-183">Nella finestra del terminale git eseguire il comando `cd` per passare alla cartella azure-cosmos-db-graph-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="a1cad-183">In the git terminal window, `cd` to the azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="a1cad-184">Nella finestra del terminale git digitare `mvn package` per installare i pacchetti Java necessari.</span><span class="sxs-lookup"><span data-stu-id="a1cad-184">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="a1cad-185">Nella finestra del terminale git eseguire `mvn exec:java -D exec.mainClass=GetStarted.Program` per avviare l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="a1cad-185">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

<span data-ttu-id="a1cad-186">La finestra del terminale mostra l'aggiunta dei vertici al grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-186">The terminal window displays the vertices being added to the graph.</span></span> <span data-ttu-id="a1cad-187">Al termine del programma, tornare al portale di Azure nel browser Internet.</span><span class="sxs-lookup"><span data-stu-id="a1cad-187">Once the program completes, switch back to the Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="a1cad-188">Verificare e aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="a1cad-188">Review and add sample data</span></span>

<span data-ttu-id="a1cad-189">È ora possibile tornare a Esplora dati e visualizzare i vertici aggiunti al grafo, quindi aggiungere altri punti dati.</span><span class="sxs-lookup"><span data-stu-id="a1cad-189">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="a1cad-190">In Esplora dati espandere **sample-database**/**sample-graph**, fare clic su **Graph** (Grafo) e infine su **Applica filtro**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-190">In Data Explorer, expand the **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Creare nuovi documenti in Esplora dati nel portale di Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="a1cad-192">Nell'elenco **Risultati** verificare i nuovi utenti aggiunti al grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-192">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="a1cad-193">Selezionare **ben**. Come si può notare, è connesso a robin.</span><span class="sxs-lookup"><span data-stu-id="a1cad-193">Select **ben** and notice that he's connected to robin.</span></span> <span data-ttu-id="a1cad-194">È possibile spostare i vertici nello strumento di esplorazione del grafo, fare zoom avanti e indietro ed espandere le dimensioni dell'area dello strumento di esplorazione del grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-194">You can move the vertices around on the graph explorer, zoom in and out, and expand the size of the graph explorer surface.</span></span> 

   ![Nuovi vertici nel grafo in Esplora dati nel portale di Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="a1cad-196">È ora possibile aggiungere alcuni nuovi utenti al grafo tramite Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="a1cad-196">Let's add a few new users to the graph using the Data Explorer.</span></span> <span data-ttu-id="a1cad-197">Fare clic sul pulsante **New Vertex** (Nuovo vertice) per aggiungere dati al grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-197">Click the **New Vertex** button to add data to your graph.</span></span>

   ![Creare nuovi documenti in Esplora dati nel portale di Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="a1cad-199">Immettere un'etichetta di tipo *person* e quindi inserire le chiavi e i valori seguenti per creare il primo vertice nel grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-199">Enter a label of *person* then enter the following keys and values to create the first vertex in the graph.</span></span> <span data-ttu-id="a1cad-200">Si noti che è possibile creare proprietà univoche per ogni persona del grafo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="a1cad-201">È necessaria solo la chiave id.</span><span class="sxs-lookup"><span data-stu-id="a1cad-201">Only the id key is required.</span></span>

    <span data-ttu-id="a1cad-202">key</span><span class="sxs-lookup"><span data-stu-id="a1cad-202">key</span></span>|<span data-ttu-id="a1cad-203">value</span><span class="sxs-lookup"><span data-stu-id="a1cad-203">value</span></span>|<span data-ttu-id="a1cad-204">Note</span><span class="sxs-lookup"><span data-stu-id="a1cad-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="a1cad-205">id</span><span class="sxs-lookup"><span data-stu-id="a1cad-205">id</span></span>|<span data-ttu-id="a1cad-206">ashley</span><span class="sxs-lookup"><span data-stu-id="a1cad-206">ashley</span></span>|<span data-ttu-id="a1cad-207">Identificatore univoco per il vertice.</span><span class="sxs-lookup"><span data-stu-id="a1cad-207">The unique identifier for the vertex.</span></span> <span data-ttu-id="a1cad-208">Se non si specifica alcun ID, ne verrà generato automaticamente uno.</span><span class="sxs-lookup"><span data-stu-id="a1cad-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="a1cad-209">gender</span><span class="sxs-lookup"><span data-stu-id="a1cad-209">gender</span></span>|<span data-ttu-id="a1cad-210">female</span><span class="sxs-lookup"><span data-stu-id="a1cad-210">female</span></span>| 
    <span data-ttu-id="a1cad-211">tech</span><span class="sxs-lookup"><span data-stu-id="a1cad-211">tech</span></span> | <span data-ttu-id="a1cad-212">java</span><span class="sxs-lookup"><span data-stu-id="a1cad-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="a1cad-213">In questa esercitazione introduttiva viene creata una raccolta non partizionata.</span><span class="sxs-lookup"><span data-stu-id="a1cad-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="a1cad-214">Se tuttavia si crea una raccolta partizionata specificando una chiave di partizione durante la creazione della raccolta, sarà necessario includere la chiave di partizione come chiave in ogni nuovo vertice.</span><span class="sxs-lookup"><span data-stu-id="a1cad-214">However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="a1cad-215">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-215">Click **OK**.</span></span> <span data-ttu-id="a1cad-216">Potrebbe essere necessario espandere la schermata per vedere il pulsante **OK** nella parte inferiore dello schermo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-216">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

6. <span data-ttu-id="a1cad-217">Fare di nuovo clic su **New Vertex** (Nuovo vertice) e aggiungere un altro nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="a1cad-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="a1cad-218">Immettere un'etichetta di tipo *person* e quindi specificare le chiavi e i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="a1cad-218">Enter a label of *person* then enter the following keys and values:</span></span>

    <span data-ttu-id="a1cad-219">key</span><span class="sxs-lookup"><span data-stu-id="a1cad-219">key</span></span>|<span data-ttu-id="a1cad-220">value</span><span class="sxs-lookup"><span data-stu-id="a1cad-220">value</span></span>|<span data-ttu-id="a1cad-221">Note</span><span class="sxs-lookup"><span data-stu-id="a1cad-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="a1cad-222">id</span><span class="sxs-lookup"><span data-stu-id="a1cad-222">id</span></span>|<span data-ttu-id="a1cad-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="a1cad-223">rakesh</span></span>|<span data-ttu-id="a1cad-224">Identificatore univoco per il vertice.</span><span class="sxs-lookup"><span data-stu-id="a1cad-224">The unique identifier for the vertex.</span></span> <span data-ttu-id="a1cad-225">Se non si specifica alcun ID, ne verrà generato automaticamente uno.</span><span class="sxs-lookup"><span data-stu-id="a1cad-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="a1cad-226">gender</span><span class="sxs-lookup"><span data-stu-id="a1cad-226">gender</span></span>|<span data-ttu-id="a1cad-227">male</span><span class="sxs-lookup"><span data-stu-id="a1cad-227">male</span></span>| 
    <span data-ttu-id="a1cad-228">school</span><span class="sxs-lookup"><span data-stu-id="a1cad-228">school</span></span>|<span data-ttu-id="a1cad-229">MIT</span><span class="sxs-lookup"><span data-stu-id="a1cad-229">MIT</span></span>| 

7. <span data-ttu-id="a1cad-230">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-230">Click **OK**.</span></span> 

8. <span data-ttu-id="a1cad-231">Fare clic su **Applica filtro** usando il filtro `g.V()` predefinito.</span><span class="sxs-lookup"><span data-stu-id="a1cad-231">Click **Apply Filter** with the default `g.V()` filter.</span></span> <span data-ttu-id="a1cad-232">Tutti gli utenti sono ora visualizzati nell'elenco **Risultati**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-232">All of the users now show in the **Results** list.</span></span> <span data-ttu-id="a1cad-233">Quando si aggiungono altri dati, è possibile usare i filtri per limitare i risultati visualizzati.</span><span class="sxs-lookup"><span data-stu-id="a1cad-233">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="a1cad-234">Per impostazione predefinita, Esplora dati usa `g.V()` per recuperare tutti i vertici in un grafo, ma è possibile cambiare questa impostazione per specificare una [query per grafi](tutorial-query-graph.md), ad esempio `g.V().count()`, per restituire il conteggio di tutti i vertici nel grafo in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a1cad-234">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph, but you can change that to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span>

9. <span data-ttu-id="a1cad-235">È ora possibile connettere rakesh e ashley.</span><span class="sxs-lookup"><span data-stu-id="a1cad-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="a1cad-236">Assicurarsi che il valore **ashley** sia selezionato nell'elenco **Risultati**, quindi fare clic sul pulsante di modifica accanto a **Destinazioni** in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="a1cad-236">Ensure **ashley** in selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span></span> <span data-ttu-id="a1cad-237">Potrebbe essere necessario allargare la finestra per visualizzare l'area **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-237">You may need to widen your window to see the **Properties** area.</span></span>

   ![Cambiare la destinazione di un vertice in un grafo](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="a1cad-239">Nella casella **Destinazione** digitare *rakesh* e nella casella **Edge label** (Etichetta bordo) digitare *knows*, quindi fare selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="a1cad-239">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check box.</span></span>

   ![Aggiungere una connessione tra ashley e rakesh in Esplora dati](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="a1cad-241">Selezionare ora **rakesh** dall'elenco Risultati. Come si può notare ashley e rakesh sono connessi.</span><span class="sxs-lookup"><span data-stu-id="a1cad-241">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![Due vertici connessi in Esplora dati](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="a1cad-243">È anche possibile usare Esplora dati per creare stored procedure, funzioni definite dall'utente e trigger per eseguire la logica di business sul lato server e aumentare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="a1cad-243">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="a1cad-244">Esplora dati espone tutti i tipi di accesso ai dati a livello di codice predefiniti disponibili nelle API, ma consente anche di accedere facilmente ai dati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1cad-244">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>



## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a1cad-245">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a1cad-245">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a1cad-246">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="a1cad-246">Clean up resources</span></span>

<span data-ttu-id="a1cad-247">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a1cad-247">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="a1cad-248">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="a1cad-248">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="a1cad-249">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="a1cad-249">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1cad-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1cad-250">Next steps</span></span>

<span data-ttu-id="a1cad-251">In questa guida di avvio rapido si è appreso come creare un account Azure Cosmos DB, come creare un grafo con Esplora dati e come eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="a1cad-251">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="a1cad-252">È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="a1cad-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1cad-253">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="a1cad-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

