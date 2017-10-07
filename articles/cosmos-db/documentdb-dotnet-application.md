---
title: 'Esercitazione su ASP.NET MVC per Azure Cosmos DB: sviluppo di un''applicazione Web | Microsoft Docs'
description: "ASP.NET MVC toocreate esercitazione un'applicazione web MVC utilizza Azure Cosmos DB. Si archivieranno documenti JSON e si accederà ai dati da un'app todo ospitata in siti Web di Azure - Esercitazione dettagliata su MVC ASP.NET."
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
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="68be7-105"><a name="_Toc395809351"></a>Esercitazione su ASP.NET MVC: Sviluppo di applicazioni Web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="68be7-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68be7-106">.NET</span><span class="sxs-lookup"><span data-stu-id="68be7-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="68be7-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="68be7-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="68be7-108">Java</span><span class="sxs-lookup"><span data-stu-id="68be7-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="68be7-109">Python</span><span class="sxs-lookup"><span data-stu-id="68be7-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="68be7-110">toohighlight illustrato in modo efficiente, è possibile utilizzare Azure Cosmos DB toostore e query documenti JSON, in questo articolo fornisce una procedura dettagliata end-to-end che mostra come un'app todo tramite Azure Cosmos DB toobuild.</span><span class="sxs-lookup"><span data-stu-id="68be7-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="68be7-111">attività Hello verranno archiviate come documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="68be7-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Cattura di schermata dell'elenco attività hello applicazione web MVC creato da questa esercitazione - esercitazione ASP NET MVC dettagliate](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="68be7-113">Questa procedura dettagliata viene illustrato come toouse hello Azure Cosmos DB servizio toostore e accedere ai dati da un'applicazione web MVC ASP.NET ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="68be7-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="68be7-114">Se si sta cercando un'esercitazione che consente solo di Azure Cosmos DB, e non hello componenti ASP.NET MVC, vedere [compilare un'applicazione console Azure Cosmos DB c#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68be7-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="68be7-115">Questa esercitazione presuppone già una certa esperienza nell'uso di MCV ASP.NET e di Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="68be7-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="68be7-116">Se si tooASP.NET nuova o hello [strumenti prerequisiti](#_Toc395637760), si consiglia di scaricare il progetto di esempio completo hello da [GitHub] [ GitHub] e seguendo le istruzioni di hello in In questo esempio.</span><span class="sxs-lookup"><span data-stu-id="68be7-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="68be7-117">Quando l'applicazione viene compilata, è possibile esaminare informazioni dettagliate di toogain questo articolo sul codice hello nel contesto di hello del progetto hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="68be7-118"><a name="_Toc395637760"></a>Prerequisiti per questa esercitazione sul database</span><span class="sxs-lookup"><span data-stu-id="68be7-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="68be7-119">Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver seguito hello:</span><span class="sxs-lookup"><span data-stu-id="68be7-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="68be7-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="68be7-120">An active Azure account.</span></span> <span data-ttu-id="68be7-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="68be7-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="68be7-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68be7-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="68be7-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="68be7-123">OR</span></span>

    <span data-ttu-id="68be7-124">Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="68be7-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="68be7-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="68be7-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="68be7-126">Microsoft Azure SDK per .NET per Visual Studio 2017, disponibili tramite hello programma di installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68be7-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="68be7-127">Tutte le schermate di hello in questo articolo sono state prese utilizzando Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="68be7-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="68be7-128">Se il sistema è configurato con una versione diversa, che è possibile che le schermate e le opzioni non corrispondono completamente, ma se si soddisfa hello sopra prerequisiti dovrebbe funzionare questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="68be7-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="68be7-129"><a name="_Toc395637761"></a>Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="68be7-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="68be7-130">Creare prima di tutto un account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="68be7-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="68be7-131">Se è già un account SQL (DocumentDB) per Azure Cosmos DB o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[creare una nuova applicazione MVC ASP.NET](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="68be7-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="68be7-132">Verrà ora descritto come toocreate una nuova applicazione MVC ASP.NET da hello interamente progettato.</span><span class="sxs-lookup"><span data-stu-id="68be7-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="68be7-133"><a name="_Toc395637762"></a>Passaggio 2: Creare una nuova applicazione MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="68be7-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="68be7-134">In Visual Studio, su hello **File** menu, scegliere troppo**New**e quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="68be7-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="68be7-135">Hello **nuovo progetto** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="68be7-136">In hello **tipi di progetto** riquadro espandere **modelli**, **Visual c#**, **Web**, quindi selezionare **applicazione Web ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="68be7-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Cattura di schermata della finestra di dialogo Nuovo progetto hello con tipo di progetto applicazione Web ASP.NET hello evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="68be7-138">In hello **nome** casella, nome del progetto hello hello di tipo.</span><span class="sxs-lookup"><span data-stu-id="68be7-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="68be7-139">Questa esercitazione viene utilizzato il nome di hello "attività".</span><span class="sxs-lookup"><span data-stu-id="68be7-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="68be7-140">Se si sceglie un valore diverso da questo toouse, ogni volta che questa esercitazione parla hello dello spazio dei nomi di attività, è necessario tooadjust hello fornito codice esempi toouse qualsiasi denominata dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="68be7-141">Fare clic su **Sfoglia** toonavigate toohello cartella in cui sarebbe come progetto di hello toocreate e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="68be7-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="68be7-142">Hello **nuova applicazione Web ASP.NET** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Cattura di schermata della finestra di dialogo nuova applicazione Web ASP.NET hello con modello di applicazione MVC hello evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="68be7-144">Nel riquadro Modelli hello selezionare **MVC**.</span><span class="sxs-lookup"><span data-stu-id="68be7-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="68be7-145">Fare clic su **OK** e consentire a Visual Studio di eseguire le operazioni necessarie per il modello ASP.NET MVC vuoto di scaffolding hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="68be7-146">Una volta Visual Studio ha terminato la creazione di un'applicazione MVC boilerplate hello è un'applicazione ASP.NET vuota che è possibile eseguire in locale.</span><span class="sxs-lookup"><span data-stu-id="68be7-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="68be7-147">Si verrà trattata progetto hello in esecuzione in locale perché si è certi che abbiamo hello rilevato tutti ASP.NET "Hello World" dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="68be7-148">Segue un' tooadding retta Azure Cosmos DB toothis progetto e la compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="68be7-149"><a name="_Toc395637767"></a>Passaggio 3: Aggiungere il progetto applicazione web di Azure Cosmos DB tooyour MVC</span><span class="sxs-lookup"><span data-stu-id="68be7-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="68be7-150">Ora che è disponibile la maggior parte dei plumbing di ASP.NET MVC hello necessaria per questa soluzione, iniziamo toohello vero scopo di questa esercitazione, aggiunta di applicazione web di Azure Cosmos DB tooour MVC.</span><span class="sxs-lookup"><span data-stu-id="68be7-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="68be7-151">Hello Azure Cosmos DB .NET SDK è incluso nel pacchetto e distribuito come pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="68be7-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="68be7-152">tooget hello pacchetto NuGet in Visual Studio, usare Gestione pacchetti NuGet di hello in Visual Studio facendo clic sul progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="68be7-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Cattura di schermata di hello fare doppio clic su Opzioni per il progetto di applicazione web hello in Esplora soluzioni, con Gestione pacchetti NuGet evidenziato.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="68be7-154">Hello **Gestisci pacchetti NuGet** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="68be7-155">In hello NuGet **Sfoglia** digitare ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="68be7-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="68be7-156">(nome del pacchetto hello non è stato aggiornato tooAzure DB Cosmos.)</span><span class="sxs-lookup"><span data-stu-id="68be7-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="68be7-157">Dai risultati di hello, installare hello **Microsoft.Azure.DocumentDB da Microsoft** pacchetto.</span><span class="sxs-lookup"><span data-stu-id="68be7-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="68be7-158">Ciò Scarica e installa il pacchetto di Azure Cosmos DB hello, nonché tutte le dipendenze, ad esempio newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="68be7-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="68be7-159">Fare clic su **OK** in hello **anteprima** finestra e **accetto** in hello **dell'accettazione della licenza** finestra toocomplete hello installazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Cattura di screen della finestra Gestisci pacchetti NuGet hello con hello libreria Client di Microsoft Azure DocumentDB evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="68be7-161">In alternativa è possibile utilizzare il pacchetto di hello tooinstall Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="68be7-162">toodo in questo caso, hello **strumenti** menu, fare clic su **Gestione pacchetti NuGet**, quindi fare clic su **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="68be7-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="68be7-163">Al prompt dei comandi hello, digitare il seguente hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="68be7-164">Dopo aver installato il pacchetto di hello, la soluzione di Visual Studio dovrebbe essere simile a seguito di hello con due nuovi riferimenti aggiunti, Microsoft.Azure.Documents.Client e newtonsoft. JSON.</span><span class="sxs-lookup"><span data-stu-id="68be7-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Cattura screen di due riferimenti hello aggiunti toohello progetto di dati JSON in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="68be7-166"><a name="_Toc395637763"></a>Passaggio 4: Configurare l'applicazione ASP.NET MVC hello</span><span class="sxs-lookup"><span data-stu-id="68be7-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="68be7-167">A questo punto aggiungere modelli, visualizzazioni e controller toothis MVC applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="68be7-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="68be7-168">[Aggiungere un modello](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="68be7-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="68be7-169">[Aggiungere un controller](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="68be7-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="68be7-170">[Aggiungere visualizzazioni](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="68be7-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="68be7-171"><a name="_Toc395637764"></a>Aggiungere un modello di dati JSON</span><span class="sxs-lookup"><span data-stu-id="68be7-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="68be7-172">Si inizia creando hello **M** in MVC hello modello.</span><span class="sxs-lookup"><span data-stu-id="68be7-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="68be7-173">In **Esplora**, hello rapida **modelli** cartella, fare clic su **Aggiungi**e quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="68be7-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="68be7-174">Hello **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="68be7-175">Denominare la nuova classe **Item.cs** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="68be7-176">In questo nuovo **Item.cs** file, aggiungere ultimo segue hello dopo hello *utilizzando l'istruzione*.</span><span class="sxs-lookup"><span data-stu-id="68be7-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="68be7-177">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="68be7-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="68be7-178">con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="68be7-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="68be7-179">Tutti i dati nel database di Azure Cosmos viene trasmessa in transito hello e archiviata come JSON.</span><span class="sxs-lookup"><span data-stu-id="68be7-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="68be7-180">toocontrol hello modo gli oggetti serializzati o deserializzati dal JSON.NET è possibile utilizzare hello **JsonProperty** attributo come dimostrato nel hello **elemento** classe appena creata.</span><span class="sxs-lookup"><span data-stu-id="68be7-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="68be7-181">In caso contrario **hanno** toodo questo ma si desidera che le proprietà seguono le convenzioni di denominazione di hello JSON camelCase tooensure.</span><span class="sxs-lookup"><span data-stu-id="68be7-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="68be7-182">Non solo è possibile controllare il formato di hello hello del nome della proprietà quando entra in JSON, ma è possibile rinominare le proprietà .NET completamente come con hello **descrizione** proprietà.</span><span class="sxs-lookup"><span data-stu-id="68be7-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="68be7-183"><a name="_Toc395637765"></a>Aggiungere un controller</span><span class="sxs-lookup"><span data-stu-id="68be7-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="68be7-184">Che si occupa di hello **M**, ora è possibile crearne hello **C** in una classe controller MVC.</span><span class="sxs-lookup"><span data-stu-id="68be7-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="68be7-185">In **Esplora**, hello rapida **controller** cartella, fare clic su **Aggiungi**e quindi fare clic su **Controller**.</span><span class="sxs-lookup"><span data-stu-id="68be7-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="68be7-186">Hello **aggiungere lo scaffolding** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="68be7-187">Selezionare **Controller MVC 5 - Vuoto** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Cattura di schermata della hello aggiungere lo scaffolding di finestra di dialogo hello Controller MVC 5 - opzione vuoto evidenziato](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="68be7-189">Assegnare al controller il nome **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="68be7-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Cattura di schermata della finestra di dialogo Aggiungi Controller hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="68be7-191">Una volta creato il file hello, la soluzione di Visual Studio dovrebbe essere simile seguente hello con nuovo file ItemController.cs hello in **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="68be7-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="68be7-192">viene inoltre visualizzato Hello Item.cs file creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="68be7-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Cattura di schermata della soluzione di Visual Studio - Esplora soluzioni con file ItemController.cs nuovo hello e Item.cs file evidenziato hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="68be7-194">È possibile chiudere ItemController.cs, si ritornerà tooit in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="68be7-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="68be7-195"><a name="_Toc395637766"></a>Aggiungere visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="68be7-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="68be7-196">A questo punto, è possibile crearne hello **V** in MVC hello viste:</span><span class="sxs-lookup"><span data-stu-id="68be7-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="68be7-197">[Aggiungere una visualizzazione Indice elemento](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="68be7-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="68be7-198">[Aggiungere una visualizzazione Nuovo elemento](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="68be7-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="68be7-199">[Aggiungere una visualizzazione Modifica elemento](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="68be7-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="68be7-200"><a name="AddItemIndexView"></a>Aggiungere una visualizzazione Indice elemento</span><span class="sxs-lookup"><span data-stu-id="68be7-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="68be7-201">In **Esplora**, espandere hello **viste** cartella, il pulsante destro del mouse hello vuoto **elemento** cartella in cui verrà creata automaticamente quando si aggiunge hello  **ItemController** in precedenza, fare clic su **Aggiungi**, quindi fare clic su **vista**.</span><span class="sxs-lookup"><span data-stu-id="68be7-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Cattura di schermata della finestra Esplora soluzioni con cartella elemento hello creato da Visual Studio con i comandi Aggiungi visualizzazione hello evidenziati](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="68be7-203">In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68be7-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="68be7-204">In hello **nome vista** digitare ***indice***.</span><span class="sxs-lookup"><span data-stu-id="68be7-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="68be7-205">In hello **modello** , quindi selezionare ***elenco***.</span><span class="sxs-lookup"><span data-stu-id="68be7-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="68be7-206">In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.</span><span class="sxs-lookup"><span data-stu-id="68be7-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="68be7-207">Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="68be7-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Schermata di finestra di dialogo Aggiungi visualizzazione hello cattura di schermata](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="68be7-209">Una volta impostati tutti questi valori, fare clic su **Aggiungi** , in modo che venga creata una nuova visualizzazione modello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68be7-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="68be7-210">Al termine, si aprirà file cshtml hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="68be7-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="68be7-211">È possibile chiudere il file in Visual Studio come si tornerà tooit in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="68be7-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="68be7-212"><a name="AddNewIndexView"></a>Aggiungere una visualizzazione Nuovo elemento</span><span class="sxs-lookup"><span data-stu-id="68be7-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="68be7-213">Toohow simile è stato creato un **indice dell'elemento** vista, si creerà una nuova visualizzazione per la creazione di nuovi **elementi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="68be7-214">In **Esplora**, hello rapida **elemento** cartella fare nuovamente clic **Aggiungi**e quindi fare clic su **vista**.</span><span class="sxs-lookup"><span data-stu-id="68be7-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="68be7-215">In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68be7-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="68be7-216">In hello **nome vista** digitare ***crea***.</span><span class="sxs-lookup"><span data-stu-id="68be7-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="68be7-217">In hello **modello** , quindi selezionare ***crea***.</span><span class="sxs-lookup"><span data-stu-id="68be7-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="68be7-218">In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.</span><span class="sxs-lookup"><span data-stu-id="68be7-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="68be7-219">Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="68be7-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="68be7-220">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="68be7-221"><a name="_Toc395888515"></a>Aggiungere una visualizzazione Modifica elemento</span><span class="sxs-lookup"><span data-stu-id="68be7-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="68be7-222">Infine, aggiungere una visualizzazione ultima per la modifica di un **elemento** in hello esattamente come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="68be7-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="68be7-223">In **Esplora**, hello rapida **elemento** cartella fare nuovamente clic **Aggiungi**e quindi fare clic su **vista**.</span><span class="sxs-lookup"><span data-stu-id="68be7-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="68be7-224">In hello **Aggiungi visualizzazione** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68be7-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="68be7-225">In hello **nome vista** digitare ***modifica***.</span><span class="sxs-lookup"><span data-stu-id="68be7-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="68be7-226">In hello **modello** , quindi selezionare ***modifica***.</span><span class="sxs-lookup"><span data-stu-id="68be7-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="68be7-227">In hello **classe modello** , quindi selezionare ***elemento (todo. I modelli)***.</span><span class="sxs-lookup"><span data-stu-id="68be7-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="68be7-228">Nella casella di pagina di layout hello, digitare ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="68be7-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="68be7-229">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-229">Click **Add**.</span></span>

<span data-ttu-id="68be7-230">Al termine, chiudere tutti i documenti cshtml hello in Visual Studio come abbiamo restituiranno viste toothese in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="68be7-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="68be7-231"><a name="_Toc395637769"></a>Passaggio 5: Completamento dell'aggiunta di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="68be7-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="68be7-232">Ora che stuff MVC standard hello viene preso in considerazione, passiamo codice hello tooadding per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="68be7-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="68be7-233">In questa sezione verrà aggiunto codice che segue toohandle hello:</span><span class="sxs-lookup"><span data-stu-id="68be7-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="68be7-234">[Creare un elenco di elementi incompleti](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="68be7-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="68be7-235">[Aggiungere elementi](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="68be7-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="68be7-236">[Modificare elementi](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="68be7-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="68be7-237"><a name="_Toc395637770"></a>Elenco di elementi incompleti in un'applicazione Web MVC</span><span class="sxs-lookup"><span data-stu-id="68be7-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="68be7-238">Hello prima cosa, toodo qui è aggiungere una classe che contiene hello logica tooconnect tooand utilizzo di tutti i database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="68be7-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="68be7-239">Per questa esercitazione si sarà incapsulare tutti questa logica in classe repository tooa chiamato DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="68be7-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="68be7-240">In **Esplora**destro del mouse sul progetto hello, fare clic su **Aggiungi**, quindi fare clic su **classe**.</span><span class="sxs-lookup"><span data-stu-id="68be7-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="68be7-241">Nome nuova classe hello **DocumentDBRepository** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="68be7-242">In hello appena creato **DocumentDBRepository** classe e aggiungere il seguente hello *utilizzando istruzioni* sopra hello *dello spazio dei nomi* dichiarazione</span><span class="sxs-lookup"><span data-stu-id="68be7-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="68be7-243">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="68be7-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="68be7-244">con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="68be7-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="68be7-245">Si desidera leggere alcuni valori dalla configurazione, quindi aprire hello **Web. config** file dell'applicazione e aggiungere hello seguenti righe di sotto hello `<AppSettings>` sezione.</span><span class="sxs-lookup"><span data-stu-id="68be7-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="68be7-246">Aggiornare i valori hello per *endpoint* e *authKey* utilizzando il pannello chiavi hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68be7-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="68be7-247">Utilizzare hello **URI** dal Pannello di chiavi hello come valore di hello dell'impostazione di endpoint hello e utilizzare hello **chiave primaria**, o **chiave SECONDARIA** dal Pannello di chiavi hello come valore di hello di hello impostazione authKey.</span><span class="sxs-lookup"><span data-stu-id="68be7-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="68be7-248">Che farà associando repository Azure Cosmos DB hello, ora si aggiungere la logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="68be7-249">Hello in primo luogo è necessario toodo in grado di toobe con un'applicazione elenco da fare è elementi incompleto di toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="68be7-250">Copiare e incollare hello seguente frammento di codice in un punto qualsiasi all'interno di hello **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="68be7-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="68be7-251">Aprire hello **ItemController** è aggiunto in precedenza e aggiungere il seguente hello *utilizzando istruzioni* sopra dichiarazione dello spazio dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="68be7-252">Se il progetto non è denominato "todo", è necessario tooupdate utilizzando "l'attività. Modelli". nome di hello tooreflect del progetto.</span><span class="sxs-lookup"><span data-stu-id="68be7-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="68be7-253">A questo punto sostituire il codice</span><span class="sxs-lookup"><span data-stu-id="68be7-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="68be7-254">con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="68be7-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="68be7-255">Aprire **Global.asax.cs** e aggiungere hello seguente riga toohello **Application_Start** (metodo)</span><span class="sxs-lookup"><span data-stu-id="68be7-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="68be7-256">A questo punto la soluzione deve essere in grado di toobuild senza errori.</span><span class="sxs-lookup"><span data-stu-id="68be7-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="68be7-257">Se si esegue ora l'applicazione hello, si passa toohello **HomeController** hello e **indice** visualizzazione di tale controller.</span><span class="sxs-lookup"><span data-stu-id="68be7-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="68be7-258">Questo è il comportamento predefinito hello per il progetto di modello MVC hello che è stato scelto all'avvio di hello ma non vogliamo che!</span><span class="sxs-lookup"><span data-stu-id="68be7-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="68be7-259">È necessario modificare hello routing su questo tooalter applicazione MVC questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="68be7-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="68be7-260">Aprire ***App\_Start\RouteConfig.cs*** e individuare una riga hello inizia con "valori predefiniti:" e modificarlo hello tooresemble seguente.</span><span class="sxs-lookup"><span data-stu-id="68be7-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="68be7-261">A questo punto indica ASP.NET MVC che se non è stato specificato un valore in hello URL toocontrol hello comportamento di routing che invece di **Home**, utilizzare **elemento** come controller di hello e utente **indice** come visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="68be7-262">Ora se si esegue un'applicazione hello, chiama nel **ItemController** che chiamare nella classe repository toohello e utilizzare hello GetItems metodo tooreturn tutti hello elementi incompleti toohello **viste** \\ **Elemento**\\**indice** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="68be7-263">Se compilato ed eseguito ora, il progetto avrà un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="68be7-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Cattura di schermata dell'applicazione web elenco attività hello creata da questa esercitazione database](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="68be7-265"><a name="_Toc395637771"></a>Aggiungere elementi</span><span class="sxs-lookup"><span data-stu-id="68be7-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="68be7-266">Consente di inserire si alcuni elementi al database in modo che abbiamo più di un toolook di griglia vuota in.</span><span class="sxs-lookup"><span data-stu-id="68be7-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="68be7-267">Aggiungere codice troppo Azure Cosmos DBRepository ItemController toopersist hello record nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="68be7-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="68be7-268">Aggiungere hello seguente metodo tooyour **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="68be7-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="68be7-269">È sufficiente, questo metodo accetta un oggetto passato tooit e rende persistente nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="68be7-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="68be7-270">Aprire il file ItemController.cs hello e aggiungere hello seguente frammento di codice all'interno di classe hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="68be7-271">Si tratta come ASP.NET MVC sa quale toodo per hello **crea** azione.</span><span class="sxs-lookup"><span data-stu-id="68be7-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="68be7-272">In questo caso il rendering solo hello associati Create.cshtml vista creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="68be7-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="68be7-273">È ora necessario codice in questo controller che accetterà invio hello da hello **crea** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="68be7-274">Aggiungere hello successivo blocco di codice toohello classe ItemController.cs che indica quali toodo con un POST di form per questo controller di ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="68be7-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="68be7-275">Questo codice chiama in toohello DocumentDBRepository e utilizza hello CreateItemAsync metodo toopersist hello nuovo todo toohello database degli elementi.</span><span class="sxs-lookup"><span data-stu-id="68be7-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="68be7-276">**Nota sulla sicurezza**: hello **ValidateAntiForgeryToken** attributo viene utilizzato qui toohelp proteggere l'applicazione contro attacchi di cross-site request forgery.</span><span class="sxs-lookup"><span data-stu-id="68be7-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="68be7-277">È più tooit rispetto all'aggiunta solo di questo attributo, le visualizzazioni necessario toowork con questo token antifalsificazione anche.</span><span class="sxs-lookup"><span data-stu-id="68be7-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="68be7-278">Per ulteriori informazioni sul soggetto hello ed esempi di come tooimplement questo correttamente, vedere [impedendo Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="68be7-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="68be7-279">nel codice sorgente Hello [GitHub] [ GitHub] dispone di implementazione completa di hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="68be7-280">**Nota sulla sicurezza**: Utilizziamo inoltre hello **associare** attributo toohelp parametro di metodo hello proteggersi da attacchi di registrazione eccessiva.</span><span class="sxs-lookup"><span data-stu-id="68be7-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="68be7-281">Per altre informazioni dettagliate, vedere [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] (Operazioni CRUD di base in MVC ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="68be7-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="68be7-282">Questa operazione conclude hello codice necessario tooadd nuovi elementi tooour database.</span><span class="sxs-lookup"><span data-stu-id="68be7-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="68be7-283"><a name="_Toc395637772"></a>Modificare elementi</span><span class="sxs-lookup"><span data-stu-id="68be7-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="68be7-284">C'è una cosa ultimo per noi toodo, ovvero tooadd hello possibilità tooedit **elementi** nel database di hello e toomark come completato.</span><span class="sxs-lookup"><span data-stu-id="68be7-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="68be7-285">Hello visualizzazione per la modifica è già stato aggiunto il progetto toohello, pertanto è sufficiente tooadd alcune code tooour controller e toohello **DocumentDBRepository** classe nuovamente.</span><span class="sxs-lookup"><span data-stu-id="68be7-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="68be7-286">Aggiungere hello seguente toohello **DocumentDBRepository** classe.</span><span class="sxs-lookup"><span data-stu-id="68be7-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="68be7-287">primo di questi metodi, Hello **GetItem** recupera un elemento dal database di Azure Cosmos passato toohello back- **ItemController** e quindi su toohello **modifica** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="68be7-288">Hello secondo dei metodi di hello è stato appena aggiunto sostituisce hello **documento** nel database di Azure Cosmos con versione di hello di hello **documento** passati da hello **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="68be7-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="68be7-289">Aggiungere hello seguente toohello **ItemController** classe.</span><span class="sxs-lookup"><span data-stu-id="68be7-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="68be7-290">Hello primo metodo gestisca hello Http GET che si verifica quando si fa clic sull'utente hello nella hello **modifica** collegamento da hello **indice** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="68be7-291">Questo metodo recupera una [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) dal database di Azure Cosmos e lo passa a toohello **modifica** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="68be7-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="68be7-292">Hello **modifica** vista eseguirà quindi toohello un Http POST **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="68be7-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="68be7-293">secondo metodo Hello abbiamo aggiunto handle passando hello aggiornato oggetto tooAzure DB Cosmos toobe persistenti nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="68be7-294">Questo è tutto, ovvero tutto il necessario toorun l'applicazione, elenco incompleto **elementi**, aggiungere nuovi **elementi**e modificare **elementi**.</span><span class="sxs-lookup"><span data-stu-id="68be7-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="68be7-295"><a name="_Toc395637773"></a>Passaggio 6: Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="68be7-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="68be7-296">nel computer locale, un'applicazione hello tootest hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="68be7-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="68be7-297">In un'applicazione hello toobuild Visual Studio in modalità di debug, premere F5.</span><span class="sxs-lookup"><span data-stu-id="68be7-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="68be7-298">Deve compilare un'applicazione hello e avviare un browser con una pagina di griglia vuota hello che abbiamo visto prima:</span><span class="sxs-lookup"><span data-stu-id="68be7-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Cattura di schermata dell'applicazione web elenco attività hello creata da questa esercitazione database](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="68be7-300">Fare clic su hello **Crea nuovo** collegamento e aggiungere i valori toohello **nome** e **descrizione** campi.</span><span class="sxs-lookup"><span data-stu-id="68be7-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="68be7-301">Lasciare hello **completato** casella di controllo è deselezionata in caso contrario hello nuovo **elemento** verranno aggiunti in uno stato completato e non verrà visualizzato nell'elenco iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Cattura di schermata della visualizzazione di creazione di hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="68be7-303">Fare clic su **crea** e si è reindirizzato toohello Indietro **indice** Vista e **elemento** viene visualizzato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Cattura di schermata della visualizzazione dell'indice hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="68be7-305">È gratuito tooadd alcune ulteriori **elementi** tooyour elenco di attività.</span><span class="sxs-lookup"><span data-stu-id="68be7-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="68be7-306">Fare clic su **modifica** tooan Avanti **elemento** in elenco hello e si provengono toohello **modifica** vista in cui è possibile aggiornare le proprietà dell'oggetto, tra cui hello  **Completamento** flag.</span><span class="sxs-lookup"><span data-stu-id="68be7-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="68be7-307">Se si contrassegna hello **completa** flag e fare clic su **salvare**, hello **elemento** viene rimosso dall'elenco di hello di attività non completate.</span><span class="sxs-lookup"><span data-stu-id="68be7-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Cattura di schermata della visualizzazione dell'indice con hello completato casella selezionata hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="68be7-309">Dopo aver verificato app hello, premere Ctrl + F5 toostop Debug applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="68be7-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="68be7-310">Si è pronti toodeploy!</span><span class="sxs-lookup"><span data-stu-id="68be7-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="68be7-311"><a name="_Toc395637774"></a>Passaggio 7: Distribuire tooAzure applicazione hello servizio App</span><span class="sxs-lookup"><span data-stu-id="68be7-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="68be7-312">Dopo aver creato un'applicazione hello completo funzioni correttamente con Azure Cosmos DB verrà toodeploy questo tooAzure app web del servizio App.</span><span class="sxs-lookup"><span data-stu-id="68be7-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="68be7-313">toopublish tutti questa applicazione è necessario toodo è destro del mouse sul progetto hello in **Esplora** e fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="68be7-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Cattura di schermata di hello opzione pubblica in Esplora soluzioni](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="68be7-315">In hello **pubblica** la finestra di dialogo, fare clic su **servizio App di Microsoft Azure**, quindi selezionare **Crea nuovo** toocreate un servizio App profilo oppure fare clic su **selezionare Esistente** toouse un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="68be7-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Finestra di dialogo Pubblica in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="68be7-317">Se si dispone di un profilo del Servizio app di Azure esistente, immettere il nome della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="68be7-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="68be7-318">Hello utilizzare **vista** filtrare toosort dal gruppo di risorse o tipo di risorsa, quindi selezionare il servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="68be7-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Finestra di dialogo del servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="68be7-320">Fare clic su un nuovo profilo di servizio App di Azure, toocreate **Crea nuovo** in hello **pubblica** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="68be7-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="68be7-321">In hello **Crea servizio App** finestra di dialogo, immettere il nome dell'App Web e sottoscrizione appropriata, gruppo di risorse e piano di servizio App, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="68be7-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Finestra di dialogo Crea servizio app in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="68be7-323">Dopo alcuni secondi, Visual Studio completerà la pubblicazione dell'applicazione Web e avvierà un browser in cui sarà possibile ammirare il proprio lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="68be7-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="68be7-324"><a name="_Toc395637775"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68be7-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="68be7-325">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="68be7-325">Congratulations!</span></span> <span data-ttu-id="68be7-326">Appena compilato ASP.NET MVC prima dell'applicazione web tramite Azure Cosmos DB e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="68be7-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="68be7-327">codice sorgente per l'applicazione hello completa, inclusi i dettagli di hello Hello ed eliminare funzionalità non incluse in questa esercitazione può essere scaricato o clonato [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="68be7-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="68be7-328">Pertanto se si desidera aggiungere app tooyour, selezionare codice hello e aggiungerlo toothis app.</span><span class="sxs-lookup"><span data-stu-id="68be7-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="68be7-329">applicazione tooyour tooadd funzionalità aggiuntive revisione hello API disponibili in hello [libreria .NET di Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) e si ritiene che libera toocontribute toohello libreria .NET di Azure Cosmos DB su [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="68be7-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
