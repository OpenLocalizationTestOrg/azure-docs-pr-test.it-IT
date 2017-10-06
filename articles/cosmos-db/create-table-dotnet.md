---
title: un'applicazione Azure Cosmos DB .NET utilizzando aaaBuild hello tabella API | Documenti Microsoft
description: Come iniziare a usare l'API di tabella di Azure Cosmos DB tramite .NET
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="59fb6-103">Azure Cosmos DB: Compilare un'applicazione .NET usando hello tabella API</span><span class="sxs-lookup"><span data-stu-id="59fb6-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="59fb6-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="59fb6-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="59fb6-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="59fb6-106">Questa Guida introduttiva illustra come un database di Azure Cosmos toocreate account e creare una tabella all'interno di tale account hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59fb6-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="59fb6-107">Verranno quindi scrivere codice tooinsert, aggiornamento ed eliminare entità ed eseguire alcune query utilizzando hello nuovo [Premium di archiviazione di Windows Azure Table](https://aka.ms/premiumtablenuget) pacchetto NuGet (anteprima).</span><span class="sxs-lookup"><span data-stu-id="59fb6-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="59fb6-108">Questa libreria ha hello stesse classi e le firme del metodo come pubblico hello [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ma ha anche hello possibilità tooconnect tooAzure DB Cosmos gli account tramite hello [tabella API](table-introduction.md) (anteprima).</span><span class="sxs-lookup"><span data-stu-id="59fb6-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="59fb6-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="59fb6-109">Prerequisites</span></span>

<span data-ttu-id="59fb6-110">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="59fb6-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="59fb6-111">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="59fb6-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="59fb6-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="59fb6-113">Aggiungere una tabella</span><span class="sxs-lookup"><span data-stu-id="59fb6-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="59fb6-114">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="59fb6-114">Add sample data</span></span>

<span data-ttu-id="59fb6-115">È ora possibile aggiungere dati tooyour nuova tabella utilizzando Esplora dati (anteprima).</span><span class="sxs-lookup"><span data-stu-id="59fb6-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="59fb6-116">In Esplora dati espandere **sample-table**, fare clic su **Entità** e quindi su **Aggiungi entità**.</span><span class="sxs-lookup"><span data-stu-id="59fb6-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Creare nuove entità in Esplora dati nel portale di Azure hello](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="59fb6-118">Ora aggiungere una casella di valore dati toohello PartitionKey e RowKey casella del valore e fare clic su **Aggiungi entità**.</span><span class="sxs-lookup"><span data-stu-id="59fb6-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Impostare hello chiave di partizione e chiave di riga per una nuova entità](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="59fb6-120">È ora possibile aggiungere altre entità tooyour tabella, modificare le entità o eseguire query sui dati in Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="59fb6-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="59fb6-121">Esplora dati è inoltre in cui è possibile ridimensionare la velocità effettiva e aggiungere una tabella tooyour trigger, stored procedure e funzioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="59fb6-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="59fb6-122">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="59fb6-122">Clone hello sample application</span></span>

<span data-ttu-id="59fb6-123">Ora si clonare un'app di tabella da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="59fb6-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="59fb6-124">Si noterà quanto sia facile toowork con i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="59fb6-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="59fb6-125">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="59fb6-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="59fb6-126">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="59fb6-127">Aprire quindi il file di soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59fb6-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="59fb6-128">Esaminare il codice hello</span><span class="sxs-lookup"><span data-stu-id="59fb6-128">Review hello code</span></span>

<span data-ttu-id="59fb6-129">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="59fb6-130">File Program.cs aprire hello e trovare le righe di codice creano hello risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59fb6-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="59fb6-131">Hello CloudTableClient viene inizializzato.</span><span class="sxs-lookup"><span data-stu-id="59fb6-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="59fb6-132">Se non esiste, viene creata una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="59fb6-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="59fb6-133">Viene creato un nuovo contenitore di tabelle.</span><span class="sxs-lookup"><span data-stu-id="59fb6-133">A new Table container is created.</span></span> <span data-ttu-id="59fb6-134">È possibile osservare questo tooregular molto simile a codice archiviazione tabelle di Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="59fb6-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="59fb6-135">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="59fb6-135">Update your connection string</span></span>

<span data-ttu-id="59fb6-136">Ora informazioni sulla stringa di connessione hello verrà aggiornata in modo l'app in grado di comunicare tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="59fb6-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="59fb6-137">In Visual Studio, aprire il file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="59fb6-138">In hello [portale di Azure](http://portal.azure.com/)in hello Azure Cosmos DB menu di navigazione a sinistra, fare clic su **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="59fb6-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="59fb6-139">Quindi nel riquadro nuova hello fare clic su pulsante Copia hello hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="59fb6-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Visualizzare e copiare Endpoint hello e chiave dell'Account nel riquadro di stringa di connessione hello](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="59fb6-141">Incollare il valore di hello nel file app. config hello come valore di hello di hello PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="59fb6-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="59fb6-142">È possibile lasciare hello StandardStorageConnectionString come è.</span><span class="sxs-lookup"><span data-stu-id="59fb6-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="59fb6-143">È stato aggiornato a questo punto l'app con tutte le informazioni di hello deve toocommunicate con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="59fb6-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="59fb6-144">Eseguire app web hello</span><span class="sxs-lookup"><span data-stu-id="59fb6-144">Run hello web app</span></span>

1. <span data-ttu-id="59fb6-145">In Visual Studio, fare clic su hello **PremiumTableGetStarted** nel progetto **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="59fb6-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="59fb6-146">In hello NuGet **Sfoglia** digitare *Windowsazure PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="59fb6-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="59fb6-147">Controllare hello **Includi versione preliminare** casella.</span><span class="sxs-lookup"><span data-stu-id="59fb6-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="59fb6-148">Dai risultati di hello, installare hello **Windowsazure PremiumTable** libreria.</span><span class="sxs-lookup"><span data-stu-id="59fb6-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="59fb6-149">Consente di installare anteprima hello pacchetto Azure Cosmos DB tabella API, nonché tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="59fb6-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="59fb6-150">Si tratta di un pacchetto NuGet diverso rispetto a pacchetto di archiviazione di Azure hello utilizzato per l'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="59fb6-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="59fb6-151">Premere CTRL + F5 applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="59fb6-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="59fb6-152">finestra della console Hello Visualizza dati hello aggiunti, recuperare, eseguire una query, sostituito o eliminate dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="59fb6-153">Al termine dell'esecuzione dello script hello, premere qualsiasi finestra di console hello tooclose chiave.</span><span class="sxs-lookup"><span data-stu-id="59fb6-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Output della console di avvio rapido di hello](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="59fb6-155">Se si desidera che le nuove entità hello toosee in Esplora dati, un commento solo le righe 188 208 in program.cs in modo che non vengono eliminati, eseguire nuovamente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="59fb6-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="59fb6-156">È ora possibile passare nuovamente tooData Explorer, fare clic su **aggiornamento**, espandere hello **persone** tabella e fare clic su **entità**e quindi utilizzare questi nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="59fb6-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nuove entità in Esplora dati](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="59fb6-158">Esaminare i contratti di servizio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="59fb6-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="59fb6-159">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="59fb6-159">Clean up resources</span></span>

<span data-ttu-id="59fb6-160">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="59fb6-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="59fb6-161">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="59fb6-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="59fb6-162">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="59fb6-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59fb6-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59fb6-163">Next steps</span></span>

<span data-ttu-id="59fb6-164">In questa Guida rapida, si è appreso come creare una tabella utilizzando Esplora dati hello toocreate un account Azure Cosmos DB ed eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="59fb6-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="59fb6-165">Ora è possibile eseguire una query con i dati utilizzando hello API di tabella.</span><span class="sxs-lookup"><span data-stu-id="59fb6-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="59fb6-166">Query tramite tabella API hello</span><span class="sxs-lookup"><span data-stu-id="59fb6-166">Query using hello Table API</span></span>](tutorial-query-table.md)

