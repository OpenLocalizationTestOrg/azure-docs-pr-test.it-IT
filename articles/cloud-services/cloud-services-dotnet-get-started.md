---
title: Introduzione a Servizi cloud di Azure e ASP.NET | Documentazione Microsoft
description: "Informazioni sulla creazione di un app a più livelli con ASP.NET MVC e Azure. L'app viene eseguita in un servizio cloud, con un ruolo Web e un ruolo di lavoro. Usa Entity Framework, il database SQL e le code e i BLOB di archiviazione di Azure."
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
ms.openlocfilehash: d2c197db73477d06d86d1c4faa8c4a2f58c7b391
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="510ff-105">Introduzione a Servizi cloud di Azure e ASP.NET</span><span class="sxs-lookup"><span data-stu-id="510ff-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="510ff-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="510ff-106">Overview</span></span>
<span data-ttu-id="510ff-107">Questa esercitazione illustra come creare un'applicazione .NET multilivello con un front-end MVC ASP.NET e come distribuirla in un [servizio cloud di Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="510ff-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="510ff-108">L'applicazione usa il [database SQL di Azure](http://msdn.microsoft.com/library/azure/ee336279), il [servizio BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) e il [Servizio di accodamento di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="510ff-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="510ff-109">È possibile [scaricare il progetto di Visual Studio](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) da MSDN Code Gallery.</span><span class="sxs-lookup"><span data-stu-id="510ff-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="510ff-110">Questa esercitazione illustra come compilare ed eseguire localmente l'applicazione, come distribuirla in Azure ed eseguirla nel cloud e come creare un'applicazione completamente nuova.</span><span class="sxs-lookup"><span data-stu-id="510ff-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="510ff-111">È possibile iniziare creando un'applicazione completamente nuova, quindi eseguire i passaggi relativi a test e distribuzione in un secondo momento, se si preferisce.</span><span class="sxs-lookup"><span data-stu-id="510ff-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="510ff-112">Applicazione Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="510ff-112">Contoso Ads application</span></span>
<span data-ttu-id="510ff-113">Questa applicazione è un BBS pubblicitario.</span><span class="sxs-lookup"><span data-stu-id="510ff-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="510ff-114">Gli utenti creano un'inserzione tramite l'immissione di testo e il caricamento di un'immagine.</span><span class="sxs-lookup"><span data-stu-id="510ff-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="510ff-115">Possono visualizzare un elenco di annunci con immagini di anteprima e visualizzare l'immagine con le dimensioni originali quando selezionano un annuncio per vederne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="510ff-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![Elenco di inserzioni](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="510ff-117">L'applicazione usa il [modello di lavoro incentrato sulle code](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) per delegare a un processo back-end il lavoro di creazione delle anteprime, che comporta un utilizzo elevato della CPU.</span><span class="sxs-lookup"><span data-stu-id="510ff-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="510ff-118">Architettura alternativa: siti Web e processi Web</span><span class="sxs-lookup"><span data-stu-id="510ff-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="510ff-119">Questa esercitazione mostra come eseguire front-end e back-end in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="510ff-120">In alternativa, si può eseguire il front-end in un [sito Web di Azure](/services/web-sites/) e si può usare la funzionalità [Processi Web](http://go.microsoft.com/fwlink/?LinkId=390226), attualmente disponibile in anteprima, per il back-end.</span><span class="sxs-lookup"><span data-stu-id="510ff-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="510ff-121">Per un'esercitazione che usa Processi Web, vedere [Introduzione all'uso dell'SDK di Processi Web di Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="510ff-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="510ff-122">Per informazioni su come scegliere i servizi ideali per lo scenario specifico, vedere [Confronto tra Siti Web, Servizi cloud e Macchine virtuali di Azure](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="510ff-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="510ff-123">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="510ff-123">What you'll learn</span></span>
* <span data-ttu-id="510ff-124">Abilitare il sistema per lo sviluppo in Azure installando Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="510ff-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="510ff-125">Creare un progetto di servizio cloud di Visual Studio con un ruolo Web MVC ASP.NET e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="510ff-126">Testare il progetto di servizio cloud localmente, tramite l'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="510ff-127">Pubblicare il progetto cloud in un servizio cloud di Azure e testarlo tramite un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="510ff-128">Caricare file e archiviarli nel servizio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="510ff-129">Usare il servizio di accodamento di Azure per la comunicazione tra livelli.</span><span class="sxs-lookup"><span data-stu-id="510ff-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="510ff-130">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="510ff-130">Prerequisites</span></span>
<span data-ttu-id="510ff-131">Nell'esercitazione si presuppone che l'utente abbia familiarità con i [concetti di base relativi ai servizi cloud di Azure](cloud-services-choose-me.md), ad esempio con la terminologia *ruolo Web* e *ruolo di lavoro*.</span><span class="sxs-lookup"><span data-stu-id="510ff-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="510ff-132">Si presuppone anche che si sia in grado di usare progetti [MVC ASP.NET](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) o [Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="510ff-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="510ff-133">L'applicazione di esempio usa MVC, ma la maggior parte dell'esercitazione è applicabile anche a Web Form.</span><span class="sxs-lookup"><span data-stu-id="510ff-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="510ff-134">È possibile eseguire l'app localmente senza sottoscrizione di Azure, ma sarà necessaria una sottoscrizione per distribuire l'applicazione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="510ff-135">Se non si dispone di un account, è possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) oppure [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="510ff-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="510ff-136">Le istruzioni dell'esercitazione sono applicabili ai prodotti seguenti:</span><span class="sxs-lookup"><span data-stu-id="510ff-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="510ff-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="510ff-137">Visual Studio 2013</span></span>
* <span data-ttu-id="510ff-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="510ff-138">Visual Studio 2015</span></span>
* <span data-ttu-id="510ff-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="510ff-139">Visual Studio 2017</span></span>

<span data-ttu-id="510ff-140">Se uno di questi prodotti non è disponibile, Visual Studio potrà essere installato automaticamente quando si installa Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="510ff-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="510ff-141">Architettura dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="510ff-141">Application architecture</span></span>
<span data-ttu-id="510ff-142">L'app archivia inserzioni pubblicitarie in un database SQL usando Code First di Entity Framework per creare le tabelle e accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="510ff-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="510ff-143">Il database archivia due URL per ogni annuncio, uno per l'immagine con dimensioni normali e uno per l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="510ff-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![Tabella di inserzioni](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="510ff-145">Quando un utente carica un'immagine, il front-end in esecuzione in un ruolo Web archivia l'immagine in un [BLOB di Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), quindi archivia le informazioni sulle inserzioni nel database con un URL che fa riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="510ff-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="510ff-146">e, al tempo stesso, scrive un messaggio in una coda di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="510ff-147">Un processo back-end in esecuzione in un ruolo di lavoro esegue periodicamente il polling della coda alla ricerca di nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="510ff-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="510ff-148">Quando compare un nuovo messaggio, il ruolo di lavoro crea un'anteprima per quell'immagine e aggiorna il campo di database relativo all'URL dell'anteprima per quell'inserzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="510ff-149">Il diagramma seguente mostra l'interazione tra le parti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-149">The following diagram shows how the parts of the application interact.</span></span>

![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="510ff-151">Download ed esecuzione della soluzione completata</span><span class="sxs-lookup"><span data-stu-id="510ff-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="510ff-152">Scaricare e decomprimere la [soluzione completata](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="510ff-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="510ff-153">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="510ff-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="510ff-154">Scegliere **Apri progetto** dal menu **File**, passare alla cartella in cui è stata scaricata la soluzione, quindi aprire il file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="510ff-155">Premere CTRL+MAIUSC+B per compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="510ff-156">Per impostazione predefinita, Visual Studio ripristina automaticamente il contenuto del pacchetto NuGet, che non era incluso nel file con estensione *zip* .</span><span class="sxs-lookup"><span data-stu-id="510ff-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="510ff-157">In caso di mancato ripristino dei pacchetti, installarli manualmente passando alla finestra di dialogo **Gestisci pacchetti NuGet per la soluzione**, quindi facendo clic sul pulsante **Ripristina** in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="510ff-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="510ff-158">In **Esplora soluzioni** verificare che come progetto di avvio sia selezionato **ContosoAdsCloudService**.</span><span class="sxs-lookup"><span data-stu-id="510ff-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="510ff-159">Se si usa Visual Studio 2015 o versione successiva, modificare la stringa di connessione di SQL Server nel file *Web.config* dell'applicazione per il progetto ContosoAdsWeb e nel file *ServiceConfiguration.Local.cscfg* per il progetto ContosoAdsCloudService.</span><span class="sxs-lookup"><span data-stu-id="510ff-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="510ff-160">In ogni caso, cambiare "(localdb)\v11.0" in "(localdb)\MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="510ff-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="510ff-161">Premere CTRL+F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="510ff-162">Quando si esegue localmente un progetto di servizio cloud, Visual Studio richiama automaticamente l'*emulatore di calcolo* di Azure e l'*emulatore di archiviazione* di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="510ff-163">L'emulatore di calcolo usa le risorse del computer per simulare gli ambienti del ruolo Web e del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="510ff-164">L'emulatore di archiviazione usa un database [LocalDB di SQL Server Express](http://msdn.microsoft.com/library/hh510202.aspx) per simulare la risorsa di archiviazione cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="510ff-165">Alla prima esecuzione di un progetto di servizio cloud, per l'avvio degli emulatori sarà necessario circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="510ff-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="510ff-166">Dopo l'avvio dell'emulatore, nel browser predefinito verrà visualizzata la home page dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Architettura di Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="510ff-168">Fare clic su **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="510ff-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="510ff-169">Immettere alcuni dati di test e selezionare un'immagine *jpg* da caricare, quindi fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="510ff-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![Pagina di creazione](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="510ff-171">L'app passa alla pagina di indice, ma non mostra alcuna anteprima per la nuova inserzione, poiché l'elaborazione non è stata ancora eseguita.</span><span class="sxs-lookup"><span data-stu-id="510ff-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="510ff-172">Attendere un attimo, quindi aggiornare la pagina di indice per visualizzare l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="510ff-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![Pagina di indice](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="510ff-174">Fare clic su **Details** per visualizzare l'immagine con dimensioni normali per l'inserzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![Pagina dei dettagli](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="510ff-176">L'applicazione è stata eseguita interamente nel computer locale, senza connessione al cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="510ff-177">L'emulatore di archiviazione archivia i dati di coda e BLOB in un database LocalDB di SQL Server Express e l'applicazione archivia i dati relativi alle inserzioni in un altro database LocalDB.</span><span class="sxs-lookup"><span data-stu-id="510ff-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="510ff-178">Code First di Entity Framework ha creato automaticamente il database delle inserzioni al primo tentativo di accesso da parte dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="510ff-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="510ff-179">Nella sezione seguente la soluzione sarà configurata per usare le risorse cloud di Azure per code, BLOB e per il database dell'applicazione in caso di esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="510ff-180">Se si vuole, è possibile continuare l'esecuzione locale usando tuttavia le risorse di archiviazione e database del cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="510ff-181">È sufficiente impostare le stringhe di connessione, come sarà illustrato in seguito.</span><span class="sxs-lookup"><span data-stu-id="510ff-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="510ff-182">Distribuire l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-182">Deploy the application to Azure</span></span>
<span data-ttu-id="510ff-183">Per eseguire l'applicazione nel cloud, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="510ff-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="510ff-184">Creare un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="510ff-185">Creare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="510ff-186">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="510ff-187">Configurare la soluzione per l'uso del database SQL di Azure in caso di esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="510ff-188">Configurare la soluzione per l'uso dell'account di archiviazione di Azure in caso di esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="510ff-189">Distribuire il progetto nel servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="510ff-190">Creazione di un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-190">Create an Azure cloud service</span></span>
<span data-ttu-id="510ff-191">Un servizio cloud in Azure è l'ambiente in cui sarà eseguita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="510ff-192">Accedere al [portale di Azure](https://portal.azure.com) nel browser.</span><span class="sxs-lookup"><span data-stu-id="510ff-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="510ff-193">Fare clic su **Nuovo > Calcolo > Servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="510ff-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="510ff-194">Nella casella di input Nome DNS immettere un prefisso URL per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="510ff-195">L'URL deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="510ff-195">This URL has to be unique.</span></span>  <span data-ttu-id="510ff-196">Se il prefisso scelto è già in uso, verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="510ff-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="510ff-197">Specificare un nuovo gruppo di risorse per il servizio.</span><span class="sxs-lookup"><span data-stu-id="510ff-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="510ff-198">Fare clic su **Crea nuovo** e quindi digitare un nome nella casella di input Gruppo di risorse, ad esempio CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="510ff-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="510ff-199">Scegliere l'area geografica in cui si vuole distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="510ff-200">Questo campo specifica in quale data center viene ospitato il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="510ff-201">Per un'applicazione di produzione, scegliere l'area più vicina ai clienti.</span><span class="sxs-lookup"><span data-stu-id="510ff-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="510ff-202">Per questa esercitazione, scegliere l'area geografica più vicina alla propria ubicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="510ff-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="510ff-203">Click **Create**.</span></span>

    <span data-ttu-id="510ff-204">L'immagine seguente illustra la creazione di un servizio cloud il cui URL è CSvccontosoads.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="510ff-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![Nuovo servizio cloud](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="510ff-206">Creare un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-206">Create an Azure SQL database</span></span>
<span data-ttu-id="510ff-207">Quando l'app è in esecuzione nel cloud, userà un database basato sul cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="510ff-208">Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo > Database > Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="510ff-208">In the [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="510ff-209">Nella casella **Nome database** immettere *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="510ff-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="510ff-210">In **Gruppo di risorse** fare clic su **Usa esistente** e selezionare il gruppo di risorse usato per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="510ff-211">Nella schermata illustrata di seguito fare clic su **Server - Configurare le impostazioni necessarie** e **Creare un nuovo server**.</span><span class="sxs-lookup"><span data-stu-id="510ff-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Tunnel al server di database](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="510ff-213">In alternativa, se la sottoscrizione è già associata a un server, sarà possibile selezionare quel server dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="510ff-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="510ff-214">Nella casella **Nome server** immettere *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="510ff-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="510ff-215">Immettere un **Nome di accesso** e una **Password** per l'amministratore.</span><span class="sxs-lookup"><span data-stu-id="510ff-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="510ff-216">Se si seleziona **Creare un nuovo server** non si immetteranno un nome e una password esistenti in questa casella,</span><span class="sxs-lookup"><span data-stu-id="510ff-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="510ff-217">ma un nuovo nome e una nuova password definiti in questo momento e da usare in seguito per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="510ff-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="510ff-218">Se è stato selezionato un server creato in precedenza, sarà richiesta la password dell'account utente di amministrazione già creato.</span><span class="sxs-lookup"><span data-stu-id="510ff-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="510ff-219">Scegliere la stessa **località** selezionata per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="510ff-220">Quando il servizio cloud e il database si trovano in data center diversi (aree diverse), la latenza aumenterà e sarà addebitato il costo relativo alla larghezza di banda esterna al data center.</span><span class="sxs-lookup"><span data-stu-id="510ff-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="510ff-221">La larghezza di banda nell'ambito di un data center è gratuita.</span><span class="sxs-lookup"><span data-stu-id="510ff-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="510ff-222">Selezionare **Consenti ai servizi di Azure di accedere al server**.</span><span class="sxs-lookup"><span data-stu-id="510ff-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="510ff-223">Fare clic su **Seleziona** per il nuovo server.</span><span class="sxs-lookup"><span data-stu-id="510ff-223">Click **Select** for the new server.</span></span>

    ![Nuovo server di database SQL](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="510ff-225">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="510ff-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="510ff-226">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-226">Create an Azure storage account</span></span>
<span data-ttu-id="510ff-227">Un account di archiviazione di Azure offre risorse per l'archiviazione di dati di code e BLOB nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="510ff-228">In un'applicazione effettiva si creano in genere account separati per i dati dell'applicazione rispetto ai dati di registrazione e account separati per i dati di test rispetto ai dati di produzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="510ff-229">In questa esercitazione sarà usato un solo account.</span><span class="sxs-lookup"><span data-stu-id="510ff-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="510ff-230">Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo > Archiviazione > Account di archiviazione: BLOB, File, Tabelle, Code**.</span><span class="sxs-lookup"><span data-stu-id="510ff-230">In the [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="510ff-231">Nella casella **Nome** immettere un prefisso URL.</span><span class="sxs-lookup"><span data-stu-id="510ff-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="510ff-232">La combinazione di questo prefisso e del testo visualizzato sotto la casella corrisponderà all'URL univoco dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="510ff-233">Se il prefisso immesso è già stato usato, sarà necessario scegliere un prefisso diverso.</span><span class="sxs-lookup"><span data-stu-id="510ff-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="510ff-234">Impostare **Modello di distribuzione** su *Classica*.</span><span class="sxs-lookup"><span data-stu-id="510ff-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="510ff-235">Nell'elenco a discesa **Replica** scegliere **Archiviazione con ridondanza locale**.</span><span class="sxs-lookup"><span data-stu-id="510ff-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="510ff-236">Quando per un account di archiviazione è abilitata la replica geografica, il contenuto archiviato viene replicato in un data center secondario per permettere il failover in caso di emergenza grave nella posizione primaria.</span><span class="sxs-lookup"><span data-stu-id="510ff-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="510ff-237">La replica geografica può comportare costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="510ff-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="510ff-238">Per gli account di test e di sviluppo si preferisce in genere non pagare per la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="510ff-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="510ff-239">Per altre informazioni, vedere la pagina relativa alla [creazione, gestione o eliminazione di un account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="510ff-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="510ff-240">In **Gruppo di risorse** fare clic su **Usa esistente** e selezionare il gruppo di risorse usato per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="510ff-241">Scegliere dall'elenco a discesa **Località** la stessa area geografica selezionata per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="510ff-242">Quando il servizio cloud e l'account di archiviazione si trovano in data center diversi (aree diverse), la latenza aumenterà e verrà addebitato il costo relativo alla larghezza di banda esterna al data center.</span><span class="sxs-lookup"><span data-stu-id="510ff-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="510ff-243">La larghezza di banda nell'ambito di un data center è gratuita.</span><span class="sxs-lookup"><span data-stu-id="510ff-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="510ff-244">I gruppi di affinità di Azure offrono un meccanismo per ridurre la distanza tra le risorse in un data center e di conseguenza la latenza.</span><span class="sxs-lookup"><span data-stu-id="510ff-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="510ff-245">In questa esercitazione non vengono utilizzati gruppi di affinità.</span><span class="sxs-lookup"><span data-stu-id="510ff-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="510ff-246">Per altre informazioni, vedere [Come creare un gruppo di affinità in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="510ff-246">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="510ff-247">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="510ff-247">Click **Create**.</span></span>

    ![Nuovo account di archiviazione](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="510ff-249">La seguente figura illustra la creazione di un account di archiviazione con l'URL `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="510ff-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="510ff-250">Configurare la soluzione per l'uso del database SQL di Azure in caso di esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="510ff-251">Il progetto Web e il progetto ruolo di lavoro dispongono di una stringa di connessione di database specifica e quando l'app è in esecuzione in Azure ogni progetto deve fare riferimento al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="510ff-252">Sarà necessario usare una [trasformazione Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) per il ruolo Web e un'impostazione dell'ambiente del servizio cloud per il ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="510ff-253">In questa sezione e nella sezione successiva, le credenziali vengono archiviate in file di progetto.</span><span class="sxs-lookup"><span data-stu-id="510ff-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="510ff-254">[Non archiviare dati sensibili in archivi pubblici di codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="510ff-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="510ff-255">Nel progetto ContosoAdsWeb aprire il file di trasformazione *Web.Release.config* per il file *Web.config* dell'applicazione, eliminare il blocco di commento che include un elemento `<connectionStrings>` e sostituirlo incollando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="510ff-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="510ff-256">Lasciare aperto il file per la modifica.</span><span class="sxs-lookup"><span data-stu-id="510ff-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="510ff-257">Nel [portale di Azure](https://portal.azure.com) fare clic su **Database SQL** nel riquadro sinistro, selezionare il database creato per l'esercitazione, quindi fare clic su **Mostra stringhe di connessione**.</span><span class="sxs-lookup"><span data-stu-id="510ff-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Mostra stringhe di connessione](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="510ff-259">Il portale visualizza le stringhe di connessione, con un segnaposto per la password.</span><span class="sxs-lookup"><span data-stu-id="510ff-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![Stringhe di connessione](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="510ff-261">Nel file di trasformazione *Web.Release.config* eliminare `{connectionstring}` e incollare al suo posto la stringa di connessione ADO.NET dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="510ff-262">Nella stringa di connessione incollata nel file di trasformazione *Web.Release.config* sostituire `{your_password_here}` con la password creata per il nuovo database SQL.</span><span class="sxs-lookup"><span data-stu-id="510ff-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="510ff-263">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="510ff-263">Save the file.</span></span>  
6. <span data-ttu-id="510ff-264">Selezionare e copiare la stringa di connessione, senza le virgolette tra cui è racchiusa, per usarla nei passaggi seguenti per la configurazione del progetto di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="510ff-265">In **Esplora soluzioni**, in **Ruoli** nel progetto di servizio cloud fare clic con il pulsante destro del mouse su **ContosoAdsWorker**, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="510ff-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="510ff-267">Fare clic sulla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="510ff-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="510ff-268">Impostare **Configurazione servizio** su **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="510ff-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="510ff-269">Selezionare il campo **Valore** per l'impostazione `ContosoAdsDbConnectionString` e quindi incollare la stringa di connessione copiata dalla sezione precedente dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![Stringa di connessione del database per il ruolo di lavoro](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="510ff-271">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="510ff-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="510ff-272">Configurare la soluzione per l'uso dell'account di archiviazione di Azure in caso di esecuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="510ff-273">Le stringhe di connessione per l'account di archiviazione di Azure per il progetto ruolo Web e il progetto ruolo di lavoro sono archiviate nelle impostazioni di ambiente nel progetto di servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="510ff-274">Per ogni progetto è disponibile un insieme di impostazioni distinto da usare quando l'applicazione viene eseguita localmente e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="510ff-275">Saranno aggiornate le impostazioni di ambiente cloud per i progetti di ruolo Web e di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="510ff-276">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **ContosoAdsWeb** nella sezione **Ruoli** del progetto **ContosoAdsCloudService**, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="510ff-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="510ff-278">Fare clic sulla scheda **Impostazioni** . Nella casella di riepilogo **Configurazione servizio** selezionare **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="510ff-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Configurazione del cloud](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="510ff-280">Se si seleziona la voce **StorageConnectionString**, verrà visualizzato un pulsante con puntini di sospensione (**...**) all'estremità destra della riga.</span><span class="sxs-lookup"><span data-stu-id="510ff-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="510ff-281">Fare clic su tale pulsante per aprire la finestra di dialogo **Crea Stringa di connessione all'account di archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="510ff-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![Casella di creazione della stringa di connessione](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="510ff-283">Nella finestra di dialogo **Crea stringa di connessione a risorsa di archiviazione** fare clic su **Sottoscrizione** scegliere l'account di archiviazione creato in precedenza, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="510ff-284">Se non è già stato effettuato l'accesso, saranno richieste le credenziali dell'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Crea Stringa di connessione di archiviazione](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="510ff-286">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="510ff-286">Save your changes.</span></span>
6. <span data-ttu-id="510ff-287">Eseguire la stessa procedura usata per la stringa di connessione `StorageConnectionString` per impostare la stringa di connessione `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="510ff-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="510ff-288">Questa stringa di connessione è usata per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="510ff-289">Eseguire la stessa procedura usata per il ruolo **ContosoAdsWeb** per impostare entrambe le stringhe di connessione per il ruolo **ContosoAdsWorker**.</span><span class="sxs-lookup"><span data-stu-id="510ff-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="510ff-290">Ricordarsi di impostare **Configurazione servizio** su **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="510ff-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="510ff-291">Le impostazioni dell'ambiente di ruolo configurate tramite l'interfaccia utente di Visual Studio sono archiviate nei seguenti file del progetto ContosoAdsCloudService:</span><span class="sxs-lookup"><span data-stu-id="510ff-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="510ff-292">*ServiceDefinition.csdef* : definisce i nomi delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="510ff-293">*ServiceConfiguration.Cloud.cscfg* : fornisce valori per l'esecuzione dell'app nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="510ff-294">*ServiceConfiguration.Local.cscfg* : fornisce valori per l'esecuzione locale dell'app.</span><span class="sxs-lookup"><span data-stu-id="510ff-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="510ff-295">Il file ServiceDefinition.csdef include ad esempio le definizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="510ff-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="510ff-296">E il file *ServiceConfiguration.Cloud.cscfg* include i valori immessi per queste impostazioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="510ff-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="510ff-297">L'impostazione `<Instances>` specifica il numero di macchine virtuali in cui Azure eseguirà il codice del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="510ff-298">La sezione [Passaggi successivi](#next-steps) include collegamenti ad altre informazioni sulla scalabilità orizzontale di un servizio cloud,</span><span class="sxs-lookup"><span data-stu-id="510ff-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="510ff-299">Distribuire il progetto in Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="510ff-300">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto cloud **ContosoAdsCloudService**, quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="510ff-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Menu Pubblica](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="510ff-302">Nel passaggio **Accedi** della procedura guidata **Pubblica applicazione Azure** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="510ff-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Passaggio Accedi](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="510ff-304">Nel passaggio **Impostazioni** della procedura guidata, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="510ff-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![Passaggio Impostazioni](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="510ff-306">Le impostazioni predefinite della scheda **Advanced** sono corrette per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="510ff-307">Per informazioni sulla scheda Avanzate, vedere [Procedura guidata Pubblica l'applicazione Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="510ff-307">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="510ff-308">Nel passaggio **Riepilogo** fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="510ff-308">In the **Summary** step, click **Publish**.</span></span>

    ![Passaggio Riepilogo](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="510ff-310">La finestra **Log attività di Azure** sarà aperta in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="510ff-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="510ff-311">Fare clic sull'icona della freccia verso destra per espandere i dettagli della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="510ff-312">Il completamento della distribuzione richiede fino a 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="510ff-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Finestra Log attività di Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="510ff-314">Quando lo stato della distribuzione è completato, fare clic sull' **URL dell'app Web** per avviare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="510ff-315">È ora possibile testare l'applicazione creando, visualizzando e modificando alcune inserzioni, esattamente come durante l'esecuzione locale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="510ff-316">Al termine dei test, eliminare o arrestare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="510ff-317">Anche se non lo si usa, il servizio cloud accumulerà addebiti, poiché le risorse delle macchine virtuali sono riservate per il servizio.</span><span class="sxs-lookup"><span data-stu-id="510ff-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="510ff-318">Se lo si lascia in esecuzione, chiunque individui l'URL potrà creare e visualizzare inserzioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="510ff-319">Nel [portale di Azure](https://portal.azure.com) passare alla scheda **Panoramica** per il servizio cloud, quindi fare clic sul pulsante **Elimina** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="510ff-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="510ff-320">Se si vuole semplicemente impedire ad altri utenti di accedere al sito, fare invece clic su **Arresta** .</span><span class="sxs-lookup"><span data-stu-id="510ff-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="510ff-321">In questo caso, continueranno a essere generati addebiti.</span><span class="sxs-lookup"><span data-stu-id="510ff-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="510ff-322">È possibile eseguire una procedura analoga per eliminare il database SQL e l'account di archiviazione quando non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="510ff-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="510ff-323">Creazione di un'applicazione completamente nuova</span><span class="sxs-lookup"><span data-stu-id="510ff-323">Create the application from scratch</span></span>
<span data-ttu-id="510ff-324">Se non è stata ancora scaricata l' [applicazione completa](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), scaricarla ora.</span><span class="sxs-lookup"><span data-stu-id="510ff-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="510ff-325">I file del progetto scaricato saranno copiati nel nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="510ff-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="510ff-326">Per creare l'applicazione Contoso Ads sono necessari i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="510ff-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="510ff-327">Creare una soluzione servizio cloud di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="510ff-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="510ff-328">Aggiornare e aggiungere pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="510ff-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="510ff-329">Impostare i riferimenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="510ff-329">Set project references.</span></span>
* <span data-ttu-id="510ff-330">Configurare le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="510ff-330">Configure connection strings.</span></span>
* <span data-ttu-id="510ff-331">Aggiungere file di codice.</span><span class="sxs-lookup"><span data-stu-id="510ff-331">Add code files.</span></span>

<span data-ttu-id="510ff-332">Dopo la creazione della soluzione, esaminare il codice univoco per i progetti di servizio cloud e per i BLOB e le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="510ff-333">Creare una soluzione servizio cloud di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="510ff-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="510ff-334">In Visual Studio scegliere **Nuovo progetto** from the **File** .</span><span class="sxs-lookup"><span data-stu-id="510ff-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="510ff-335">Nel riquadro sinistro della finestra di dialogo **Nuovo progetto** espandere **Visual C#**, scegliere i modelli **Cloud**, quindi selezionare il modello **Servizio cloud di Azure**.</span><span class="sxs-lookup"><span data-stu-id="510ff-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="510ff-336">Assegnare al progetto e alla soluzione il nome ContosoAdsCloudService, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nuovo progetto](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="510ff-338">Nella finestra di dialogo **Nuovo servizio cloud Azure** aggiungere un ruolo Web e un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="510ff-339">Assegnare il nome ContosoAdsWeb al ruolo Web e il nome ContosoAdsWorker al ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="510ff-340">Usare l'icona a forma di matita nel riquadro di destra per modificare i nomi predefiniti dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="510ff-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![Nuovo progetto di servizio cloud](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="510ff-342">Quando appare la finestra di dialogo **Nuovo progetto ASP.NET** per il ruolo Web, scegliere il modello MVC, quindi fare clic su **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="510ff-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![Modifica autenticazione](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="510ff-344">Nella finestra di dialogo **Modifica autenticazione** fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![No Authentication](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="510ff-346">Nella finestra di dialogo **Nuovo progetto ASP.NET** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="510ff-347">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, non su uno dei progetti, quindi scegliere **Aggiungi - Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="510ff-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="510ff-348">Nella finestra di dialogo **Aggiungi nuovo progetto** scegliere **Windows** in **Visual C#** nel riquadro sinistro e quindi fare clic sul modello **Libreria di classi**.</span><span class="sxs-lookup"><span data-stu-id="510ff-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="510ff-349">Assegnare il nome *ContosoAdsCommon*al progetto, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="510ff-350">È necessario che i progetti di ruolo Web e di ruolo di lavoro facciano riferimento al contesto e al modello di dati di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="510ff-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="510ff-351">In alternativa, è possibile definire le classi correlate a Entity Framework nel progetto di ruolo Web e fare riferimento a tale progetto dal progetto di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="510ff-352">Nell'approccio alternativo, tuttavia, il progetto di ruolo di lavoro includerebbe un riferimento ad assembly Web non necessari.</span><span class="sxs-lookup"><span data-stu-id="510ff-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="510ff-353">Aggiornare e aggiungere pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="510ff-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="510ff-354">Aprire la finestra di dialogo **Gestisci pacchetti NuGet** per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="510ff-355">Nella parte superiore della finestra selezionare **Aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="510ff-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="510ff-356">Cercare il pacchetto *WindowsAzure.Storage*. Se è incluso nell'elenco, selezionarlo e selezionare i progetti Web e di lavoro in cui aggiornarlo e quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="510ff-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="510ff-357">La libreria del client di archiviazione viene aggiornata con frequenza maggiore rispetto ai modelli di progetto di Visual Studio. È quindi possibile che la versione disponibile in un progetto appena creato debba essere aggiornata.</span><span class="sxs-lookup"><span data-stu-id="510ff-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="510ff-358">Nella parte superiore della finestra selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="510ff-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="510ff-359">Individuare il pacchetto NuGet *EntityFramework* e installarlo nei tre progetti.</span><span class="sxs-lookup"><span data-stu-id="510ff-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="510ff-360">Trovare il pacchetto NuGet *Microsoft.WindowsAzure.ConfigurationManager* e installarlo nel progetto del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="510ff-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="510ff-361">Configurare le preferenze del progetto</span><span class="sxs-lookup"><span data-stu-id="510ff-361">Set project references</span></span>
1. <span data-ttu-id="510ff-362">Nel progetto ContosoAdsWeb configurare un riferimento al progetto ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="510ff-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="510ff-363">Fare clic con il pulsante destro del mouse sul progetto ContosoAdsWeb, quindi scegliere **Riferimenti** - **Aggiungi riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="510ff-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="510ff-364">Nella finestra di dialogo **Gestione riferimenti** selezionare **Soluzione - Progetti** nel riquadro di sinistra, selezionare **ContosoAdsCommon**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="510ff-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="510ff-365">Nel progetto ContosoAdsWorker configurare un riferimento al progetto ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="510ff-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="510ff-366">ContosoAdsCommon includerà il modello di dati e la classe contesto di Entity Framework, che saranno usati dal front-end e dal back-end.</span><span class="sxs-lookup"><span data-stu-id="510ff-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="510ff-367">Nel progetto ContosoAdsWorker configurare un riferimento a `System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="510ff-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="510ff-368">Questo assembly è usato dal back-end per convertire le immagini in anteprime.</span><span class="sxs-lookup"><span data-stu-id="510ff-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="510ff-369">Configurare le stringhe di connessione</span><span class="sxs-lookup"><span data-stu-id="510ff-369">Configure connection strings</span></span>
<span data-ttu-id="510ff-370">In questa sezione verranno configurate le stringhe di connessione di Archiviazione di Azure e SQL per il test in locale.</span><span class="sxs-lookup"><span data-stu-id="510ff-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="510ff-371">Le istruzioni di distribuzione disponibili in precedenza in questa esercitazione illustrano come configurare le stringhe di connessione per l'esecuzione dell'app nel cloud.</span><span class="sxs-lookup"><span data-stu-id="510ff-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="510ff-372">Nel progetto ContosoAdsWeb aprire il file Web.config dell'applicazione e inserire il seguente elemento `connectionStrings` dopo l'elemento `configSections`.</span><span class="sxs-lookup"><span data-stu-id="510ff-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="510ff-373">Se si usa Visual Studio 2015 o versione successiva, sostituire "v11.0" con "MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="510ff-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="510ff-374">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="510ff-374">Save your changes.</span></span>
3. <span data-ttu-id="510ff-375">Nel progetto ContosoAdsCloudService fare clic con il pulsante destro del mouse su ContosoAdsWeb in **Ruoli**, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="510ff-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Proprietà del ruolo](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="510ff-377">Nella finestra delle proprietà di **ContosAdsWeb [Role]** fare clic sulla scheda **Impostazioni**, quindi su **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="510ff-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="510ff-378">Lasciare l'opzione **Configurazione servizio** impostata su **Tutte le configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="510ff-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="510ff-379">Aggiungere un'impostazione denominata *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="510ff-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="510ff-380">Impostare il **Tipo** su *ConnectionString*, quindi impostare il **Valore** su *UseDevelopmentStorage=true*.</span><span class="sxs-lookup"><span data-stu-id="510ff-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![Nuova stringa di connessione](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="510ff-382">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="510ff-382">Save your changes.</span></span>
7. <span data-ttu-id="510ff-383">Eseguire la stessa procedura per aggiungere una stringa di connessione di archiviazione nelle proprietà del ruolo ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="510ff-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="510ff-384">Nella finestra delle proprietà di **ContosoAdsWorker [Ruolo]** aggiungere un'altra stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="510ff-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="510ff-385">Nome: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="510ff-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="510ff-386">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="510ff-386">Type: String</span></span>
   * <span data-ttu-id="510ff-387">Valore: incollare la stessa stringa di connessione usata per il progetto di ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="510ff-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="510ff-388">L'esempio seguente si riferisce a Visual Studio 2013,</span><span class="sxs-lookup"><span data-stu-id="510ff-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="510ff-389">quindi se si copia questo esempio e si usa Visual Studio 2015 o versione successiva è necessario modificare l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="510ff-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="510ff-390">Aggiungere file di codice</span><span class="sxs-lookup"><span data-stu-id="510ff-390">Add code files</span></span>
<span data-ttu-id="510ff-391">In questa sezione, i file di codice saranno copiati dalla soluzione scaricata alla nuova soluzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="510ff-392">Le sezioni seguenti illustrano e spiegano parti chiave del codice.</span><span class="sxs-lookup"><span data-stu-id="510ff-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="510ff-393">Per aggiungere file a un progetto o a una cartella, fare clic con il pulsante destro del mouse sul progetto o sulla cartella, quindi scegliere **Aggiungi** - **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="510ff-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="510ff-394">Selezionare i file da aggiungere, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="510ff-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="510ff-395">Se viene richiesto di confermare che si vogliono sostituire i file esistenti, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="510ff-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="510ff-396">Nel progetto ContosoAdsCommon eliminare il file *Class1.cs* e sostituirlo con i file *Ad.cs* e *ContosoAdscontext.cs* dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="510ff-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="510ff-397">Nel progetto ContosoAdsWeb aggiungere i file seguenti dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="510ff-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="510ff-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="510ff-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="510ff-399">Nella cartella *Views\Shared*: *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="510ff-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="510ff-400">Nella cartella *Views\Home*: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="510ff-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="510ff-401">Nella cartella *Controllers*: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="510ff-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="510ff-402">Nella cartella *Views\Ad* (creare prima di tutto la cartella): cinque file *.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="510ff-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="510ff-403">Nel progetto ContosoAdsWorker aggiungere il file *WorkerRole.cs* dal progetto scaricato.</span><span class="sxs-lookup"><span data-stu-id="510ff-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="510ff-404">È ora possibile compilare ed eseguire l'applicazione come indicato in precedenza nell'organizzazione e l'app userà le risorse locali del database e dell'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="510ff-405">Le sezioni seguenti illustrano il codice correlato all'uso dell'ambiente, dei BLOB e delle code di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="510ff-406">Questa esercitazione non spiega come creare controlli e visualizzazioni MVC usando lo scaffolding, come scrivere codice di Entity Framework da usare con database SQL Server oppure le nozioni di base della programmazione asincrona in ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="510ff-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="510ff-407">Per informazioni su questi argomenti, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="510ff-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="510ff-408">Introduzione a MVC 5</span><span class="sxs-lookup"><span data-stu-id="510ff-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="510ff-409">Introduzione a EF 6 e MVC 5</span><span class="sxs-lookup"><span data-stu-id="510ff-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="510ff-410">[Introduzione alla programmazione asincrona in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="510ff-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="510ff-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="510ff-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="510ff-412">Il file Ad.cs definisce un'enumerazione per le categorie di inserzione e una classe di entità POCO per le informazioni sulle inserzioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="510ff-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="510ff-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="510ff-414">La classe ContosoAdsContext specifica che la classe Ad è usata in una raccolta DbSet, che sarà archiviata da Entity Framework in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="510ff-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="510ff-415">La classe ha due costruttori.</span><span class="sxs-lookup"><span data-stu-id="510ff-415">The class has two constructors.</span></span> <span data-ttu-id="510ff-416">Il primo è usato dal progetto Web e specifica il nome di una stringa di connessione archiviata nel file Web.config.</span><span class="sxs-lookup"><span data-stu-id="510ff-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="510ff-417">Il secondo costruttore permette di passare la stringa di connessione effettiva usata dal progetto di ruolo di lavoro, non avendo questo un file Web.config.</span><span class="sxs-lookup"><span data-stu-id="510ff-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="510ff-418">In precedenza è stato indicato il percorso di archiviazione di questa stringa di connessione e più avanti sarà illustrato il modo in cui il codice recupera la stringa di connessione durante la creazione di istanze della classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="510ff-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="510ff-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="510ff-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="510ff-420">Il codice chiamato dal metodo `Application_Start` crea un contenitore BLOB *images* e una coda *images*, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="510ff-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="510ff-421">In questo modo, ogni volta che si inizia a usare un nuovo account di archiviazione o a usare l'emulatore di archiviazione in un nuovo computer, il contenitore BLOB e la coda necessari saranno creati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="510ff-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="510ff-422">Il codice ottiene l'accesso all'account di archiviazione tramite la stringa di connessione del file *.cscfg* .</span><span class="sxs-lookup"><span data-stu-id="510ff-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="510ff-423">Ottiene quindi un riferimento al contenitore BLOB *images* , crea il contenitore se non esiste già e configura le autorizzazioni di accesso nel nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="510ff-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="510ff-424">Per impostazione predefinita, i nuovi contenitori permettono l'accesso ai BLOB solo ai client con credenziali dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="510ff-425">Per il sito Web è necessario che i BLOB siano pubblici, in modo che sia possibile visualizzare immagini usando gli URL che fanno riferimento ai BLOB delle immagini.</span><span class="sxs-lookup"><span data-stu-id="510ff-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="510ff-426">Tramite codice analogo si ottiene un riferimento alla coda *images* e si crea una nuova coda.</span><span class="sxs-lookup"><span data-stu-id="510ff-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="510ff-427">In questo caso non sono necessarie modifiche alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="510ff-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="510ff-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="510ff-429">Il file *_Layout.cshtml* imposta il nome dell'app nell'intestazione e nel piè di pagina e crea una voce di menu "Ads" (Annunci).</span><span class="sxs-lookup"><span data-stu-id="510ff-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="510ff-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="510ff-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="510ff-431">Il file *Views\Home\Index.cshtml* visualizza i collegamenti di categoria nella home page.</span><span class="sxs-lookup"><span data-stu-id="510ff-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="510ff-432">I collegamenti passano il valore Integer dell'enumerazione `Category` in una variabile querystring alla pagina Ads Index.</span><span class="sxs-lookup"><span data-stu-id="510ff-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="510ff-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="510ff-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="510ff-434">Nel file *AdController.cs* il costruttore chiama il metodo `InitializeStorage` per creare oggetti della libreria del client di Archiviazione di Azure che forniscono un'API per l'uso di BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="510ff-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="510ff-435">Il codice ottiene quindi un riferimento al contenitore BLOB *images*, come illustrato in precedenza in *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="510ff-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="510ff-436">Durante questa operazione, imposta un [criterio per l'esecuzione di nuovi tentativi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) predefinito appropriato per un'app Web.</span><span class="sxs-lookup"><span data-stu-id="510ff-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="510ff-437">Il criterio per l'esecuzione di nuovi tentativi predefinito per il backoff esponenziale potrebbe sospendere l'app Web per più di un minuto in caso di nuovi tentativi ripetuti per un errore temporaneo.</span><span class="sxs-lookup"><span data-stu-id="510ff-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="510ff-438">Il criterio di ripetizione dei tentativi specificato qui attende tre secondi dopo ogni tentativo, fino a un massimo di tre tentativi.</span><span class="sxs-lookup"><span data-stu-id="510ff-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="510ff-439">Tramite codice analogo si ottiene un riferimento alla coda *images* .</span><span class="sxs-lookup"><span data-stu-id="510ff-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="510ff-440">La maggior parte del codice del controller è tipica per l'uso di un modello di dati Entity Framework con una classe DbContext.</span><span class="sxs-lookup"><span data-stu-id="510ff-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="510ff-441">Un'eccezione è costituita dal metodo `Create` HttpPost che carica un file e lo salva nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="510ff-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="510ff-442">Lo strumento di associazione di modelli fornisce un oggetto [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) al metodo.</span><span class="sxs-lookup"><span data-stu-id="510ff-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="510ff-443">Se l'utente ha selezionato un file da caricare, il codice carica il file, lo salva in un BLOB e aggiorna il record del database Ad con un URL che fa riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="510ff-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="510ff-444">Il codice che esegue il caricamento si trova nel metodo `UploadAndSaveBlobAsync` .</span><span class="sxs-lookup"><span data-stu-id="510ff-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="510ff-445">Crea un nome GUID per il BLOB, aggiorna e salva il file, quindi restituisce un riferimento al BLOB salvato.</span><span class="sxs-lookup"><span data-stu-id="510ff-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="510ff-446">Dopo aver caricato un BLOB e aggiornato il database, il metodo `Create` HttpPost crea un messaggio di coda per segnalare al processo back-end che un'immagine è pronta per la conversione in anteprima.</span><span class="sxs-lookup"><span data-stu-id="510ff-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="510ff-447">Il codice per il metodo `Edit` HttpPost è simile, con la differenza che se l'utente seleziona un nuovo file immagine, sarà necessario eliminare eventuali BLOB già esistenti.</span><span class="sxs-lookup"><span data-stu-id="510ff-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="510ff-448">L’esempio successivo riporta il codice per l'eliminazione dei BLOB in caso di eliminazione di un'inserzione.</span><span class="sxs-lookup"><span data-stu-id="510ff-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="510ff-449">ContosoAdsWeb - Views\Ad\Index.cshtml e Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="510ff-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="510ff-450">Il file *Index.cshtml* mostra le anteprime insieme agli altri dati delle inserzioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="510ff-451">Il file *Details.cshtml* mostra l'immagine con dimensioni normali.</span><span class="sxs-lookup"><span data-stu-id="510ff-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="510ff-452">ContosoAdsWeb - Views\Ad\Create.cshtml ed Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="510ff-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="510ff-453">I file *Create.cshtml* e *Edit.cshtml* specificano la codifica di moduli che permette al controller di ottenere l'oggetto `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="510ff-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="510ff-454">Un elemento `<input>` segnala al browser che è necessario fornire una finestra di selezione del file.</span><span class="sxs-lookup"><span data-stu-id="510ff-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="510ff-455">ContosoAdsWorker - WorkerRole.cs - Metodo OnStart</span><span class="sxs-lookup"><span data-stu-id="510ff-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="510ff-456">L'ambiente del ruolo di lavoro di Azure chiama il metodo `OnStart` nella classe `WorkerRole` durante la fase di avvio del ruolo di lavoro e chiama il metodo `Run` al termine dell'esecuzione del metodo `OnStart`.</span><span class="sxs-lookup"><span data-stu-id="510ff-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="510ff-457">Il metodo `OnStart` ottiene la stringa di connessione del database dal file con estensione *cscfg* e la passa alla classe DbContext di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="510ff-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="510ff-458">Per impostazione predefinita, sarà usato il provider SQLClient. Non è quindi necessario specificare alcun provider.</span><span class="sxs-lookup"><span data-stu-id="510ff-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="510ff-459">In seguito, il metodo ottiene un riferimento all'account di archiviazione e crea il contenitore BLOB e la coda, se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="510ff-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="510ff-460">Il codice da usare è simile a quello già usato per il metodo `Application_Start` del ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="510ff-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="510ff-461">ContosoAdsWorker - WorkerRole.cs - Metodo Run</span><span class="sxs-lookup"><span data-stu-id="510ff-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="510ff-462">Il metodo `Run` è chiamato al termine del processo di inizializzazione del metodo `OnStart`.</span><span class="sxs-lookup"><span data-stu-id="510ff-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="510ff-463">Il metodo esegue un ciclo infinito che cerca nuovi messaggi di coda e li elabora quando arrivano.</span><span class="sxs-lookup"><span data-stu-id="510ff-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="510ff-464">Dopo ogni iterazione del ciclo, se non sono stati trovati messaggi di coda, il programma rimane inattivo per un secondo.</span><span class="sxs-lookup"><span data-stu-id="510ff-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="510ff-465">Ciò impedisce al ruolo di lavoro di generare costi eccessivi relativi al tempo della CPU e alle transazioni di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="510ff-466">Come ricordato da Microsoft Customer Advisory Team, uno sviluppatore aveva scordato di includere questo dettaglio, aveva eseguito la distribuzione in produzione ed era partito per le ferie.</span><span class="sxs-lookup"><span data-stu-id="510ff-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="510ff-467">Al ritorno, si era reso conto che la dimenticanza era costata più cara delle ferie.</span><span class="sxs-lookup"><span data-stu-id="510ff-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="510ff-468">A volte il contenuto di un messaggio di coda provoca un errore di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="510ff-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="510ff-469">Questo messaggio è definito un *messaggio non elaborabile*. Se è stato appena registrato un errore e il ciclo è stato riavviato, è possibile che si tenti di elaborare questo messaggio all'infinito.</span><span class="sxs-lookup"><span data-stu-id="510ff-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="510ff-470">Il blocco CATCH include quindi un'istruzione IF che verifica il numero di volte in cui l'app ha tentato di elaborare il messaggio corrente. Se il numero è superiore a 5, il messaggio sarà eliminato dalla coda.</span><span class="sxs-lookup"><span data-stu-id="510ff-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="510ff-471">`ProcessQueueMessage` è chiamato quando viene trovato un messaggio della coda.</span><span class="sxs-lookup"><span data-stu-id="510ff-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="510ff-472">Questo codice legge il database per ottenere l'URL dell'immagine. converte l'immagine in un'anteprima, salva l'anteprima in un BLOB, aggiorna il database con l'URL del BLOB dell'anteprima ed elimina il messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="510ff-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="510ff-473">Il codice nel metodo `ConvertImageToThumbnailJPG` usa le classi disponibili nello spazio dei nomi System.Drawing per maggiore semplicità.</span><span class="sxs-lookup"><span data-stu-id="510ff-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="510ff-474">Le classi in questo spazio dei nomi, tuttavia, sono state progettate per l'uso con Windows Form.</span><span class="sxs-lookup"><span data-stu-id="510ff-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="510ff-475">Non sono supportate per l'uso in un servizio Windows o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="510ff-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="510ff-476">Per altre informazioni sulle opzioni di elaborazione delle immagini, vedere [Generazione dinamica delle immagini](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) e [Informazioni dettagliate sul ridimensionamento delle immagini](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="510ff-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="510ff-477">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="510ff-477">Troubleshooting</span></span>
<span data-ttu-id="510ff-478">In caso di problemi durante l'esecuzione delle istruzioni di questa esercitazione, di seguito sono indicati alcuni errori comuni e le relative soluzioni.</span><span class="sxs-lookup"><span data-stu-id="510ff-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="510ff-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="510ff-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="510ff-480">L'oggetto `RoleEnvironment` è fornito da Azure quando si esegue un'applicazione in Azure o in caso di esecuzione in modalità locale tramite l'emulatore di calcolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="510ff-481">Se questo errore è visualizzato durante l'esecuzione locale, assicurarsi di avere impostato il progetto ContosoAdsCloudService come progetto di avvio.</span><span class="sxs-lookup"><span data-stu-id="510ff-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="510ff-482">In questo modo, il progetto sarà configurato per l'esecuzione con l'emulatore di calcolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="510ff-483">L'applicazione usa RoleEnvironment di Azure anche per ottenere i valori delle stringhe di connessione archiviati nei file con estensione *cscfg*. È quindi possibile che questa eccezione sia generata da una stringa di connessione mancante.</span><span class="sxs-lookup"><span data-stu-id="510ff-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="510ff-484">Assicurarsi di avere creato l'impostazione StorageConnectionString per entrambe le configurazioni, cloud e locale, nel progetto ContosoAdsWeb e di avere creato entrambe le stringhe di connessione per entrambe le configurazioni nel progetto ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="510ff-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="510ff-485">Se si esegue una ricerca di tipo **Trova tutto** per StorageConnectionString nell'intera soluzione, dovrebbero essere rilevate 9 occorrenze in 6 file.</span><span class="sxs-lookup"><span data-stu-id="510ff-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="510ff-486">Non è possibile eseguire l'override sulla porta xxx.</span><span class="sxs-lookup"><span data-stu-id="510ff-486">Cannot override to port xxx.</span></span> <span data-ttu-id="510ff-487">Nuova porta con valore inferiore al minimo consentito 8080 per HTTP protocollo</span><span class="sxs-lookup"><span data-stu-id="510ff-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="510ff-488">Provare a cambiare il numero di porta usato dal progetto Web.</span><span class="sxs-lookup"><span data-stu-id="510ff-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="510ff-489">Fare clic con il pulsante destro del mouse sul progetto ContosoAdsWeb, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="510ff-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="510ff-490">Fare clic sulla scheda **Web**, quindi cambiare il numero di porta nell'impostazione **URL progetto**.</span><span class="sxs-lookup"><span data-stu-id="510ff-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="510ff-491">Per un'altra soluzione alternativa che potrebbe risolvere il problema, vedere la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="510ff-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="510ff-492">Altri errori durante l'esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="510ff-492">Other errors when running locally</span></span>
<span data-ttu-id="510ff-493">Per impostazione predefinita, i nuovi progetti di servizio cloud usano l'emulatore di calcolo rapido di Azure per simulare l'ambiente di Azure.</span><span class="sxs-lookup"><span data-stu-id="510ff-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="510ff-494">Si tratta di una versione semplificata dell'emulatore di calcolo e in alcuni casi l'emulatore di calcolo completo funzionerà mentre la versione rapida non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="510ff-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="510ff-495">Per modificare il progetto in modo che usi l'emulatore completo, fare clic con il pulsante destro del mouse sul progetto ContosoAdsCloudService, quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="510ff-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="510ff-496">Nella finestra **Proprietà** fare clic sulla scheda **Web**, quindi selezionare il pulsante di opzione **Usa emulatore completo**.</span><span class="sxs-lookup"><span data-stu-id="510ff-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="510ff-497">Per eseguire l'applicazione con l'emulatore completo, sarà necessario aprire Visual Studio con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="510ff-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="510ff-498">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="510ff-498">Next steps</span></span>
<span data-ttu-id="510ff-499">L'applicazione Contoso Ads è intenzionalmente semplice, in modo da essere idonea per un'esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="510ff-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="510ff-500">Ad esempio, non implementa l'[inserimento di dipendenze](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) o i [modelli di archivio e unità di lavoro](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), non usa un'[interfaccia per l'elaborazione](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), non usa [migrazioni Code First EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire le modifiche ai modelli di dati o la [resilienza di connessione EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) per gestire gli errori di rete temporanei e così via.</span><span class="sxs-lookup"><span data-stu-id="510ff-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="510ff-501">Di seguito sono indicate alcune applicazioni di esempio per servizi cloud che illustrano procedure di codifica più simili a quelle del mondo reale, elencate in ordine di complessità crescente:</span><span class="sxs-lookup"><span data-stu-id="510ff-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="510ff-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="510ff-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="510ff-503">Concettualmente simile a Contoso Ads, implementa però più funzionalità e procedure più simili a quelle del mondo reale.</span><span class="sxs-lookup"><span data-stu-id="510ff-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="510ff-504">[Applicazione multilivello di Servizi cloud di Azure con tabelle, code e BLOB](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="510ff-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="510ff-505">Introduce le tabelle di archiviazione di Azure, nonché i BLOB e le code.</span><span class="sxs-lookup"><span data-stu-id="510ff-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="510ff-506">Basata su una versione precedente di Azure SDK per .NET, richiederà alcune modifiche per funzionare con la versione corrente.</span><span class="sxs-lookup"><span data-stu-id="510ff-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="510ff-507">[Nozioni fondamentali su Servizi cloud in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="510ff-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="510ff-508">Un esempio completo che illustra una vasta gamma di procedure consigliate, creato dal gruppo Microsoft Patterns and Practices.</span><span class="sxs-lookup"><span data-stu-id="510ff-508">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="510ff-509">Per informazioni generali sullo sviluppo per il cloud, vedere l'articolo relativo alla [creazione di applicazioni cloud funzionanti con Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="510ff-509">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="510ff-510">Per un video introduttivo relativo alle procedure consigliate e ai modelli per Archiviazione di Azure, vedere il video relativo a [novità, procedure consigliate e modelli per Archiviazione di Microsoft Azure](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="510ff-510">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="510ff-511">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="510ff-511">For more information, see the following resources:</span></span>

* [<span data-ttu-id="510ff-512">Servizi cloud di Azure - Parte 1: Introduzione</span><span class="sxs-lookup"><span data-stu-id="510ff-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="510ff-513">Come gestire i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="510ff-513">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="510ff-514">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="510ff-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="510ff-515">Come scegliere un provider di servizi cloud</span><span class="sxs-lookup"><span data-stu-id="510ff-515">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
