---
title: Creare un'applicazione .NET Azure Cosmos DB tramite l'API di tabella | Microsoft Docs
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
ms.openlocfilehash: 29e7eebda5177d6e852ef04ad82d9d38a8d30ed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-table-api"></a><span data-ttu-id="31046-103">Azure Cosmos DB: Creare un'applicazione .NET tramite l'API di tabella</span><span class="sxs-lookup"><span data-stu-id="31046-103">Azure Cosmos DB: Build a .NET application using the Table API</span></span>

<span data-ttu-id="31046-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31046-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="31046-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave/valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31046-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="31046-106">Questa guida di avvio rapido mostra come creare un account Azure Cosmos DB e come creare una tabella nell'account tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="31046-106">This quick start demonstrates how to create an Azure Cosmos DB account, and create a table within that account using the Azure portal.</span></span> <span data-ttu-id="31046-107">Si scriverà quindi il codice per inserire, aggiornare ed eliminare le entità, oltre che eseguire alcune query usando il nuovo pacchetto [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) disponibile su NuGet.</span><span class="sxs-lookup"><span data-stu-id="31046-107">You'll then write code to insert, update, and delete entities, and run some queries using the new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="31046-108">Questa libreria include le stesse classi e firme di metodi disponibili nella versione pubblica di [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ma permette anche di connettersi agli account Azure Cosmos DB tramite l'[API di tabella](table-introduction.md) (anteprima).</span><span class="sxs-lookup"><span data-stu-id="31046-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31046-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31046-109">Prerequisites</span></span>

<span data-ttu-id="31046-110">Se Visual Studio 2017 non è ancora installato, è possibile scaricare e usare la versione **gratuita** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="31046-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="31046-111">Durante l'installazione di Visual Studio abilitare **Sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="31046-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="31046-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="31046-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="31046-113">Aggiungere una tabella</span><span class="sxs-lookup"><span data-stu-id="31046-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="31046-114">Aggiungere dati di esempio</span><span class="sxs-lookup"><span data-stu-id="31046-114">Add sample data</span></span>

<span data-ttu-id="31046-115">È ora possibile aggiungere dati alla nuova tabella usando Esplora dati (anteprima).</span><span class="sxs-lookup"><span data-stu-id="31046-115">You can now add data to your new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="31046-116">In Esplora dati espandere **sample-table**, fare clic su **Entità** e quindi su **Aggiungi entità**.</span><span class="sxs-lookup"><span data-stu-id="31046-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Creare nuove entità in Esplora dati nel portale di Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="31046-118">Aggiungere ora i dati alle caselle dei valori di PartitionKey e RowKey e quindi fare clic su **Aggiunti entità**.</span><span class="sxs-lookup"><span data-stu-id="31046-118">Now add data to the PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Configurare la chiave di partizione e la chiave di riga per una nuova entità](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="31046-120">È ora possibile aggiungere altre entità alla tabella, modificare le entità o eseguire query sui dati in Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="31046-120">You can now add more entities to your table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="31046-121">Esplora dati è anche lo strumento in cui è possibile ridimensionare la velocità effettiva e aggiungere stored procedure, funzioni definite dall'utente e trigger alla tabella.</span><span class="sxs-lookup"><span data-stu-id="31046-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers to your table.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="31046-122">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="31046-122">Clone the sample application</span></span>

<span data-ttu-id="31046-123">A questo punto è possibile clonare un'app Table da GitHub, impostare la stringa di connessione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="31046-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="31046-124">Come si noterà, è facile usare i dati a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="31046-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="31046-125">Aprire una finestra del terminale Git, ad esempio Git Bash, ed eseguire il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="31046-125">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="31046-126">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="31046-126">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="31046-127">Aprire quindi il file della soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31046-127">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="31046-128">Esaminare il codice</span><span class="sxs-lookup"><span data-stu-id="31046-128">Review the code</span></span>

<span data-ttu-id="31046-129">Ecco una breve analisi di ciò che accade nell'app.</span><span class="sxs-lookup"><span data-stu-id="31046-129">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="31046-130">Aprire il file Program.cs. Come si noterà, queste righe di codice creano le risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31046-130">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="31046-131">Viene inizializzato CloudTableClient.</span><span class="sxs-lookup"><span data-stu-id="31046-131">The CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="31046-132">Se non esiste, viene creata una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="31046-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="31046-133">Viene creato un nuovo contenitore di tabelle.</span><span class="sxs-lookup"><span data-stu-id="31046-133">A new Table container is created.</span></span> <span data-ttu-id="31046-134">Si noterà che questo codice è molto simile al normale SDK di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="31046-134">You will notice this code very similar to regular Azure Table storage SDK.</span></span> 

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

## <a name="update-your-connection-string"></a><span data-ttu-id="31046-135">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="31046-135">Update your connection string</span></span>

<span data-ttu-id="31046-136">Verranno ora aggiornate le informazioni sulla stringa di connessione, in modo che l'app possa comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31046-136">Now we'll update the connection string information so your app can talk to Azure Cosmos DB.</span></span> 

1. <span data-ttu-id="31046-137">In Visual Studio aprire il file app.config.</span><span class="sxs-lookup"><span data-stu-id="31046-137">In Visual Studio, open the app.config file.</span></span> 

2. <span data-ttu-id="31046-138">Nel [portale di Azure](http://portal.azure.com/) nel menu di spostamento a sinistra di Azure Cosmos DB scegliere **Stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="31046-138">In the [Azure portal](http://portal.azure.com/), in the Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="31046-139">Nel nuovo riquadro fare quindi clic sul pulsante Copia per la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="31046-139">Then in the new pane click the copy button for the connection string.</span></span> 

    ![Visualizzare e copiare l'endpoint e la chiave dell'account nel riquadro Stringa di connessione](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="31046-141">Incollare il valore nel file app.config come il valore di PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="31046-141">Paste the value into the app.config file as the value of the PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="31046-142">È possibile lasciare inalterato StandardStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="31046-142">You can leave the StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="31046-143">L'app è stata aggiornata con tutte le informazioni necessarie per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31046-143">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-web-app"></a><span data-ttu-id="31046-144">Eseguire l'app Web</span><span class="sxs-lookup"><span data-stu-id="31046-144">Run the web app</span></span>

1. <span data-ttu-id="31046-145">In Visual Studio fare clic con il pulsante destro del mouse sul progetto **PremiumTableGetStarted** in **Esplora soluzioni** e quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="31046-145">In Visual Studio, right-click on the **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="31046-146">Nella casella **Sfoglia** di NuGet digitare *WindowsAzure.Storage-PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="31046-146">In the NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="31046-147">Selezionare la casella **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="31046-147">Check the **Include prerelease** box.</span></span> 

4. <span data-ttu-id="31046-148">Dai risultati installare la libreria **WindowsAzure.Storage-PremiumTable**.</span><span class="sxs-lookup"><span data-stu-id="31046-148">From the results, install the **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="31046-149">Viene installato il pacchetto dell'API di tabella di Azure Cosmos DB di anteprima, insieme a tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="31046-149">This installs the preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="31046-150">Si noti che si tratta di un pacchetto NuGet diverso rispetto al pacchetto di Archiviazione di Azure usato dall'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="31046-150">Note that this is a different NuGet package than the Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="31046-151">Premere CTRL + F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="31046-151">Click CTRL + F5 to run the application.</span></span>

    <span data-ttu-id="31046-152">La finestra della console mostra i dati aggiunti, recuperati, sottoposti a query, sostituiti ed eliminati dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="31046-152">The console window displays the data being added, retrieved, queried, replaced and deleted from the table.</span></span> <span data-ttu-id="31046-153">Al termine dello script, premere qualsiasi tasto per chiudere la finestra della console.</span><span class="sxs-lookup"><span data-stu-id="31046-153">When the script completes, press any key to close the console window.</span></span> 
    
    ![Output della console della guida rapida](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="31046-155">Per visualizzare le nuove entità in Esplora dati, è sufficiente impostare come commento le righe 188-208 nel file program.cs, in modo che non vengano eliminate, quindi eseguire di nuovo l'esempio.</span><span class="sxs-lookup"><span data-stu-id="31046-155">If you want to see the new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run the sample again.</span></span> 

    <span data-ttu-id="31046-156">È ora possibile tornare a Esplora dati, fare clic su **Aggiorna**, espandere la tabella **people**, fare clic su **Entità** e infine usare i nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="31046-156">You can now go back to Data Explorer, click **Refresh**, expand the **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nuove entità in Esplora dati](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="31046-158">Esaminare i contratti di servizio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31046-158">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="31046-159">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="31046-159">Clean up resources</span></span>

<span data-ttu-id="31046-160">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite questa guida di avvio rapido nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="31046-160">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="31046-161">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="31046-161">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="31046-162">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="31046-162">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31046-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31046-163">Next steps</span></span>

<span data-ttu-id="31046-164">In questa guida di avvio rapido si è appreso come creare un account Azure Cosmos DB, come creare una tabella con Esplora dati e come eseguire un'app.</span><span class="sxs-lookup"><span data-stu-id="31046-164">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="31046-165">È ora possibile eseguire query sui dati tramite l'API di tabella.</span><span class="sxs-lookup"><span data-stu-id="31046-165">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="31046-166">Eseguire query tramite l'API di tabella</span><span class="sxs-lookup"><span data-stu-id="31046-166">Query using the Table API</span></span>](tutorial-query-table.md)

