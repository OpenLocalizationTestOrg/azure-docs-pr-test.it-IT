---
title: 'Azure Cosmos DB: Creare un''app web con .NET e hello MongoDB API | Documenti Microsoft'
description: "Visualizza un esempio di codice .NET è possibile utilizzare query tooand tooconnect hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="5672a-103">DB Cosmos Azure: Creare un'app di web API MongoDB con .NET e hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5672a-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="5672a-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5672a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="5672a-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="5672a-106">Questa Guida introduttiva viene illustrato come un account Azure Cosmos DB toocreate, database di documenti e l'utilizzo di raccolta hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5672a-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="5672a-107">Verrà quindi compilare e distribuire un'app web di elenco attività basata su hello [driver .NET MongoDB](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="5672a-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5672a-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5672a-108">Prerequisites</span></span>

<span data-ttu-id="5672a-109">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5672a-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="5672a-110">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="5672a-111">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="5672a-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="5672a-112">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="5672a-112">Clone hello sample application</span></span>

<span data-ttu-id="5672a-113">Ora si app clone un'API di MongoDB da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="5672a-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="5672a-114">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="5672a-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="5672a-115">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5672a-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="5672a-116">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="5672a-117">Aprire quindi il file di soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5672a-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="5672a-118">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="5672a-118">Review hello code</span></span>

<span data-ttu-id="5672a-119">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="5672a-120">Aprire hello **Dal.cs** file hello **DAL** directory consentirà di individuare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5672a-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="5672a-121">Inizializzare hello Mongo Client.</span><span class="sxs-lookup"><span data-stu-id="5672a-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="5672a-122">Recuperare il database di hello e la raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="5672a-123">Recuperare tutti i documenti.</span><span class="sxs-lookup"><span data-stu-id="5672a-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="5672a-124">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="5672a-124">Update your connection string</span></span>

<span data-ttu-id="5672a-125">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="5672a-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="5672a-126">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **stringa di connessione**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="5672a-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="5672a-127">Si utilizzerà nel file di Dal.cs hello nel passaggio successivo hello hello copia pulsanti sul lato destro hello di hello toocopy di hello schermata Username, Password e Host.</span><span class="sxs-lookup"><span data-stu-id="5672a-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="5672a-128">Aprire hello **Dal.cs** file hello **DAL** directory.</span><span class="sxs-lookup"><span data-stu-id="5672a-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="5672a-129">Copia il **username** valore dal portale di hello (con il pulsante di copia hello) e renderlo hello valore hello **username** nel **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="5672a-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="5672a-130">Quindi copiare il **host** valore dal portale hello e renderlo hello valore hello **host** nel **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="5672a-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="5672a-131">Infine copiare il **password** valore dal portale hello e renderlo hello valore hello **password** nel **Dal.cs** file.</span><span class="sxs-lookup"><span data-stu-id="5672a-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="5672a-132">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5672a-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="5672a-133">Eseguire app web hello</span><span class="sxs-lookup"><span data-stu-id="5672a-133">Run hello web app</span></span>

1. <span data-ttu-id="5672a-134">In Visual Studio, fare clic su progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5672a-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="5672a-135">In hello NuGet **Sfoglia** digitare *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="5672a-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="5672a-136">Dai risultati di hello, installare hello **MongoDB.Driver** libreria.</span><span class="sxs-lookup"><span data-stu-id="5672a-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="5672a-137">Consente di installare il pacchetto di MongoDB.Driver hello, nonché tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="5672a-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="5672a-138">Premere CTRL + F5 applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="5672a-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="5672a-139">L'app viene visualizzata nel browser.</span><span class="sxs-lookup"><span data-stu-id="5672a-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="5672a-140">Fare clic su **crea** in hello browser e creare alcune nuove attività nell'applicazione elenco attività.</span><span class="sxs-lookup"><span data-stu-id="5672a-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="5672a-141">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5672a-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="5672a-142">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="5672a-142">Clean up resources</span></span>

<span data-ttu-id="5672a-143">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5672a-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="5672a-144">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="5672a-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="5672a-145">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="5672a-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5672a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5672a-146">Next steps</span></span>

<span data-ttu-id="5672a-147">In questa Guida rapida, si è appreso come un account Azure Cosmos DB toocreate ed eseguire un'app web utilizzando hello API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5672a-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="5672a-148">È ora possibile importare account Cosmos DB tooyour di dati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="5672a-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5672a-149">Importare dati in Azure Cosmos DB per hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="5672a-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

