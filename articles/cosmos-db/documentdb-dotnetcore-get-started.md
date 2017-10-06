---
title: 'Azure Cosmos DB: Introduzione all''API DocumentDB con l''esercitazione per .NET Core | Microsoft Docs'
description: Un'esercitazione che consente di creare un database online e l'applicazione console c# utilizzando hello Azure Cosmos DB DocumentDB API .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="40836-103">Azure Cosmos DB: Introduzione all'API DocumentDB hello e .NET Core</span><span class="sxs-lookup"><span data-stu-id="40836-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40836-104">.NET</span><span class="sxs-lookup"><span data-stu-id="40836-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="40836-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="40836-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="40836-106">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="40836-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="40836-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="40836-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="40836-108">Java</span><span class="sxs-lookup"><span data-stu-id="40836-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="40836-109">C++</span><span class="sxs-lookup"><span data-stu-id="40836-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="40836-110">Introduzione toohello API DocumentDB DB Cosmos Azure introduzione esercitazione .NET Core.</span><span class="sxs-lookup"><span data-stu-id="40836-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="40836-111">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40836-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="40836-112">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="40836-112">We'll cover:</span></span>

* <span data-ttu-id="40836-113">Creazione e connessione account Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="40836-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="40836-114">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40836-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="40836-115">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="40836-115">Creating an online database</span></span>
* <span data-ttu-id="40836-116">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="40836-116">Creating a collection</span></span>
* <span data-ttu-id="40836-117">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="40836-117">Creating JSON documents</span></span>
* <span data-ttu-id="40836-118">Esecuzione di query hello raccolta</span><span class="sxs-lookup"><span data-stu-id="40836-118">Querying hello collection</span></span>
* <span data-ttu-id="40836-119">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="40836-119">Replacing a document</span></span>
* <span data-ttu-id="40836-120">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="40836-120">Deleting a document</span></span>
* <span data-ttu-id="40836-121">L'eliminazione di database hello</span><span class="sxs-lookup"><span data-stu-id="40836-121">Deleting hello database</span></span>

<span data-ttu-id="40836-122">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="40836-122">Don't have time?</span></span> <span data-ttu-id="40836-123">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="40836-123">Don't worry!</span></span> <span data-ttu-id="40836-124">la soluzione completa di Hello è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="40836-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="40836-125">Passare toohello [ottenere hello soluzione completa sezione](#GetSolution) per istruzioni rapide.</span><span class="sxs-lookup"><span data-stu-id="40836-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="40836-126">Desidera toobuild un Xamarin iOS, Android o form applicazione utilizzando hello DocumentDB API e SDK di .NET Core?</span><span class="sxs-lookup"><span data-stu-id="40836-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="40836-127">vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="40836-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="40836-128">Hello Azure Cosmos DB .NET Core SDK usata in questa esercitazione non è ancora compatibile con le app Universal Windows Platform (UWP).</span><span class="sxs-lookup"><span data-stu-id="40836-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="40836-129">Per una versione di anteprima di hello .NET Core SDK che supporta le app UWP, inviare posta elettronica troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="40836-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="40836-130">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="40836-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40836-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40836-131">Prerequisites</span></span>
<span data-ttu-id="40836-132">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="40836-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="40836-133">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="40836-133">An active Azure account.</span></span> <span data-ttu-id="40836-134">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="40836-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="40836-135">In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="40836-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="40836-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="40836-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="40836-137">Se si sta lavorando MacOS o Linux, è possibile sviluppare applicazioni di .NET Core dalla riga di comando hello installando hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) per piattaforma hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="40836-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="40836-138">Se si lavora in Windows, è possibile sviluppare applicazioni .NET Core dalla riga di comando hello installando hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="40836-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="40836-139">È possibile usare il proprio editor o scaricare [Visual Studio Code](https://code.visualstudio.com/), gratuito e utilizzabile in Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="40836-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="40836-140">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40836-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="40836-141">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40836-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="40836-142">Se si dispone già di un account a cui si vuole toouse, è possibile andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="40836-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="40836-143">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[soluzione di Visual Studio del programma di installazione](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="40836-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="40836-144"><a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40836-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="40836-145">Aprire **Visual Studio 2017** nel computer.</span><span class="sxs-lookup"><span data-stu-id="40836-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="40836-146">In hello **File** dal menu **New**, quindi scegliere **progetto**.</span><span class="sxs-lookup"><span data-stu-id="40836-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="40836-147">In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **.NET Core** / **Applicazione console (.NET Core)**, denominare il progetto **DocumentDBGettingStarted**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="40836-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Cattura di schermata della finestra Nuovo progetto hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="40836-149">In hello **Esplora**, fare clic con il pulsante destro su **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="40836-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="40836-150">Senza uscire dal menu di hello, fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="40836-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Cattura di schermata del diritto hello Menu selezionato per hello progetto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="40836-152">In hello **NuGet** scheda, fare clic su **Sfoglia** nella parte superiore di hello della finestra hello e tipo **azure documentdb** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="40836-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="40836-153">All'interno dei risultati di hello, trovare **Microsoft.Azure.DocumentDB.Core** e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="40836-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="40836-154">ID del pacchetto per la libreria Client di DocumentDB per .NET Core hello Hello è [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="40836-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="40836-155">Se si fa riferimento a una versione di .NET Framework, ad esempio net461, non supportata da questo pacchetto .NET Core NuGet, usare [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) che supporta tutte le versioni di .NET Framework a partire da .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="40836-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="40836-156">Al prompt di hello, accettare il contratto di licenza hello e le installazioni di pacchetto NuGet di hello.</span><span class="sxs-lookup"><span data-stu-id="40836-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="40836-157">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="40836-157">Great!</span></span> <span data-ttu-id="40836-158">Ora che è stata completata l'installazione di hello, iniziamo a scrivere del codice.</span><span class="sxs-lookup"><span data-stu-id="40836-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="40836-159">Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="40836-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="40836-160"><a id="Connect"></a>Passaggio 3: Connettere l'account di Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="40836-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="40836-161">In primo luogo, aggiungere questi riferimenti inizio toohello dell'applicazione c#, nel file Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="40836-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="40836-162">In ordine toocomplete questa esercitazione, accertarsi di aggiungere le dipendenze di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="40836-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="40836-163">Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.</span><span class="sxs-lookup"><span data-stu-id="40836-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="40836-164">Successivamente, head toohello [portale Azure](https://portal.azure.com) tooretrieve URI e chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="40836-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="40836-165">Hello Azure Cosmos DB URI e chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="40836-166">In hello portale di Azure, passare tooyour Azure Cosmos DB account e quindi fare clic su **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="40836-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="40836-167">Copiare hello URI dal portale di hello e incollarlo in `<your endpoint URI>` nel file program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="40836-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="40836-168">Quindi copia hello chiave primaria dal portale hello e incollarlo in `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="40836-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="40836-169">Se si utilizza hello Azure Cosmos DB emulatore, usare `https://localhost:8081` come endpoint hello e chiave di autorizzazione ben definito di hello da [come toodevelop utilizzando hello Azure Cosmos DB emulatore](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="40836-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="40836-170">Verificare che tooremove hello < e >, ma lasciare hello doppie virgolette che racchiudono l'endpoint e la chiave.</span><span class="sxs-lookup"><span data-stu-id="40836-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Cattura di schermata del portale di Azure utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c# hello.][keys]

<span data-ttu-id="40836-173">Si inizierà a un'applicazione hello recupero avviata mediante la creazione di una nuova istanza di hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="40836-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="40836-174">Di sotto di hello **Main** metodo, aggiungere la nuova attività asincrona chiamata **GetStartedDemo**, che creerà il nuovo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="40836-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="40836-175">Aggiungere l'esempio di codice seguente hello toorun l'attività asincrona dal **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="40836-176">Hello **Main** metodo intercettare le eccezioni e scriverli toohello console.</span><span class="sxs-lookup"><span data-stu-id="40836-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
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
```

<span data-ttu-id="40836-177">Hello premere **DocumentDBGettingStarted** pulsante toobuild ed eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="40836-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="40836-178">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-178">Congratulations!</span></span> <span data-ttu-id="40836-179">È una connessione account Azure Cosmos DB tooan, Ora esaminiamo un utilizzo delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40836-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="40836-180">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="40836-180">Step 4: Create a database</span></span>
<span data-ttu-id="40836-181">Prima di aggiungere codice hello per la creazione di un database, aggiungere un metodo di supporto per la scrittura di toohello console.</span><span class="sxs-lookup"><span data-stu-id="40836-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="40836-182">Copiare e incollare hello **WriteToConsoleAndPromptToContinue** metodo sotto hello **GetStartedDemo** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="40836-183">Il database di Azure Cosmos [database](documentdb-resources.md#databases) possono essere create usando hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="40836-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="40836-184">Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="40836-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="40836-185">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo di sotto di creazione di client hello.</span><span class="sxs-lookup"><span data-stu-id="40836-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="40836-186">Verrà creato un database denominato *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="40836-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="40836-187">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-188">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-188">Congratulations!</span></span> <span data-ttu-id="40836-189">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="40836-190"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="40836-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="40836-191">**CreateDocumentCollectionAsync** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="40836-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="40836-192">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="40836-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="40836-193">Oggetto [raccolta](documentdb-resources.md#collections) possono essere create usando hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="40836-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="40836-194">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="40836-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="40836-195">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo di sotto di creazione del database hello.</span><span class="sxs-lookup"><span data-stu-id="40836-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="40836-196">Verrà creata una raccolta di documenti denominata *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="40836-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="40836-197">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-198">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-198">Congratulations!</span></span> <span data-ttu-id="40836-199">La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="40836-200"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="40836-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="40836-201">Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="40836-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="40836-202">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="40836-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="40836-203">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="40836-203">We can now insert one or more documents.</span></span> <span data-ttu-id="40836-204">Se si dispongono già di dati desiderato toostore nel database, è possibile utilizzare Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="40836-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="40836-205">Innanzitutto, è necessario toocreate un **famiglia** classe che rappresenta gli oggetti archiviati all'interno di Azure Cosmos DB in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="40836-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="40836-206">Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**.</span><span class="sxs-lookup"><span data-stu-id="40836-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="40836-207">Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="40836-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="40836-208">Creare queste classi aggiungendo le seguenti classi secondario interne dopo hello hello **GetStartedDemo** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="40836-209">Copiare e incollare hello **famiglia**, **padre**, **figlio**, **Pet**, e **indirizzo** classi sotto Hello **WriteToConsoleAndPromptToContinue** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="40836-210">Copiare e incollare hello **CreateFamilyDocumentIfNotExists** metodo sotto il **CreateDocumentCollectionIfNotExists** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="40836-211">Inserire due documenti, uno per hello Andersen famiglia e hello Wakefield famiglia.</span><span class="sxs-lookup"><span data-stu-id="40836-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="40836-212">Copiare e incollare il codice hello che segue `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** metodo di sotto di creazione della raccolta documenti hello.</span><span class="sxs-lookup"><span data-stu-id="40836-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="40836-213">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-214">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-214">Congratulations!</span></span> <span data-ttu-id="40836-215">La creazione di due documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramma che illustra relazione gerarchica di hello tra account hello, database online hello, raccolta hello e documenti hello utilizzato dai hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="40836-217"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40836-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="40836-218">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="40836-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="40836-219">Hello codice di esempio seguente vengono illustrate diverse query - utilizzando entrambi SQL di Azure Cosmos DB sintassi, nonché LINQ - che è possibile eseguire hello è inseriti nel passaggio precedente hello documenti.</span><span class="sxs-lookup"><span data-stu-id="40836-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="40836-220">Copiare e incollare hello **ExecuteSimpleQuery** metodo sotto il **CreateFamilyDocumentIfNotExists** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="40836-221">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo sotto la creazione di documenti secondo hello.</span><span class="sxs-lookup"><span data-stu-id="40836-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="40836-222">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-223">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-223">Congratulations!</span></span> <span data-ttu-id="40836-224">L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="40836-225">Hello diagramma seguente illustra come query di database SQL di Azure Cosmos hello sintassi viene chiamata insieme hello creata e hello stessa logica si applica anche query con LINQ toohello.</span><span class="sxs-lookup"><span data-stu-id="40836-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagramma che illustra ambito hello e il significato della query hello utilizzato da hello NoSQL esercitazione toocreate un'applicazione console c#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="40836-227">Hello [FROM](documentdb-sql-query.md#FromClause) parola chiave è facoltativa in query hello perché le query di database di Azure Cosmos sono già tooa con ambito singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="40836-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="40836-228">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="40836-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="40836-229">DocumentDB dedurrà famiglie, alla radice o il nome di variabile hello scelto, raccolta corrente hello di riferimento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="40836-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="40836-230"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="40836-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="40836-231">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="40836-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="40836-232">Copiare e incollare hello **ReplaceFamilyDocument** metodo sotto il **ExecuteSimpleQuery** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="40836-233">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo sotto l'esecuzione di query hello.</span><span class="sxs-lookup"><span data-stu-id="40836-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="40836-234">Dopo la sostituzione del documento hello, verrà eseguito hello stessa query nuovamente tooview hello modificato documento.</span><span class="sxs-lookup"><span data-stu-id="40836-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="40836-235">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-236">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-236">Congratulations!</span></span> <span data-ttu-id="40836-237">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="40836-238"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="40836-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="40836-239">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="40836-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="40836-240">Copiare e incollare hello **DeleteFamilyDocument** metodo sotto il **ReplaceFamilyDocument** metodo.</span><span class="sxs-lookup"><span data-stu-id="40836-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="40836-241">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo di sotto di esecuzione della query secondo hello.</span><span class="sxs-lookup"><span data-stu-id="40836-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="40836-242">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-243">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-243">Congratulations!</span></span> <span data-ttu-id="40836-244">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="40836-245"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare database hello</span><span class="sxs-lookup"><span data-stu-id="40836-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="40836-246">L'eliminazione hello creata database rimuoverà database hello e tutte le risorse di elementi figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="40836-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="40836-247">Copia e Incolla seguenti di hello codice tooyour **GetStartedDemo** metodo sotto il documento hello eliminare toodelete hello intero database e tutte le risorse di elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="40836-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="40836-248">Hello premere **DocumentDBGettingStarted** pulsante toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="40836-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="40836-249">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-249">Congratulations!</span></span> <span data-ttu-id="40836-250">L'eliminazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="40836-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="40836-251"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#</span><span class="sxs-lookup"><span data-stu-id="40836-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="40836-252">Hello premere **DocumentDBGettingStarted** pulsante in un'applicazione hello toobuild Visual Studio in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="40836-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="40836-253">Si dovrebbe vedere l'output di hello dell'app nella finestra di console hello avviata get.</span><span class="sxs-lookup"><span data-stu-id="40836-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="40836-254">output di Hello saranno visualizzati i risultati di hello di hello query è aggiunto e deve corrispondere il testo di esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="40836-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="40836-255">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="40836-255">Congratulations!</span></span> <span data-ttu-id="40836-256">È stata completata l'esercitazione hello e dispone di un'applicazione di console lavoro c#!</span><span class="sxs-lookup"><span data-stu-id="40836-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="40836-257"><a id="GetSolution"></a>Ottenere una soluzione di esercitazione completa hello</span><span class="sxs-lookup"><span data-stu-id="40836-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="40836-258">soluzione GetStarted hello toobuild che contiene tutti gli esempi di hello in questo articolo, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="40836-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="40836-259">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="40836-259">An active Azure account.</span></span> <span data-ttu-id="40836-260">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="40836-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="40836-261">Un [account Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="40836-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="40836-262">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) soluzione disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="40836-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="40836-263">toorestore hello riferimenti toohello API DocumentDB Azure Cosmos DB SDK per .NET Core in Visual Studio, fare doppio clic su hello **GetStarted** soluzione in Esplora soluzioni e quindi fare clic su **Abilita ripristino dei pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="40836-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="40836-264">Quindi, nel file Program.cs hello, aggiornare i valori EndpointUrl e AuthorizationKey hello come descritto in [connettere account Azure Cosmos DB tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="40836-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40836-265">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40836-265">Next steps</span></span>
* <span data-ttu-id="40836-266">Per un'esercitazione su MVC ASP.NET più complessa,</span><span class="sxs-lookup"><span data-stu-id="40836-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="40836-267">vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="40836-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="40836-268">Desidera toodevelop un Xamarin iOS, Android o form applicazione utilizzando hello API DocumentDB Azure Cosmos DB SDK per .NET Core?</span><span class="sxs-lookup"><span data-stu-id="40836-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="40836-269">vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="40836-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="40836-270">Desidera tooperform scala e test delle prestazioni con Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="40836-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="40836-271">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="40836-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="40836-272">Informazioni su come troppo[richieste, utilizzo e archiviazione di monitoraggio Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="40836-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="40836-273">Eseguire query su questo set di dati di esempio in hello [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="40836-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="40836-274">toolearn più sul modello di programmazione di hello, vedere [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="40836-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
