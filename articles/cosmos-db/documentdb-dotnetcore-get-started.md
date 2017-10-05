---
title: 'Azure Cosmos DB: Introduzione all''API DocumentDB con l''esercitazione per .NET Core | Microsoft Docs'
description: Esercitazione che consente di creare un database online e un'applicazione console in C# usando Azure Cosmos DB DocumentDB API .NET Core SDK.
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
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="cff02-103">Azure Cosmos DB: Introduzione all'API DocumentDB e a .NET Core</span><span class="sxs-lookup"><span data-stu-id="cff02-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cff02-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cff02-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="cff02-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="cff02-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="cff02-106">Node.js per MongoDB</span><span class="sxs-lookup"><span data-stu-id="cff02-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="cff02-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="cff02-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="cff02-108">Java</span><span class="sxs-lookup"><span data-stu-id="cff02-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="cff02-109">C++</span><span class="sxs-lookup"><span data-stu-id="cff02-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="cff02-110">Introduzione all'API DocumentDB per Azure Cosmos DB con l'esercitazione su .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cff02-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="cff02-111">Dopo aver seguito questa esercitazione, si otterrà un'applicazione console che consente di creare e ridefinire le query delle risorse Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cff02-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="cff02-112">Tratteremo questo argomento:</span><span class="sxs-lookup"><span data-stu-id="cff02-112">We'll cover:</span></span>

* <span data-ttu-id="cff02-113">Creazione e connessione a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cff02-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="cff02-114">Configurare una soluzione Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cff02-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="cff02-115">Creazione di un database online</span><span class="sxs-lookup"><span data-stu-id="cff02-115">Creating an online database</span></span>
* <span data-ttu-id="cff02-116">Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="cff02-116">Creating a collection</span></span>
* <span data-ttu-id="cff02-117">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="cff02-117">Creating JSON documents</span></span>
* <span data-ttu-id="cff02-118">Esecuzione di query sulla raccolta</span><span class="sxs-lookup"><span data-stu-id="cff02-118">Querying the collection</span></span>
* <span data-ttu-id="cff02-119">Sostituzione di un documento</span><span class="sxs-lookup"><span data-stu-id="cff02-119">Replacing a document</span></span>
* <span data-ttu-id="cff02-120">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="cff02-120">Deleting a document</span></span>
* <span data-ttu-id="cff02-121">Eliminazione del database</span><span class="sxs-lookup"><span data-stu-id="cff02-121">Deleting the database</span></span>

<span data-ttu-id="cff02-122">Non si ha tempo?</span><span class="sxs-lookup"><span data-stu-id="cff02-122">Don't have time?</span></span> <span data-ttu-id="cff02-123">Nessun problema.</span><span class="sxs-lookup"><span data-stu-id="cff02-123">Don't worry!</span></span> <span data-ttu-id="cff02-124">La soluzione completa è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="cff02-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="cff02-125">Per istruzioni rapide, vedere la sezione [Ottenere la soluzione completa](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="cff02-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="cff02-126">Per compilare un'applicazione Xamarin iOS, Android o Forms usando l'API DocumentDB e .NET Core SDK,</span><span class="sxs-lookup"><span data-stu-id="cff02-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="cff02-127">vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cff02-128">Azure Cosmos DB .NET Core SDK usato in questa esercitazione non è ancora compatibile con le app della piattaforma UWP (Universal Windows Platform).</span><span class="sxs-lookup"><span data-stu-id="cff02-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="cff02-129">Per una versione di anteprima di .NET Core SDK che supporta le app della piattaforma UWP, inviare un messaggio di posta elettronica a [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cff02-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="cff02-130">Ecco come procedere.</span><span class="sxs-lookup"><span data-stu-id="cff02-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cff02-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cff02-131">Prerequisites</span></span>
<span data-ttu-id="cff02-132">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="cff02-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="cff02-133">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cff02-133">An active Azure account.</span></span> <span data-ttu-id="cff02-134">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cff02-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="cff02-135">In alternativa, per questa esercitazione è possibile usare l'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="cff02-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cff02-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="cff02-137">Se si usa MacOS o Linux, è possibile sviluppare app .NET Core dalla riga di comando installando [.NET Core SDK](https://www.microsoft.com/net/core#macos) per la piattaforma scelta.</span><span class="sxs-lookup"><span data-stu-id="cff02-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="cff02-138">Se si usa Windows, è possibile sviluppare app .NET Core dalla riga di comando installando [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="cff02-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="cff02-139">È possibile usare il proprio editor o scaricare [Visual Studio Code](https://code.visualstudio.com/), gratuito e utilizzabile in Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="cff02-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="cff02-140">Passaggio 1: Creare un account di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cff02-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="cff02-141">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cff02-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="cff02-142">Se si ha già un account, è possibile ignorare questo passaggio e passare a [Configurare la soluzione Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cff02-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="cff02-143">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cff02-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="cff02-144"><a id="SetupVS"></a>Passaggio 2: Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cff02-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="cff02-145">Aprire **Visual Studio 2017** nel computer.</span><span class="sxs-lookup"><span data-stu-id="cff02-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="cff02-146">Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="cff02-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="cff02-147">Nella finestra di dialogo **Nuovo progetto** selezionare **Modelli** / **Visual C#** / **.NET Core**/**Applicazione console (.NET Core)**, assegnare il nome **DocumentDBGettingStarted** al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cff02-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Screenshot della finestra Nuovo progetto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="cff02-149">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="cff02-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="cff02-150">Senza uscire dal menu fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cff02-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Screenshot del menu selezionato con il pulsante destro del mouse per il progetto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="cff02-152">Nella scheda **NuGet** fare clic su **Sfoglia** nella parte superiore della finestra e digitare **azure documentdb** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="cff02-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="cff02-153">Nei risultati trovare **Microsoft.Azure.DocumentDB.Core** e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="cff02-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="cff02-154">L'ID pacchetto per la libreria client di DocumentDB per .NET Core è [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="cff02-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="cff02-155">Se si fa riferimento a una versione di .NET Framework, ad esempio net461, non supportata da questo pacchetto .NET Core NuGet, usare [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) che supporta tutte le versioni di .NET Framework a partire da .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cff02-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="cff02-156">Quando richiesto, accettare le installazioni del pacchetto NuGet e il contratto di licenza.</span><span class="sxs-lookup"><span data-stu-id="cff02-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="cff02-157">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cff02-157">Great!</span></span> <span data-ttu-id="cff02-158">Ora che abbiamo completato l'installazione, iniziamo a scrivere il codice.</span><span class="sxs-lookup"><span data-stu-id="cff02-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="cff02-159">Un progetto di codice completo di questa esercitazione è disponibile in [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="cff02-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="cff02-160"><a id="Connect"></a>Passaggio 3: Connettersi a un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cff02-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="cff02-161">In primo luogo, aggiungere questi riferimenti all'inizio dell'applicazione c#, nel file Program.cs:</span><span class="sxs-lookup"><span data-stu-id="cff02-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="cff02-162">Per completare questa esercitazione, assicurarsi di aggiungere le dipendenze illustrate sopra.</span><span class="sxs-lookup"><span data-stu-id="cff02-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="cff02-163">Aggiungere ora queste due costanti e la variabile *client* sotto la classe pubblica *Program*.</span><span class="sxs-lookup"><span data-stu-id="cff02-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="cff02-164">Passare quindi al [portale di Azure](https://portal.azure.com) per recuperare l'URI e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="cff02-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="cff02-165">L'URI e la chiave primaria di Azure Cosmos DB sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="cff02-166">Nel portale di Azure passare all'account Azure Cosmos DB e quindi fare clic su **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="cff02-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="cff02-167">Copiare l'URI dal portale e incollarlo in `<your endpoint URI>` nel file program.cs.</span><span class="sxs-lookup"><span data-stu-id="cff02-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="cff02-168">Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla in `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="cff02-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="cff02-169">Se si usa l'emulatore Azure Cosmos DB, usare `https://localhost:8081` come endpoint e la chiave di autorizzazione ben definita di [Come sviluppare usando l'emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="cff02-170">Assicurarsi di rimuovere < e > lasciando le virgolette doppie che racchiudono l'endpoint e la chiave.</span><span class="sxs-lookup"><span data-stu-id="cff02-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console C#.][keys]

<span data-ttu-id="cff02-173">Per avviare l'applicazione introduttiva, si creerà una nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cff02-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="cff02-174">Sotto il metodo **Main** aggiungere la nuova attività asincrona denominata **GetStartedDemo** che creerà la nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cff02-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="cff02-175">Aggiungere questo codice per eseguire l'attività asincrona dal metodo **Main** .</span><span class="sxs-lookup"><span data-stu-id="cff02-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="cff02-176">Il metodo **Main** rileva le eccezioni e le scrive nella console.</span><span class="sxs-lookup"><span data-stu-id="cff02-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="cff02-177">Premere il pulsante **DocumentDBGettingStarted** per compilare ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="cff02-178">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-178">Congratulations!</span></span> <span data-ttu-id="cff02-179">La connessione a un account Azure Cosmos DB è stata stabilita. Ora è possibile esaminare l'uso delle risorse di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cff02-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="cff02-180">Passaggio 4: Creare un database</span><span class="sxs-lookup"><span data-stu-id="cff02-180">Step 4: Create a database</span></span>
<span data-ttu-id="cff02-181">Prima di aggiungere il codice per la creazione di un database, aggiungere un metodo helper per la scrittura nella console.</span><span class="sxs-lookup"><span data-stu-id="cff02-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="cff02-182">Copiare e incollare il metodo **WriteToConsoleAndPromptToContinue** sotto il metodo **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="cff02-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="cff02-183">È possibile creare un [database](documentdb-resources.md#databases) di Azure Cosmos DB usando il metodo [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cff02-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="cff02-184">Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="cff02-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="cff02-185">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del client.</span><span class="sxs-lookup"><span data-stu-id="cff02-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="cff02-186">Verrà creato un database denominato *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="cff02-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="cff02-187">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-188">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-188">Congratulations!</span></span> <span data-ttu-id="cff02-189">La creazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="cff02-190"><a id="CreateColl"></a>Passaggio 5: Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="cff02-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="cff02-191">**CreateDocumentCollectionAsync** crea una nuova raccolta con velocità effettiva riservata, che presenta implicazioni in termini di prezzi.</span><span class="sxs-lookup"><span data-stu-id="cff02-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="cff02-192">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="cff02-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="cff02-193">È possibile creare una [raccolta](documentdb-resources.md#collections) usando il metodo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cff02-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="cff02-194">Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="cff02-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="cff02-195">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del database.</span><span class="sxs-lookup"><span data-stu-id="cff02-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="cff02-196">Verrà creata una raccolta di documenti denominata *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="cff02-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="cff02-197">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-198">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-198">Congratulations!</span></span> <span data-ttu-id="cff02-199">La creazione di una raccolta di documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="cff02-200"><a id="CreateDoc"></a>Passaggio 6: Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="cff02-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="cff02-201">È possibile creare un [documento](documentdb-resources.md#documents) usando il metodo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cff02-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="cff02-202">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="cff02-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="cff02-203">Ora è possibile inserire uno o più documenti.</span><span class="sxs-lookup"><span data-stu-id="cff02-203">We can now insert one or more documents.</span></span> <span data-ttu-id="cff02-204">Se sono già disponibili dati da archiviare nel database, è possibile usare lo [strumento di migrazione dei dati](import-data.md)di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cff02-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="cff02-205">È necessario creare prima di tutto una classe **Family** che rappresenterà gli oggetti archiviati in Azure Cosmos DB in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="cff02-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="cff02-206">Verranno create anche le sottoclassi **Parent**, **Child**, **Pet** e **Address** da usare in **Family**.</span><span class="sxs-lookup"><span data-stu-id="cff02-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="cff02-207">Si noti che i documenti devono avere una proprietà **Id** serializzata come **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="cff02-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="cff02-208">Creare queste classi aggiungendo le classi secondarie interne seguenti dopo il metodo **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="cff02-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="cff02-209">Copiare e incollare le classi **Family**, **Parent**, **Child**, **Pet** e **Address** sotto il metodo **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="cff02-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="cff02-210">Copiare e incollare il metodo **CreateFamilyDocumentIfNotExists** sotto il metodo **CreateDocumentCollectionIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="cff02-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="cff02-211">Inserire anche due documenti, relativi rispettivamente alla famiglia Andersen e alla famiglia Wakefield.</span><span class="sxs-lookup"><span data-stu-id="cff02-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="cff02-212">Copiare e incollare il codice riportato dopo `// ADD THIS PART TO YOUR CODE` nel metodo **GetStartedDemo** sotto il codice di creazione della raccolta di documenti.</span><span class="sxs-lookup"><span data-stu-id="cff02-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="cff02-213">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-214">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-214">Congratulations!</span></span> <span data-ttu-id="cff02-215">La creazione di due documenti di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagramma che illustra la relazione gerarchica tra l'account, il database online, la raccolta e i documenti usati nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="cff02-217"><a id="Query"></a>Passaggio 7: Eseguire query sulle risorse di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cff02-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="cff02-218">Azure Cosmos DB supporta [query complesse](documentdb-sql-query.md) sui documenti JSON archiviati in ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="cff02-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="cff02-219">Il codice di esempio seguente mostra diverse query che usano la sintassi SQL di Azure Cosmos DB e LINQ e che possono essere eseguite sui documenti inseriti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="cff02-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="cff02-220">Copiare e incollare il metodo **ExecuteSimpleQuery** sotto il metodo **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="cff02-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="cff02-221">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di creazione del secondo documento.</span><span class="sxs-lookup"><span data-stu-id="cff02-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="cff02-222">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-223">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-223">Congratulations!</span></span> <span data-ttu-id="cff02-224">L'esecuzione di una query in una raccolta di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="cff02-225">Il diagramma seguente illustra il modo in cui la sintassi di query di SQL di Azure Cosmos DB viene chiamata sulla raccolta creata e la stessa logica viene applicata alla query di LINQ.</span><span class="sxs-lookup"><span data-stu-id="cff02-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagramma che illustra l'ambito e il significato della query usata nell'esercitazione su NoSQL per creare un'applicazione console C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="cff02-227">La parola chiave [FROM](documentdb-sql-query.md#FromClause) è facoltativa nella query perché le query di Azure Cosmos DB sono già limitate a una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="cff02-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="cff02-228">Di conseguenza, "FROM Families f" può essere scambiata con "FROM root r" o con il nome di qualsiasi altra variabile scelta.</span><span class="sxs-lookup"><span data-stu-id="cff02-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="cff02-229">DocumentDB dedurrà che Families, root o il nome della variabile scelta, si riferisce per impostazione predefinita alla raccolta attuale.</span><span class="sxs-lookup"><span data-stu-id="cff02-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="cff02-230"><a id="ReplaceDocument"></a>Passaggio 8: Sostituire un documento JSON</span><span class="sxs-lookup"><span data-stu-id="cff02-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="cff02-231">Azure Cosmos DB supporta la sostituzione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="cff02-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="cff02-232">Copiare e incollare il metodo **ReplaceFamilyDocument** sotto il metodo **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="cff02-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="cff02-233">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="cff02-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="cff02-234">Dopo aver sostituito il documento, verrà eseguita di nuovo la stessa query per visualizzare il documento modificato.</span><span class="sxs-lookup"><span data-stu-id="cff02-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="cff02-235">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-236">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-236">Congratulations!</span></span> <span data-ttu-id="cff02-237">La sostituzione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="cff02-238"><a id="DeleteDocument"></a>Passaggio 9: Eliminare un documento JSON</span><span class="sxs-lookup"><span data-stu-id="cff02-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="cff02-239">Azure Cosmos DB supporta l'eliminazione di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="cff02-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="cff02-240">Copiare e incollare il metodo **DeleteFamilyDocument** sotto il metodo **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="cff02-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="cff02-241">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di esecuzione della seconda query.</span><span class="sxs-lookup"><span data-stu-id="cff02-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="cff02-242">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-243">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-243">Congratulations!</span></span> <span data-ttu-id="cff02-244">L'eliminazione di un documento di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="cff02-245"><a id="DeleteDatabase"></a>Passaggio 10: Eliminare il database</span><span class="sxs-lookup"><span data-stu-id="cff02-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="cff02-246">Se si elimina il database creato, verrà rimosso il database e tutte le risorse figlio (raccolte, documenti e così via).</span><span class="sxs-lookup"><span data-stu-id="cff02-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="cff02-247">Copiare e incollare il codice seguente nel metodo **GetStartedDemo** sotto il codice di eliminazione del documento per eliminare l'intero database e tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="cff02-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="cff02-248">Premere il pulsante **DocumentDBGettingStarted** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cff02-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="cff02-249">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-249">Congratulations!</span></span> <span data-ttu-id="cff02-250">L'eliminazione di un database di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="cff02-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="cff02-251"><a id="Run"></a>Passaggio 11: Eseguire l'intera applicazione console C#</span><span class="sxs-lookup"><span data-stu-id="cff02-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="cff02-252">Premere il pulsante **DocumentDBGettingStarted** in Visual Studio per compilare l'applicazione in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="cff02-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="cff02-253">Verrà visualizzato l'output dell'app introduttiva nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="cff02-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="cff02-254">L'output visualizzerà i risultati delle query aggiunte e dovrà corrispondere al testo di esempio riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cff02-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="cff02-255">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="cff02-255">Congratulations!</span></span> <span data-ttu-id="cff02-256">L'esercitazione è stata completata ed è stata creata un'applicazione console C# funzionante.</span><span class="sxs-lookup"><span data-stu-id="cff02-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="cff02-257"><a id="GetSolution"></a> Ottenere la soluzione completa per l'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cff02-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="cff02-258">Per creare la soluzione GetStarted completa contenente tutti gli esempi riportati in questo articolo, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="cff02-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="cff02-259">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cff02-259">An active Azure account.</span></span> <span data-ttu-id="cff02-260">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cff02-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="cff02-261">Un [account Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="cff02-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="cff02-262">La soluzione [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="cff02-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="cff02-263">Per ripristinare i riferimenti all'API DocumentDB per Azure Cosmos DB .NET Core SDK in Visual Studio, fare clic con il pulsante destro del mouse sulla soluzione **GetStarted** in Esplora soluzioni e quindi scegliere **Abilita ripristino dei pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cff02-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="cff02-264">Nel file Program.cs aggiornare quindi i valori EndpointUrl e AuthorizationKey come illustrato nell'articolo [Connettersi a un account Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="cff02-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cff02-265">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cff02-265">Next steps</span></span>
* <span data-ttu-id="cff02-266">Per un'esercitazione su MVC ASP.NET più complessa,</span><span class="sxs-lookup"><span data-stu-id="cff02-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="cff02-267">vedere [Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="cff02-268">Per sviluppare un'applicazione Xamarin iOS, Android o Forms usando l'API DocumentDB per Azure Cosmos DB .NET Core SDK,</span><span class="sxs-lookup"><span data-stu-id="cff02-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="cff02-269">vedere [Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="cff02-270">Per la scalabilità e i test delle prestazioni con Azure Cosmos DB,</span><span class="sxs-lookup"><span data-stu-id="cff02-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="cff02-271">vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="cff02-272">Informazioni su come [Monitorare le richieste, l'utilizzo e le risorse di archiviazione di Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="cff02-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="cff02-273">Eseguire query sul set di dati di esempio illustrato nella pagina [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="cff02-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="cff02-274">Per altre informazioni sul modello di programmazione, vedere [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="cff02-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
