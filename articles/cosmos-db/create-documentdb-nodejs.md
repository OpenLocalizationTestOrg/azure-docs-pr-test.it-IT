---
title: 'Azure Cosmos DB: Compilare un''app con Node.js e hello API DocumentDB | Documenti Microsoft'
description: "Visualizza un esempio di codice Node.js è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="7f6e2-103">DB Cosmos Azure: Creare un'applicazione API DocumentDB con Node.js e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7f6e2-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="7f6e2-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7f6e2-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7f6e2-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7f6e2-107">Quindi compilazione e l'esecuzione di un'applicazione console basata su hello [API Node.js di DocumentDB](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="7f6e2-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f6e2-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7f6e2-108">Prerequisites</span></span>

* <span data-ttu-id="7f6e2-109">Prima di poter eseguire questo esempio, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="7f6e2-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="7f6e2-110">[Node.js](https://nodejs.org/en/) 0.10.29 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="7f6e2-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="7f6e2-111">Git</span><span class="sxs-lookup"><span data-stu-id="7f6e2-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7f6e2-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="7f6e2-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7f6e2-113">Aggiungere una raccolta</span><span class="sxs-lookup"><span data-stu-id="7f6e2-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7f6e2-114">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="7f6e2-114">Clone hello sample application</span></span>

<span data-ttu-id="7f6e2-115">Ora si app clone un'API DocumentDB da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7f6e2-116">Viene visualizzato quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7f6e2-117">Aprire una finestra terminale git, ad esempio git bash, e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="7f6e2-118">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="7f6e2-119">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="7f6e2-119">Review hello code</span></span>

<span data-ttu-id="7f6e2-120">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="7f6e2-121">Aprire hello `app.js` file si scopre che le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="7f6e2-122">Hello `documentClient` viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="7f6e2-123">Viene creato un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7f6e2-124">Viene creata una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7f6e2-125">Vengono creati alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="7f6e2-126">Viene eseguita una query SQL su JSON.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="7f6e2-127">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7f6e2-127">Update your connection string</span></span>

<span data-ttu-id="7f6e2-128">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7f6e2-129">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7f6e2-130">È possibile usare i pulsanti copia hello per il lato destro hello di hello toocopy di hello schermata URI e chiave primaria in hello `config.js` file nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Visualizzare e copiare una chiave di accesso nel portale di Azure hello, pannello di chiavi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="7f6e2-132">In aprire hello `config.js` file.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="7f6e2-133">Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave endpoint hello `config.js`.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="7f6e2-134">Quindi copiare il valore di chiave primaria dal portale di hello e renderlo hello valore hello `config.primaryKey` in `config.js`.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="7f6e2-135">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="7f6e2-136">Eseguire app hello</span><span class="sxs-lookup"><span data-stu-id="7f6e2-136">Run hello app</span></span>
1. <span data-ttu-id="7f6e2-137">Eseguire `npm install` in un terminal tooinstall necessari moduli npm</span><span class="sxs-lookup"><span data-stu-id="7f6e2-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="7f6e2-138">Eseguire `node app.js` in un terminal toostart l'applicazione del nodo.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="7f6e2-139">È ora possibile tornare indietro tooData Esplora e vedere query, modificare e funzionare con questi nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7f6e2-140">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7f6e2-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7f6e2-141">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="7f6e2-141">Clean up resources</span></span>

<span data-ttu-id="7f6e2-142">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7f6e2-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="7f6e2-143">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="7f6e2-144">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f6e2-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f6e2-145">Next steps</span></span>

<span data-ttu-id="7f6e2-146">In questa Guida rapida, si è appreso come creare una raccolta utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="7f6e2-147">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="7f6e2-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f6e2-148">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f6e2-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


