---
title: 'Azure Cosmos DB: Esercitazione introduttiva per l''API DocumentDB | Microsoft Docs'
description: Esercitazione che crea un database online e un'applicazione console in C# con l'API DocumentDB.
keywords: esercitazione su nosql, database online, applicazione console C#
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="c8a85-104">Azure Cosmos DB: Esercitazione introduttiva per l'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c8a85-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8a85-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c8a85-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="c8a85-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c8a85-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="c8a85-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="c8a85-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="c8a85-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="c8a85-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="c8a85-109">Java</span><span class="sxs-lookup"><span data-stu-id="c8a85-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="c8a85-110">C++</span><span class="sxs-lookup"><span data-stu-id="c8a85-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="c8a85-111">Esercitazione introduttiva per l'API DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8a85-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="c8a85-112">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8a85-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="c8a85-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="c8a85-113">We'll cover:</span></span>

* <span data-ttu-id="c8a85-114">Creazione e connessione a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8a85-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="c8a85-115">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c8a85-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="c8a85-116">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="c8a85-116">Creating an online database</span></span>
* <span data-ttu-id="c8a85-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="c8a85-117">Creating a collection</span></span>
* <span data-ttu-id="c8a85-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="c8a85-118">Creating JSON documents</span></span>
* <span data-ttu-id="c8a85-119">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="c8a85-119">Querying the collection</span></span>
* <span data-ttu-id="c8a85-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="c8a85-120">Replacing a document</span></span>
* <span data-ttu-id="c8a85-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="c8a85-121">Deleting a document</span></span>
* <span data-ttu-id="c8a85-122">Eliminazione del database</span><span class="sxs-lookup"><span data-stu-id="c8a85-122">Deleting the database</span></span>

<span data-ttu-id="c8a85-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="c8a85-123">Don't have time?</span></span> <span data-ttu-id="c8a85-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="c8a85-124">Don't worry!</span></span> <span data-ttu-id="c8a85-125">La soluzione completa è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c8a85-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="c8a85-126">Per istruzioni rapide, vedere la sezione [Ottenere la soluzione completa per l'esercitazione su NoSQL](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="c8a85-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="c8a85-127">Successivamente, utilizzare i pulsanti di voti all'inizio o alla fine di questa pagina per fornire feedback.</span><span class="sxs-lookup"><span data-stu-id="c8a85-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="c8a85-128">Se si desidera contattarci, è possibile includere l'indirizzo di posta elettronica nel commento per il follow-up.</span><span class="sxs-lookup"><span data-stu-id="c8a85-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="c8a85-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="c8a85-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8a85-130">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c8a85-130">Prerequisites</span></span>
<span data-ttu-id="c8a85-131">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c8a85-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="c8a85-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="c8a85-132">An active Azure account.</span></span> <span data-ttu-id="c8a85-133">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c8a85-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="c8a85-134">In alternativa, per questa esercitazione è possibile usare l'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c8a85-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="c8a85-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c8a85-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="c8a85-136">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8a85-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="c8a85-137">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8a85-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="c8a85-138">Se si ha già un account, è possibile ignorare questo passaggio e passare a [Configurare la soluzione Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="c8a85-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="c8a85-139">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="c8a85-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="c8a85-140"><a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c8a85-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="c8a85-141">Aprire **Visual Studio 2017** nel computer.</span><span class="sxs-lookup"><span data-stu-id="c8a85-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="c8a85-142">Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="c8a85-143">Nella finestra di dialogo **Nuovo progetto** selezionare **Modelli** / **Visual C#** / **Applicazione console**, assegnare un nome al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="c8a85-144">![Screenshot della finestra Nuovo progetto](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="c8a85-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="c8a85-145">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla nuova applicazione console, disponibile nella soluzione di Visual Studio, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Screenshot del menu selezionato con il pulsante destro del mouse per il progetto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="c8a85-147">Nella scheda **NuGet** fare clic su **Sfoglia** e digitare **azure documentdb** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c8a85-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="c8a85-148">Nei risultati trovare **Microsoft.Azure.DocumentDB** e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="c8a85-149">L'ID pacchetto per la libreria client dell'API DocumentDB di Azure Cosmos DB è [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="c8a85-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="c8a85-150">![Screenshot del menu di NuGet per l'individuazione dell'SDK client di Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="c8a85-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="c8a85-151">Se viene visualizzato un messaggio sulla verifica delle modifiche alla soluzione, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="c8a85-152">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="c8a85-153">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c8a85-153">Great!</span></span> <span data-ttu-id="c8a85-154">Ora che abbiamo completato l'installazione, iniziamo a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="c8a85-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="c8a85-155">Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c8a85-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="c8a85-156"><a id="Connect"></a>Passaggio 3: Connettersi a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8a85-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="c8a85-157">In primo luogo, aggiungere questi riferimenti all'inizio dell'applicazione c#, nel file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="c8a85-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="c8a85-158">Per completare l'esercitazione, assicurarsi di aggiungere le dipendenze illustrate sopra.</span><span class="sxs-lookup"><span data-stu-id="c8a85-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="c8a85-159">Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.</span><span class="sxs-lookup"><span data-stu-id="c8a85-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="c8a85-160">Tornare al [portale di Azure](https://portal.azure.com) per recuperare l'URL e la chiave primaria dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="c8a85-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="c8a85-161">L'URL e la chiave primaria dell'endpoint sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="c8a85-162">Nel portale di Azure passare all'account Azure Cosmos DB e quindi fare clic su **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="c8a85-163">Copiare l'URI dal portale e incollarlo in `<your endpoint URL>` nel file program.cs.</span><span class="sxs-lookup"><span data-stu-id="c8a85-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="c8a85-164">Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla in `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="c8a85-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console C#.][keys]

<span data-ttu-id="c8a85-167">Verrà quindi avviata l'applicazione tramite la creazione di una nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="c8a85-168">Sotto il metodo **Main** aggiungere la nuova attività asincrona denominata **GetStartedDemo** che creerà la nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="c8a85-169">Aggiungere questo codice per eseguire l'attività asincrona dal metodo **Main** .</span><span class="sxs-lookup"><span data-stu-id="c8a85-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="c8a85-170">Il metodo **Main** rileva le eccezioni e le scrive nella console.</span><span class="sxs-lookup"><span data-stu-id="c8a85-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="c8a85-171">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-171">Press **F5** to run your application.</span></span> <span data-ttu-id="c8a85-172">L'output della finestra della console mostra il messaggio `End of demo, press any key to exit.`, che conferma che è stata stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="c8a85-173">È quindi possibile chiudere la finestra della console.</span><span class="sxs-lookup"><span data-stu-id="c8a85-173">You can then close the console window.</span></span> 

<span data-ttu-id="c8a85-174">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-174">Congratulations!</span></span> <span data-ttu-id="c8a85-175">La connessione a un account Azure Cosmos DB è stata stabilita. Ora è possibile esaminare l'uso delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8a85-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="c8a85-176">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="c8a85-176">Step 4: Create a database</span></span>
<span data-ttu-id="c8a85-177">Prima di aggiungere il codice per la creazione di un database, aggiungere un metodo helper per la scrittura nella console.</span><span class="sxs-lookup"><span data-stu-id="c8a85-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="c8a85-178">Copiare e incollare il metodo **WriteToConsoleAndPromptToContinue** dopo il metodo **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="c8a85-179">È possibile creare un [database](documentdb-resources.md#databases) di Azure Cosmos DB usando il metodo [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c8a85-180">Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="c8a85-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="c8a85-181">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di creazione del client.</span><span class="sxs-lookup"><span data-stu-id="c8a85-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="c8a85-182">Verrà creato un database denominato *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="c8a85-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="c8a85-183">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-184">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-184">Congratulations!</span></span> <span data-ttu-id="c8a85-185">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="c8a85-186"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="c8a85-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="c8a85-187">**CreateDocumentCollectionIfNotExistsAsync** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="c8a85-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="c8a85-188">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c8a85-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="c8a85-189">È possibile creare una [raccolta](documentdb-resources.md#collections) usando il metodo [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c8a85-190">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="c8a85-191">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di creazione del database.</span><span class="sxs-lookup"><span data-stu-id="c8a85-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="c8a85-192">Verrà creata una raccolta di documenti denominata *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="c8a85-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="c8a85-193">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-194">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-194">Congratulations!</span></span> <span data-ttu-id="c8a85-195">La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="c8a85-196"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="c8a85-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="c8a85-197">È possibile creare un [documento](documentdb-resources.md#documents) usando il metodo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c8a85-198">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="c8a85-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="c8a85-199">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="c8a85-199">We can now insert one or more documents.</span></span> <span data-ttu-id="c8a85-200">Se sono già disponibili dati da archiviare nel database, è possibile usare lo [strumento di migrazione dei dati](import-data.md) di Azure Cosmos DB per importare i dati in un database.</span><span class="sxs-lookup"><span data-stu-id="c8a85-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="c8a85-201">È necessario creare prima di tutto una classe **Family** che rappresenterà gli oggetti archiviati in Azure Cosmos DB in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c8a85-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="c8a85-202">Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="c8a85-203">Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="c8a85-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="c8a85-204">Creare queste classi aggiungendo le classi secondarie interne seguenti dopo il metodo **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="c8a85-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="c8a85-205">Copiare e incollare le classi **Family**, **Parent**, **Child**, **Pet** e **Address** dopo il metodo **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

<span data-ttu-id="c8a85-206">Copiare e incollare il metodo **CreateFamilyDocumentIfNotExists** sotto il metodo **Address**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

<span data-ttu-id="c8a85-207">Inserire anche due documenti, relativi rispettivamente alla famiglia Andersen e alla famiglia Wakefield.</span><span class="sxs-lookup"><span data-stu-id="c8a85-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="c8a85-208">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di creazione della raccolta di documenti.</span><span class="sxs-lookup"><span data-stu-id="c8a85-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="c8a85-209">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-210">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-210">Congratulations!</span></span> <span data-ttu-id="c8a85-211">La creazione di due documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramma che illustra la relazione gerarchica tra l'account, il database online, la raccolta e i documenti usati nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="c8a85-213"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8a85-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="c8a85-214">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="c8a85-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="c8a85-215">Il codice di esempio seguente mostra diverse query che usano la sintassi SQL di Azure Cosmos DB e LINQ e che possono essere eseguite sui documenti inseriti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c8a85-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="c8a85-216">Copiare e incollare il metodo **ExecuteSimpleQuery** dopo il metodo **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="c8a85-217">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di creazione del secondo documento.</span><span class="sxs-lookup"><span data-stu-id="c8a85-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="c8a85-218">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-219">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-219">Congratulations!</span></span> <span data-ttu-id="c8a85-220">L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="c8a85-221">Il diagramma seguente illustra il modo in cui la sintassi di query di SQL di Azure Cosmos DB viene chiamata sulla raccolta creata e la stessa logica viene applicata alla query di LINQ.</span><span class="sxs-lookup"><span data-stu-id="c8a85-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagramma che illustra l'ambito e il significato della query usata nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="c8a85-223">La parola chiave [FROM](documentdb-sql-query.md#FromClause) è facoltativa nella query perché le query di Azure Cosmos DB sono già limitate a una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="c8a85-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="c8a85-224">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="c8a85-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="c8a85-225">Azure Cosmos DB dedurrà che Families, root o il nome della variabile scelta, si riferisce per impostazione predefinita alla raccolta attuale.</span><span class="sxs-lookup"><span data-stu-id="c8a85-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="c8a85-226"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="c8a85-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="c8a85-227">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="c8a85-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="c8a85-228">Copiare e incollare il metodo **ReplaceFamilyDocument** dopo il metodo **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="c8a85-229">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di esecuzione della query, alla fine del metodo.</span><span class="sxs-lookup"><span data-stu-id="c8a85-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="c8a85-230">Dopo aver sostituito il documento, verrà eseguita di nuovo la stessa query per visualizzare il documento modificato.</span><span class="sxs-lookup"><span data-stu-id="c8a85-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="c8a85-231">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-232">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-232">Congratulations!</span></span> <span data-ttu-id="c8a85-233">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c8a85-234"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="c8a85-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="c8a85-235">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="c8a85-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="c8a85-236">Copiare e incollare il metodo **DeleteFamilyDocument** dopo il metodo **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="c8a85-237">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di esecuzione della seconda query, alla fine del metodo.</span><span class="sxs-lookup"><span data-stu-id="c8a85-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="c8a85-238">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-239">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-239">Congratulations!</span></span> <span data-ttu-id="c8a85-240">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c8a85-241"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare il database</span><span class="sxs-lookup"><span data-stu-id="c8a85-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="c8a85-242">Se si elimina il database creato, verrà rimosso il database e tutte le risorse figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="c8a85-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="c8a85-243">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** dopo il codice di eliminazione del documento per eliminare l'intero database e tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="c8a85-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="c8a85-244">Premere **F5** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="c8a85-245">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-245">Congratulations!</span></span> <span data-ttu-id="c8a85-246">L'eliminazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="c8a85-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="c8a85-247"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#</span><span class="sxs-lookup"><span data-stu-id="c8a85-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="c8a85-248">Premere F5 in Visual Studio per compilare l'applicazione in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="c8a85-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="c8a85-249">Verrà visualizzato l'output dell'app introduttiva nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="c8a85-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="c8a85-250">L'output visualizzerà i risultati delle query aggiunte e dovrà corrispondere al testo di esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c8a85-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="c8a85-251">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="c8a85-251">Congratulations!</span></span> <span data-ttu-id="c8a85-252">L'esercitazione è stata completata ed è stata creata un'applicazione console C# funzionante.</span><span class="sxs-lookup"><span data-stu-id="c8a85-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="c8a85-253"><a id="GetSolution"></a> Ottenere la soluzione completa per l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c8a85-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="c8a85-254">Se non si ha tempo per completare le procedure dell'esercitazione o se si vogliono solo scaricare gli esempi di codice, è possibile ottenerli da [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c8a85-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="c8a85-255">Per compilare la soluzione GetStarted, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8a85-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="c8a85-256">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="c8a85-256">An active Azure account.</span></span> <span data-ttu-id="c8a85-257">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c8a85-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="c8a85-258">Un [account Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="c8a85-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="c8a85-259">La soluzione [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="c8a85-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="c8a85-260">Per ripristinare i riferimenti a Azure Cosmos DB .NET SDK in Visual Studio, fare clic con il pulsante destro del mouse sulla soluzione **GetStarted** in Esplora soluzioni e quindi scegliere **Abilita ripristino dei pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c8a85-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="c8a85-261">Nel file App.config aggiornare quindi i valori EndpointUrl e AuthorizationKey come illustrato nell'articolo [Connettersi a un account Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="c8a85-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="c8a85-262">Per completare la procedura, è sufficiente procedere alla compilazione.</span><span class="sxs-lookup"><span data-stu-id="c8a85-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="c8a85-263">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8a85-263">Next steps</span></span>
* <span data-ttu-id="c8a85-264">Per un'esercitazione su MVC ASP.NET più complessa,</span><span class="sxs-lookup"><span data-stu-id="c8a85-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="c8a85-265">vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="c8a85-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="c8a85-266">Per la scalabilità e i test delle prestazioni con Azure Cosmos DB,</span><span class="sxs-lookup"><span data-stu-id="c8a85-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="c8a85-267">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="c8a85-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="c8a85-268">Informazioni su come [monitorare le richieste, l'utilizzo e le risorse di archiviazione di Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="c8a85-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="c8a85-269">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="c8a85-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="c8a85-270">Per altre informazioni su Azure Cosmos DB, vedere [Introduzione ad Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="c8a85-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
