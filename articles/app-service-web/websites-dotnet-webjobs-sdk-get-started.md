---
title: un processo Web .NET in Azure App Service aaaCreate | Documenti Microsoft
description: "Informazioni sulla creazione di un app a più livelli con ASP.NET MVC e Azure. Hello front-end viene eseguito in un'app web in Azure App Service e hello back-end esegue come un processo Web. app Hello Usa Entity Framework, Database SQL e le code di archiviazione di Azure e BLOB."
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
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="90822-105">Creare un processo Web .NET nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="90822-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="90822-106">Questa esercitazione viene illustrato come toowrite codice per una semplice applicazione ASP.NET MVC 5 multilivello che usa hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="90822-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="90822-107">scopo di hello Hello [WebJobs SDK](websites-webjobs-resources.md) è toosimplify hello codice scritto per attività comuni che possono eseguire un processo Web, ad esempio l'elaborazione di immagini, l'elaborazione della coda, aggregazione RSS, manutenzione di file e l'invio di messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="90822-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="90822-108">Hello WebJobs SDK include funzionalità per l'utilizzo di archiviazione di Azure e Bus di servizio per la pianificazione di attività e la gestione degli errori e per molti altri scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="90822-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="90822-109">Inoltre, ha progettato toobe estendibile e vi è un [repository del codice sorgente aperta per le estensioni](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="90822-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="90822-110">applicazione di esempio Hello è un servizio BBS pubblicità.</span><span class="sxs-lookup"><span data-stu-id="90822-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="90822-111">Gli utenti possono caricare le immagini per gli annunci e un processo di back-end converte toothumbnails immagini hello.</span><span class="sxs-lookup"><span data-stu-id="90822-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="90822-112">pagina di elenco annuncio Hello mostrate le anteprime di hello e pagina dettagli di annuncio hello Mostra immagine ingrandita hello.</span><span class="sxs-lookup"><span data-stu-id="90822-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="90822-113">Di seguito è riportata una schermata:</span><span class="sxs-lookup"><span data-stu-id="90822-113">Here's a screenshot:</span></span>

![Elenco di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="90822-115">Questa applicazione di esempio funziona con le [code di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) e con i [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="90822-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="90822-116">Hello esercitazione viene illustrato come toodeploy hello applicazione troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) e [Database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="90822-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="90822-117"><a id="prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90822-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="90822-118">Hello esercitazione si presuppone che si conosca come toowork con [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) progetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90822-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="90822-119">esercitazione Hello è stato inizialmente scritto per Visual Studio 2013, ma può essere utilizzato con le versioni successive di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90822-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="90822-120">Se si utilizza Visual Studio 2015 o 2017, prendere nota prima di eseguire un'applicazione hello in locale, è necessario modificare hello `Data Source` fa parte della stringa di connessione di SQL Server LocalDB hello nei file Web. config e App. config di hello da `Data Source=(localdb)\v11.0` troppo`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="90822-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="90822-121"><a name="note"></a>È necessario avere un toocomplete account Azure in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="90822-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="90822-122">È possibile [aprire un account Azure, gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): si ottiene crediti che è possibile utilizzare tootry out a pagamento di servizi di Azure e anche dopo che consentono, è possibile tenere conto di hello e utilizzare servizi di Azure gratuiti, ad esempio siti Web.</span><span class="sxs-lookup"><span data-stu-id="90822-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="90822-123">Carta di credito non verranno mai addebitata, a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.</span><span class="sxs-lookup"><span data-stu-id="90822-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="90822-124">I [sottoscrittori di Visual Studio possono attivare il credito Azure mensile](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): con la sottoscrizione ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.</span><span class="sxs-lookup"><span data-stu-id="90822-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="90822-125">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="90822-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="90822-126">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="90822-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="90822-127"><a id="learn"></a>Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="90822-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="90822-128">Hello esercitazione vengono illustrate le modalità hello toodo seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="90822-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="90822-129">Abilitare il computer per lo sviluppo di Azure installando hello Azure SDK (solo per Visual Studio 2013 e 2015 utenti).</span><span class="sxs-lookup"><span data-stu-id="90822-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="90822-130">Creare un progetto di applicazione Console che distribuisce automaticamente come un processo Web di Azure quando si distribuisce il progetto di web associato hello.</span><span class="sxs-lookup"><span data-stu-id="90822-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="90822-131">Testare un back-end WebJobs SDK in locale nel computer di sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="90822-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="90822-132">Pubblicare un'applicazione con un'app web di processi Web back-end tooa nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="90822-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="90822-133">Caricare i file e archiviarli in hello servizio Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="90822-134">Utilizzare hello Azure WebJobs SDK toowork con BLOB e code di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="90822-135"><a id="contosoads"></a>Architettura dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="90822-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="90822-136">applicazione di esempio Hello utilizza hello [basate su coda di lavoro modello](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carico di lavoro hello intenso della CPU di creazione di anteprime tooa back-end processo.</span><span class="sxs-lookup"><span data-stu-id="90822-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="90822-137">app Hello archivia gli annunci in un database SQL, mediante Entity Framework Code First toocreate hello le tabelle e accedere ai dati hello.</span><span class="sxs-lookup"><span data-stu-id="90822-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="90822-138">Per ogni annuncio, database hello archivia due URL: uno per dimensioni effettive hello e uno per l'anteprima di hello.</span><span class="sxs-lookup"><span data-stu-id="90822-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Tabella di inserzioni](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="90822-140">Quando un utente carica un'immagine, hello web app memorizza immagine hello in un [blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e archivia le informazioni sugli annunci hello in database hello con un URL che punta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="90822-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="90822-141">AT hello stesso tempo, viene scritto un tooan messaggio coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="90822-142">In un processo di back-end in esecuzione come un processo Web di Azure, hello WebJobs SDK esegue il polling della coda di hello per i nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="90822-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="90822-143">Quando viene visualizzato un nuovo messaggio, hello processo Web viene creata un'anteprima dell'immagine e aggiornamenti hello campo del database URL anteprima per quell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="90822-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="90822-144">Di seguito è riportato un diagramma che illustra l'interagiscono tra le parti di un'applicazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="90822-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Architettura di Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="90822-146">le istruzioni dell'esercitazione Hello applicano tooAzure SDK per .NET 2.7.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="90822-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="90822-147"><a id="storage"></a>Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="90822-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="90822-148">Un account di archiviazione di Azure fornisce risorse per l'archiviazione dei dati di code e blob nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="90822-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="90822-149">Viene utilizzato anche per dashboard hello da hello dati di registrazione toostore WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="90822-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="90822-150">In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione.</span><span class="sxs-lookup"><span data-stu-id="90822-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="90822-151">In questa esercitazione sarà usato un solo account.</span><span class="sxs-lookup"><span data-stu-id="90822-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="90822-152">Aprire hello **Esplora Server** finestra in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90822-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="90822-153">Pulsante destro del mouse hello **Azure** nodo e quindi fare clic su **connettersi tooMicrosoft sottoscrizione Azure...** .</span><span class="sxs-lookup"><span data-stu-id="90822-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Connettersi tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="90822-155">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="90822-156">Fare doppio clic su **archiviazione** in hello nodo di Azure e quindi fare clic su **crea Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="90822-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Crea account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="90822-158">In hello **crea Account di archiviazione** finestra di dialogo immettere un nome per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="90822-159">nome Hello deve essere univoco (nessun altro account di archiviazione di Azure può avere hello stesso nome).</span><span class="sxs-lookup"><span data-stu-id="90822-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="90822-160">Se specifica un nome hello è già in uso, si otterrà un toochange possibilità è.</span><span class="sxs-lookup"><span data-stu-id="90822-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="90822-161">Hello tooaccess URL l'account di archiviazione sarà *{nome}*. c.</span><span class="sxs-lookup"><span data-stu-id="90822-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="90822-162">Set hello **regione o gruppo di affinità** riepilogo toohello area più vicina tooyou.</span><span class="sxs-lookup"><span data-stu-id="90822-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="90822-163">Questa impostazione specifica il data center di Azure che ospiterà l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90822-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="90822-164">Per questa esercitazione è possibile selezionare qualsiasi area senza riscontrare differenze evidenti.</span><span class="sxs-lookup"><span data-stu-id="90822-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="90822-165">Per un'app web di produzione, è tuttavia il server web e il toobe di account di archiviazione in hello stesso latenza toominimize di area e i dati in uscita addebiti.</span><span class="sxs-lookup"><span data-stu-id="90822-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="90822-166">app web Hello (che verrà creato in un secondo momento) deve essere Data Center più vicino possibile toohello browser, accedere alle app web hello in latenza toominimize ordine.</span><span class="sxs-lookup"><span data-stu-id="90822-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="90822-167">Set hello **replica** elenco a discesa elenco troppo**ridondanza locale**.</span><span class="sxs-lookup"><span data-stu-id="90822-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="90822-168">Quando la replica geografica è abilitata per un account di archiviazione, il contenuto di hello archiviato è posizione tooa replicati Data Center secondario tooenable failover toothat in caso di un errore grave nella posizione primaria hello.</span><span class="sxs-lookup"><span data-stu-id="90822-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="90822-169">La replica geografica può comportare costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="90822-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="90822-170">Per gli account di sviluppo e test, in genere non si desidera toopay per la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="90822-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="90822-171">Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="90822-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="90822-172">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90822-172">Click **Create**.</span></span>

    ![Nuovo account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="90822-174"><a id="download"></a>Scaricare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="90822-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="90822-175">Scaricare e decomprimere hello [completato soluzione](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="90822-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="90822-176">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90822-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="90822-177">Da hello **File** dal menu **aprire > progetto/soluzione**, passare toowhere soluzione hello è stato scaricato e quindi aprire il file di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="90822-178">Premere soluzione hello toobuild CTRL + MAIUSC + B.</span><span class="sxs-lookup"><span data-stu-id="90822-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="90822-179">Per impostazione predefinita, Visual Studio vengono automaticamente ripristinati contenuto del pacchetto NuGet hello, che non era incluso nel hello *zip* file.</span><span class="sxs-lookup"><span data-stu-id="90822-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="90822-180">Se non ripristino i pacchetti hello, installarli manualmente, passare toohello **Gestisci pacchetti NuGet per la soluzione** finestra di dialogo e fare clic su hello **ripristinare** pulsante in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="90822-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="90822-181">In **Esplora**, assicurarsi che **ContosoAdsWeb** sia selezionato come progetto di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="90822-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="90822-182"><a id="configurestorage"></a>Configurare l'account di archiviazione di hello applicazione toouse</span><span class="sxs-lookup"><span data-stu-id="90822-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="90822-183">Aprire l'applicazione hello *Web. config* file nel progetto ContosoAdsWeb hello.</span><span class="sxs-lookup"><span data-stu-id="90822-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="90822-184">file Hello contiene una stringa di connessione SQL e una stringa di connessione di archiviazione di Azure per l'utilizzo di BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="90822-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="90822-185">stringa di connessione SQL Hello punta tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span><span class="sxs-lookup"><span data-stu-id="90822-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="90822-186">stringa di connessione di archiviazione Hello è riportato un esempio con segnaposto per hello chiave account di archiviazione nome e l'accesso.</span><span class="sxs-lookup"><span data-stu-id="90822-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="90822-187">Si sarà sostituire con una stringa di connessione con nome hello e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90822-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="90822-188">stringa di connessione di archiviazione Hello è denominato AzureWebJobsStorage perché è hello Nome hello che webjobs SDK viene utilizzato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="90822-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="90822-189">Hello stesso nome viene usato in modo da valore stringa di una sola connessione tooset hello ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="90822-190">In **Esplora Server**, fare doppio clic su account di archiviazione in hello **archiviazione** nodo e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="90822-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Fare clic su proprietà Account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="90822-192">In hello **proprietà** finestra, fare clic su **chiavi dell'Account di archiviazione**, quindi fare clic sui puntini di sospensione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Chiavi dell'account di archiviazione](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="90822-194">Hello copia **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="90822-194">Copy hello **Connection String**.</span></span>

    ![Get the storage account keys](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="90822-196">Sostituire una stringa di connessione di archiviazione hello in hello *Web. config* file con stringa di connessione hello appena copiato.</span><span class="sxs-lookup"><span data-stu-id="90822-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="90822-197">Assicurarsi di selezionare tutti gli elementi all'interno di virgolette hello hello virgolette prima di incollare escluso.</span><span class="sxs-lookup"><span data-stu-id="90822-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="90822-198">Aprire hello *app* file nel progetto ContosoAdsWebJob hello.</span><span class="sxs-lookup"><span data-stu-id="90822-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="90822-199">Questo file ha due stringhe di connessione di archiviazione, una per i dati dell'applicazione e l'altra per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="90822-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="90822-200">È possibile usare account di archiviazione separati per i dati applicazione e la registrazione oppure usare [più account di archiviazione per i dati](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="90822-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="90822-201">In questa esercitazione viene usato un singolo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90822-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="90822-202">le stringhe di connessione Hello dotati di segnaposto per le chiavi account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-202">hello connection strings have placeholders for hello storage account keys.</span></span>

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

    <span data-ttu-id="90822-203">Per impostazione predefinita, hello WebJobs SDK esegue la ricerca di stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="90822-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="90822-204">In alternativa, è possibile [archiviare la stringa di connessione hello tuttavia si desidera e passarlo in modo esplicito toohello `JobHost` oggetto](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="90822-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="90822-205">Sostituire entrambe le stringhe di connessione di archiviazione con stringa di connessione hello copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="90822-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="90822-206">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="90822-206">Save your changes.</span></span>

## <span data-ttu-id="90822-207"><a id="run"></a>Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="90822-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="90822-208">front-end web di hello toostart dell'applicazione hello, premere CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="90822-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="90822-209">browser predefinito Hello apre toohello home page.</span><span class="sxs-lookup"><span data-stu-id="90822-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="90822-210">(progetto web hello viene eseguita perché sono state apportate il progetto di avvio hello.)</span><span class="sxs-lookup"><span data-stu-id="90822-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="90822-212">toostart hello processo Web backend dell'applicazione hello, fare doppio clic su progetto ContosoAdsWebJob hello in **Esplora**, quindi fare clic su **Debug** > **Avvia nuova istanza** .</span><span class="sxs-lookup"><span data-stu-id="90822-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="90822-213">Una finestra dell'applicazione console aprirà e visualizzerà la registrazione messaggi che indica l'oggetto JobHost SDK processi Web hello avviata toorun.</span><span class="sxs-lookup"><span data-stu-id="90822-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Finestra dell'applicazione console che mostra il back-end hello è in esecuzione](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="90822-215">Nel browser fare clic su **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="90822-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="90822-216">Immettere alcuni dati di test, selezionare tooupload un'immagine e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="90822-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Pagina di creazione](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="90822-218">app Hello va toohello pagina di indice, ma non è presente un'anteprima per ad nuovo hello perché tale elaborazione non si è ancora verificato.</span><span class="sxs-lookup"><span data-stu-id="90822-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="90822-219">Nel frattempo, dopo un breve periodo di attesa registrazione nella finestra dell'applicazione hello console verrà visualizzato un messaggio che un messaggio nella coda è stato ricevuto ed elaborato.</span><span class="sxs-lookup"><span data-stu-id="90822-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="90822-221">Dopo aver visualizzato la registrazione dei messaggi nella finestra dell'applicazione console hello hello, aggiornare hello indice toosee hello miniatura.</span><span class="sxs-lookup"><span data-stu-id="90822-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Pagina di indice](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="90822-223">Fare clic su **dettagli** per le dimensioni effettive hello toosee Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90822-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Pagina dei dettagli](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="90822-225">Si è in esecuzione un'applicazione hello nel computer locale e utilizza un Server SQL database si trova sul computer, ma funziona con le code e BLOB hello cloud.</span><span class="sxs-lookup"><span data-stu-id="90822-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="90822-226">Nella seguente sezione hello viene eseguita un'applicazione hello nel cloud hello, utilizzando un database cloud nonché cloud BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="90822-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="90822-227"><a id="runincloud"></a>Eseguire un'applicazione hello nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="90822-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="90822-228">L'utente eseguirà hello seguente un'applicazione nel cloud hello hello toorun passaggi:</span><span class="sxs-lookup"><span data-stu-id="90822-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="90822-229">Distribuire le app tooWeb.</span><span class="sxs-lookup"><span data-stu-id="90822-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="90822-230">Visual Studio creerà automaticamente una nuova app Web in servizio app e un'istanza di database SQL.</span><span class="sxs-lookup"><span data-stu-id="90822-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="90822-231">Configurare hello web app toouse l'account di archiviazione e database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="90822-232">Dopo aver creato alcune annunci durante l'esecuzione nel cloud hello, verranno visualizzati hello hello toosee di WebJobs SDK dashboard rich toooffer ha funzionalità di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="90822-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="90822-233">Distribuire le app tooWeb</span><span class="sxs-lookup"><span data-stu-id="90822-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="90822-234">Chiudere il browser hello e finestra dell'applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="90822-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="90822-235">Seguire i passaggi hello hello [pubblicare tooAzure con il Database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sezione.</span><span class="sxs-lookup"><span data-stu-id="90822-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="90822-236">Dopo aver completato i passaggi di hello per la distribuzione, continuare con le attività rimanenti hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="90822-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="90822-237">Configurare l'account di archiviazione e database SQL di Azure di hello web app toouse</span><span class="sxs-lookup"><span data-stu-id="90822-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="90822-238">È una protezione ottimale troppo[evitare di inserire le informazioni riservate, ad esempio le stringhe di connessione nei file archiviati nel repository del codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="90822-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="90822-239">Azure offre un modo toodo: è possibile impostare la stringa di connessione e altri valori dell'impostazione nell'ambiente Azure hello e le API di configurazione ASP.NET prelevano automaticamente questi valori quando l'applicazione hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="90822-240">È possibile impostare questi valori in Azure utilizzando **Esplora Server**, hello portale di Azure, Windows PowerShell o hello interfaccia della riga di comando multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="90822-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="90822-241">Per altre informazioni, vedere il blog sul [funzionamento delle stringhe di applicazione e di connessione](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="90822-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="90822-242">In questa sezione, utilizzare **Esplora Server** tooset valori di stringa di connessione in Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="90822-243">In **Esplora server** fare clic con il pulsante destro del mouse sull'app Web in **Azure > Servizio app > {gruppo di risorse}**, quindi scegliere **Visualizza impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="90822-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="90822-244">Hello **App Web di Azure** verrà visualizzata la finestra su hello **configurazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="90822-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="90822-245">Modifica nome hello del nome di toohello stringa di connessione di hello DefaultConnection scelto quando è stato configurato il database SQL hello in hello [pubblicare tooAzure con il Database SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) articolo.</span><span class="sxs-lookup"><span data-stu-id="90822-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="90822-246">Azure viene creato automaticamente la stringa di connessione durante la creazione di app web hello con un database associato, ha già il valore di stringa di connessione corretta hello.</span><span class="sxs-lookup"><span data-stu-id="90822-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="90822-247">Si desidera modificare solo toowhat nome hello che il codice sta cercando.</span><span class="sxs-lookup"><span data-stu-id="90822-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="90822-248">Aggiungere due nuove stringhe di connessione denominate AzureWebJobsStorage e AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="90822-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="90822-249">Impostare il tipo di database hello troppo**personalizzato**, set hello connessione stringa valore toohello stesso valore utilizzato in precedenza per hello e *Web. config* e *app* file.</span><span class="sxs-lookup"><span data-stu-id="90822-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="90822-250">(Assicurarsi includere hello intera stringa di connessione, non solo chiave di accesso hello e non includere virgolette hello.)</span><span class="sxs-lookup"><span data-stu-id="90822-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="90822-251">Queste stringhe di connessione vengono utilizzate da hello WebJobs SDK, uno per i dati dell'applicazione e uno per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="90822-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="90822-252">Come illustrato in precedenza, hello per i dati dell'applicazione viene usato anche dal codice di hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="90822-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="90822-253">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90822-253">Click **Save**.</span></span>

    ![Stringhe di connessione nel portale di Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="90822-255">In **Esplora Server**, fare doppio clic su hello web app e quindi fare clic su **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="90822-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="90822-256">Al termine dell'app web hello, fare nuovamente doppio clic su hello web app e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="90822-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="90822-257">Hello processo Web viene avviato automaticamente quando si esegue la pubblicazione, ma arresta quando si esegue una configurazione di modifica.</span><span class="sxs-lookup"><span data-stu-id="90822-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="90822-258">toorestart, è possibile riavviare l'app web hello o riavviare i processi Web hello in hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="90822-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="90822-259">È in genere consigliato toorestart hello web app dopo una modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="90822-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="90822-260">Aggiornare hello finestra del browser con URL dell'app web hello nella relativa barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="90822-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="90822-261">verrà visualizzata la pagina home Hello.</span><span class="sxs-lookup"><span data-stu-id="90822-261">hello home page appears.</span></span>
8. <span data-ttu-id="90822-262">Creare un annuncio, come quando si [veniva eseguita localmente di un'applicazione hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="90822-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="90822-263">pagina di indice Hello Mostra senza un'anteprima inizialmente.</span><span class="sxs-lookup"><span data-stu-id="90822-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="90822-264">Aggiornare la pagina hello dopo alcuni secondi e hello anteprima viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="90822-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="90822-265">Se non viene visualizzata l'anteprima di hello, potrebbe essere toowait un minuto per hello processo Web toorestart.</span><span class="sxs-lookup"><span data-stu-id="90822-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="90822-266">Se dopo un periodo di tempo, non viene comunque visualizzato anteprima hello quando si aggiorna la pagina di hello, hello processo Web potrebbe non avere avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="90822-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="90822-267">In tal caso, passare toohello **servizi App** pannello in hello [portale di Azure](https://portal.azure.com/), individuare l'app web e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="90822-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="90822-268">Hello visualizzazione dashboard WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="90822-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="90822-269">In hello [portale di Azure](https://portal.azure.com/)selezionare hello **pannello App servizi**, individuare l'app web e selezionare **processi Web**.</span><span class="sxs-lookup"><span data-stu-id="90822-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="90822-270">Seleziona hello **registri** scheda.</span><span class="sxs-lookup"><span data-stu-id="90822-270">Select hello **Logs** tab.</span></span>

    ![Scheda Log](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="90822-272">Una nuova scheda del browser apre toohello dashboard WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="90822-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="90822-273">dashboard di Hello mostra che hello processo Web è in esecuzione e Mostra un elenco di funzioni nel codice che hello che webjobs SDK è attivato.</span><span class="sxs-lookup"><span data-stu-id="90822-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="90822-274">Fare clic su uno hello funzioni toosee dettagli dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="90822-274">Click one of hello functions toosee details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="90822-277">Hello **funzione riproduzione** in questa pagina, hello WebJobs SDK framework toocall hello funzione nuovamente e consente di definire una funzione di probabilità toochange hello dati passati toohello prima.</span><span class="sxs-lookup"><span data-stu-id="90822-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="90822-278">Al termine di test, prendere in considerazione l'eliminazione di hello web app, l'account di archiviazione e l'istanza del Database SQL.</span><span class="sxs-lookup"><span data-stu-id="90822-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="90822-279">Hello web app è gratuita, ma l'account di archiviazione SQL hello e l'istanza di database essere addebitati i costi (sebbene, minima a causa di piccole dimensioni toohello).</span><span class="sxs-lookup"><span data-stu-id="90822-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="90822-280">Inoltre, se si lascia hello web app in esecuzione, tutti gli utenti che consente di trovare l'URL può creare e visualizzare annunci.</span><span class="sxs-lookup"><span data-stu-id="90822-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="90822-281">Eliminare l'app Web</span><span class="sxs-lookup"><span data-stu-id="90822-281">Delete your web app</span></span>
<span data-ttu-id="90822-282">Nel portale di hello passare toohello **servizi App** pannello, individuare e selezionare l'app web e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="90822-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="90822-283">Se si desidera tootemporarily impedire ad altri utenti di accedere alle app web hello, fare clic su **arrestare** invece.</span><span class="sxs-lookup"><span data-stu-id="90822-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="90822-284">In tal caso, gli addebiti continueranno tooaccrue per hello account di archiviazione e Database SQL.</span><span class="sxs-lookup"><span data-stu-id="90822-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="90822-285">Eliminare l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="90822-285">Delete your storage account</span></span>
<span data-ttu-id="90822-286">toodelete l'account di archiviazione, vedere [eliminare un account di archiviazione](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="90822-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="90822-287">Eliminare il database</span><span class="sxs-lookup"><span data-stu-id="90822-287">Delete your database</span></span>
<span data-ttu-id="90822-288">toodelete del database SQL del database, vedere hello [API REST di Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentazione.</span><span class="sxs-lookup"><span data-stu-id="90822-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="90822-289"><a id="create"></a>Creare un'applicazione hello da zero</span><span class="sxs-lookup"><span data-stu-id="90822-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="90822-290">In questa sezione verranno eseguite hello quanto segue:</span><span class="sxs-lookup"><span data-stu-id="90822-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="90822-291">Creare una soluzione Visual Studio con un progetto Web.</span><span class="sxs-lookup"><span data-stu-id="90822-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="90822-292">Aggiungere un progetto libreria di classi per i dati di hello livello di accesso condiviso tra hello front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="90822-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="90822-293">Aggiungere un progetto di applicazione Console per hello back-end con processi Web abilitata la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90822-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="90822-294">Aggiungere i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="90822-294">Add NuGet packages.</span></span>
* <span data-ttu-id="90822-295">Impostare i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="90822-295">Set project references.</span></span>
* <span data-ttu-id="90822-296">Copiare il file di codice e la configurazione dell'applicazione da applicazione hello scaricato indicata nella sezione precedente di hello di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="90822-297">Esaminare le parti hello del codice di hello che funzionano con code e BLOB di Azure e hello WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="90822-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="90822-298">Creare una soluzione Visual Studio con un progetto Web e un progetto libreria di classi</span><span class="sxs-lookup"><span data-stu-id="90822-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="90822-299">In Visual Studio scegliere **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="90822-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="90822-300">In hello **nuovo progetto** finestra di dialogo, scegliere **Visual c#** > **Web** > **applicazione Web ASP.NET(.NETFramework)**.</span><span class="sxs-lookup"><span data-stu-id="90822-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="90822-301">Nome progetto hello ContosoAdsWeb, assegnare soluzione hello ContosoAdsWebJobsSDK (modificare il nome di soluzione hello se si inseriranno in hello stessa cartella hello scaricato soluzione), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Nuovo progetto](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="90822-303">In hello **nuova applicazione Web ASP.NET** finestra di dialogo, scegliere il modello MVC hello e selezionare **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="90822-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Modifica autenticazione](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="90822-305">In hello **Modifica autenticazione** finestra di dialogo, scegliere **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="90822-307">In hello **nuova applicazione Web ASP.NET** finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="90822-308">Visual Studio crea una soluzione di hello e progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="90822-309">In **Esplora**, fare doppio clic soluzione hello (non il progetto hello) e scegliere **Aggiungi** > **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="90822-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="90822-310">In hello **Aggiungi nuovo progetto** finestra di dialogo, scegliere **Visual c#** > **Windows Desktop classico** > **libreria di classi (.NET Framework)** modello.</span><span class="sxs-lookup"><span data-stu-id="90822-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="90822-311">Progetto hello nome *ContosoAdsCommon*, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="90822-312">Questo progetto conterrà il contesto di Entity Framework hello e il modello di dati di hello che hello front-end e back-end verrà utilizzata.</span><span class="sxs-lookup"><span data-stu-id="90822-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="90822-313">In alternativa, è possibile definire classi correlate a EF hello nel progetto web hello e fare riferimento a tale progetto dal progetto processo Web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="90822-314">Tuttavia, quindi il progetto processo Web avrebbe un assembly tooweb di riferimento, che non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="90822-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="90822-315">Aggiungere un progetto applicazione console con la distribuzione dei processi Web abilitata.</span><span class="sxs-lookup"><span data-stu-id="90822-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="90822-316">Fare clic sul progetto web hello (soluzione non hello o progetto libreria di classi hello) e quindi fare clic su **Aggiungi** > **nuovo progetto processo Web di Azure**.</span><span class="sxs-lookup"><span data-stu-id="90822-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="90822-318">In hello **Aggiungi processo Web di Azure** finestra di dialogo immettere ContosoAdsWebJob come entrambi hello **nome progetto** hello e **nome del processo Web**.</span><span class="sxs-lookup"><span data-stu-id="90822-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="90822-319">Lasciare **modalità processo Web eseguire** impostare troppo**eseguire continuamente**.</span><span class="sxs-lookup"><span data-stu-id="90822-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="90822-320">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-320">Click **OK**.</span></span>

   <span data-ttu-id="90822-321">Visual Studio crea un'applicazione Console che è toodeploy configurato come un processo Web ogni volta che si distribuisce il progetto di web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="90822-322">toodo, che eseguita hello seguenti attività dopo aver creato il progetto hello:</span><span class="sxs-lookup"><span data-stu-id="90822-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="90822-323">Aggiungere un *Settings pubblicare processo Web* file nella cartella proprietà di progetto processo Web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="90822-324">Aggiungere un *processi Web list.json* file nella cartella proprietà di progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="90822-325">Installato hello pacchetto Microsoft.Web.WebJobs.Publish NuGet nel progetto processo Web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="90822-326">Per ulteriori informazioni su queste modifiche, vedere [come toodeploy processi Web usando Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="90822-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="90822-327">Aggiungere i pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="90822-327">Add NuGet packages</span></span>
<span data-ttu-id="90822-328">modello di Hello nuovo progetto per un progetto processo Web viene installato automaticamente come pacchetto NuGet di processi Web SDK hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="90822-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="90822-329">Una delle dipendenze WebJobs SDK viene installato automaticamente nel progetto processo Web hello è hello hello Azure Storage Client Library (SCL).</span><span class="sxs-lookup"><span data-stu-id="90822-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="90822-330">Tuttavia, è necessario tooadd è toohello web progetto toowork con BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="90822-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="90822-331">Aprire hello **Gestisci pacchetti NuGet** finestra di dialogo per la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="90822-332">Nel riquadro sinistro hello selezionare **i pacchetti installati**.</span><span class="sxs-lookup"><span data-stu-id="90822-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="90822-333">Trovare hello *di archiviazione di Azure* pacchetto e quindi fare clic su **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="90822-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="90822-334">In hello **selezionare progetti** casella, seleziona hello **ContosoAdsWeb** casella di controllo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90822-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="90822-335">Tutti i tre progetti utilizzano hello toowork di Entity Framework con i dati nel Database SQL.</span><span class="sxs-lookup"><span data-stu-id="90822-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="90822-336">Nel riquadro sinistro hello selezionare **Online**.</span><span class="sxs-lookup"><span data-stu-id="90822-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="90822-337">Trovare hello *EntityFramework* NuGet package e installarlo in tutti e tre i progetti.</span><span class="sxs-lookup"><span data-stu-id="90822-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="90822-338">Configurare le preferenze del progetto</span><span class="sxs-lookup"><span data-stu-id="90822-338">Set project references</span></span>
<span data-ttu-id="90822-339">Entrambi i progetti processi Web e i web funzionano con il database SQL di hello, pertanto sia necessario un progetto di riferimento toohello ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="90822-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="90822-340">Nel progetto ContosoAdsWeb hello impostare un progetto di riferimento toohello ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="90822-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="90822-341">(Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **Aggiungi** > **riferimento**.</span><span class="sxs-lookup"><span data-stu-id="90822-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="90822-342">In hello **gestione riferimenti** nella finestra di dialogo **progetti** > **soluzione** > **ContosoAdsCommon**, quindi fare clic su **OK**.)</span><span class="sxs-lookup"><span data-stu-id="90822-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="90822-343">progetto processo Web Hello necessita di riferimenti per l'utilizzo di immagini e per l'accesso alle stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="90822-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="90822-344">Nel progetto ContosoAdsWebJob hello, impostare un riferimento troppo`System.Drawing` e `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="90822-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="90822-345">Aggiungere il codice e i file di configurazione</span><span class="sxs-lookup"><span data-stu-id="90822-345">Add code and configuration files</span></span>
<span data-ttu-id="90822-346">In questa esercitazione non viene visualizzato come troppo[creare controller MVC e viste mediante scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), come troppo[scrivere codice di Entity Framework compatibile con i database di SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), o [hello concetti di base programmazione in ASP.NET 4.5 asincrona](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="90822-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="90822-347">Pertanto, tutti i toodo rimane è copiare file di codice e la configurazione di soluzione hello scaricato in una nuova soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="90822-348">Dopo che a tale scopo, hello nelle sezioni seguenti mostrano e spiegano chiave parti di codice hello.</span><span class="sxs-lookup"><span data-stu-id="90822-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="90822-349">tooadd file tooa progetto o una cartella, progetto hello pulsante destro del mouse o una cartella e fare clic su **Aggiungi** > **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="90822-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="90822-350">Hello seleziona i file desiderati e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="90822-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="90822-351">Se viene richiesto se si desidera che i file esistenti tooreplace, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="90822-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="90822-352">Nel progetto ContosoAdsCommon hello, eliminare hello *Class1.cs* aggiuntivo relativo hello sul posto i seguenti file dal progetto scaricato hello e dei file.</span><span class="sxs-lookup"><span data-stu-id="90822-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="90822-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-353">*Ad.cs*</span></span>
   * <span data-ttu-id="90822-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="90822-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="90822-356">Nel progetto ContosoAdsWeb hello, aggiungere i seguenti file dal progetto scaricato hello hello.</span><span class="sxs-lookup"><span data-stu-id="90822-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="90822-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="90822-357">*Web.config*</span></span>
   * <span data-ttu-id="90822-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="90822-359">In hello *controller* cartella: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="90822-360">In hello *Views\Shared* cartella: *layout. cshtml* file</span><span class="sxs-lookup"><span data-stu-id="90822-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="90822-361">In hello *Views\Home* cartella: *cshtml*</span><span class="sxs-lookup"><span data-stu-id="90822-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="90822-362">In hello *Views\Ad* cartella (Crea cartella hello innanzitutto): cinque *. cshtml* file</span><span class="sxs-lookup"><span data-stu-id="90822-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="90822-363">Nel progetto ContosoAdsWebJob hello, aggiungere i seguenti file dal progetto scaricato hello hello.</span><span class="sxs-lookup"><span data-stu-id="90822-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="90822-364">*App. config* (Modifica filtro del tipo di file hello troppo**tutti i file**)</span><span class="sxs-lookup"><span data-stu-id="90822-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="90822-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-365">*Program.cs*</span></span>
   * <span data-ttu-id="90822-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="90822-366">*Functions.cs*</span></span>

<span data-ttu-id="90822-367">È ora possibile compilare, eseguire e distribuire un'applicazione hello come indicato in precedenza nell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="90822-368">Prima di a tale scopo, tuttavia, arrestare hello processo Web che è ancora in esecuzione nell'app web prima di hello che è distribuito.</span><span class="sxs-lookup"><span data-stu-id="90822-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="90822-369">In caso contrario, tale processo Web verrà elaborare messaggi della coda creati in locale o da app hello in esecuzione in una nuova app web, tutti usino hello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90822-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="90822-370"><a id="code"></a>Esaminare il codice dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="90822-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="90822-371">Nelle sezioni seguenti Hello viene codice hello correlati tooworking con hello WebJobs SDK e BLOB di archiviazione di Azure e code.</span><span class="sxs-lookup"><span data-stu-id="90822-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="90822-372">Per hello codice toohello specifico WebJobs SDK, visitare toohello [Program.cs e Functions.cs](#programcs) sezioni.</span><span class="sxs-lookup"><span data-stu-id="90822-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="90822-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="90822-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="90822-374">file Ad.cs Hello definisce un'enumerazione per le categorie di Active Directory e una classe di entità POCO per informazioni di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90822-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="90822-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="90822-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="90822-376">classe ContosoAdsContext Hello specifica classe annuncio hello viene utilizzato in una raccolta di DbSet, Entity Framework vengono archiviati in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="90822-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="90822-377">classe Hello dispone di due costruttori.</span><span class="sxs-lookup"><span data-stu-id="90822-377">hello class has two constructors.</span></span> <span data-ttu-id="90822-378">Hello innanzitutto viene utilizzato dal progetto web hello e specifica il nome di hello di una stringa di connessione che viene archiviato nel file Web. config hello o ambiente di runtime di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="90822-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="90822-379">costruttore secondo Hello consente toopass nella stringa di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="90822-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="90822-380">Poiché non dispone di un file Web. config, che è necessario dal progetto processo Web hello.</span><span class="sxs-lookup"><span data-stu-id="90822-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="90822-381">Illustrato in precedenza in questa stringa di connessione è stata archiviata e verrà visualizzato in un secondo momento come codice hello recupera la stringa di connessione hello quando viene creata un'istanza di classe DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="90822-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="90822-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="90822-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="90822-383">Hello `BlobInformation` classe è utilizzata toostore informazioni di un blob dell'immagine in un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="90822-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="90822-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="90822-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="90822-385">Codice che viene chiamato da hello `Application_Start` metodo crea un *immagini* contenitore blob e un *immagini* coda se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="90822-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="90822-386">In questo modo si garantisce che ogni volta che si avvia con un nuovo account di archiviazione, hello necessari coda e il contenitore blob vengono creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="90822-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="90822-387">Hello account di archiviazione toohello di accesso di codice ottiene tramite la stringa di connessione di archiviazione hello da hello *Web. config* file o l'ambiente di runtime di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="90822-388">Quindi, ottiene un riferimento toohello *immagini* contenitore blob, crea hello contenitore se non esiste già, e imposta le autorizzazioni per il nuovo contenitore di hello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90822-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="90822-389">Per impostazione predefinita, i nuovi contenitori consentono solo client con BLOB tooaccess credenziali account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90822-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="90822-390">app web Hello deve hello BLOB toobe pubblico in modo da poter visualizzare immagini con URL che BLOB immagine toohello punto.</span><span class="sxs-lookup"><span data-stu-id="90822-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

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

<span data-ttu-id="90822-391">Codice simile Ottiene un riferimento toohello *thumbnailrequest* coda e crea una nuova coda.</span><span class="sxs-lookup"><span data-stu-id="90822-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="90822-392">In questo caso non sono necessarie modifiche alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="90822-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="90822-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="90822-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="90822-394">Hello *layout. cshtml* file imposta nome di app hello nell'intestazione di hello e piè di pagina e viene creata una voce di menu "Annunci".</span><span class="sxs-lookup"><span data-stu-id="90822-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="90822-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="90822-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="90822-396">Hello *Views\Home\Index.cshtml* file vengono visualizzati i collegamenti di categoria nella home page di hello.</span><span class="sxs-lookup"><span data-stu-id="90822-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="90822-397">collegamenti Hello passare hello integer di hello `Category` enum in una pagina di indice di annunci toohello variabile di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="90822-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="90822-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="90822-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="90822-399">In hello *AdController.cs* file, hello costruttore chiamate hello `InitializeStorage` gli oggetti di Azure Storage Client Library toocreate metodo che forniscono un'API per l'utilizzo di BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="90822-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="90822-400">Quindi, codice hello Ottiene un riferimento toohello *immagini* blob contenitore, come illustrato in precedenza nella *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="90822-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="90822-401">Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="90822-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="90822-402">criteri di ripetizione di backoff esponenziale predefiniti Hello potrebbe bloccarsi hello web app per più di un minuto ripetuti tentativi per un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="90822-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="90822-403">criteri di ripetizione Hello specificato qui attende 3 secondi dopo ogni cercare i tentativi di toothree.</span><span class="sxs-lookup"><span data-stu-id="90822-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="90822-404">Codice simile Ottiene un riferimento toohello *immagini* coda.</span><span class="sxs-lookup"><span data-stu-id="90822-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="90822-405">La maggior parte del codice del controller hello è tipico per l'utilizzo di un modello di dati di Entity Framework utilizzando una classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="90822-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="90822-406">Un'eccezione è hello HttpPost `Create` metodo, che consente di caricare un file e lo salva nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="90822-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="90822-407">Raccoglitore di modelli Hello offre un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello metodo dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="90822-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="90822-408">Se l'utente hello selezionato tooupload un file, codice hello Carica file hello, viene salvato in un blob e aggiorna i record di database di Active Directory hello con un URL che punta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="90822-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="90822-409">Hello codice hello caricamento è in hello `UploadAndSaveBlobAsync` metodo.</span><span class="sxs-lookup"><span data-stu-id="90822-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="90822-410">Crea un nome GUID per il blob hello, caricamenti e Salva il file di hello e restituisce un blob di riferimento toohello salvato.</span><span class="sxs-lookup"><span data-stu-id="90822-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="90822-411">Dopo aver hello HttpPost `Create` metodo carica un blob e gli aggiornamenti hello database, viene creato un processo coda messaggi tooinform hello back-end che un'immagine è pronta per l'anteprima di conversione tooa.</span><span class="sxs-lookup"><span data-stu-id="90822-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="90822-412">codice per hello HttpPost Hello `Edit` metodo è simile, ad eccezione del fatto che se l'utente di hello seleziona un nuovo file di immagine, è necessario eliminare tutti i blob che esistono già per questo annuncio.</span><span class="sxs-lookup"><span data-stu-id="90822-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="90822-413">Ecco il codice hello che elimina BLOB quando si elimina un annuncio:</span><span class="sxs-lookup"><span data-stu-id="90822-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="90822-414">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="90822-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="90822-415">Hello *cshtml* file Visualizza l'anteprima con hello altri dati di Active Directory:</span><span class="sxs-lookup"><span data-stu-id="90822-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="90822-416">Hello *Details.cshtml* file Visualizza immagine ingrandita hello:</span><span class="sxs-lookup"><span data-stu-id="90822-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="90822-417">ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="90822-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="90822-418">Hello *Create.cshtml* e *Edit.cshtml* file specificano di codifica che consente di hello hello tooget controller `HttpPostedFileBase` oggetto.</span><span class="sxs-lookup"><span data-stu-id="90822-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="90822-419">Un `<input>` elemento indica hello browser tooprovide una finestra di dialogo di selezione file.</span><span class="sxs-lookup"><span data-stu-id="90822-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="90822-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="90822-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="90822-421">Quando hello Avvia processo Web, hello `Main` chiamate al metodo hello WebJobs SDK `JobHost.RunAndBlock` esecuzione delle funzioni attivate sul thread corrente hello toobegin del metodo.</span><span class="sxs-lookup"><span data-stu-id="90822-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="90822-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Metodo GenerateThumbnail</span><span class="sxs-lookup"><span data-stu-id="90822-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="90822-423">Hello WebJobs SDK chiama questo metodo quando viene ricevuto un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="90822-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="90822-424">metodo Hello crea un'immagine di anteprima e inserisce hello anteprima URL nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="90822-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

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
            // be instantiated and disposed within hello function.
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

* <span data-ttu-id="90822-425">Hello `QueueTrigger` attributo indirizza hello WebJobs SDK toocall questo metodo quando viene ricevuto un nuovo messaggio nella coda thumbnailrequest hello.</span><span class="sxs-lookup"><span data-stu-id="90822-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="90822-426">Hello `BlobInformation` oggetto nel messaggio della coda hello viene automaticamente deserializzato in hello `blobInfo` parametro.</span><span class="sxs-lookup"><span data-stu-id="90822-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="90822-427">Al termine del metodo hello, viene eliminato il messaggio di coda hello.</span><span class="sxs-lookup"><span data-stu-id="90822-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="90822-428">Se il metodo hello non riesce prima del completamento, il messaggio di coda hello non viene eliminato; Dopo la scadenza di un lease di 10 minuti, il messaggio hello è toobe rilasciato nuovamente prelevato ed elaborato.</span><span class="sxs-lookup"><span data-stu-id="90822-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="90822-429">Questa sequenza non verrà ripetuta all'infinito se un messaggio genera sempre un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="90822-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="90822-430">Dopo 5 non riuscito tentativi tooprocess un messaggio, messaggio hello viene spostata tooa coda denominata {queuename}-messaggi non elaborabili.</span><span class="sxs-lookup"><span data-stu-id="90822-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="90822-431">Hello il numero massimo di tentativi è configurabile.</span><span class="sxs-lookup"><span data-stu-id="90822-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="90822-432">Hello due `Blob` gli attributi forniscono gli oggetti che sono associati tooblobs: blob dell'immagine esistente toohello uno e uno tooa nuova anteprima blob creato con il metodo hello.</span><span class="sxs-lookup"><span data-stu-id="90822-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="90822-433">I nomi di BLOB provengono dalle proprietà di hello `BlobInformation` oggetto ricevuto nel messaggio della coda hello (`BlobName` e `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="90822-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="90822-434">tooget hello le funzionalità complete di hello libreria Client di archiviazione, è possibile utilizzare hello `CloudBlockBlob` toowork di classe con i BLOB.</span><span class="sxs-lookup"><span data-stu-id="90822-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="90822-435">Se si desidera che il codice tooreuse che è stato scritto toowork con `Stream` oggetti, è possibile utilizzare hello `Stream` classe.</span><span class="sxs-lookup"><span data-stu-id="90822-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="90822-436">Per ulteriori informazioni su come toowrite funzioni che utilizzano attributi WebJobs SDK, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="90822-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="90822-437">Coda di archiviazione con hello WebJobs SDK come toouse Azure</span><span class="sxs-lookup"><span data-stu-id="90822-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="90822-438">La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="90822-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="90822-439">La modalità di archiviazione con tabelle di Azure toouse hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="90822-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="90822-440">Come toouse del Bus di servizio di Azure con hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="90822-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="90822-441">Se l'app web viene eseguito su più macchine virtuali, verrà eseguito contemporaneamente più processi Web, e in alcuni scenari il possibile risultato hello stesso dati elaborati più volte.</span><span class="sxs-lookup"><span data-stu-id="90822-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="90822-442">Questo non costituisce un problema se si usa coda incorporato hello, blob e trigger di Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="90822-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="90822-443">Hello SDK assicura che le funzioni verranno elaborate solo una volta per ogni messaggio o di un blob.</span><span class="sxs-lookup"><span data-stu-id="90822-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="90822-444">Per informazioni sull'arresto normale tooimplement, vedere [spegnimento](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="90822-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="90822-445">Hello codice hello `ConvertImageToThumbnailJPG` (metodo) (non illustrato) utilizza le classi hello `System.Drawing` dello spazio dei nomi per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="90822-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="90822-446">Tuttavia, le classi di hello in questo spazio dei nomi sono state progettate per l'uso con Windows Form.</span><span class="sxs-lookup"><span data-stu-id="90822-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="90822-447">Non sono supportate per l'uso in un servizio Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="90822-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="90822-448">Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="90822-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="90822-449">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90822-449">Next steps</span></span>
<span data-ttu-id="90822-450">In questa esercitazione, si è visto una semplice applicazione multilivello che usa WebJobs SDK hello per l'elaborazione back-end.</span><span class="sxs-lookup"><span data-stu-id="90822-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="90822-451">Questa sezione offre alcuni suggerimenti per ottenere altre informazioni sulle applicazioni ASP.NET multilivello e sui processi Web.</span><span class="sxs-lookup"><span data-stu-id="90822-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="90822-452">Funzionalità mancanti</span><span class="sxs-lookup"><span data-stu-id="90822-452">Missing features</span></span>
<span data-ttu-id="90822-453">un'applicazione Hello è semplici per un'esercitazione Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="90822-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="90822-454">In un'applicazione reale è necessario implementare [inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) hello e [repository e un'unità di lavoro modelli](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), utilizzare [un'interfaccia per la registrazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilizzare [ Migrazioni Code First di Entity Framework](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dati le modifiche del modello e utilizzare [resilienza delle connessioni EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage degli errori di rete temporanea.</span><span class="sxs-lookup"><span data-stu-id="90822-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="90822-455">Scalabilità di Processi Web</span><span class="sxs-lookup"><span data-stu-id="90822-455">Scaling WebJobs</span></span>
<span data-ttu-id="90822-456">Processi Web eseguito nel contesto di hello di un'app web e non sono scalabili separatamente.</span><span class="sxs-lookup"><span data-stu-id="90822-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="90822-457">Ad esempio, se si dispone di un'istanza di app web Standard, si dispone solo un'istanza di esecuzione del processo in background e utilizza alcune risorse di server hello (CPU, memoria, e così via) che altrimenti sarebbero disponibili tooserve il contenuto web.</span><span class="sxs-lookup"><span data-stu-id="90822-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="90822-458">Se il traffico varia in base all'ora del giorno o giorno della settimana e back-end hello l'elaborazione è necessario toodo possono rimanere in attesa, è possibile pianificare i processi Web toorun orari di scarso traffico.</span><span class="sxs-lookup"><span data-stu-id="90822-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="90822-459">Se il carico hello è ancora troppo elevato per la soluzione, è possibile eseguire back-end hello come un processo Web in un'app web separato dedicato a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="90822-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="90822-460">Sarà quindi possibile scalare l'app Web back-end indipendentemente dall'app Web front-end.</span><span class="sxs-lookup"><span data-stu-id="90822-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="90822-461">Per altre informazioni, vedere [Scalabilità di Processi Web](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="90822-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="90822-462">Come evitare gli arresti per timeout delle app Web</span><span class="sxs-lookup"><span data-stu-id="90822-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="90822-463">toomake che i processi Web sono sempre in esecuzione e in esecuzione in tutte le istanze dell'app web, si dispone di hello tooenable [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funzionalità.</span><span class="sxs-lookup"><span data-stu-id="90822-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="90822-464">Utilizzo di hello WebJobs SDK di fuori di processi Web</span><span class="sxs-lookup"><span data-stu-id="90822-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="90822-465">Toorun non dispone di un programma che usa WebJobs SDK hello in Azure in un processo Web.</span><span class="sxs-lookup"><span data-stu-id="90822-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="90822-466">Può essere eseguito in locale e anche in altri ambienti, ad esempio un ruolo di lavoro dei servizi cloud o un servizio di Windows.</span><span class="sxs-lookup"><span data-stu-id="90822-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="90822-467">Tuttavia, è possibile accedere solo hello dashboard WebJobs SDK tramite un'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="90822-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="90822-468">dashboard di hello toouse tooconnect hello web app toohello account di archiviazione in uso mediante l'impostazione di stringa di connessione AzureWebJobsDashboard hello sul hello **configura** scheda del portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="90822-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="90822-469">Quindi, è possibile ottenere toohello Dashboard tramite hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="90822-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="90822-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="90822-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="90822-471">Per ulteriori informazioni, vedere [ottenere un dashboard per lo sviluppo locale con hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ma si noti che consente di visualizzare un nome di stringa di connessione precedente.</span><span class="sxs-lookup"><span data-stu-id="90822-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="90822-472">Altra documentazione sui processi Web</span><span class="sxs-lookup"><span data-stu-id="90822-472">More WebJobs documentation</span></span>
<span data-ttu-id="90822-473">Per altre informazioni, vedere [Risorse di documentazione di Processi Web di Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="90822-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
