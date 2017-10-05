---
title: Creare un processo Web .NET nel servizio app di Azure | Microsoft Docs
description: "Informazioni sulla creazione di un app a più livelli con ASP.NET MVC e Azure. Il front-end viene eseguito in un'app Web nel servizio app di Azure e il back-end viene eseguito come processo Web. L'app usa Entity Framework, il database SQL e i BLOB e le code di archiviazione di Azure."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="73efb-105">Creare un processo Web .NET nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="73efb-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="73efb-106">Questa esercitazione illustra come scrivere codice per una semplice applicazione ASP.NET MVC 5 multilivello che usa [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="73efb-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="73efb-107">Lo scopo di [WebJobs SDK](websites-webjobs-resources.md) è semplificare il codice scritto per le attività comuni che possono essere eseguite da un processo Web, ad esempio l'elaborazione di immagini, l'elaborazione della coda, l'aggregazione RSS, la manutenzione di file e l'invio di messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="73efb-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="73efb-108">WebJobs SDK offre funzionalità incorporate per l'uso dell'Archiviazione di Azure e del bus di servizio, per la pianificazione di attività, per la gestione degli errori e per molti altri scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="73efb-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="73efb-109">È progettato per l'estensibilità e ha a disposizione un [repository open source di estensioni](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="73efb-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="73efb-110">Questa applicazione di esempio è un BBS pubblicitario.</span><span class="sxs-lookup"><span data-stu-id="73efb-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="73efb-111">Gli utenti possono caricare immagini per le inserzioni e un processo back-end converte le immagini in anteprime.</span><span class="sxs-lookup"><span data-stu-id="73efb-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="73efb-112">La pagina di elenco di inserzioni illustra le anteprime e la pagina di dettagli delle inserzioni mostra l'immagine con le dimensioni originali.</span><span class="sxs-lookup"><span data-stu-id="73efb-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="73efb-113">Di seguito è riportata una schermata:</span><span class="sxs-lookup"><span data-stu-id="73efb-113">Here's a screenshot:</span></span>

![Elenco di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="73efb-115">Questa applicazione di esempio funziona con le [code di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) e con i [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="73efb-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="73efb-116">L'esercitazione illustra come distribuire l'applicazione nel [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e nel [database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="73efb-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="73efb-117"><a id="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="73efb-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="73efb-118">L'esercitazione presuppone che si sappia usare progetti [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73efb-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="73efb-119">L'esercitazione in origine è stata scritta per Visual Studio 2013, ma può essere usata con versioni successive di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73efb-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="73efb-120">Se si usa Visual Studio 2015 o 2017, tenere presente che, prima di eseguire localmente l'applicazione, sarà necessario cambiare la parte `Data Source` della stringa di connessione LocalDB di SQL Server nei file Web.config e App.config da `Data Source=(localdb)\v11.0` a `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="73efb-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="73efb-121"><a name="note"></a>Per completare l'esercitazione, è necessario un account Azure:</span><span class="sxs-lookup"><span data-stu-id="73efb-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="73efb-122">È possibile [aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): si riceveranno crediti da usare per provare i servizi di Azure a pagamento e, anche dopo avere esaurito i crediti, è possibile mantenere l'account per usare i servizi di Azure gratuiti, ad esempio Siti Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="73efb-123">La carta di credito non verrà mai addebitata, a meno l'utente non modifichi le impostazioni e che richieda esplicitamente di essere addebitato.</span><span class="sxs-lookup"><span data-stu-id="73efb-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="73efb-124">I [sottoscrittori di Visual Studio possono attivare il credito Azure mensile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): con la sottoscrizione ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="73efb-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="73efb-125">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="73efb-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="73efb-126">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="73efb-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="73efb-127"><a id="learn"></a>Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="73efb-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="73efb-128">L'esercitazione mostra come eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="73efb-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="73efb-129">Abilitare il computer per lo sviluppo in Azure installando Azure SDK (solo per utenti di Visual Studio 2013 e 2015).</span><span class="sxs-lookup"><span data-stu-id="73efb-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="73efb-130">Creare un progetto di applicazione console che esegue automaticamente l'implementazione come processo Web di Azure quando si implementa il progetto Web associato.</span><span class="sxs-lookup"><span data-stu-id="73efb-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="73efb-131">Testare un back-end di WebJobs SDK localmente sul computer di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="73efb-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="73efb-132">Pubblicare un'applicazione con un back-end di processi Web in un'app Web nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="73efb-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="73efb-133">Caricare file e archiviarli nel servizio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="73efb-134">Usare Azure WebJobs SDK per lavorare con code e BLOB di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="73efb-135"><a id="contosoads"></a>Architettura dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="73efb-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="73efb-136">L'applicazione di esempio usa il [modello di lavoro incentrato sulle code](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) per delegare a un processo back-end il lavoro di creazione delle anteprime, che comporta un utilizzo elevato della CPU.</span><span class="sxs-lookup"><span data-stu-id="73efb-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="73efb-137">L'app archivia inserzioni pubblicitarie in un database SQL usando Code First di Entity Framework per creare le tabelle e accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="73efb-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="73efb-138">Il database archivia due URL per ogni inserzione, uno per l'immagine con dimensioni normali e uno per l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="73efb-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Tabella di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="73efb-140">Quando un utente carica un'immagine, l'app Web archivia l'immagine in un [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), quindi archivia le informazioni sulle inserzioni nel database con un URL che fa riferimento al BLOB</span><span class="sxs-lookup"><span data-stu-id="73efb-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="73efb-141">e, al tempo stesso, scrive un messaggio in una coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="73efb-142">In un processo back-end in esecuzione come processo Web di Azure, WebJobs SDK esegue il polling della coda alla ricerca di nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="73efb-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="73efb-143">Quando compare un nuovo messaggio, il processo Web crea un'anteprima per quell'immagine e aggiorna il campo di database relativo all'URL dell'anteprima per quell'inserzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="73efb-144">Il diagramma seguente mostra l'interazione tra le parti dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="73efb-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Architettura di Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="73efb-146">Le istruzioni dell'esercitazione si applicano ad Azure SDK per .NET 2.7.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="73efb-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="73efb-147"><a id="storage"></a>Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="73efb-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="73efb-148">Un account di archiviazione di Azure offre risorse per l'archiviazione di dati di code e BLOB nel cloud.</span><span class="sxs-lookup"><span data-stu-id="73efb-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="73efb-149">Viene anche usato da WebJobs SDK per archiviare i dati di registrazione per il dashboard.</span><span class="sxs-lookup"><span data-stu-id="73efb-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="73efb-150">In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="73efb-151">In questa esercitazione sarà usato un solo account.</span><span class="sxs-lookup"><span data-stu-id="73efb-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="73efb-152">Aprire la finestra **Esplora server** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73efb-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="73efb-153">Fare clic con il pulsante destro del mouse sul nodo **Azure** e quindi scegliere **Connessione alla sottoscrizione di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="73efb-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Connect to Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="73efb-155">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="73efb-156">Fare clic con il pulsante destro del mouse su **Archiviazione** sotto il nodo Azure e quindi scegliere **Crea account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="73efb-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Crea account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="73efb-158">Nella finestra di dialogo **Crea account di archiviazione** immettere un nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="73efb-159">Il nome deve essere univoco. Nessun altro account di archiviazione di Azure può avere lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="73efb-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="73efb-160">Se il nome immesso è già in uso, sarà possibile cambiarlo.</span><span class="sxs-lookup"><span data-stu-id="73efb-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="73efb-161">L'URL per accedere all'account di archiviazione sarà *{nome}*.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="73efb-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="73efb-162">Nell'elenco a discesa **Regione o gruppo di affinità** impostare l'area geografica più vicina.</span><span class="sxs-lookup"><span data-stu-id="73efb-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="73efb-163">Questa impostazione specifica il data center di Azure che ospiterà l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="73efb-164">Per questa esercitazione è possibile selezionare qualsiasi area senza riscontrare differenze evidenti.</span><span class="sxs-lookup"><span data-stu-id="73efb-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="73efb-165">Tuttavia, per un'app Web di produzione è consigliabile che il server Web e l'account di archiviazione siano nella stessa area geografica per poter ridurre al minimo la latenza e il costo per l'uscita dei dati.</span><span class="sxs-lookup"><span data-stu-id="73efb-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="73efb-166">Il data center dell'app Web (che si creerà più avanti) deve essere eseguito il più vicino possibile ai browser che accedono all'app Web per poter da ridurre al minimo la latenza.</span><span class="sxs-lookup"><span data-stu-id="73efb-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="73efb-167">Nell'elenco a discesa **Replica** scegliere **Localmente ridondante**.</span><span class="sxs-lookup"><span data-stu-id="73efb-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="73efb-168">Quando per un account di archiviazione è abilitata la replica geografica, il contenuto archiviato è replicato in un data center secondario per permettere il failover in tale posizione in caso di errore grave nella posizione primaria.</span><span class="sxs-lookup"><span data-stu-id="73efb-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="73efb-169">La replica geografica può comportare costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="73efb-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="73efb-170">Per gli account di test e di sviluppo si preferisce in genere non pagare per la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="73efb-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="73efb-171">Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="73efb-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="73efb-172">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="73efb-172">Click **Create**.</span></span>

    ![Nuovo account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="73efb-174"><a id="download"></a>Scaricare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="73efb-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="73efb-175">Scaricare e decomprimere la [soluzione completata](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="73efb-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="73efb-176">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73efb-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="73efb-177">Nel menu **File** scegliere **Apri > Progetto/Soluzione**, passare alla cartella in cui è stata scaricata la soluzione, quindi aprire il file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="73efb-178">Premere CTRL+MAIUSC+B per compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="73efb-179">Per impostazione predefinita, Visual Studio ripristina automaticamente il contenuto del pacchetto NuGet, che non era incluso nel file con estensione *zip* .</span><span class="sxs-lookup"><span data-stu-id="73efb-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="73efb-180">In caso di mancato ripristino dei pacchetti, installarli manualmente passando alla finestra di dialogo **Gestisci pacchetti NuGet per la soluzione**, quindi facendo clic sul pulsante **Ripristina** in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="73efb-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="73efb-181">In **Esplora soluzioni** verificare che come progetto di avvio sia selezionato **ContosoAdsWeb**.</span><span class="sxs-lookup"><span data-stu-id="73efb-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="73efb-182"><a id="configurestorage"></a>Configurare l'applicazione per l'uso dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="73efb-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="73efb-183">Aprire il file *Web.config* dell'applicazione nel progetto ContosoAdsWeb.</span><span class="sxs-lookup"><span data-stu-id="73efb-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="73efb-184">Il file contiene una stringa di connessione di SQL e una stringa di connessione di archiviazione di Azure per usare i BLOB e le code.</span><span class="sxs-lookup"><span data-stu-id="73efb-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="73efb-185">La stringa di connessione di SQL punta a un database [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) .</span><span class="sxs-lookup"><span data-stu-id="73efb-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="73efb-186">La stringa di connessione di archiviazione è un esempio contenente i segnaposto per il nome dell'account di archiviazione e la chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="73efb-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="73efb-187">La si sostituirà con una stringa di connessione contenente il nome e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="73efb-188">La stringa di connessione di archiviazione si chiama AzureWebJobsStorage perché questo è il nome usato da WebJobs SDK per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="73efb-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="73efb-189">Poiché qui viene usato lo stesso nome, è necessario impostare solo un valore della stringa di connessione nell'ambiente di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="73efb-190">In **Esplora server** fare clic con il pulsante destro del mouse sull'account di archiviazione sotto il nodo **Archiviazione** e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="73efb-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Fare clic su proprietà Account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="73efb-192">Nella finestra **Proprietà** fare clic su **Chiavi account di archiviazione** e quindi sui puntini di sospensione.</span><span class="sxs-lookup"><span data-stu-id="73efb-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Chiavi dell'account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="73efb-194">Copiare la **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="73efb-194">Copy the **Connection String**.</span></span>

    ![Get the storage account keys](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="73efb-196">Sostituire la stringa di connessione di archiviazione nel file *Web.config* con la stringa di connessione appena copiata.</span><span class="sxs-lookup"><span data-stu-id="73efb-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="73efb-197">Assicurarsi di selezionare tutti gli elementi nelle virgolette, ma di non includere le virgolette prima di incollare.</span><span class="sxs-lookup"><span data-stu-id="73efb-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="73efb-198">Aprire il file *App.config* nel progetto ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="73efb-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="73efb-199">Questo file ha due stringhe di connessione di archiviazione, una per i dati dell'applicazione e l'altra per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="73efb-200">È possibile usare account di archiviazione separati per i dati applicazione e la registrazione oppure usare [più account di archiviazione per i dati](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="73efb-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="73efb-201">In questa esercitazione viene usato un singolo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="73efb-202">Le stringhe di connessione sono segnaposto per le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-202">The connection strings have placeholders for the storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="73efb-203">Per impostazione predefinita, WebJobs SDK cerca le stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="73efb-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="73efb-204">Come alternativa, è possibile [archiviare la stringa di connessione come si preferisce e passarla in modo esplicito all'`JobHost`oggetto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="73efb-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="73efb-205">Sostituire entrambe le stringhe di connessione di archiviazione con la stringa di connessione copiata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="73efb-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="73efb-206">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="73efb-206">Save your changes.</span></span>

## <span data-ttu-id="73efb-207"><a id="run"></a>Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="73efb-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="73efb-208">Per avviare il front-end Web dell'applicazione, premere CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="73efb-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="73efb-209">Nel browser predefinito verrà aperta la home page.</span><span class="sxs-lookup"><span data-stu-id="73efb-209">The default browser opens to the home page.</span></span> <span data-ttu-id="73efb-210">Viene eseguito il progetto Web perché è stato impostato come progetto di avvio.</span><span class="sxs-lookup"><span data-stu-id="73efb-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="73efb-212">Per avviare il back-end processo Web dell'applicazione, fare clic con il pulsante destro del mouse sul progetto ContosoAdsWebJob in **Esplora soluzioni** e scegliere **Debug**  > **Avvia nuova istanza**.</span><span class="sxs-lookup"><span data-stu-id="73efb-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="73efb-213">Si apre una finestra dell'applicazione console in cui sono visualizzati messaggi di registrazione indicanti che l'esecuzione dell'oggetto JobHost di WebJobs SDK è iniziata.</span><span class="sxs-lookup"><span data-stu-id="73efb-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Console application window showing that the backend is running](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="73efb-215">Nel browser fare clic su **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="73efb-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="73efb-216">Immettere alcuni dati di test, selezionare un'immagine da caricare e quindi fare clic su **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="73efb-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Pagina di creazione](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="73efb-218">L'app passa alla pagina di indice, ma non mostra alcuna anteprima per la nuova inserzione, poiché l'elaborazione non è stata ancora eseguita.</span><span class="sxs-lookup"><span data-stu-id="73efb-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="73efb-219">Intanto, dopo una breve attesa un messaggio di registrazione nella finestra dell'applicazione console mostra che una coda di messaggi è stata ricevuta ed elaborata.</span><span class="sxs-lookup"><span data-stu-id="73efb-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="73efb-221">Dopo aver letto i messaggi di registrazione nella finestra dell'applicazione console, aggiornare la pagina di indice per visualizzare le anteprime.</span><span class="sxs-lookup"><span data-stu-id="73efb-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Pagina di indice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="73efb-223">Fare clic su **Details** per visualizzare l'immagine con dimensioni normali per l'inserzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Pagina dei dettagli](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="73efb-225">L'applicazione è stata eseguita sul computer locale e usa un database di SQL Server sul computer, ma lavora con le code e i BLOB nel cloud.</span><span class="sxs-lookup"><span data-stu-id="73efb-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="73efb-226">Nella sezione seguente si eseguirà l'applicazione nel cloud, usando un database cloud e BLOB e code cloud.</span><span class="sxs-lookup"><span data-stu-id="73efb-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="73efb-227"><a id="runincloud"></a>Eseguire l'applicazione nel cloud</span><span class="sxs-lookup"><span data-stu-id="73efb-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="73efb-228">Per eseguire l'applicazione nel cloud, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="73efb-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="73efb-229">Distribuire su App Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-229">Deploy to Web Apps.</span></span> <span data-ttu-id="73efb-230">Visual Studio creerà automaticamente una nuova app Web in servizio app e un'istanza di database SQL.</span><span class="sxs-lookup"><span data-stu-id="73efb-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="73efb-231">Configurare l'app Web per l'uso del database SQL e dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="73efb-232">Dopo aver creato alcuni annunci durante l'esecuzione nel cloud, verrà visualizzato il dashboard di WebJobs SDK con le funzionalità di monitoraggio complete disponibili.</span><span class="sxs-lookup"><span data-stu-id="73efb-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="73efb-233">Distribuire in App Web</span><span class="sxs-lookup"><span data-stu-id="73efb-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="73efb-234">Chiudere il browser e la finestra dell'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="73efb-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="73efb-235">Seguire i passaggi nella sezione [Pubblicare in Azure con il database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="73efb-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="73efb-236">Dopo avere completato i passaggi per la distribuzione, continuare con le attività rimanenti di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="73efb-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="73efb-237">Configurare l'app Web per l'uso del database SQL e dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="73efb-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="73efb-238">Come procedura consigliata per la sicurezza, [evitare di inserire informazioni sensibili, come le stringhe di connessione, in file archiviati nei repository di codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="73efb-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="73efb-239">è possibile impostare i valori delle stringhe di connessione e di altre impostazioni nell'ambiente di Azure. Le API di configurazione di ASP.NET rilevano automaticamente questi valori quando l'app viene eseguita in Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="73efb-240">È possibile impostare questi valori in Azure con **Esplora server**, il portale di Azure, Windows PowerShell o l'interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="73efb-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="73efb-241">Per altre informazioni, vedere il blog sul [funzionamento delle stringhe di applicazione e di connessione](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="73efb-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="73efb-242">In questa sezione si userà **Esplora server** per impostare i valori delle stringhe di connessione in Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="73efb-243">In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web in **Azure > Servizio app > {gruppo di risorse}**, quindi scegliere **Visualizza impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="73efb-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="73efb-244">La finestra **App Web di Azure** si apre nella scheda **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="73efb-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="73efb-245">Sostituire il nome della stringa di connessione DefaultConnection con il nome scelto quando si è configurato il database SQL nell'articolo [Pubblicare in Azure con il database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="73efb-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="73efb-246">Poiché Azure ha creato automaticamente questa stringa di connessione quando si è creata l'app Web con un database associato, il valore della stringa di connessione è già quello corretto.</span><span class="sxs-lookup"><span data-stu-id="73efb-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="73efb-247">Si sta solo sostituendo il nome con quello cercato dal codice.</span><span class="sxs-lookup"><span data-stu-id="73efb-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="73efb-248">Aggiungere due nuove stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="73efb-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="73efb-249">Impostare il tipo di database su **Personalizzato** e il valore della stringa di connessione sullo stesso valore usato prima per i file *Web.config* e *App.config*.</span><span class="sxs-lookup"><span data-stu-id="73efb-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="73efb-250">Assicurarsi di includere l'intera stringa di connessione, non solo la chiave di accesso, e non includere le virgolette.</span><span class="sxs-lookup"><span data-stu-id="73efb-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="73efb-251">Queste stringhe di connessione vengono usate da WebJobs SDK, una per i dati dell'applicazione e l'altra per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="73efb-252">Come illustrato in precedenza, quella per i dati dell'applicazione viene usata anche dal codice front-end Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="73efb-253">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="73efb-253">Click **Save**.</span></span>

    ![Stringhe di connessione nel portale di Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="73efb-255">In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web, quindi scegliere **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="73efb-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="73efb-256">Dopo che l'app Web viene arrestata, fare nuovamente clic con il pulsante destro del mouse sull'app Web e scegliere **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="73efb-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="73efb-257">Il processo Web viene avviato automaticamente al momento della pubblicazione, ma si arresta quando si apporta una modifica alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="73efb-258">Per riavviarlo, è possibile riavviare l'app Web o riavviare il processo Web nel [portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="73efb-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="73efb-259">In genere è consigliabile riavviare l'app Web dopo una modifica alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="73efb-260">Aggiornare la finestra del browser con l'URL dell'app Web nella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="73efb-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="73efb-261">Viene visualizzata la home page.</span><span class="sxs-lookup"><span data-stu-id="73efb-261">The home page appears.</span></span>
8. <span data-ttu-id="73efb-262">Creare un annuncio, come quando [l'applicazione è stata eseguita in locale](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="73efb-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="73efb-263">La pagina di indice inizialmente viene visualizzata senza alcuna anteprima.</span><span class="sxs-lookup"><span data-stu-id="73efb-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="73efb-264">Aggiornare la pagina dopo alcuni secondi e l'anteprima verrà visualizzata.</span><span class="sxs-lookup"><span data-stu-id="73efb-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="73efb-265">Se l'anteprima non viene visualizzata, potrebbe essere necessario attendere circa un minuto per il completamento del riavvio del processo Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="73efb-266">Se dopo alcuni minuti l'anteprima non viene visualizzata quando si aggiorna la pagina, il processo Web potrebbe non essere stato avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="73efb-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="73efb-267">In tal caso, andare al pannello **Servizi app** nel [portale di Azure](https://portal.azure.com/), individuare l'app Web e quindi fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="73efb-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="73efb-268">Visualizzare il dashboard di WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="73efb-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="73efb-269">Nel [portale di Azure](https://portal.azure.com/) selezionare il pannello **Servizi app**, individuare l'app Web e selezionare **Processi Web**.</span><span class="sxs-lookup"><span data-stu-id="73efb-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="73efb-270">Selezionare la scheda **Log**.</span><span class="sxs-lookup"><span data-stu-id="73efb-270">Select the **Logs** tab.</span></span>

    ![Scheda Log](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="73efb-272">Una nuova scheda del browser si apre nel dashboard di WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="73efb-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="73efb-273">Il dashboard mostra che il processo Web è in esecuzione e mostra un elenco di funzioni nel codice, attivate da WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="73efb-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="73efb-274">Fare clic su una delle funzioni per visualizzare i dettagli sull'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-274">Click one of the functions to see details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="73efb-277">Facendo clic sul pulsante **Riproduci funzione** di questa pagina, il framework WebJobs SDK chiama nuovamente la funzione ed è possibile modificare i dati passati prima alla funzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="73efb-278">Al termine del test, considerare la possibilità di eliminare l'app Web, l'account di archiviazione e l'istanza di database SQL.</span><span class="sxs-lookup"><span data-stu-id="73efb-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="73efb-279">L'app Web è gratuita, ma l'account di archiviazione e l'istanza di database SQL causano un incremento delle spese (anche se minime date le dimensioni ridotte).</span><span class="sxs-lookup"><span data-stu-id="73efb-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="73efb-280">In più, se si lascia l'app Web in esecuzione, chiunque individui l'URL potrà creare e visualizzare inserzioni.</span><span class="sxs-lookup"><span data-stu-id="73efb-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="73efb-281">Eliminare l'app Web</span><span class="sxs-lookup"><span data-stu-id="73efb-281">Delete your web app</span></span>
<span data-ttu-id="73efb-282">Nel portale andare al pannello **Servizi app**, individuare e selezionare l'app Web e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="73efb-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="73efb-283">Se si vuole semplicemente impedire ad altri utenti di accedere all'app Web, fare invece clic su **Arresta** .</span><span class="sxs-lookup"><span data-stu-id="73efb-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="73efb-284">In questo caso, continueranno a essere generati addebiti per il database SQL e l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="73efb-285">Eliminare l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="73efb-285">Delete your storage account</span></span>
<span data-ttu-id="73efb-286">Per eliminare l'account di archiviazione, vedere [Eliminare un account di archiviazione](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="73efb-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="73efb-287">Eliminare il database</span><span class="sxs-lookup"><span data-stu-id="73efb-287">Delete your database</span></span>
<span data-ttu-id="73efb-288">Per eliminare il database SQL, vedere la documentazione [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) (API REST di database SQL di Azure).</span><span class="sxs-lookup"><span data-stu-id="73efb-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="73efb-289"><a id="create"></a>Creare un'applicazione completamente nuova</span><span class="sxs-lookup"><span data-stu-id="73efb-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="73efb-290">In questa sezione verranno eseguite le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="73efb-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="73efb-291">Creare una soluzione Visual Studio con un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="73efb-292">Aggiungere un progetto libreria di classi per il livello di accesso ai dati condiviso tra il front-end e il back-end.</span><span class="sxs-lookup"><span data-stu-id="73efb-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="73efb-293">Aggiungere un progetto applicazione console per il back-end, con la distribuzione dei processi Web abilitata.</span><span class="sxs-lookup"><span data-stu-id="73efb-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="73efb-294">Aggiungere i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="73efb-294">Add NuGet packages.</span></span>
* <span data-ttu-id="73efb-295">Impostare i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="73efb-295">Set project references.</span></span>
* <span data-ttu-id="73efb-296">Copiare il codice dell'applicazione e i file di configurazione dall'applicazione scaricata con cui si è lavorato nella sezione precedente dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="73efb-297">Esaminare le parti del codice che usano i BLOB e le code di Azure e WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="73efb-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="73efb-298">Creare una soluzione Visual Studio con un progetto Web e un progetto libreria di classi</span><span class="sxs-lookup"><span data-stu-id="73efb-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="73efb-299">In Visual Studio scegliere **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="73efb-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="73efb-300">Nella finestra di dialogo **Nuovo progetto** scegliere **Visual C#** > **Web** > **Applicazione Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="73efb-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="73efb-301">Assegnare al progetto il nome ContosoAdsWeb e alla soluzione il nome ContosoAdsWebJobsSDK (cambiare il nome della soluzione se la si inserirà nella stessa cartella della soluzione scaricata) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Nuovo progetto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="73efb-303">Nella finestra di dialogo **Nuova applicazione Web ASP.NET** scegliere il modello MVC e selezionare **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="73efb-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Modifica autenticazione](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="73efb-305">Nella finestra di dialogo **Modifica autenticazione** fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="73efb-307">Nella finestra di dialogo **Nuova applicazione Web ASP.NET** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="73efb-308">Visual Studio crea la soluzione e il progetto Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="73efb-309">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, non sul progetto, quindi scegliere **Aggiungi** > **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="73efb-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="73efb-310">Nella finestra di dialogo **Aggiungi nuovo progetto**, scegliere **Visual C#** > **Desktop classico di Windows** >  modello **Libreria di classi (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="73efb-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="73efb-311">Assegnare il nome *ContosoAdsCommon*al progetto, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="73efb-312">Questo progetto conterrà il contesto Entity Framework e il modello di dati che verranno usati sia dal front-end che dal back-end.</span><span class="sxs-lookup"><span data-stu-id="73efb-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="73efb-313">In alternativa, è possibile definire le classi correlate a Entity Framework nel progetto Web e fare riferimento a tale progetto dal progetto processo Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="73efb-314">In tale caso, tuttavia, il progetto processo Web includerebbe un riferimento ad assembly Web non necessari.</span><span class="sxs-lookup"><span data-stu-id="73efb-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="73efb-315">Aggiungere un progetto applicazione console con la distribuzione dei processi Web abilitata.</span><span class="sxs-lookup"><span data-stu-id="73efb-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="73efb-316">Fare clic con il pulsante destro del mouse sul progetto Web (non sulla soluzione o sul progetto libreria di classi) e quindi scegliere **Aggiungi** > **Nuovo progetto processo Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="73efb-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="73efb-318">Nella finestra di dialogo **Aggiungi processo Web Azure** immettere ContosoAdsWebJob sia come **Nome progetto** che come **Nome processo Web**.</span><span class="sxs-lookup"><span data-stu-id="73efb-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="73efb-319">Lasciare **Modalità di esecuzione processo Web** impostato su **Esegui in modo continuo**.</span><span class="sxs-lookup"><span data-stu-id="73efb-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="73efb-320">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-320">Click **OK**.</span></span>

   <span data-ttu-id="73efb-321">Visual Studio crea un'applicazione console configurata per la distribuzione come processo Web quando si implementa il progetto Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="73efb-322">A tale scopo dopo la creazione del progetto ha eseguito le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="73efb-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="73efb-323">Aggiunta di un file *webjob-publish-settings.json* nella cartella delle proprietà del progetto processo Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="73efb-324">Aggiunta di un file *webjobs-list.json* nella cartella delle proprietà del progetto Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="73efb-325">Installazione del pacchetto NuGet Microsoft.Web.WebJobs.Publish nel progetto processo Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="73efb-326">Per altre informazioni su queste modifiche, vedere [Distribuzione di processi Web usando Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="73efb-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="73efb-327">Aggiungere i pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="73efb-327">Add NuGet packages</span></span>
<span data-ttu-id="73efb-328">Il modello nuovo-progetto per un progetto processo Web installa automaticamente il pacchetto NuGet per WebJobs SDK [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="73efb-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="73efb-329">Una delle dipendenze di WebJobs SDK installata automaticamente nel progetto processo Web è la libreria client di archiviazione di Azure (SCL, Storage Client Library).</span><span class="sxs-lookup"><span data-stu-id="73efb-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="73efb-330">Tuttavia, è necessario aggiungerla al progetto Web per usare i BLOB e le code.</span><span class="sxs-lookup"><span data-stu-id="73efb-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="73efb-331">Aprire la finestra di dialogo **Gestisci pacchetti NuGet** per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="73efb-332">Nel riquadro sinistro selezionare **Pacchetti installati**.</span><span class="sxs-lookup"><span data-stu-id="73efb-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="73efb-333">Trovare il pacchetto *Archiviazione di Azure* e quindi fare clic su **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="73efb-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="73efb-334">Nella finestra di dialogo **Seleziona progetti** selezionare la casella di controllo **ContosoAdsWeb** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="73efb-335">Tutti e tre i progetti usano Entity Framework per lavorare con i dati nel database SQL.</span><span class="sxs-lookup"><span data-stu-id="73efb-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="73efb-336">Nel riquadro sinistro selezionare **Online**.</span><span class="sxs-lookup"><span data-stu-id="73efb-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="73efb-337">Individuare il pacchetto NuGet *EntityFramework* e installarlo nei tre progetti.</span><span class="sxs-lookup"><span data-stu-id="73efb-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="73efb-338">Configurare le preferenze del progetto</span><span class="sxs-lookup"><span data-stu-id="73efb-338">Set project references</span></span>
<span data-ttu-id="73efb-339">Sia il progetto Web che il progetto processo Web useranno il database SQL, quindi hanno entrambi bisogno di un riferimento al progetto ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="73efb-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="73efb-340">Nel progetto ContosoAdsWeb configurare un riferimento al progetto ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="73efb-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="73efb-341">Fare clic con il pulsante destro del mouse sul progetto ContosoAdsWeb, quindi scegliere **Aggiungi** > **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="73efb-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="73efb-342">Nella finestra di dialogo **Gestione riferimenti** selezionare **Progetti** > **Soluzione** > **ContosoAdsCommon**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="73efb-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="73efb-343">Il progetto processo Web ha bisogno di riferimenti per usare le immagini e per accedere alle stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="73efb-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="73efb-344">Nel progetto ContosoAdsWebJob configurare un riferimento a `System.Drawing` e a `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="73efb-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="73efb-345">Aggiungere il codice e i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="73efb-345">Add code and configuration files</span></span>
<span data-ttu-id="73efb-346">Questa esercitazione non mostra come creare [controlli e visualizzazioni MVC usando lo scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), come [scrivere codice di Entity Framework da usare con database SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc) oppure le [nozioni di base della programmazione asincrona in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="73efb-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="73efb-347">Quindi resta solo da copiare il codice e i file di configurazione dalla soluzione scaricata alla nuova soluzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="73efb-348">Una volta eseguita l'operazione, vedere le sezioni seguenti che illustrano e spiegano parti chiave del codice.</span><span class="sxs-lookup"><span data-stu-id="73efb-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="73efb-349">Per aggiungere file a un progetto o a una cartella, fare clic con il pulsante destro del mouse sul progetto o sulla cartella, quindi scegliere **Aggiungi** > **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="73efb-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="73efb-350">Selezionare i file da aggiungere, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="73efb-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="73efb-351">Se viene richiesto di confermare che si vogliono sostituire i file esistenti, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="73efb-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="73efb-352">Nel progetto ContosoAdsCommon eliminare il file *Class1.cs* e sostituirlo con i file seguenti dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="73efb-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="73efb-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-353">*Ad.cs*</span></span>
   * <span data-ttu-id="73efb-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="73efb-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="73efb-356">Nel progetto ContosoAdsWeb aggiungere i file seguenti dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="73efb-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="73efb-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="73efb-357">*Web.config*</span></span>
   * <span data-ttu-id="73efb-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="73efb-359">Nella cartella *Controllers*: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="73efb-360">Nella cartella *Views\Shared*: il file *_Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="73efb-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="73efb-361">Nella cartella *Views\Home*: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="73efb-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="73efb-362">Nella cartella *Views\Ad* (creare prima di tutto la cartella): cinque file *.cshtml*</span><span class="sxs-lookup"><span data-stu-id="73efb-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="73efb-363">Nel progetto ContosoAdsWebJob aggiungere i file seguenti dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="73efb-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="73efb-364">*App.config* (impostare il filtro del tipo di file su **Tutti i file**)</span><span class="sxs-lookup"><span data-stu-id="73efb-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="73efb-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-365">*Program.cs*</span></span>
   * <span data-ttu-id="73efb-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="73efb-366">*Functions.cs*</span></span>

<span data-ttu-id="73efb-367">Ora è possibile compilare, eseguire e implementare l'applicazione come indicato in precedenza nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="73efb-368">Prima però arrestare il processo Web ancora in esecuzione nella prima app Web in cui è stata eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73efb-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="73efb-369">In caso contrario, il processo Web elaborerà i messaggi delle code creati localmente o dall'app in esecuzione in una nuova app Web, perché usano tutti lo stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="73efb-370"><a id="code"></a>Verificare il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="73efb-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="73efb-371">Le sezioni seguenti illustrano il codice correlato all'uso di WebJobs SDK e dei BLOB e delle code di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="73efb-372">Per il codice specifico di WebJobs SDK, passare alle sezioni [Program.cs e Functions.cs](#programcs) .</span><span class="sxs-lookup"><span data-stu-id="73efb-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="73efb-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="73efb-374">Il file Ad.cs definisce un'enumerazione per le categorie di inserzione e una classe di entità POCO per le informazioni sulle inserzioni.</span><span class="sxs-lookup"><span data-stu-id="73efb-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="73efb-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="73efb-376">La classe ContosoAdsContext specifica che la classe Ad è usata in una raccolta DbSet, che sarà archiviata da Entity Framework in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="73efb-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

<span data-ttu-id="73efb-377">La classe ha due costruttori.</span><span class="sxs-lookup"><span data-stu-id="73efb-377">The class has two constructors.</span></span> <span data-ttu-id="73efb-378">Il primo è usato dal progetto Web e specifica il nome di una stringa di connessione archiviata nel file Web.config o nell'ambiente di runtime di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="73efb-379">Il secondo costruttore permette di passare la stringa di connessione effettiva,</span><span class="sxs-lookup"><span data-stu-id="73efb-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="73efb-380">come richiesto dal progetto processo Web, poiché non dispone di un file Web.config.</span><span class="sxs-lookup"><span data-stu-id="73efb-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="73efb-381">In precedenza è stato indicato il percorso di archiviazione di questa stringa di connessione e più avanti sarà illustrato il modo in cui il codice recupera la stringa di connessione durante la creazione di istanze della classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="73efb-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="73efb-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="73efb-383">La classe `BlobInformation` viene usata per archiviare le informazioni su un BLOB di immagine in un messaggio di una coda.</span><span class="sxs-lookup"><span data-stu-id="73efb-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="73efb-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="73efb-385">Il codice chiamato dal metodo `Application_Start` crea un contenitore BLOB *images* e una coda *images*, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="73efb-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="73efb-386">In questo modo, ogni volta che si inizia a usare un nuovo account di archiviazione, il contenitore BLOB e la coda necessari saranno creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="73efb-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="73efb-387">Il codice ottiene l'accesso all'account di archiviazione tramite la stringa di connessione di archiviazione del file *Web.config* o dell'ambiente di runtime di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="73efb-388">Ottiene quindi un riferimento al contenitore BLOB *images*, crea il contenitore se non esiste già e configura le autorizzazioni di accesso nel nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="73efb-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="73efb-389">Per impostazione predefinita, i nuovi contenitori consentono l'accesso ai BLOB solo ai client con credenziali dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="73efb-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="73efb-390">Per l'app Web è necessario che i BLOB siano pubblici, in modo che sia possibile visualizzare immagini usando gli URL che fanno riferimento ai BLOB delle immagini.</span><span class="sxs-lookup"><span data-stu-id="73efb-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="73efb-391">Tramite codice analogo si ottiene un riferimento alla coda *thumbnailrequest* e si crea una nuova coda.</span><span class="sxs-lookup"><span data-stu-id="73efb-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="73efb-392">In questo caso non sono necessarie modifiche alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="73efb-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="73efb-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="73efb-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="73efb-394">Il file *_Layout.cshtml* imposta il nome dell'app nell'intestazione e nel piè di pagina e crea una voce di menu "Ads" (Annunci).</span><span class="sxs-lookup"><span data-stu-id="73efb-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="73efb-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="73efb-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="73efb-396">Il file *Views\Home\Index.cshtml* visualizza i collegamenti di categoria nella home page.</span><span class="sxs-lookup"><span data-stu-id="73efb-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="73efb-397">I collegamenti passano il valore Integer dell'enumerazione `Category` in una variabile querystring alla pagina Ads Index.</span><span class="sxs-lookup"><span data-stu-id="73efb-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="73efb-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="73efb-399">Nel file *AdController.cs* il costruttore chiama il metodo `InitializeStorage` per creare oggetti della libreria del client di Archiviazione di Azure che forniscono un'API per l'uso di BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="73efb-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="73efb-400">Il codice ottiene quindi un riferimento al contenitore BLOB *images*, come illustrato prima in *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="73efb-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="73efb-401">Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="73efb-402">Il criterio per l'esecuzione di nuovi tentativi predefinito per il backoff esponenziale potrebbe sospendere l'app Web per più di un minuto in caso di nuovi tentativi ripetuti per un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="73efb-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="73efb-403">Il criterio di ripetizione dei tentativi specificato qui attende tre secondi dopo ogni tentativo, fino a un massimo di tre tentativi.</span><span class="sxs-lookup"><span data-stu-id="73efb-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="73efb-404">Tramite codice analogo si ottiene un riferimento alla coda *images* .</span><span class="sxs-lookup"><span data-stu-id="73efb-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="73efb-405">La maggior parte del codice del controller è tipica per l'uso di un modello di dati Entity Framework con una classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="73efb-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="73efb-406">Un'eccezione è costituita dal metodo `Create` HttpPost che carica un file e lo salva nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="73efb-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="73efb-407">Lo strumento di associazione di modelli fornisce un oggetto [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) al metodo.</span><span class="sxs-lookup"><span data-stu-id="73efb-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="73efb-408">Se l'utente ha selezionato un file da caricare, il codice carica il file, lo salva in un BLOB e aggiorna il record del database Ad con un URL che fa riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="73efb-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="73efb-409">Il codice che esegue il caricamento si trova nel metodo `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="73efb-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="73efb-410">Crea un nome GUID per il BLOB, aggiorna e salva il file, quindi restituisce un riferimento al BLOB salvato.</span><span class="sxs-lookup"><span data-stu-id="73efb-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

<span data-ttu-id="73efb-411">Dopo avere caricato un BLOB e aggiornato il database, il metodo `Create` HttpPost crea un messaggio di coda per segnalare al processo back-end che un'immagine è pronta per la conversione in anteprima.</span><span class="sxs-lookup"><span data-stu-id="73efb-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="73efb-412">Il codice per il metodo `Edit` HttpPost è simile, ma, se l'utente seleziona un nuovo file immagine, eventuali BLOB già esistenti per questo annuncio dovranno essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="73efb-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="73efb-413">Di seguito è riportato il codice per l'eliminazione dei BLOB in caso di eliminazione di un'inserzione:</span><span class="sxs-lookup"><span data-stu-id="73efb-413">Here is the code that deletes blobs when you delete an ad:</span></span>

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="73efb-414">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="73efb-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="73efb-415">Il file *Index.cshtml* mostra le anteprime insieme agli altri dati delle inserzioni:</span><span class="sxs-lookup"><span data-stu-id="73efb-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="73efb-416">Il file *Details.cshtml* mostra l'immagine con dimensioni normali:</span><span class="sxs-lookup"><span data-stu-id="73efb-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="73efb-417">ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="73efb-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="73efb-418">I file *Create.cshtml* e *Edit.cshtml* specificano la codifica di moduli che permette al controller di ottenere l'oggetto `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="73efb-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="73efb-419">Un elemento `<input>` segnala al browser che è necessario fornire una finestra di selezione del file.</span><span class="sxs-lookup"><span data-stu-id="73efb-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="73efb-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="73efb-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="73efb-421">Quando viene avviato il processo Web, il metodo `Main` chiama il metodo di WebJobs SDK `JobHost.RunAndBlock` per iniziare l'esecuzione di funzioni attivate sul thread corrente.</span><span class="sxs-lookup"><span data-stu-id="73efb-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="73efb-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Metodo GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="73efb-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="73efb-423">WebJobs SDK chiama questo metodo quando viene ricevuto un messaggio di una coda.</span><span class="sxs-lookup"><span data-stu-id="73efb-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="73efb-424">Il metodo crea un'anteprima e inserisce l'URL dell'anteprima nel database.</span><span class="sxs-lookup"><span data-stu-id="73efb-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="73efb-425">L'attributo `QueueTrigger` indica a WebJobs SDK di chiamare questo metodo quando viene ricevuto un nuovo messaggio nella coda thumbnailrequest.</span><span class="sxs-lookup"><span data-stu-id="73efb-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="73efb-426">L'oggetto `BlobInformation` nel messaggio della coda viene automaticamente deserializzato nel parametro `blobInfo`.</span><span class="sxs-lookup"><span data-stu-id="73efb-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="73efb-427">Al completamento del metodo, il messaggio della coda viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="73efb-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="73efb-428">Se il metodo non riesce prima del completamento, il messaggio della coda non viene eliminato. Dopo un lease di 10 minuti scade e il messaggio viene rilasciato per essere nuovamente prelevato ed elaborato.</span><span class="sxs-lookup"><span data-stu-id="73efb-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="73efb-429">Questa sequenza non verrà ripetuta all'infinito se un messaggio genera sempre un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="73efb-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="73efb-430">Dopo 5 tentativi non riusciti di elaborare un messaggio, il messaggio viene spostato in una coda denominata {queuename}-poison.</span><span class="sxs-lookup"><span data-stu-id="73efb-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="73efb-431">Il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="73efb-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="73efb-432">I due `Blob` attributi forniscono oggetti associati ai BLOB: uno al BLOB di immagini esistenti e uno a un nuovo BLOB di anteprima creato dal metodo.</span><span class="sxs-lookup"><span data-stu-id="73efb-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="73efb-433">I nomi dei BLOB derivano dalle proprietà dell'oggetto `BlobInformation` ricevuto nel messaggio della coda (`BlobName` e `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="73efb-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="73efb-434">Per ottenere le funzionalità complete della libreria del client di archiviazione, è possibile usare la classe `CloudBlockBlob` per utilizzare i BLOB.</span><span class="sxs-lookup"><span data-stu-id="73efb-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="73efb-435">Per riutilizzare il codice scritto per lavorare con gli oggetti `Stream`, è possibile usare la classe `Stream`.</span><span class="sxs-lookup"><span data-stu-id="73efb-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="73efb-436">Per altre informazioni su come scrivere funzioni che usano attributi di WebJobs SDK, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="73efb-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="73efb-437">Come usare il servizio di archiviazione di accodamento di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="73efb-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="73efb-438">Come usare il servizio di archiviazione BLOB di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="73efb-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="73efb-439">Come usare il servizio di archiviazione tabelle di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="73efb-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="73efb-440">Come usare il bus di servizio di Azure con WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="73efb-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="73efb-441">Se l'applicazione Web viene eseguita su più VM, verranno eseguiti contemporaneamente più processi Web e in alcuni casi ciò può implicare che gli stessi dati verranno elaborati più volte.</span><span class="sxs-lookup"><span data-stu-id="73efb-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="73efb-442">Ciò non costituisce un problema se si utilizzano la coda, i BLOB e i trigger del bus di servizio integrati.</span><span class="sxs-lookup"><span data-stu-id="73efb-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="73efb-443">L’SDK garantisce che le funzioni verranno elaborate una sola volta per ogni messaggio o BLOB.</span><span class="sxs-lookup"><span data-stu-id="73efb-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="73efb-444">Per altre informazioni su come implementare l'arresto normale, vedere [Arresto normale](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="73efb-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="73efb-445">Il codice nel metodo `ConvertImageToThumbnailJPG` (non mostrato) usa le classi disponibili nello spazio dei nomi `System.Drawing` per maggiore semplicità.</span><span class="sxs-lookup"><span data-stu-id="73efb-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="73efb-446">Le classi in questo spazio dei nomi, tuttavia, sono state progettate per l'uso con Windows Form.</span><span class="sxs-lookup"><span data-stu-id="73efb-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="73efb-447">Non sono supportate per l'uso in un servizio Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="73efb-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="73efb-448">Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="73efb-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="73efb-449">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73efb-449">Next steps</span></span>
<span data-ttu-id="73efb-450">In questa esercitazione è stata illustrata una semplice applicazione a più livelli che usa WebJobs SDK per l'elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="73efb-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="73efb-451">Questa sezione offre alcuni suggerimenti per ottenere altre informazioni sulle applicazioni ASP.NET multilivello e sui processi Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="73efb-452">Funzionalità mancanti</span><span class="sxs-lookup"><span data-stu-id="73efb-452">Missing features</span></span>
<span data-ttu-id="73efb-453">L'applicazione è semplice, in modo da essere idonea per un'esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="73efb-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="73efb-454">In un'applicazione concreta si implementano l'[inserimento delle dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) e i [modelli relativi a repository e unità di lavoro](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), si usa un'[interfaccia per la registrazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), si usano le migrazioni [Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire le modifiche ai modelli di dati e si usa la [resilienza delle connessioni EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire gli errori di rete temporanei.</span><span class="sxs-lookup"><span data-stu-id="73efb-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="73efb-455">Scalabilità di Processi Web</span><span class="sxs-lookup"><span data-stu-id="73efb-455">Scaling WebJobs</span></span>
<span data-ttu-id="73efb-456">I processi Web vengono eseguiti nel contesto di un'app Web e non sono scalabili separatamente.</span><span class="sxs-lookup"><span data-stu-id="73efb-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="73efb-457">Ad esempio, se si ha un'istanza di un'app Web standard, si ha una sola istanza del processo in background in esecuzione, che usa alcune delle risorse del server (CPU, memoria e così via) che altrimenti sarebbero disponibili per la gestione del contenuto Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="73efb-458">Se il traffico varia in base all'ora del giorno o al giorno della settimana e se non è necessario eseguire subito l'elaborazione back-end, è possibile pianificare l'esecuzione dei processi Web nelle ore in cui il traffico è meno intenso.</span><span class="sxs-lookup"><span data-stu-id="73efb-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="73efb-459">Se il carico è comunque troppo elevato per la soluzione, è possibile eseguire il back-end come processo Web in un'app Web separata, dedicata a quello scopo specifico.</span><span class="sxs-lookup"><span data-stu-id="73efb-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="73efb-460">Sarà quindi possibile scalare l'app Web back-end indipendentemente dall'app Web front-end.</span><span class="sxs-lookup"><span data-stu-id="73efb-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="73efb-461">Per altre informazioni, vedere [Scalabilità di Processi Web](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="73efb-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="73efb-462">Come evitare gli arresti per timeout delle app Web</span><span class="sxs-lookup"><span data-stu-id="73efb-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="73efb-463">Per assicurarsi che i processi Web siano sempre in esecuzione e che siano in esecuzione in tutte le istanze dell'app Web, è necessario abilitare la funzionalità [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) .</span><span class="sxs-lookup"><span data-stu-id="73efb-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="73efb-464">Uso di WebJobs SDK al di fuori dei processi Web</span><span class="sxs-lookup"><span data-stu-id="73efb-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="73efb-465">Un programma che usa WebJobs SDK non deve essere eseguito in Azure in un processo Web.</span><span class="sxs-lookup"><span data-stu-id="73efb-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="73efb-466">Può essere eseguito in locale e anche in altri ambienti, ad esempio un ruolo di lavoro dei servizi cloud o un servizio di Windows.</span><span class="sxs-lookup"><span data-stu-id="73efb-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="73efb-467">Tuttavia, è possibile accedere al dashboard di WebJobs SDK solo da un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73efb-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="73efb-468">Per usare il dashboard è necessario connettere l'app Web all'account di archiviazione in uso, impostando la stringa di connessione AzureWebJobsDashboard nella scheda **Configura** del portale classico.</span><span class="sxs-lookup"><span data-stu-id="73efb-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="73efb-469">Sarà quindi possibile andare al dashboard usando l'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="73efb-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="73efb-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="73efb-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="73efb-471">Per altre informazioni, vedere [Accesso a un dashboard per lo sviluppo locale con WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), in cui tuttavia viene usato un vecchio nome per la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="73efb-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="73efb-472">Altra documentazione sui processi Web</span><span class="sxs-lookup"><span data-stu-id="73efb-472">More WebJobs documentation</span></span>
<span data-ttu-id="73efb-473">Per altre informazioni, vedere [Risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="73efb-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
