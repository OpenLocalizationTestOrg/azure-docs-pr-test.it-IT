---
title: aaaGet avviato con servizi Cloud di Azure e ASP.NET | Documenti Microsoft
description: Informazioni su come toocreate un'applicazione multilivello con ASP.NET MVC e Azure. app Hello viene eseguito in un servizio cloud, con ruolo web e il ruolo di lavoro. Usa Entity Framework, il database SQL e le code e i BLOB di archiviazione di Azure.
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="10543-105">Introduzione a Servizi cloud di Azure e ASP.NET</span><span class="sxs-lookup"><span data-stu-id="10543-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="10543-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="10543-106">Overview</span></span>
<span data-ttu-id="10543-107">Questa esercitazione viene illustrato come un'applicazione .NET a più livelli con un front-end, ASP.NET MVC toocreate e distribuirlo tooan [servizio cloud di Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="10543-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="10543-108">Hello applicazione utilizza [Database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [servizio Blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), hello e [servizio di Accodamento Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="10543-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="10543-109">È possibile [scaricare il progetto di Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) da hello MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="10543-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="10543-110">Hello esercitazione viene illustrato come toobuild ed eseguire un'applicazione hello in locale, come toodeploy, tooAzure e hello esecuzione nel cloud e come toobuild da zero.</span><span class="sxs-lookup"><span data-stu-id="10543-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="10543-111">È possibile avviare una compilazione da zero e quindi hello test e distribuire i passaggi in un secondo momento se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="10543-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="10543-112">Applicazione Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="10543-112">Contoso Ads application</span></span>
<span data-ttu-id="10543-113">un'applicazione Hello è un servizio BBS pubblicità.</span><span class="sxs-lookup"><span data-stu-id="10543-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="10543-114">Gli utenti creano un'inserzione tramite l'immissione di testo e il caricamento di un'immagine.</span><span class="sxs-lookup"><span data-stu-id="10543-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="10543-115">È possibile visualizzare un elenco di annunci con immagini di anteprima, e possono essere visualizzate immagine ingrandita hello quando selezionano un' dettagli hello toosee di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10543-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Elenco di inserzioni](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="10543-117">un'applicazione Hello utilizza hello [basate su coda di lavoro modello](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff carico di lavoro hello intenso della CPU di creazione di processo di back-end tooa anteprime.</span><span class="sxs-lookup"><span data-stu-id="10543-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="10543-118">Architettura alternativa: siti Web e processi Web</span><span class="sxs-lookup"><span data-stu-id="10543-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="10543-119">Questa esercitazione viene illustrato come toorun sia front-end e back-end in un Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="10543-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="10543-120">In alternativa, è hello toorun front-end in un [sito Web di Azure](/services/web-sites/) e utilizzare hello [processi Web](http://go.microsoft.com/fwlink/?LinkId=390226) funzionalità (attualmente in anteprima) per hello back-end.</span><span class="sxs-lookup"><span data-stu-id="10543-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="10543-121">Per un'esercitazione che utilizza i processi Web, vedere [introduzione hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="10543-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="10543-122">Per informazioni su come toochoose hello servizi che meglio si adatta lo scenario, vedere [confronto siti Web di Azure, servizi Cloud e macchine virtuali](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="10543-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="10543-123">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="10543-123">What you'll learn</span></span>
* <span data-ttu-id="10543-124">Come tooenable il computer per lo sviluppo di Azure installando hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="10543-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="10543-125">Toocreate Visual Studio cloud come progetto di servizio con un ruolo web ASP.NET MVC e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10543-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="10543-126">Tootest hello come progetto di servizio cloud localmente, utilizzando l'emulatore di archiviazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10543-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="10543-127">La modalità toopublish hello cloud progetto tooan Azure servizio cloud e di test utilizzando un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="10543-128">Come tooupload file e archiviarli nel servizio Blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10543-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="10543-129">Toouse hello come servizio di Accodamento di Azure per la comunicazione tra i livelli.</span><span class="sxs-lookup"><span data-stu-id="10543-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10543-130">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="10543-130">Prerequisites</span></span>
<span data-ttu-id="10543-131">Hello esercitazione presuppone la conoscenza [concetti di base su Azure cloud services](cloud-services-choose-me.md) , ad esempio *ruolo web* e *ruolo di lavoro* terminologia.</span><span class="sxs-lookup"><span data-stu-id="10543-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="10543-132">Si presuppone inoltre che si conosca come toowork con [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) progetti in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10543-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="10543-133">applicazione di esempio Hello Usa MVC, ma la maggior parte dell'esercitazione hello si applica anche tooWeb form.</span><span class="sxs-lookup"><span data-stu-id="10543-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="10543-134">È possibile eseguire l'applicazione hello in locale senza una sottoscrizione di Azure, ma è necessario un cloud di toohello dall'applicazione hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="10543-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="10543-135">Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="10543-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="10543-136">le istruzioni dell'esercitazione Hello usare uno dei seguenti prodotti hello:</span><span class="sxs-lookup"><span data-stu-id="10543-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="10543-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="10543-137">Visual Studio 2013</span></span>
* <span data-ttu-id="10543-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="10543-138">Visual Studio 2015</span></span>
* <span data-ttu-id="10543-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="10543-139">Visual Studio 2017</span></span>

<span data-ttu-id="10543-140">Se non si dispone di uno di questi, Visual Studio siano installato automaticamente quando si installa hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="10543-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="10543-141">Architettura dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="10543-141">Application architecture</span></span>
<span data-ttu-id="10543-142">app Hello archivia gli annunci in un database SQL, mediante Entity Framework Code First toocreate hello le tabelle e accedere ai dati hello.</span><span class="sxs-lookup"><span data-stu-id="10543-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="10543-143">Per ogni annuncio, hello database archivia due URL, uno per hello dimensioni effettive e uno per l'anteprima di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Tabella di inserzioni](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="10543-145">Quando un utente carica un'immagine, hello front-end in esecuzione in un ruolo web archivia l'immagine di hello in un [blob di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), e archivia le informazioni sugli annunci hello in database hello con un URL che punta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="10543-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="10543-146">AT hello stesso tempo, viene scritto un tooan messaggio coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="10543-147">Un processo di back-end in esecuzione in un ruolo di lavoro periodicamente esegue il polling della coda di hello per i nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="10543-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="10543-148">Quando viene visualizzato un nuovo messaggio, il ruolo di lavoro hello viene creata un'anteprima dell'immagine e aggiornamenti hello campo del database URL anteprima per quell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="10543-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="10543-149">Hello diagramma seguente viene illustrato come le parti di un'applicazione hello hello interagiscono.</span><span class="sxs-lookup"><span data-stu-id="10543-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="10543-151">Scaricare ed eseguire la soluzione hello completata</span><span class="sxs-lookup"><span data-stu-id="10543-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="10543-152">Scaricare e decomprimere hello [completato soluzione](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="10543-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="10543-153">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10543-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="10543-154">Da hello **File** dal menu **Apri progetto**, passare toowhere soluzione hello è stato scaricato e quindi aprire il file di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="10543-155">Premere soluzione hello toobuild CTRL + MAIUSC + B.</span><span class="sxs-lookup"><span data-stu-id="10543-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="10543-156">Per impostazione predefinita, Visual Studio vengono automaticamente ripristinati contenuto del pacchetto NuGet hello, che non era incluso nel hello *zip* file.</span><span class="sxs-lookup"><span data-stu-id="10543-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="10543-157">Se non ripristino i pacchetti hello, installarli manualmente, passare toohello **Gestisci pacchetti NuGet per la soluzione** la finestra di dialogo e fare clic su hello **ripristinare** pulsante in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="10543-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="10543-158">In **Esplora**, assicurarsi che **ContosoAdsCloudService** sia selezionato come progetto di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="10543-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="10543-159">Se si utilizza Visual Studio 2015 o versione successiva, modificare la stringa di connessione di hello in un'applicazione hello *Web. config* file di progetto ContosoAdsWeb hello in hello *ServiceConfiguration.Local.* file di progetto ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="10543-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="10543-160">In ogni caso, modificare "(localdb) \v11.0" troppo "(localdb) \MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="10543-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="10543-161">Premere CTRL + F5 toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="10543-162">Quando si esegue un progetto servizio cloud in locale, Visual Studio richiama automaticamente hello Azure *emulatore di calcolo* e Azure *emulatore di archiviazione*.</span><span class="sxs-lookup"><span data-stu-id="10543-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="10543-163">Usa emulatore di calcolo Hello il ruolo del computer risorse toosimulate hello web e ambienti di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10543-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="10543-164">Usa emulatore di archiviazione Hello un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) archiviazione cloud di Azure toosimulate nel database.</span><span class="sxs-lookup"><span data-stu-id="10543-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="10543-165">Hello prima esecuzione di un progetto di servizio cloud, accetta un minuto dell'hello emulatori toostart backup.</span><span class="sxs-lookup"><span data-stu-id="10543-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="10543-166">Al termine dell'avvio dell'emulatore, browser predefinito hello verrà visualizzata la home page dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="10543-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="10543-168">Fare clic su **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="10543-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="10543-169">Immettere alcuni dati di test e selezionare un *jpg* immagine tooupload e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="10543-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Pagina di creazione](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="10543-171">app Hello va toohello pagina di indice, ma non è presente un'anteprima per ad nuovo hello perché tale elaborazione non si è ancora verificato.</span><span class="sxs-lookup"><span data-stu-id="10543-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="10543-172">Attendere qualche istante, quindi aggiornare hello indice toosee hello miniatura.</span><span class="sxs-lookup"><span data-stu-id="10543-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Pagina di indice](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="10543-174">Fare clic su **dettagli** per le dimensioni effettive hello toosee Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10543-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Pagina dei dettagli](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="10543-176">Si è in esecuzione un'applicazione hello interamente nel computer locale, senza cloud toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="10543-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="10543-177">emulatore di archiviazione Hello archivia coda hello e dati blob in un database di SQL Server Express LocalDB e un'applicazione hello archivia i dati di Active Directory hello in un altro database di LocalDB.</span><span class="sxs-lookup"><span data-stu-id="10543-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="10543-178">Database di Entity Framework Code First hello creati automaticamente ad hello prima volta tooaccess ha tentato di app web hello.</span><span class="sxs-lookup"><span data-stu-id="10543-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="10543-179">Nella seguente sezione hello si configurerà hello soluzione toouse cloud di Azure le risorse per le code, BLOB e database dell'applicazione hello quando viene eseguito nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="10543-180">Se si desidera toocontinue toorun localmente ma si utilizzano le risorse di archiviazione e database cloud, è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="10543-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="10543-181">È sufficiente impostare le stringhe di connessione, si noterà come toodo.</span><span class="sxs-lookup"><span data-stu-id="10543-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="10543-182">Distribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="10543-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="10543-183">L'utente eseguirà hello seguente un'applicazione nel cloud hello hello toorun passaggi:</span><span class="sxs-lookup"><span data-stu-id="10543-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="10543-184">Creare un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="10543-185">Creare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="10543-186">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="10543-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="10543-187">Configurare hello soluzione toouse il database SQL di Azure quando è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="10543-188">Configurare hello soluzione toouse l'account di archiviazione di Azure quando è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="10543-189">Distribuire il servizio cloud di Azure di hello progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="10543-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="10543-190">Creazione di un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="10543-190">Create an Azure cloud service</span></span>
<span data-ttu-id="10543-191">Un servizio cloud di Azure è un'applicazione hello hello ambiente verrà eseguita in.</span><span class="sxs-lookup"><span data-stu-id="10543-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="10543-192">Nel browser aprire hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10543-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="10543-193">Fare clic su **Nuovo > Calcolo > Servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="10543-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="10543-194">Nella casella input nome DNS hello, immettere un prefisso di URL per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="10543-195">Questo URL è toobe univoco.</span><span class="sxs-lookup"><span data-stu-id="10543-195">This URL has toobe unique.</span></span>  <span data-ttu-id="10543-196">Se il prefisso hello che scelto è già in uso, si otterrà un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="10543-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="10543-197">Specificare un nuovo gruppo di risorse per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="10543-198">Fare clic su **Crea nuovo** e quindi digitare un nome in hello risorse input casella di gruppo, ad esempio CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="10543-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="10543-199">Scegliere hello area in cui un'applicazione hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="10543-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="10543-200">Questo campo specifica in quale data center viene ospitato il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="10543-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="10543-201">Per un'applicazione di produzione, scegliere i clienti tooyour di hello area più vicini.</span><span class="sxs-lookup"><span data-stu-id="10543-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="10543-202">Per questa esercitazione, scegliere tooyou di hello area più vicina.</span><span class="sxs-lookup"><span data-stu-id="10543-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="10543-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="10543-203">Click **Create**.</span></span>

    <span data-ttu-id="10543-204">In hello seguente immagine, viene creato un servizio cloud con hello CSvccontosoads.cloudapp.net URL.</span><span class="sxs-lookup"><span data-stu-id="10543-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Nuovo servizio cloud](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="10543-206">Creare un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="10543-206">Create an Azure SQL database</span></span>
<span data-ttu-id="10543-207">Quando l'applicazione hello viene eseguito nel cloud hello, utilizza un database basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="10543-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="10543-208">In hello [portale di Azure](https://portal.azure.com), fare clic su **nuovo > database > Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="10543-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="10543-209">In hello **nome del Database** immettere *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="10543-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="10543-210">In hello **gruppo di risorse**, fare clic su **utilizzare esistente** e gruppo di risorse selezionare hello utilizzato per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="10543-211">In hello seguente immagine, fare clic su **Server - Configurare le impostazioni necessarie** e **creare un nuovo server**.</span><span class="sxs-lookup"><span data-stu-id="10543-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Server toodatabase tunnel](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="10543-213">In alternativa, se la sottoscrizione contiene già un server, è possibile selezionare il server dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="10543-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="10543-214">In hello **nome Server** immettere *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="10543-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="10543-215">Immettere un **Nome di accesso** e una **Password** per l'amministratore.</span><span class="sxs-lookup"><span data-stu-id="10543-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="10543-216">Se si seleziona **Creare un nuovo server** non si immetteranno un nome e una password esistenti in questa casella,</span><span class="sxs-lookup"><span data-stu-id="10543-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="10543-217">Si sta immettendo un nuovo nome e una password che si definiscono toouse ora in un secondo momento quando si accede a database hello.</span><span class="sxs-lookup"><span data-stu-id="10543-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="10543-218">Se si seleziona un server in cui è stato creato in precedenza, verrà chiesto di account utente con privilegi amministrativi toohello password hello già stato creato.</span><span class="sxs-lookup"><span data-stu-id="10543-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="10543-219">Scegliere hello stesso **percorso** scelto per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="10543-220">Quando il servizio di cloud hello e database sono in diversi Data Center (diverse aree geografiche), latenza aumenta e verrà addebitato della larghezza di banda fuori hello data center.</span><span class="sxs-lookup"><span data-stu-id="10543-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="10543-221">La larghezza di banda nell'ambito di un data center è gratuita.</span><span class="sxs-lookup"><span data-stu-id="10543-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="10543-222">Controllare **server tooaccess di servizi di azure Consenti**.</span><span class="sxs-lookup"><span data-stu-id="10543-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="10543-223">Fare clic su **selezionare** per nuovo server hello.</span><span class="sxs-lookup"><span data-stu-id="10543-223">Click **Select** for hello new server.</span></span>

    ![Nuovo server di database SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="10543-225">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="10543-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="10543-226">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="10543-226">Create an Azure storage account</span></span>
<span data-ttu-id="10543-227">Un account di archiviazione di Azure fornisce risorse per l'archiviazione dei dati di code e blob nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="10543-228">In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione.</span><span class="sxs-lookup"><span data-stu-id="10543-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="10543-229">In questa esercitazione sarà usato un solo account.</span><span class="sxs-lookup"><span data-stu-id="10543-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="10543-230">In hello [portale di Azure](https://portal.azure.com), fare clic su **nuovo > archiviazione > - account di archiviazione blob, file, tabella e coda**.</span><span class="sxs-lookup"><span data-stu-id="10543-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="10543-231">In hello **nome** , immettere un prefisso di URL.</span><span class="sxs-lookup"><span data-stu-id="10543-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="10543-232">Questo testo prefisso e hello che viene visualizzato nella casella hello sarà account archiviazione tooyour hello univoco URL.</span><span class="sxs-lookup"><span data-stu-id="10543-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="10543-233">Se il prefisso hello che immesso è già stato utilizzato da un altro utente, sarà necessario toochoose un prefisso diverso.</span><span class="sxs-lookup"><span data-stu-id="10543-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="10543-234">Set hello **modello di distribuzione** troppo*classico*.</span><span class="sxs-lookup"><span data-stu-id="10543-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="10543-235">Set hello **replica** elenco a discesa elenco troppo**archiviazione localmente ridondante**.</span><span class="sxs-lookup"><span data-stu-id="10543-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="10543-236">Quando la replica geografica è abilitata per un account di archiviazione, il contenuto di hello archiviato è replicata tooa Data Center secondario tooenable failover se si verifica un errore grave nella posizione primaria hello.</span><span class="sxs-lookup"><span data-stu-id="10543-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="10543-237">La replica geografica può comportare costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="10543-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="10543-238">Per gli account di sviluppo e test, in genere non si desidera toopay per la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="10543-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="10543-239">Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="10543-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="10543-240">In hello **gruppo di risorse**, fare clic su **utilizzare esistente** e gruppo di risorse selezionare hello utilizzato per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="10543-241">Set hello **percorso** toohello riepilogo stessa area scelto per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="10543-242">Quando si trovano in Data Center diversi account di servizio e l'archiviazione cloud hello (diverse aree geografiche), latenza aumenta e verrà addebitato della larghezza di banda fuori hello data center.</span><span class="sxs-lookup"><span data-stu-id="10543-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="10543-243">La larghezza di banda nell'ambito di un data center è gratuita.</span><span class="sxs-lookup"><span data-stu-id="10543-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="10543-244">Gruppi di affinità di Azure forniscono una distanza di hello meccanismo toominimize tra le risorse in un data center, che è possibile ridurre la latenza.</span><span class="sxs-lookup"><span data-stu-id="10543-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="10543-245">In questa esercitazione non vengono utilizzati gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="10543-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="10543-246">Per ulteriori informazioni, vedere [come tooCreate un'affinità di gruppo in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="10543-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="10543-247">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="10543-247">Click **Create**.</span></span>

    ![Nuovo account di archiviazione](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="10543-249">Nell'immagine di hello, viene creato un account di archiviazione con URL hello `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="10543-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="10543-250">Configurare il database SQL di Azure hello soluzione toouse durante l'esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="10543-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="10543-251">Hello progetto web e progetto ruolo di lavoro ogni hello la propria stringa di connessione database e ogni database SQL di Azure di toopoint toohello è necessario quando l'applicazione hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="10543-252">Si userà un [trasformazione Web. config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) per ruolo web hello e un'impostazione di ambiente del servizio cloud per il ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="10543-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="10543-253">In questa sezione e la sezione successiva di hello, archiviare le credenziali nei file di progetto.</span><span class="sxs-lookup"><span data-stu-id="10543-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="10543-254">[Non archiviare dati sensibili in archivi pubblici di codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="10543-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="10543-255">Nel progetto ContosoAdsWeb hello aprire hello *Web.Release.config* file di trasformazione per un'applicazione hello *Web. config* file, eliminare il blocco di commento hello che contiene un `<connectionStrings>` elemento e incollare Hello seguente codice al suo posto.</span><span class="sxs-lookup"><span data-stu-id="10543-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="10543-256">Lasciare aperta per la modifica di file hello.</span><span class="sxs-lookup"><span data-stu-id="10543-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="10543-257">In hello [portale di Azure](https://portal.azure.com), fare clic su **database SQL** nel riquadro di sinistra hello, fare clic su database hello creato per questa esercitazione e quindi fare clic su **Mostra stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="10543-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Mostra stringhe di connessione](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="10543-259">portale Hello consente di visualizzare le stringhe di connessione, con un segnaposto per la password di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Stringhe di connessione](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="10543-261">In hello *Web.Release.config* trasformare il file, eliminare `{connectionstring}` e incollare nel relativo hello sul posto, la stringa di connessione ADO.NET da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="10543-262">Nella stringa di connessione hello incollata nel hello *Web.Release.config* file di trasformazione, sostituire `{your_password_here}` con password hello creata per il nuovo database di SQL hello.</span><span class="sxs-lookup"><span data-stu-id="10543-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="10543-263">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="10543-263">Save hello file.</span></span>  
6. <span data-ttu-id="10543-264">Selezionare e copiare la stringa di connessione hello (senza hello che racchiudono le virgolette) per l'utilizzo in hello alla procedura seguente per la configurazione di progetto di ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="10543-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="10543-265">In **Esplora**in **ruoli** nel progetto servizio cloud hello destro **ContosoAdsWorker** e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="10543-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="10543-267">Fare clic su hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="10543-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="10543-268">Modifica **configurazione del servizio** troppo**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="10543-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="10543-269">Seleziona hello **valore** field per hello `ContosoAdsDbConnectionString` impostazione e quindi incollare stringa di connessione hello copiato dalla sezione precedente di hello di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Stringa di connessione del database per il ruolo di lavoro](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="10543-271">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="10543-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="10543-272">Configurare l'account di archiviazione di Azure hello soluzione toouse durante l'esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="10543-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="10543-273">Stringhe di connessione di account di archiviazione di Azure per il progetto di ruolo web hello e progetto di ruolo di lavoro hello vengono archiviate nelle impostazioni di ambiente nel progetto di servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="10543-274">Per ogni progetto, è presente un set separato di impostazioni toobe utilizzata quando un'applicazione hello in esecuzione in locale e al momento dell'esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="10543-275">Si aggiornerà le impostazioni di ambiente cloud hello per i progetti di ruolo web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10543-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="10543-276">In **Esplora**, fare doppio clic su **ContosoAdsWeb** in **ruoli** in hello **ContosoAdsCloudService** del progetto e quindi fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="10543-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="10543-278">Fare clic su hello **impostazioni** scheda. In hello **configurazione del servizio** elenco a discesa scegliere **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="10543-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Configurazione del cloud](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="10543-280">Seleziona hello **StorageConnectionString** voce, è possibile notare i puntini di sospensione (**...** ) ubicato a destra hello della riga hello.</span><span class="sxs-lookup"><span data-stu-id="10543-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="10543-281">Fare clic su hello tooopen pulsante puntini di sospensione di hello **crea stringa di connessione Account di archiviazione** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="10543-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Casella di creazione della stringa di connessione](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="10543-283">In hello **crea stringa di connessione di archiviazione** la finestra di dialogo, fare clic su **sottoscrizione**, scegliere account di archiviazione hello creato in precedenza e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="10543-284">Se non è già stato effettuato l'accesso, saranno richieste le credenziali dell'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Crea Stringa di connessione di archiviazione](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="10543-286">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="10543-286">Save your changes.</span></span>
6. <span data-ttu-id="10543-287">Seguire hello stessa procedura utilizzata per hello `StorageConnectionString` hello tooset stringa di connessione `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="10543-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="10543-288">Questa stringa di connessione è usata per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="10543-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="10543-289">Seguire hello stessa procedura utilizzata per hello **ContosoAdsWeb** tooset ruolo entrambe le stringhe di connessione per hello **ContosoAdsWorker** ruolo.</span><span class="sxs-lookup"><span data-stu-id="10543-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="10543-290">Non dimenticare tooset **configurazione del servizio** troppo**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="10543-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="10543-291">impostazioni di ambiente ruolo Hello che sia stato configurato utilizzando hello dell'interfaccia utente di Visual Studio vengono archiviate nel seguente file di progetto ContosoAdsCloudService hello hello:</span><span class="sxs-lookup"><span data-stu-id="10543-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="10543-292">*Servicedefinition. Csdef* -definisce i nomi delle impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="10543-293">*ServiceConfiguration* -fornisce valori per l'esecuzione dell'applicazione hello nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="10543-294">*Local. cscfg* -fornisce valori per l'esecuzione dell'applicazione hello in locale.</span><span class="sxs-lookup"><span data-stu-id="10543-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="10543-295">Ad esempio, hello Servicedefinition include hello seguenti definizioni:</span><span class="sxs-lookup"><span data-stu-id="10543-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="10543-296">Hello e *ServiceConfiguration* file include i valori hello immessi per tali impostazioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10543-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="10543-297">Hello `<Instances>` impostazione specifica il numero di hello di macchine virtuali che Azure verrà eseguito il lavoro hello codice del ruolo in.</span><span class="sxs-lookup"><span data-stu-id="10543-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="10543-298">Hello [passaggi successivi](#next-steps) sono incluse informazioni toomore collegamenti sulla scalabilità orizzontale di un servizio cloud,</span><span class="sxs-lookup"><span data-stu-id="10543-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="10543-299">Distribuire hello progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="10543-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="10543-300">In **Esplora**, hello rapida **ContosoAdsCloudService** cloud progetto e quindi selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="10543-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Menu Pubblica](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="10543-302">In hello **Accedi** passaggio di hello **pubblica l'applicazione Azure** procedura guidata, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="10543-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Passaggio Accedi](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="10543-304">In hello **impostazioni** passaggio della procedura guidata hello, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="10543-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Passaggio Impostazioni](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="10543-306">le impostazioni predefinite in hello Hello **avanzate** scheda sono supportate per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="10543-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="10543-307">Per informazioni sulla scheda Avanzate hello, vedere [pubblicazione guidata applicazione Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="10543-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="10543-308">In hello **riepilogo** passaggio, fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="10543-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Passaggio Riepilogo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="10543-310">Hello **Log attività Azure** finestra verrà aperta in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10543-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="10543-311">Fare clic su dettagli relativi alla distribuzione hello tooexpand icona freccia destra hello.</span><span class="sxs-lookup"><span data-stu-id="10543-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="10543-312">distribuzione di Hello può richiedere fino a too5 minuti o più toocomplete.</span><span class="sxs-lookup"><span data-stu-id="10543-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Finestra Log attività di Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="10543-314">Quando lo stato di distribuzione hello è stato completato, fare clic su hello **URL app Web** toostart un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="10543-315">È ora possibile testare l'applicazione hello creando, visualizzazione e modifica alcuni annunci, quando è stata eseguita un'applicazione hello in locale.</span><span class="sxs-lookup"><span data-stu-id="10543-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="10543-316">Quando si sta Termina test, eliminazione o l'arresto del servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="10543-317">Anche se non si utilizza servizio cloud hello, spettante addebiti perché sono riservate risorse della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="10543-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="10543-318">Se lo si lascia in esecuzione, chiunque individui l'URL potrà creare e visualizzare inserzioni.</span><span class="sxs-lookup"><span data-stu-id="10543-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="10543-319">In hello [portale di Azure](https://portal.azure.com), visitare toohello **Panoramica** scheda per il servizio cloud e quindi fare clic su hello **eliminare** pulsante nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="10543-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="10543-320">Se si desidera tootemporarily impedire ad altri utenti di accedere a hello sito, fare clic su **arrestare** invece.</span><span class="sxs-lookup"><span data-stu-id="10543-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="10543-321">In tal caso, gli addebiti continueranno tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="10543-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="10543-322">Quando non è più necessario, è possibile seguire un simile hello di toodelete procedure account di archiviazione e database SQL.</span><span class="sxs-lookup"><span data-stu-id="10543-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="10543-323">Creare un'applicazione hello da zero</span><span class="sxs-lookup"><span data-stu-id="10543-323">Create hello application from scratch</span></span>
<span data-ttu-id="10543-324">Se è stato già scaricato [applicazione hello completato](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), procedere ora.</span><span class="sxs-lookup"><span data-stu-id="10543-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="10543-325">Si saranno copiare i file dal progetto scaricato hello in nuovo progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="10543-326">La creazione di un'applicazione Contoso annunci hello prevede hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="10543-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="10543-327">Creare una soluzione servizio cloud di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10543-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="10543-328">Aggiornare e aggiungere pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="10543-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="10543-329">Impostare i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="10543-329">Set project references.</span></span>
* <span data-ttu-id="10543-330">Configurare le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="10543-330">Configure connection strings.</span></span>
* <span data-ttu-id="10543-331">Aggiungere file di codice.</span><span class="sxs-lookup"><span data-stu-id="10543-331">Add code files.</span></span>

<span data-ttu-id="10543-332">Dopo la creazione di soluzioni di hello, si verrà esaminato il codice hello in progetti di servizio univoco toocloud e BLOB di Azure e code.</span><span class="sxs-lookup"><span data-stu-id="10543-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="10543-333">Creare una soluzione servizio cloud di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10543-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="10543-334">In Visual Studio, scegliere **nuovo progetto** da hello **File** menu.</span><span class="sxs-lookup"><span data-stu-id="10543-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="10543-335">Nel riquadro di sinistra hello di hello **nuovo progetto** finestra di dialogo espandere **Visual c#** e scegliere **Cloud** modelli, quindi scegliere hello **servizioClouddiAzure** modello.</span><span class="sxs-lookup"><span data-stu-id="10543-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="10543-336">Nome progetto hello e soluzione ContosoAdsCloudService e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nuovo progetto](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="10543-338">In hello **nuovo servizio Cloud Azure** finestra di dialogo, aggiungere un ruolo web e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10543-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="10543-339">Nome di ruolo web hello ContosoAdsWeb e assegnare il ruolo di lavoro hello ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="10543-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="10543-340">(Utilizzare l'icona della matita hello in nomi predefiniti dei ruoli hello hello riquadro di destra toochange hello).</span><span class="sxs-lookup"><span data-stu-id="10543-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Nuovo progetto di servizio cloud](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="10543-342">Quando viene visualizzato hello **nuovo progetto ASP.NET** la finestra di dialogo per il ruolo web hello, scegliere il modello MVC hello e quindi fare clic su **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="10543-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Modifica autenticazione](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="10543-344">In hello **Modifica autenticazione** finestra di dialogo scegliere **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="10543-346">In hello **nuovo progetto ASP.NET** finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="10543-347">In **Esplora**, fare doppio clic soluzione hello (non uno dei progetti hello) e scegliere **Add - nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="10543-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="10543-348">In hello **Aggiungi nuovo progetto** finestra di dialogo scegliere **Windows** in **Visual c#** in hello riquadro sinistro e quindi fare clic su hello **libreria di classi** modello.</span><span class="sxs-lookup"><span data-stu-id="10543-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="10543-349">Progetto hello nome *ContosoAdsCommon*, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="10543-350">È necessario tooreference hello hello e contesto dati modello di Entity Framework da progetti di ruolo web e di lavoro.</span><span class="sxs-lookup"><span data-stu-id="10543-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="10543-351">In alternativa, è possibile definire classi correlate a EF hello nel progetto di ruolo web hello e fare riferimento a tale progetto dal progetto di ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="10543-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="10543-352">Ma in alternativa hello, il progetto di ruolo di lavoro sarebbe necessario un assembly di riferimento tooweb che non sono necessarie.</span><span class="sxs-lookup"><span data-stu-id="10543-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="10543-353">Aggiornare e aggiungere pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="10543-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="10543-354">Aprire hello **Gestisci pacchetti NuGet** la finestra di dialogo per la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="10543-355">Nella parte superiore di hello della finestra hello, selezionare **aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="10543-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="10543-356">Cercare hello *Windowsazure* del pacchetto e, se è nell'elenco di hello, selezionarlo e selezionare tooupdate di progetti web e di lavoro hello in e quindi fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="10543-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="10543-357">libreria client di archiviazione Hello viene aggiornata più frequentemente di modelli di progetto di Visual Studio, pertanto tale versione di hello sono spesso disponibili in un toobe esigenze di un nuovo progetto aggiornato.</span><span class="sxs-lookup"><span data-stu-id="10543-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="10543-358">Nella parte superiore di hello della finestra hello, selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="10543-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="10543-359">Trovare hello *EntityFramework* NuGet package e installarlo in tutti e tre i progetti.</span><span class="sxs-lookup"><span data-stu-id="10543-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="10543-360">Trovare hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package e installarlo nel progetto di ruolo di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="10543-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="10543-361">Configurare le preferenze del progetto</span><span class="sxs-lookup"><span data-stu-id="10543-361">Set project references</span></span>
1. <span data-ttu-id="10543-362">Nel progetto ContosoAdsWeb hello impostare un progetto di riferimento toohello ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="10543-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="10543-363">Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **riferimenti** - **Aggiungi riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="10543-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="10543-364">In hello **gestione riferimenti** nella finestra di dialogo **soluzione progetti** nel riquadro di sinistra hello, selezionare **ContosoAdsCommon**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10543-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="10543-365">Nel progetto ContosoAdsWorker hello impostare un progetto di riferimento toohello ContosAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="10543-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="10543-366">ContosoAdsCommon conterrà hello Entity Framework dati del modello e il contesto di classe, che verrà usato da entrambi hello front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="10543-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="10543-367">Nel progetto ContosoAdsWorker hello, impostare un riferimento troppo`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="10543-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="10543-368">L'assembly è usato da toothumbnails immagini di hello tooconvert back-end.</span><span class="sxs-lookup"><span data-stu-id="10543-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="10543-369">Configurare le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="10543-369">Configure connection strings</span></span>
<span data-ttu-id="10543-370">In questa sezione verranno configurate le stringhe di connessione di Archiviazione di Azure e SQL per il test in locale.</span><span class="sxs-lookup"><span data-stu-id="10543-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="10543-371">istruzioni di distribuzione Hello in precedenza nell'esercitazione hello spiegano come le stringhe di tooset connessione hello per quando hello app in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="10543-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="10543-372">Nel progetto ContosoAdsWeb hello, Web. config dell'applicazione hello aperto, seguente hello insert `connectionStrings` elemento dopo hello `configSections` elemento.</span><span class="sxs-lookup"><span data-stu-id="10543-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="10543-373">Se si usa Visual Studio 2015 o versione successiva, sostituire "v11.0" con "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="10543-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="10543-374">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="10543-374">Save your changes.</span></span>
3. <span data-ttu-id="10543-375">Nel progetto ContosoAdsCloudService hello, fare doppio clic su ContosoAdsWeb in **ruoli**, quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="10543-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="10543-377">In hello **ContosAdsWeb [ruolo]** finestra Proprietà, fare clic su hello **impostazioni** scheda e quindi fare clic su **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="10543-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="10543-378">Lasciare **configurazione del servizio** impostare troppo**tutte le configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="10543-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="10543-379">Aggiungere un'impostazione denominata *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="10543-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="10543-380">Impostare **tipo** troppo*ConnectionString*e impostare **valore** troppo*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="10543-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Nuova stringa di connessione](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="10543-382">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="10543-382">Save your changes.</span></span>
7. <span data-ttu-id="10543-383">Seguire hello tooadd procedura stessa stringa di connessione di archiviazione nelle proprietà del ruolo ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="10543-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="10543-384">Ancora in hello **ContosoAdsWorker [ruolo]** finestra Proprietà, aggiungere un'altra stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="10543-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="10543-385">Nome: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="10543-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="10543-386">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="10543-386">Type: String</span></span>
   * <span data-ttu-id="10543-387">Valore: Incolla hello stessa stringa di connessione è utilizzata per il progetto di ruolo web hello.</span><span class="sxs-lookup"><span data-stu-id="10543-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="10543-388">(per Visual Studio 2013 è hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="10543-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="10543-389">Non dimenticare hello toochange origine dati se si copia in questo esempio e si utilizza Visual Studio 2015 o versione successiva.)</span><span class="sxs-lookup"><span data-stu-id="10543-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="10543-390">Aggiungere file di codice</span><span class="sxs-lookup"><span data-stu-id="10543-390">Add code files</span></span>
<span data-ttu-id="10543-391">In questa sezione si copiano i file di codice da soluzione hello scaricato in una nuova soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="10543-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="10543-392">Hello nelle sezioni seguenti verrà Mostra e illustrano i componenti chiave di questo codice.</span><span class="sxs-lookup"><span data-stu-id="10543-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="10543-393">tooadd file tooa progetto o una cartella, progetto hello pulsante destro del mouse o una cartella e fare clic su **Aggiungi** - **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="10543-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="10543-394">Selezionare file hello desiderati e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="10543-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="10543-395">Se viene richiesto se si desidera che i file esistenti tooreplace, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="10543-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="10543-396">Nel progetto ContosoAdsCommon hello, eliminare hello *Class1.cs* file e aggiungere il relativo hello sul posto *Ad.cs* e *ContosoAdscontext.cs* progetto scaricare i file da hello.</span><span class="sxs-lookup"><span data-stu-id="10543-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="10543-397">Nel progetto ContosoAdsWeb hello, aggiungere i seguenti file dal progetto scaricato hello hello.</span><span class="sxs-lookup"><span data-stu-id="10543-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="10543-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="10543-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="10543-399">In hello *Views\Shared* cartella:  *\_cshtml*.</span><span class="sxs-lookup"><span data-stu-id="10543-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="10543-400">In hello *Views\Home* cartella: *cshtml*.</span><span class="sxs-lookup"><span data-stu-id="10543-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="10543-401">In hello *controller* cartella: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="10543-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="10543-402">In hello *Views\Ad* cartella (Crea cartella hello innanzitutto): cinque *. cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="10543-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="10543-403">Nel progetto ContosoAdsWorker hello aggiungere *WorkerRole.cs* da hello scaricato il progetto.</span><span class="sxs-lookup"><span data-stu-id="10543-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="10543-404">È possibile compilare ed eseguire un'applicazione hello come indicato in precedenza nell'esercitazione hello e app hello utilizzerà le risorse dell'emulatore di archiviazione e un database locale.</span><span class="sxs-lookup"><span data-stu-id="10543-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="10543-405">Nelle sezioni seguenti Hello viene codice hello tooworking correlati con hello ambiente Azure, BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="10543-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="10543-406">In questa esercitazione viene illustrato come controller MVC toocreate e utilizzare lo scaffolding di visualizzazioni, come toowrite codice di Entity Framework che funziona con i database di SQL Server, o elementi fondamentali di hello della programmazione asincrona in ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="10543-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="10543-407">Per informazioni su questi argomenti, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="10543-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="10543-408">Introduzione a MVC 5</span><span class="sxs-lookup"><span data-stu-id="10543-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="10543-409">Introduzione a EF 6 e MVC 5</span><span class="sxs-lookup"><span data-stu-id="10543-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="10543-410">[Programmazione tooasynchronous introduzione in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="10543-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="10543-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="10543-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="10543-412">file Ad.cs Hello definisce un'enumerazione per le categorie di Active Directory e una classe di entità POCO per informazioni di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10543-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="10543-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="10543-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="10543-414">classe ContosoAdsContext Hello specifica classe annuncio hello viene utilizzato in una raccolta di DbSet, Entity Framework verranno archiviati in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="10543-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
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
```

<span data-ttu-id="10543-415">classe Hello dispone di due costruttori.</span><span class="sxs-lookup"><span data-stu-id="10543-415">hello class has two constructors.</span></span> <span data-ttu-id="10543-416">Hello primo di essi viene utilizzato dal progetto web hello e specifica il nome di hello di una stringa di connessione che viene archiviato nel file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="10543-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="10543-417">costruttore secondo Hello consente toopass nella stringa di connessione effettiva hello utilizzato dal progetto di ruolo di lavoro hello, poiché non dispone di un file Web. config.</span><span class="sxs-lookup"><span data-stu-id="10543-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="10543-418">Illustrato in precedenza in questa stringa di connessione è stata archiviata e verrà visualizzato in un secondo momento come codice hello recupera la stringa di connessione hello quando viene creata un'istanza di classe DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="10543-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="10543-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="10543-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="10543-420">Codice che viene chiamato da hello `Application_Start` metodo crea un *immagini* contenitore blob e un *immagini* coda se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="10543-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="10543-421">In questo modo si garantisce che ogni volta che si inizi con un nuovo account di archiviazione, o utilizzando l'emulatore di archiviazione hello in un nuovo computer, coda e il contenitore blob necessari hello verrà creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10543-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="10543-422">Hello account di archiviazione toohello di accesso di codice ottiene tramite la stringa di connessione di archiviazione hello da hello *cscfg* file.</span><span class="sxs-lookup"><span data-stu-id="10543-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="10543-423">Viene quindi ottenuto un riferimento toohello *immagini* contenitore blob, crea hello contenitore se non esiste già, e imposta le autorizzazioni per il nuovo contenitore di hello di accesso.</span><span class="sxs-lookup"><span data-stu-id="10543-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="10543-424">Per impostazione predefinita, nuovi contenitori consentono solo client con account di archiviazione BLOB tooaccess credenziali.</span><span class="sxs-lookup"><span data-stu-id="10543-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="10543-425">sito Web di Hello deve hello BLOB toobe pubblico in modo da poter visualizzare immagini con URL che BLOB immagine toohello punto.</span><span class="sxs-lookup"><span data-stu-id="10543-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="10543-426">Codice simile Ottiene un riferimento toohello *immagini* coda e crea una nuova coda.</span><span class="sxs-lookup"><span data-stu-id="10543-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="10543-427">In questo caso non sono necessarie modifiche alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="10543-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="10543-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="10543-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="10543-429">Hello *layout. cshtml* file imposta nome di app hello nell'intestazione di hello e piè di pagina e viene creata una voce di menu "Annunci".</span><span class="sxs-lookup"><span data-stu-id="10543-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="10543-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="10543-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="10543-431">Hello *Views\Home\Index.cshtml* file vengono visualizzati i collegamenti di categoria nella home page di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="10543-432">collegamenti Hello passare hello integer di hello `Category` enum in una pagina di indice di annunci toohello variabile di stringa di query.</span><span class="sxs-lookup"><span data-stu-id="10543-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="10543-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="10543-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="10543-434">In hello *AdController.cs* file, hello costruttore chiamate hello `InitializeStorage` gli oggetti di Azure Storage Client Library toocreate metodo che forniscono un'API per l'utilizzo di BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="10543-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="10543-435">Quindi codice hello Ottiene un riferimento toohello *immagini* blob contenitore, come illustrato in precedenza nella *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="10543-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="10543-436">Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="10543-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="10543-437">criteri di ripetizione di backoff esponenziale predefiniti Hello potrebbe bloccarsi hello web app per più di un minuto ripetuti tentativi per un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="10543-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="10543-438">criteri di ripetizione Hello specificato qui attende 3 secondi dopo ogni cercare i tentativi di toothree.</span><span class="sxs-lookup"><span data-stu-id="10543-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="10543-439">Codice simile Ottiene un riferimento toohello *immagini* coda.</span><span class="sxs-lookup"><span data-stu-id="10543-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="10543-440">La maggior parte del codice del controller hello è tipico per l'utilizzo di un modello di dati di Entity Framework utilizzando una classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="10543-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="10543-441">Un'eccezione è hello HttpPost `Create` metodo, che consente di caricare un file e lo salva nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="10543-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="10543-442">Raccoglitore di modelli Hello offre un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello metodo dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="10543-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="10543-443">Se l'utente hello selezionato tooupload un file, codice hello Carica file hello, viene salvato in un blob e aggiorna i record di database di Active Directory hello con un URL che punta toohello blob.</span><span class="sxs-lookup"><span data-stu-id="10543-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="10543-444">Hello codice hello caricamento è in hello `UploadAndSaveBlobAsync` metodo.</span><span class="sxs-lookup"><span data-stu-id="10543-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="10543-445">Crea un nome GUID per il blob hello, caricamenti e Salva il file di hello e restituisce un blob di riferimento toohello salvato.</span><span class="sxs-lookup"><span data-stu-id="10543-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
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
```

<span data-ttu-id="10543-446">Dopo aver hello HttpPost `Create` metodo carica un blob e aggiornamenti hello database, viene creato un tooinform messaggio della coda il processo di back-end che un'immagine è pronta per l'anteprima tooa di conversione.</span><span class="sxs-lookup"><span data-stu-id="10543-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="10543-447">codice per hello HttpPost Hello `Edit` metodo è simile ad eccezione del fatto che se l'utente di hello seleziona un nuovo file di immagine è necessario eliminare tutti i blob che esistono già.</span><span class="sxs-lookup"><span data-stu-id="10543-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="10543-448">Hello esempio successivo Mostra codice hello che elimina BLOB quando si elimina un annuncio.</span><span class="sxs-lookup"><span data-stu-id="10543-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="10543-449">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="10543-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="10543-450">Hello *cshtml* file Visualizza l'anteprima con hello altri dati di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10543-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="10543-451">Hello *Details.cshtml* file Visualizza immagine ingrandita hello.</span><span class="sxs-lookup"><span data-stu-id="10543-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="10543-452">ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="10543-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="10543-453">Hello *Create.cshtml* e *Edit.cshtml* file specificano di codifica che consente di hello hello tooget controller `HttpPostedFileBase` oggetto.</span><span class="sxs-lookup"><span data-stu-id="10543-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="10543-454">Un `<input>` elemento indica hello browser tooprovide una finestra di dialogo di selezione file.</span><span class="sxs-lookup"><span data-stu-id="10543-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="10543-455">ContosoAdsWorker - WorkerRole.cs - Metodo OnStart</span><span class="sxs-lookup"><span data-stu-id="10543-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="10543-456">ambiente di ruolo di lavoro di Azure Hello chiama hello `OnStart` metodo hello `WorkerRole` classe quando il ruolo di lavoro hello introduzione e chiama hello `Run` metodo quando hello `OnStart` al termine di metodo.</span><span class="sxs-lookup"><span data-stu-id="10543-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="10543-457">Hello `OnStart` metodo ottiene una stringa di connessione database hello da hello *cscfg* file e lo passa a classe Entity Framework DbContext toohello.</span><span class="sxs-lookup"><span data-stu-id="10543-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="10543-458">provider SQLClient Hello viene utilizzato per impostazione predefinita, in modo che il provider di hello non toobe specificato.</span><span class="sxs-lookup"><span data-stu-id="10543-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="10543-459">Successivamente, il metodo hello Ottiene un account di archiviazione toohello di riferimento e Crea coda contenitore blob hello se non sono presenti.</span><span class="sxs-lookup"><span data-stu-id="10543-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="10543-460">codice Hello che è simile toowhat già visto nel ruolo web hello `Application_Start` metodo.</span><span class="sxs-lookup"><span data-stu-id="10543-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="10543-461">ContosoAdsWorker - WorkerRole.cs - Metodo Run</span><span class="sxs-lookup"><span data-stu-id="10543-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="10543-462">Hello `Run` metodo viene chiamato quando hello `OnStart` metodo completa le operazioni di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="10543-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="10543-463">metodo Hello esegue un ciclo infinito che verifica la presenza di nuovi messaggi in coda e li elabora quando vengono ricevuti.</span><span class="sxs-lookup"><span data-stu-id="10543-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="10543-464">Dopo ogni iterazione del ciclo di hello, se è stato trovato alcun messaggio di coda, il programma hello rimane inattivo per un secondo.</span><span class="sxs-lookup"><span data-stu-id="10543-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="10543-465">Ciò impedisce che il ruolo di lavoro hello costi eccessivo della CPU tempo e l'archiviazione delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="10543-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="10543-466">Hello Team di consulenza clienti di Microsoft indica una storia su uno sviluppatore che ha dimenticato tooinclude, distribuito tooproduction e sinistra per ferie.</span><span class="sxs-lookup"><span data-stu-id="10543-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="10543-467">Quando si è ottenuto il suo supervisione costano più ferie hello.</span><span class="sxs-lookup"><span data-stu-id="10543-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="10543-468">Talvolta il contenuto di hello di un messaggio nella coda causa un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="10543-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="10543-469">Si tratta di un *messaggio non elaborabile*, e se appena registrato un errore e riavviare il ciclo di hello, tooprocess è possibile provare all'infinito che il messaggio.</span><span class="sxs-lookup"><span data-stu-id="10543-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="10543-470">Blocco catch hello include pertanto un se istruzione che controlla toosee quante volte app hello ha tentato tooprocess hello messaggio corrente e se sono trascorsi più di 5 volte, il messaggio hello viene eliminato dalla coda di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="10543-471">`ProcessQueueMessage` è chiamato quando viene trovato un messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="10543-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="10543-472">Questo codice legge l'URL dell'immagine di hello database tooget hello, converte tooa anteprima dell'immagine di hello, Salva anteprima hello in un blob, Aggiorna database hello con URL blob anteprima hello ed elimina il messaggio di coda hello.</span><span class="sxs-lookup"><span data-stu-id="10543-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="10543-473">Hello codice hello `ConvertImageToThumbnailJPG` metodo utilizza le classi nello spazio dei nomi System. Drawing hello per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="10543-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="10543-474">Tuttavia, le classi di hello in questo spazio dei nomi sono state progettate per l'uso con Windows Form.</span><span class="sxs-lookup"><span data-stu-id="10543-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="10543-475">Non sono supportate per l'uso in un servizio Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="10543-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="10543-476">Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="10543-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="10543-477">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="10543-477">Troubleshooting</span></span>
<span data-ttu-id="10543-478">Nel caso in cui qualcosa non funziona mentre si stiano seguendo le istruzioni di hello in questa esercitazione, ecco alcuni errori comuni e come tooresolve li.</span><span class="sxs-lookup"><span data-stu-id="10543-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="10543-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="10543-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="10543-480">Hello `RoleEnvironment` oggetto viene fornito da Azure quando si esegue un'applicazione in Azure o quando si esegue in locale utilizzando l'emulatore di calcolo di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10543-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="10543-481">Se questo errore si verifica quando si esegue in locale, assicurarsi di aver impostato come progetto di avvio hello progetto ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="10543-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="10543-482">Questo imposta hello progetto toorun utilizzando l'emulatore di calcolo di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10543-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="10543-483">Una delle operazioni di hello utilizzi dell'applicazione hello hello Azure RoleEnvironment per è tooget hello valori stringa di connessione archiviate in hello *cscfg* file, in modo da un'altra causa dell'eccezione corrente è una stringa di connessione mancante.</span><span class="sxs-lookup"><span data-stu-id="10543-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="10543-484">Verificare che creato impostazione StorageConnectionString hello per i Cloud e locali configurazioni nel progetto ContosoAdsWeb hello e creato entrambe le stringhe di connessione per entrambe le configurazioni nel progetto ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="10543-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="10543-485">Se esegue un **Trova tutti** ricerca per StorageConnectionString nell'intera soluzione hello, si devono visualizzarlo 9 volte nei file di 6.</span><span class="sxs-lookup"><span data-stu-id="10543-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="10543-486">Impossibile eseguire l'override tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="10543-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="10543-487">Nuova porta con valore inferiore al minimo consentito 8080 per HTTP protocollo</span><span class="sxs-lookup"><span data-stu-id="10543-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="10543-488">Provare a modificare il numero di porta hello utilizzato dal progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="10543-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="10543-489">Fare clic sul progetto ContosoAdsWeb hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="10543-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="10543-490">Fare clic su hello **Web** scheda e quindi modificare il numero di porta hello in hello **Url progetto** impostazione.</span><span class="sxs-lookup"><span data-stu-id="10543-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="10543-491">Per un'altra alternativa che è possibile risolvere il problema di hello, vedere hello seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="10543-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="10543-492">Altri errori durante l'esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="10543-492">Other errors when running locally</span></span>
<span data-ttu-id="10543-493">Dal cloud di nuova impostazione predefinita i progetti di servizio utilizzano hello toosimulate express di hello Azure compute emulator ambiente Azure.</span><span class="sxs-lookup"><span data-stu-id="10543-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="10543-494">Si tratta di una versione leggera di emulatore di calcolo completo hello e in alcuni hello condizioni emulatore completo funzionerà versione express hello non.</span><span class="sxs-lookup"><span data-stu-id="10543-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="10543-495">toochange hello progetto toouse hello completa dell'emulatore, fare clic sul progetto ContosoAdsCloudService hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="10543-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="10543-496">In hello **proprietà** finestra fare clic su hello **Web** scheda e quindi fare clic su hello **emulatore completo utilizzare** pulsante di opzione.</span><span class="sxs-lookup"><span data-stu-id="10543-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="10543-497">In ordine toorun un'applicazione hello con l'emulatore completo hello, è necessario tooopen Visual Studio con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="10543-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10543-498">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10543-498">Next steps</span></span>
<span data-ttu-id="10543-499">applicazione Contoso annunci Hello è intenzionalmente semplici per un'esercitazione Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="10543-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="10543-500">Ad esempio, non implementa [inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o hello [repository e un'unità di lavoro modelli](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), non [utilizzare un'interfaccia per la registrazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), non utilizza [ Migrazioni Code First di Entity Framework](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage dati le modifiche del modello o [resilienza delle connessioni EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) temporaneo toomanage errori di rete e così via.</span><span class="sxs-lookup"><span data-stu-id="10543-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="10543-501">Ecco alcune applicazioni di esempio di servizio cloud in cui vengono illustrate altre procedure di codifica del mondo reale, elencati dal meno complesso toomore complessi:</span><span class="sxs-lookup"><span data-stu-id="10543-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="10543-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="10543-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="10543-503">Concettualmente simili tooContoso annunci ma implementa più funzionalità e altre procedure di codifica del mondo reale.</span><span class="sxs-lookup"><span data-stu-id="10543-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="10543-504">[Applicazione multilivello di Servizi cloud di Azure con tabelle, code e BLOB](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="10543-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="10543-505">Introduce le tabelle di archiviazione di Azure, nonché i BLOB e le code.</span><span class="sxs-lookup"><span data-stu-id="10543-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="10543-506">Basato su una versione precedente di hello Azure SDK per .NET, richiederà alcuni toowork modifiche con la versione corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="10543-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="10543-507">[Nozioni fondamentali su Servizi cloud in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="10543-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="10543-508">Un esempio completo che illustra una vasta gamma di procedure consigliate, prodotta dal gruppo di Microsoft Patterns and Practices hello.</span><span class="sxs-lookup"><span data-stu-id="10543-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="10543-509">Per informazioni generali sullo sviluppo per il cloud hello, vedere [creazione di App per Cloud del mondo reale con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="10543-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="10543-510">Per un tooAzure video di introduzione archiviazione procedure consigliate e modelli, vedere [archiviazione di Microsoft Azure-novità, le procedure consigliate e modelli](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="10543-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="10543-511">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="10543-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="10543-512">Servizi cloud di Azure - Parte 1: Introduzione</span><span class="sxs-lookup"><span data-stu-id="10543-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="10543-513">Come toomanage dei servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="10543-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="10543-514">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="10543-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="10543-515">Il provider del servizio toochoose un cloud</span><span class="sxs-lookup"><span data-stu-id="10543-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
