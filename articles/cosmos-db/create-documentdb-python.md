---
title: 'Azure Cosmos DB: Compilare un''app con Python e hello API DocumentDB | Documenti Microsoft'
description: "Visualizza un esempio di codice Python è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="c80bf-103">DB Cosmos Azure: Creare un'applicazione API DocumentDB con Python e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c80bf-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="c80bf-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c80bf-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c80bf-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="c80bf-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c80bf-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c80bf-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="c80bf-107">Quindi compilazione e l'esecuzione di un'applicazione console basata su hello [API Python di DocumentDB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="c80bf-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c80bf-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c80bf-108">Prerequisites</span></span>

* <span data-ttu-id="c80bf-109">Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="c80bf-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="c80bf-110">[Visual Studio 2015](http://www.visualstudio.com/) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c80bf-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="c80bf-111">Python Tools per Visual Studio, disponibile su [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="c80bf-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="c80bf-112">Questa esercitazione usa Python Tools per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c80bf-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="c80bf-113">Python 2.7, disponibile in [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="c80bf-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c80bf-114">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="c80bf-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c80bf-115">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="c80bf-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="c80bf-116">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="c80bf-116">Clone hello sample application</span></span>

<span data-ttu-id="c80bf-117">Ora si app clone un'API DocumentDB da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="c80bf-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="c80bf-118">Viene visualizzato quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="c80bf-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="c80bf-119">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c80bf-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="c80bf-120">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="c80bf-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="c80bf-121">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="c80bf-121">Review hello code</span></span>

<span data-ttu-id="c80bf-122">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c80bf-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="c80bf-123">File DocumentDBGetStarted.py aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c80bf-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="c80bf-124">Hello DocumentClient viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="c80bf-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="c80bf-125">Viene creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="c80bf-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="c80bf-126">Viene creata una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="c80bf-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="c80bf-127">Vengono creati alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="c80bf-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="c80bf-128">Viene eseguita una query con SQL</span><span class="sxs-lookup"><span data-stu-id="c80bf-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="c80bf-129">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="c80bf-129">Update your connection string</span></span>

<span data-ttu-id="c80bf-130">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="c80bf-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="c80bf-131">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="c80bf-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c80bf-132">È possibile usare i pulsanti copia hello per il lato destro hello di hello toocopy di hello schermata URI e chiave primaria in hello `DocumentDBGetStarted.py` file nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="c80bf-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="c80bf-134">In aprire hello `DocumentDBGetStarted.py` file.</span><span class="sxs-lookup"><span data-stu-id="c80bf-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="c80bf-135">Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave endpoint hello `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c80bf-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="c80bf-136">Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c80bf-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="c80bf-137">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c80bf-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="c80bf-138">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="c80bf-138">Run hello app</span></span>
1. <span data-ttu-id="c80bf-139">In Visual Studio, fare clic su progetto hello in **Esplora**, selezionare l'ambiente di Python corrente hello, quindi fare clic destro.</span><span class="sxs-lookup"><span data-stu-id="c80bf-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="c80bf-140">Scegliere Installa pacchetto Python, quindi digitare **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="c80bf-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="c80bf-141">Eseguire un'applicazione hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="c80bf-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="c80bf-142">L'app viene visualizzata nel browser.</span><span class="sxs-lookup"><span data-stu-id="c80bf-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="c80bf-143">È ora possibile tornare indietro tooData Esplora e vedere query, modificare e funzionare con questi nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="c80bf-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="c80bf-144">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="c80bf-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c80bf-145">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="c80bf-145">Clean up resources</span></span>

<span data-ttu-id="c80bf-146">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c80bf-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="c80bf-147">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c80bf-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="c80bf-148">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="c80bf-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c80bf-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c80bf-149">Next steps</span></span>

<span data-ttu-id="c80bf-150">In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="c80bf-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="c80bf-151">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c80bf-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c80bf-152">Importare dati in Azure Cosmos DB per hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c80bf-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


