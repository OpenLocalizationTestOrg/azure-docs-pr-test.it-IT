---
title: 'Esercitazione su ASP.NET MVC per Azure Cosmos DB: sviluppo di un''applicazione Web | Microsoft Docs'
description: "Esercitazione su MVC ASP.NET per creare un'applicazione Web MVC con Azure Cosmos DB. Si archivieranno documenti JSON e si accederà ai dati da un'app todo ospitata in siti Web di Azure - Esercitazione dettagliata su MVC ASP.NET."
keywords: esercitazione su mvc asp.net, sviluppo di applicazioni web, applicazione web mvc, esercitazione dettagliata su mvc asp net
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="5c6f9-105"><a name="_Toc395809351"></a>Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5c6f9-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c6f9-106">.NET</span><span class="sxs-lookup"><span data-stu-id="5c6f9-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="5c6f9-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5c6f9-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="5c6f9-108">Java</span><span class="sxs-lookup"><span data-stu-id="5c6f9-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="5c6f9-109">Python</span><span class="sxs-lookup"><span data-stu-id="5c6f9-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="5c6f9-110">Per illustrare come sfruttare in modo efficiente Azure Cosmos DB per archiviare ed eseguire query su documenti JSON, questo articolo include una procedura dettagliata end-to-end che illustra come creare un'app todo con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="5c6f9-111">Le attività verranno memorizzate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Schermata dell'applicazione Web MVC per un elenco di azioni creata in questa esercitazione - Esercitazione dettagliata su MVC ASP NET](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="5c6f9-113">La procedura guidata illustra come usare il servizio Azure Cosmos DB per archiviare i dati e accedervi da un'applicazione Web MVC ASP.NET ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="5c6f9-114">Se si preferisce un'esercitazione che illustra solo Azure Cosmos DB e non i componenti ASP.NET MVC, vedere [Compilare un'applicazione console C# di Azure Cosmos DB](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="5c6f9-115">Questa esercitazione presuppone già una certa esperienza nell'uso di MCV ASP.NET e di Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="5c6f9-116">Se non si ha alcuna esperienza con ASP.NET o gli [strumenti richiesti come prerequisiti](#_Toc395637760), è consigliabile scaricare il progetto di esempio completo da [GitHub][GitHub] e seguire le relative istruzioni.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="5c6f9-117">Una volta creata la soluzione, è possibile leggere questo articolo per approfondire il codice nel contesto del progetto.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="5c6f9-118"><a name="_Toc395637760"></a>Prerequisiti per questa esercitazione sul database</span><span class="sxs-lookup"><span data-stu-id="5c6f9-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="5c6f9-119">Prima di seguire le istruzioni di questo articolo, verificare che siano disponibili gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="5c6f9-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-120">An active Azure account.</span></span> <span data-ttu-id="5c6f9-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5c6f9-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="5c6f9-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="5c6f9-123">OR</span></span>

    <span data-ttu-id="5c6f9-124">Un'installazione locale dell'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="5c6f9-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="5c6f9-126">Microsoft Azure SDK per .NET per Visual Studio 2017, disponibile tramite il programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="5c6f9-127">Tutte le schermate in questo articolo sono state ottenute usando Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="5c6f9-128">Se il sistema in uso è configurato con versioni diverse, è probabile che le schermate e le opzioni non siano interamente corrispondenti. Se si soddisfano i prerequisiti precedenti, la soluzione dovrebbe funzionare comunque.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="5c6f9-129"><a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5c6f9-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="5c6f9-130">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="5c6f9-131">Se si ha già un account SQL (DocumentDB) per Azure Cosmos DB o si usa l'emulatore Azure Cosmos DB per questa esercitazione, è possibile proseguire con il passaggio [Creare una nuova applicazione MVC ASP.NET](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="5c6f9-132">Verrà ora illustrata in modo dettagliato la procedura per creare un'applicazione MVC ASP.NET completamente nuova.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="5c6f9-133"><a name="_Toc395637762"></a>Passaggio 2: Creare una nuova applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5c6f9-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="5c6f9-134">Scegliere **Nuovo** dal menu **File** di Visual Studio e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="5c6f9-135">Verrà visualizzata la finestra di dialogo **Nuovo progetto** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="5c6f9-136">Nel riquadro **Tipi progetto** espandere **Modelli**, **Visual C#**, **Web** e quindi selezionare **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Schermata della finestra di dialogo Nuovo progetto con il tipo di progetto applicazione Web ASP.NET evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="5c6f9-138">Nella casella **Nome** digitare il nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="5c6f9-139">Questa esercitazione usa il nome "todo".</span><span class="sxs-lookup"><span data-stu-id="5c6f9-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="5c6f9-140">Se si sceglie di usare un valore diverso da questo, quindi ogni volta che in questa esercitazione viene descritto lo spazio dei nomi todo, è necessario modificare gli esempi di codice forniti per usare il nome assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="5c6f9-141">Fare clic su **Sfoglia** per passare alla cartella in cui si vuole creare il progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="5c6f9-142">Viene visualizzata la finestra di dialogo **Nuova applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Schermata della finestra della nuova applicazione Web ASP.NET con il modello di applicazione MVC evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="5c6f9-144">Nel riquadro dei modelli selezionare **MVC**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="5c6f9-145">Fare clic su **OK** e lasciare che Visual Studio esegua le operazioni necessarie per lo scaffolding del modello MVC ASP.NET vuoto.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="5c6f9-146">Al termine della creazione dell'applicazione MVC standard da parte di Visual Studio, sarà disponibile un'applicazione ASP.NET vuota eseguibile in locale.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="5c6f9-147">L'esecuzione locale del progetto verrà ignorata perché è già stata mostrata per l'applicazione ASP.NET "Hello World".</span><span class="sxs-lookup"><span data-stu-id="5c6f9-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="5c6f9-148">Si passerà direttamente all'aggiunta di Azure Cosmos DB al progetto e alla compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="5c6f9-149"><a name="_Toc395637767"></a>Passaggio 3: Aggiungere Azure Cosmos DB al progetto di applicazione Web MVC</span><span class="sxs-lookup"><span data-stu-id="5c6f9-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="5c6f9-150">Ora che è disponibile la maggior parte del plumbing MVC ASP.NET necessario per questa soluzione, è possibile passare all'aggiunta di Azure Cosmos DB all'applicazione Web MVC.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="5c6f9-151">Azure Cosmos DB .NET SDK è distribuito come pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="5c6f9-152">Per ottenere il pacchetto NuGet in Visual Studio, usare Gestione pacchetti NuGet in Visual Studio facendo clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e quindi scegliendo **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Screenshot delle opzioni del menu di scelta rapida per il progetto applicazione Web in Esplora soluzioni, con Gestisci pacchetti NuGet evidenziato.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="5c6f9-154">Viene visualizzata la finestra di dialogo **Gestione pacchetti NuGet** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="5c6f9-155">Nella casella **Sfoglia** di NuGet digitare ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="5c6f9-156">Il nome del pacchetto non è stato aggiornato in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="5c6f9-157">Dai risultati installare il pacchetto **Microsoft.Azure.DocumentDB by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="5c6f9-158">Il pacchetto Azure Cosmos DB verrà scaricato e installato, con tutte le dipendenze, ad esempio Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="5c6f9-159">Fare clic su **OK** nella finestra **Anteprima** e su **Accetto** nella finestra **Accettazione della licenza** per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Schermata della finestra Gestisci pacchetti NuGet, con la libreria del client di Microsoft Azure DocumentDB evidenziata](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="5c6f9-161">In alternativa, è possibile usare la console di Gestione pacchetti per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="5c6f9-162">A tale scopo, scegliere **Gestione pacchetti NuGet** dal menu **Strumenti** e quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="5c6f9-163">Al prompt dei comandi, immettere quanto segue.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="5c6f9-164">Una volta installato il pacchetto, la soluzione di Visual Studio dovrebbe assomigliare alla seguente, con due nuovi riferimenti aggiunti, Microsoft.Azure.Documents.Client e Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Schermata dei due riferimenti aggiunti al progetto di dati JSON in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="5c6f9-166"><a name="_Toc395637763"></a>Passaggio 4: Configurare l'applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5c6f9-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="5c6f9-167">Vengono ora aggiunti i modelli, le visualizzazioni e i controller all'applicazione MVC:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="5c6f9-168">[Aggiungere un modello](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="5c6f9-169">[Aggiungere un controller](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="5c6f9-170">[Aggiungere visualizzazioni](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="5c6f9-171"><a name="_Toc395637764"></a>Aggiungere un modello di dati JSON</span><span class="sxs-lookup"><span data-stu-id="5c6f9-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="5c6f9-172">Creare prima di tutto l'elemento che corrisponde alla lettera **M** in MVC, ovvero il modello.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="5c6f9-173">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Modelli**, scegliere **Aggiungi** e quindi fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="5c6f9-174">Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="5c6f9-175">Denominare la nuova classe **Item.cs** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="5c6f9-176">In questo nuovo file **Item.cs** , aggiungere quanto segue dopo l'ultima *istruzione using*.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="5c6f9-177">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="5c6f9-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="5c6f9-178">con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-178">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="5c6f9-179">Tutti i dati presenti in Azure Cosmos DB vengono passati in rete e archiviati come JSON.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="5c6f9-180">Per controllare il modo in cui gli oggetti vengono serializzati/deserializzati da JSON.NET, è possibile usare l'attributo **JsonProperty**, come mostrato nella classe **Item** appena creata.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="5c6f9-181">Questa operazione **non è necessaria** , ma è utile per verificare che le proprietà seguano le convenzioni di denominazione maiuscole-minuscole JSON.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="5c6f9-182">Non solo è possibile controllare il formato del nome della proprietà quando viene usata in JSON, ma anche rinominare completamente le proprietà .NET, come è stato fatto con la proprietà **Description** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="5c6f9-183"><a name="_Toc395637765"></a>Aggiungere un controller</span><span class="sxs-lookup"><span data-stu-id="5c6f9-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="5c6f9-184">Una volta creato il modello **M**, si passa alla creazione di una classe controller **C** in MVC.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="5c6f9-185">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Controller**, scegliere **Aggiungi** e quindi fare clic su **Controller**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="5c6f9-186">Verrà visualizzata la finestra di dialogo **Aggiungi scaffolding** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="5c6f9-187">Selezionare **Controller MVC 5 - Vuoto** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Schermata della finestra di dialogo Aggiungi scaffolding con l'opzione Controller MVC 5 - Vuoto evidenziata](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="5c6f9-189">Assegnare al controller il nome **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="5c6f9-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Schermata della finestra di dialogo Aggiungi controller](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="5c6f9-191">Una volta creato il file, la soluzione di Visual Studio deve essere simile alla seguente, con il nuovo file ItemController.cs in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="5c6f9-192">Viene anche visualizzato il nuovo file Item.cs creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Schermata della soluzione Visual Studio - Esplora soluzioni con il nuovo file ItemController.cs e il file Item.cs evidenziati](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="5c6f9-194">È possibile chiudere il file ItemController.cs. Si tornerà a questo file in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="5c6f9-195"><a name="_Toc395637766"></a>Aggiungere visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="5c6f9-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="5c6f9-196">A questo punto è necessario creare le visualizzazioni **V** in MVC:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="5c6f9-197">[Aggiungere una visualizzazione Indice elemento](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="5c6f9-198">[Aggiungere una visualizzazione Nuovo elemento](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="5c6f9-199">[Aggiungere una visualizzazione Modifica elemento](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="5c6f9-200"><a name="AddItemIndexView"></a>Aggiungere una visualizzazione Indice elemento</span><span class="sxs-lookup"><span data-stu-id="5c6f9-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="5c6f9-201">In **Esplora soluzioni** espandere la cartella **Visualizzazioni**, fare clic con il pulsante destro del mouse sulla cartella **Item** vuota creata prima da Visual Studio quando è stato aggiunto **ItemController**, scegliere **Aggiungi** e quindi fare clic su **Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Schermata di Esplora soluzioni con la cartella Item creata da Visual Studio con i comandi Aggiungi visualizzazione evidenziati](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="5c6f9-203">Nella finestra di dialogo **Aggiungi visualizzazione** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="5c6f9-204">Nella casella **Nome visualizzazione** digitare ***Index***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="5c6f9-205">Nella casella **Modello** selezionare ***Elenco***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="5c6f9-206">Nella casella **Classe modello** selezionare ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="5c6f9-207">Nella casella della pagina di layout digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Schermata con la finestra di dialogo Aggiungi visualizzazione](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="5c6f9-209">Una volta impostati tutti questi valori, fare clic su **Aggiungi** , in modo che venga creata una nuova visualizzazione modello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="5c6f9-210">Al termine, verrà aperto il file con estensione cshtml creato.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="5c6f9-211">È ora possibile chiudere questo file in Visual Studio, perché vi si tornerà di nuovo più avanti.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="5c6f9-212"><a name="AddNewIndexView"></a>Aggiungere una visualizzazione Nuovo elemento</span><span class="sxs-lookup"><span data-stu-id="5c6f9-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="5c6f9-213">Viene ora creata una nuova visualizzazione per la creazione di nuovi oggetti **Item** in modo simile a come è stata creata una visualizzazione **Indice elemento**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="5c6f9-214">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Item**, scegliere **Aggiungi** e quindi fare clic su **Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="5c6f9-215">Nella finestra di dialogo **Aggiungi visualizzazione** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="5c6f9-216">Nella casella **Nome visualizzazione** digitare ***Create***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="5c6f9-217">Nella casella **Modello** selezionare ***Create***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="5c6f9-218">Nella casella **Classe modello** selezionare ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="5c6f9-219">Nella casella della pagina di layout digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="5c6f9-220">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="5c6f9-221"><a name="_Toc395888515"></a>Aggiungere una visualizzazione Modifica elemento</span><span class="sxs-lookup"><span data-stu-id="5c6f9-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="5c6f9-222">È infine possibile aggiungere un'ultima visualizzazione per la modifica di un oggetto **Item** , allo stesso modo in cui sono state create le altre.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="5c6f9-223">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella **Item**, scegliere **Aggiungi** e quindi fare clic su **Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="5c6f9-224">Nella finestra di dialogo **Aggiungi visualizzazione** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="5c6f9-225">Nella casella **Nome visualizzazione** digitare ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="5c6f9-226">Nella casella **Modello** selezionare ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="5c6f9-227">Nella casella **Classe modello** selezionare ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="5c6f9-228">Nella casella della pagina di layout digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="5c6f9-229">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-229">Click **Add**.</span></span>

<span data-ttu-id="5c6f9-230">Al termine, chiudere tutti i documenti con estensione cshtml in Visual Studio. Si tornerà a queste visualizzazioni in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="5c6f9-231"><a name="_Toc395637769"></a>Passaggio 5: Completamento dell'aggiunta di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5c6f9-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="5c6f9-232">Ora che le caratteristiche standard di MVC vengono prese in considerazione, è possibile aggiungere il codice per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="5c6f9-233">In questa sezione viene aggiunto il codice per gestire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="5c6f9-234">[Creare un elenco di elementi incompleti](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="5c6f9-235">[Aggiungere elementi](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="5c6f9-236">[Modificare elementi](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="5c6f9-237"><a name="_Toc395637770"></a>Elenco di elementi incompleti in un'applicazione Web MVC</span><span class="sxs-lookup"><span data-stu-id="5c6f9-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="5c6f9-238">La prima cosa da fare è aggiungere una classe che contenga tutta la logica per connettersi e usare Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="5c6f9-239">Per questa esercitazione verrà inclusa tutta questa logica in una classe di tipo archivio denominata DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="5c6f9-240">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Aggiungi** e quindi fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="5c6f9-241">Assegnare alla nuova classe il nome **DocumentDBRepository** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="5c6f9-242">Nella nuova classe **DocumentDBRepository** creata aggiungere le istruzioni *using* seguenti sopra la dichiarazione *namespace*.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="5c6f9-243">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="5c6f9-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="5c6f9-244">con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-244">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="5c6f9-245">Poiché alcuni valori vengono letti dalla configurazione, aprire il file **Web.config** dell'applicazione e aggiungere le righe seguenti dopo la sezione `<AppSettings>`.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="5c6f9-246">A questo punto, aggiornare i valori per *endpoint* e *authKey* usando il pannello Chiavi del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="5c6f9-247">Usare il valore di **URI** dal pannello Chiavi come valore dell'impostazione dell'endpoint e usare **CHIAVE PRIMARIA** oppure **CHIAVE SECONDARIA** dal pannello Chiavi come valore dell'impostazione authKey.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="5c6f9-248">Ciò consente di collegare il repository Azure Cosmos DB, ora è possibile aggiungere la logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="5c6f9-249">Un'applicazione per un elenco di azioni deve innanzitutto consentire la visualizzazione degli elementi incompleti.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="5c6f9-250">Copiare e incollare il seguente frammento di codice in un punto qualsiasi all'interno della classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="5c6f9-251">Aprire il file **ItemController** aggiunto in precedenza e aggiungere le seguenti *istruzioni using* sopra la dichiarazione dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="5c6f9-252">Se il progetto non è denominato "todo", è quindi necessario eseguire l'aggiornamento usando "todo.Models" per inserire il nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="5c6f9-253">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="5c6f9-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="5c6f9-254">con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="5c6f9-255">Aprire **Global.asax.cs** e aggiungere la riga seguente al metodo **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="5c6f9-256">A questo punto dovrebbe essere possibile compilare la soluzione senza errori.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="5c6f9-257">Se si eseguisse l'applicazione a questo punto, si passerebbe a **HomeController** e alla visualizzazione **Index** di tale controller.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="5c6f9-258">Questo è il comportamento predefinito per il progetto di modello MVC scelto inizialmente, ma è possibile cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="5c6f9-259">Per modificare questo comportamento, è possibile cambiare il routing nell'applicazione MVC.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="5c6f9-260">Aprire ***App\_Start\RouteConfig.cs***, trovare la riga che inizia con "defaults:" e modificarla in modo che sia analoga a quanto riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="5c6f9-261">Questo codice indica ad ASP.NET MVC che, se non è stato specificato alcun valore nell'URL per controllare il comportamento di routing, sarà necessario usare **Item** invece di **Home** come controller e **Index** come visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="5c6f9-262">A questo punto se si esegue l'applicazione, verrà eseguita una chiamata in **ItemController** che eseguirà una chiamata alla classe di tipo repository e userà il metodo GetItems per restituire tutti gli elementi incompleti alla visualizzazione **Views**\\**Item**\\**Index**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="5c6f9-263">Se compilato ed eseguito ora, il progetto avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Schermata dell'applicazione Web per un elenco di azioni creata in questa esercitazione del database](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="5c6f9-265"><a name="_Toc395637771"></a>Aggiungere elementi</span><span class="sxs-lookup"><span data-stu-id="5c6f9-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="5c6f9-266">Vengono ora inseriti alcuni elementi nel database, in modo che la griglia non sia più vuota.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="5c6f9-267">Sarà ora effettuata l'aggiunta di codice ad Azure Cosmos DBRepository e ItemController per rendere persistente il record in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="5c6f9-268">Aggiungere il metodo seguente alla classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="5c6f9-269">Questo metodo accetta semplicemente un oggetto passato al metodo stesso e lo rende permanente in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="5c6f9-270">Aprire il file ItemController.cs e aggiungere il seguente frammento di codice all'interno della classe.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="5c6f9-271">In tal modo, ASP.NET MVC individua le operazioni da eseguire per l'azione **Create** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="5c6f9-272">In questo caso, eseguire semplicemente il rendering della visualizzazione Create.cshtml associata creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="5c6f9-273">Nel controller è necessario avere più codici, ed il controller stesso accetterà la presentazione dal codice **Crea** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="5c6f9-274">Aggiungere il blocco di codice successivo alla classe ItemController.cs, che indica a MVC ASP.NET le operazioni da eseguire con un POST per i moduli per questo controller.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="5c6f9-275">Tale codice chiama DocumentDBRepository e utilizza il metodo CreateItemAsync per rendere persistente la nuova voce al database.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="5c6f9-276">**Nota sulla sicurezza**: l'attributo **ValidateAntiForgeryToken** viene usato qui per proteggere l'applicazione da attacchi di richiesta intersito falsa.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="5c6f9-277">Oltre ad aggiungere questo attributo, è necessario che le visualizzazioni usino questo token antifalsificazione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="5c6f9-278">Per altre informazioni sull'oggetto e sugli esempi di come implementarla correttamente, vedere [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery] (Impedire la falsificazione della richiesta tra siti).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="5c6f9-279">Il codice sorgente fornito in [GitHub][GitHub] consente l'implementazione completa.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="5c6f9-280">**Nota sulla sicurezza**: è possibile usare l'attributo **Bind** nel metodo del parametro per proteggersi da attacchi di overposting.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="5c6f9-281">Per altre informazioni dettagliate, vedere [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] (Operazioni CRUD di base in MVC ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="5c6f9-282">Questo è tutto il codice necessario per aggiungere nuovi elementi al database.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="5c6f9-283"><a name="_Toc395637772"></a>Modificare elementi</span><span class="sxs-lookup"><span data-stu-id="5c6f9-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="5c6f9-284">Vi è un'ultima operazione da eseguire ovvero l'aggiunta della possibilità di modificare oggetti **Item** nel database e di contrassegnarli come completi.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="5c6f9-285">Poiché questa visualizzazione per la modifica è già stata aggiunta al progetto, è sufficiente aggiungere il codice al controller e di nuovo alla classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="5c6f9-286">Aggiungere il codice seguente alla classe **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="5c6f9-287">Il primo di questi metodi, **GetItem**, recupera un elemento da Azure Cosmos DB, che viene passato a **ItemController** e quindi alla visualizzazione **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="5c6f9-288">Il secondo metodo appena aggiunto sostituisce il **documento** in Azure Cosmos DB con la versione del **documento** passato da **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="5c6f9-289">Aggiungere il codice seguente alla classe **ItemController** .</span><span class="sxs-lookup"><span data-stu-id="5c6f9-289">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="5c6f9-290">Il primo metodo gestisce Http GET che si verifica quando l'utente fa clic sul collegamento **Edit** dalla visualizzazione **Index**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="5c6f9-291">Questo metodo recupera un [**documento**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) da Azure Cosmos DB e lo passa alla visualizzazione **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="5c6f9-292">La visualizzazione **Edit** esegue quindi un'operazione Http POST in **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="5c6f9-293">Il secondo metodo aggiunto gestisce il passaggio dell'oggetto aggiornato ad Azure Cosmos DB in modo da renderlo permanente nel database.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="5c6f9-294">A questo punto, queste sono le procedure necessarie per eseguire l'applicazione, elencare oggetti **Item incompleti**, aggiungere nuovi oggetti **Item** e modificare oggetti **Item**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="5c6f9-295"><a name="_Toc395637773"></a>Passaggio 6: Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="5c6f9-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="5c6f9-296">Per testare l'applicazione nel computer locale, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="5c6f9-297">Premere F5 in Visual Studio per compilare l'applicazione in modalità di debug.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="5c6f9-298">L'applicazione verrà compilata e verrà avviato un browser con la pagina di griglia vuota osservata sopra:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Schermata dell'applicazione Web per un elenco di azioni creata in questa esercitazione del database](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="5c6f9-300">Fare clic sul collegamento **Crea nuovo** e specificare i valori dei campi **Nome** e **Descrizione**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="5c6f9-301">Lasciare deselezionata la casella di controllo **Completed**. In caso contrario, il nuovo oggetto **Item** verrà aggiunto con uno stato completato e non sarà visualizzato nell'elenco iniziale.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Schermata della visualizzazione Create](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="5c6f9-303">Fare clic su **Create** per tornare di nuovo alla visualizzazione **Index** e visualizzare **Item** nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Schermata della visualizzazione Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="5c6f9-305">È possibile aggiungere altri oggetti **Item** all'elenco di azioni.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="5c6f9-306">Fare clic su **Edit** accanto a un oggetto **Item** nell'elenco per tornare alla visualizzazione **Edit**, in cui è possibile aggiornare qualsiasi proprietà dell'oggetto, incluso il flag **Completed**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="5c6f9-307">Se si seleziona il flag **Completed** e si fa clic su **Salva**, l'oggetto **Item** viene rimosso dall'elenco di attività incomplete.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Schermata della visualizzazione Index con la casella Completed selezionata](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="5c6f9-309">Una volta testata l'app, premere CTRL+F5 per arrestarne il debug.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="5c6f9-310">È ora possibile distribuire l'app.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-310">You're ready to deploy!</span></span>

## <span data-ttu-id="5c6f9-311"><a name="_Toc395637774"></a>Passaggio 7: Distribuire l'applicazione nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="5c6f9-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="5c6f9-312">Poiché ora è completa e funziona correttamente con Azure Cosmos DB, è possibile distribuire questa app Web nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="5c6f9-313">Per pubblicare l'applicazione, è sufficiente fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Schermata dell'opzione Pubblica in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="5c6f9-315">Nella finestra di dialogo **Pubblica** fare clic su **Servizio app di Microsoft Azure**, quindi selezionare **Crea nuovo** per creare un profilo di servizio app o fare clic su **Seleziona esistente** per usare un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Finestra di dialogo Pubblica in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="5c6f9-317">Se si dispone di un profilo del Servizio app di Azure esistente, immettere il nome della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="5c6f9-318">Usare il filtro di **visualizzazione** per eseguire l'ordinamento in base al gruppo d risorse o al tipo di risorsa, quindi selezionare il Servizio app di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Finestra di dialogo del servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="5c6f9-320">Per creare un nuovo profilo del Servizio app di Azure, fare clic su **Crea nuovo** nella finestra di dialogo **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="5c6f9-321">Nella finestra di dialogo **Crea servizio app** immettere il nome dell'app Web e la sottoscrizione appropriata, il gruppo di risorse e il piano di servizio app, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Finestra di dialogo Crea servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="5c6f9-323">Dopo alcuni secondi, Visual Studio completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile ammirare il proprio lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="5c6f9-324"><a name="_Toc395637775"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c6f9-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="5c6f9-325">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-325">Congratulations!</span></span> <span data-ttu-id="5c6f9-326">È stata creata la prima applicazione Web MVC ASP.NET con Azure Cosmos DB che è stata quindi pubblicata in Azure.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="5c6f9-327">Il codice sorgente per l'applicazione completa, insieme alle funzionalità di eliminazione e relative ai dettagli non incluse in questa esercitazione, può essere scaricato o clonato da [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="5c6f9-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="5c6f9-328">Per aggiungere queste funzionalità all'app, recuperare il codice e aggiungerlo all'app.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="5c6f9-329">Per aggiungere altre funzionalità all'applicazione, esaminare le API disponibili nella raccolta [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) (Libreria .NET per Azure Cosmos DB), in cui è anche possibile aggiungere il proprio contributo in [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="5c6f9-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
