---
title: 'Azure Cosmos DB: Esercitazione introduttiva per l''API DocumentDB | Microsoft Docs'
description: Un'esercitazione che consente di creare un database online e l'applicazione console c# utilizzando hello API DocumentDB.
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
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="db6bf-104">Azure Cosmos DB: Esercitazione introduttiva per l'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="db6bf-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db6bf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="db6bf-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="db6bf-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="db6bf-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="db6bf-107">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="db6bf-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="db6bf-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="db6bf-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="db6bf-109">Java</span><span class="sxs-lookup"><span data-stu-id="db6bf-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="db6bf-110">C++</span><span class="sxs-lookup"><span data-stu-id="db6bf-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="db6bf-111">Benvenuto toohello API DocumentDB di Azure Cosmos DB esercitazione introduttiva!</span><span class="sxs-lookup"><span data-stu-id="db6bf-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="db6bf-112">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="db6bf-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="db6bf-113">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="db6bf-113">We'll cover:</span></span>

* <span data-ttu-id="db6bf-114">Creazione e connessione account Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="db6bf-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="db6bf-115">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db6bf-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="db6bf-116">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="db6bf-116">Creating an online database</span></span>
* <span data-ttu-id="db6bf-117">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="db6bf-117">Creating a collection</span></span>
* <span data-ttu-id="db6bf-118">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="db6bf-118">Creating JSON documents</span></span>
* <span data-ttu-id="db6bf-119">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="db6bf-119">Querying hello collection</span></span>
* <span data-ttu-id="db6bf-120">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="db6bf-120">Replacing a document</span></span>
* <span data-ttu-id="db6bf-121">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="db6bf-121">Deleting a document</span></span>
* <span data-ttu-id="db6bf-122">L'eliminazione di database hello</span><span class="sxs-lookup"><span data-stu-id="db6bf-122">Deleting hello database</span></span>

<span data-ttu-id="db6bf-123">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="db6bf-123">Don't have time?</span></span> <span data-ttu-id="db6bf-124">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="db6bf-124">Don't worry!</span></span> <span data-ttu-id="db6bf-125">la soluzione completa di Hello è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="db6bf-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="db6bf-126">Passare toohello [ottenere hello completo NoSQL soluzione di esercitazione sezione](#GetSolution) per istruzioni rapide.</span><span class="sxs-lookup"><span data-stu-id="db6bf-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="db6bf-127">Successivamente, per utilizzare hello pulsanti di voto hello sopra o sotto di questo toogive pagina ci commenti e suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="db6bf-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="db6bf-128">Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.</span><span class="sxs-lookup"><span data-stu-id="db6bf-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="db6bf-129">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="db6bf-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db6bf-130">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="db6bf-130">Prerequisites</span></span>
<span data-ttu-id="db6bf-131">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="db6bf-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="db6bf-132">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-132">An active Azure account.</span></span> <span data-ttu-id="db6bf-133">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="db6bf-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="db6bf-134">In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="db6bf-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="db6bf-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="db6bf-136">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="db6bf-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="db6bf-137">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="db6bf-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="db6bf-138">Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="db6bf-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="db6bf-139">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="db6bf-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="db6bf-140"><a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db6bf-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="db6bf-141">Aprire **Visual Studio 2017** nel computer.</span><span class="sxs-lookup"><span data-stu-id="db6bf-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="db6bf-142">In hello **File** dal menu **New**, quindi scegliere **progetto**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="db6bf-143">In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console**, nome il progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="db6bf-144">![Cattura di schermata della finestra Nuovo progetto hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="db6bf-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="db6bf-145">In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="db6bf-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Cattura di schermata del diritto hello Menu selezionato per hello progetto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="db6bf-147">In hello **Nuget** scheda, fare clic su **Sfoglia**e il tipo **azure documentdb** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="db6bf-148">All'interno dei risultati di hello, trovare **Microsoft.Azure.DocumentDB** e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="db6bf-149">ID del pacchetto per la libreria Client dell'API Azure Cosmos DB DocumentDB hello Hello è [libreria Client di Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="db6bf-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="db6bf-150">![Cattura di schermata di hello Nuget Menu per la ricerca di Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="db6bf-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="db6bf-151">Se viene visualizzato un messaggio i esaminato soluzione toohello modifiche, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="db6bf-152">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="db6bf-153">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="db6bf-153">Great!</span></span> <span data-ttu-id="db6bf-154">Ora che è stata completata l'installazione di hello, iniziamo a scrivere del codice.</span><span class="sxs-lookup"><span data-stu-id="db6bf-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="db6bf-155">Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="db6bf-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="db6bf-156"><a id="Connect"></a>Passaggio 3: Connettere l'account di Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="db6bf-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="db6bf-157">In primo luogo, aggiungere questi riferimenti inizio toohello dell'applicazione c#, nel file Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="db6bf-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="db6bf-158">Nell'esercitazione di hello toocomplete ordine, accertarsi di aggiungere le dipendenze di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="db6bf-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="db6bf-159">Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.</span><span class="sxs-lookup"><span data-stu-id="db6bf-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="db6bf-160">Successivamente, head nuovamente toohello [portale Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="db6bf-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="db6bf-161">URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="db6bf-162">In hello portale di Azure, passare tooyour Azure Cosmos DB account e quindi fare clic su **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="db6bf-163">Copiare hello URI dal portale di hello e incollarlo in `<your endpoint URL>` nel file program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="db6bf-164">Quindi copia hello chiave primaria dal portale hello e incollarlo in `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="db6bf-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Cattura di schermata del portale di Azure utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c# hello.][keys]

<span data-ttu-id="db6bf-167">Successivamente, si prenderà innanzitutto un'applicazione hello creando una nuova istanza di hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="db6bf-168">Di sotto di hello **Main** metodo, aggiungere la nuova attività asincrona chiamata **GetStartedDemo**, che creerà il nuovo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="db6bf-169">Aggiungere l'esempio di codice seguente hello toorun l'attività asincrona dal **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="db6bf-170">Hello **Main** metodo intercettare le eccezioni e scriverli toohello console.</span><span class="sxs-lookup"><span data-stu-id="db6bf-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
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
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

<span data-ttu-id="db6bf-171">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="db6bf-172">output della finestra della console Hello Visualizza messaggio hello `End of demo, press any key tooexit.` per confermare che è stata effettuata la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="db6bf-173">È quindi possibile chiudere la finestra di console hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-173">You can then close hello console window.</span></span> 

<span data-ttu-id="db6bf-174">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-174">Congratulations!</span></span> <span data-ttu-id="db6bf-175">È una connessione account Azure Cosmos DB tooan, Ora esaminiamo un utilizzo delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="db6bf-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="db6bf-176">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="db6bf-176">Step 4: Create a database</span></span>
<span data-ttu-id="db6bf-177">Prima di aggiungere codice hello per la creazione di un database, aggiungere un metodo di supporto per la scrittura di toohello console.</span><span class="sxs-lookup"><span data-stu-id="db6bf-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="db6bf-178">Copiare e incollare hello **WriteToConsoleAndPromptToContinue** metodo dopo hello **GetStartedDemo** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="db6bf-179">Il database di Azure Cosmos [database](documentdb-resources.md#databases) possono essere create usando hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="db6bf-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="db6bf-180">Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="db6bf-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="db6bf-181">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione di client hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="db6bf-182">Verrà creato un database denominato *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="db6bf-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="db6bf-183">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-184">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-184">Congratulations!</span></span> <span data-ttu-id="db6bf-185">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="db6bf-186"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="db6bf-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="db6bf-187">**CreateDocumentCollectionIfNotExistsAsync** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="db6bf-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="db6bf-188">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="db6bf-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="db6bf-189">Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="db6bf-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="db6bf-190">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="db6bf-191">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione del database hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="db6bf-192">Verrà creata una raccolta di documenti denominata *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="db6bf-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="db6bf-193">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-194">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-194">Congratulations!</span></span> <span data-ttu-id="db6bf-195">La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="db6bf-196"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="db6bf-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="db6bf-197">Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="db6bf-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="db6bf-198">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="db6bf-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="db6bf-199">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="db6bf-199">We can now insert one or more documents.</span></span> <span data-ttu-id="db6bf-200">Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare hello Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md) dati hello tooimport in un database.</span><span class="sxs-lookup"><span data-stu-id="db6bf-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="db6bf-201">Innanzitutto, è necessario toocreate un **famiglia** classe che rappresenta gli oggetti archiviati all'interno di Azure Cosmos DB in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="db6bf-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="db6bf-202">Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="db6bf-203">Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="db6bf-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="db6bf-204">Creare queste classi aggiungendo le seguenti classi secondario interne dopo hello hello **GetStartedDemo** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="db6bf-205">Copiare e incollare hello **famiglia**, **padre**, **figlio**, **Pet**, e **indirizzo** classi dopo hello **WriteToConsoleAndPromptToContinue** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="db6bf-206">Copiare e incollare hello **CreateFamilyDocumentIfNotExists** metodo sotto il **indirizzo** classe.</span><span class="sxs-lookup"><span data-stu-id="db6bf-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="db6bf-207">Inserire due documenti, uno per hello Andersen famiglia e hello Wakefield famiglia.</span><span class="sxs-lookup"><span data-stu-id="db6bf-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="db6bf-208">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione della raccolta documenti di hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="db6bf-209">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-210">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-210">Congratulations!</span></span> <span data-ttu-id="db6bf-211">La creazione di due documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramma che illustra relazione gerarchica di hello tra account hello, database online hello, raccolta hello e documenti hello utilizzato dai hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="db6bf-213"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="db6bf-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="db6bf-214">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="db6bf-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="db6bf-215">Hello codice di esempio seguente vengono illustrate diverse query - utilizzando entrambi SQL di Azure Cosmos DB sintassi, nonché LINQ - che è possibile eseguire hello è inseriti nel passaggio precedente hello documenti.</span><span class="sxs-lookup"><span data-stu-id="db6bf-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="db6bf-216">Copiare e incollare hello **ExecuteSimpleQuery** metodo dopo il **CreateFamilyDocumentIfNotExists** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="db6bf-217">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo la creazione di documenti secondo hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="db6bf-218">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-219">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-219">Congratulations!</span></span> <span data-ttu-id="db6bf-220">L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="db6bf-221">Hello diagramma seguente illustra come query di database SQL di Azure Cosmos hello sintassi viene chiamata insieme hello creata e hello stessa logica si applica anche query con LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagramma che illustra ambito hello e il significato della query hello utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="db6bf-223">Hello [FROM](documentdb-sql-query.md#FromClause) parola chiave è facoltativa in query hello perché le query di database di Azure Cosmos sono già tooa con ambito singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="db6bf-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="db6bf-224">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="db6bf-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="db6bf-225">Azure DB Cosmos dedurrà famiglie, alla radice o il nome di variabile hello scelto, raccolta corrente hello di riferimento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="db6bf-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="db6bf-226"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="db6bf-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="db6bf-227">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="db6bf-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="db6bf-228">Copiare e incollare hello **ReplaceFamilyDocument** metodo dopo il **ExecuteSimpleQuery** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="db6bf-229">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo l'esecuzione di query hello, alla fine di hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="db6bf-230">Dopo la sostituzione del documento hello, verrà eseguito hello stessa query nuovamente tooview hello modificato documento.</span><span class="sxs-lookup"><span data-stu-id="db6bf-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="db6bf-231">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-232">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-232">Congratulations!</span></span> <span data-ttu-id="db6bf-233">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="db6bf-234"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="db6bf-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="db6bf-235">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="db6bf-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="db6bf-236">Copiare e incollare hello **DeleteFamilyDocument** metodo dopo il **ReplaceFamilyDocument** metodo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="db6bf-237">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo hello seconda esecuzione della query, alla fine di hello del metodo hello.</span><span class="sxs-lookup"><span data-stu-id="db6bf-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="db6bf-238">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-239">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-239">Congratulations!</span></span> <span data-ttu-id="db6bf-240">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="db6bf-241"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare database hello</span><span class="sxs-lookup"><span data-stu-id="db6bf-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="db6bf-242">L'eliminazione hello creata database rimuoverà database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="db6bf-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="db6bf-243">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo dopo documento hello eliminare toodelete hello intero database e tutte le risorse di elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="db6bf-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="db6bf-244">Premere **F5** toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="db6bf-245">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-245">Congratulations!</span></span> <span data-ttu-id="db6bf-246">L'eliminazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="db6bf-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="db6bf-247"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#</span><span class="sxs-lookup"><span data-stu-id="db6bf-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="db6bf-248">In un'applicazione hello toobuild Visual Studio in modalità di debug, premere F5.</span><span class="sxs-lookup"><span data-stu-id="db6bf-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="db6bf-249">Si dovrebbe vedere l'output di hello dell'app get avviata in una finestra della console.</span><span class="sxs-lookup"><span data-stu-id="db6bf-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="db6bf-250">output di Hello saranno visualizzati i risultati di hello di hello query è aggiunto e deve corrispondere il testo di esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="db6bf-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

<span data-ttu-id="db6bf-251">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="db6bf-251">Congratulations!</span></span> <span data-ttu-id="db6bf-252">È stata completata l'esercitazione hello e dispone di un'applicazione di console lavoro c#!</span><span class="sxs-lookup"><span data-stu-id="db6bf-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="db6bf-253"><a id="GetSolution"></a>Ottenere una soluzione di esercitazione completa hello</span><span class="sxs-lookup"><span data-stu-id="db6bf-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="db6bf-254">Se si non ho avuto tempo hello toocomplete i passaggi in questa esercitazione, oppure solo gli esempi di codice hello di desidera toodownload, è possibile ottenere dalla [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="db6bf-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="db6bf-255">soluzione di GetStarted toobuild hello, sarà necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="db6bf-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="db6bf-256">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="db6bf-256">An active Azure account.</span></span> <span data-ttu-id="db6bf-257">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="db6bf-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="db6bf-258">Un [account Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="db6bf-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="db6bf-259">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) soluzione disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="db6bf-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="db6bf-260">toorestore hello riferimenti toohello SDK .NET di Azure Cosmos DB in Visual Studio, fare doppio clic su hello **GetStarted** soluzione in Esplora soluzioni e quindi fare clic su **abilitare il ripristino del pacchetto NuGet**.</span><span class="sxs-lookup"><span data-stu-id="db6bf-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="db6bf-261">Quindi, nel file app. config hello, aggiornare i valori EndpointUrl e AuthorizationKey hello come descritto in [connettere account Azure Cosmos DB tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="db6bf-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="db6bf-262">Per completare la procedura, è sufficiente procedere alla compilazione.</span><span class="sxs-lookup"><span data-stu-id="db6bf-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="db6bf-263">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db6bf-263">Next steps</span></span>
* <span data-ttu-id="db6bf-264">Per un'esercitazione su MVC ASP.NET più complessa,</span><span class="sxs-lookup"><span data-stu-id="db6bf-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="db6bf-265">vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="db6bf-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="db6bf-266">Desidera tooperform scala e test delle prestazioni con Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="db6bf-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="db6bf-267">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="db6bf-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="db6bf-268">Informazioni su come troppo[controlla le richieste, utilizzo e archiviazione di Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="db6bf-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="db6bf-269">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="db6bf-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="db6bf-270">toolearn ulteriori informazioni su Azure Cosmos DB, vedere [benvenuto tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="db6bf-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
