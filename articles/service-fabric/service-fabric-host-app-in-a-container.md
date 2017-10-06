---
title: un'applicazione .NET in tooAzure un contenitore Service Fabric aaaDeploy | Documenti Microsoft
description: Spiega in che modo un'applicazione .NET in Visual Studio in un contenitore Docker toopackage. Questa nuova app "container" viene quindi distribuita tooa cluster di Service Fabric.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="ad131-104">Distribuire un'applicazione .NET in un tooAzure di contenitore di Windows Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ad131-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="ad131-105">In questa esercitazione illustra come toodeploy un'applicazione ASP.NET esistente in un contenitore di Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="ad131-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="ad131-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="ad131-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad131-107">Creare un progetto Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad131-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="ad131-108">Distribuire un'applicazione esistente in un contenitore</span><span class="sxs-lookup"><span data-stu-id="ad131-108">Containerize an existing application</span></span>
> * <span data-ttu-id="ad131-109">Configurare l'integrazione continua con Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="ad131-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad131-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ad131-110">Prerequisites</span></span>

1. <span data-ttu-id="ad131-111">Installare [Docker CE per Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) in modo da poter eseguire i contenitori in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ad131-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="ad131-112">Acquisire familiarità con hello [Guida introduttiva di contenitori di Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="ad131-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="ad131-113">Scaricare hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="ad131-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="ad131-114">Installare [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="ad131-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="ad131-115">Installare hello [estensione strumenti di distribuzione continua per Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="ad131-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="ad131-116">Creare una [sottoscrizione di Azure][link-azure-subscription] e un [account di Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="ad131-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="ad131-117">Creare un cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="ad131-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="ad131-118">Un'applicazione hello inserita in un contenitore</span><span class="sxs-lookup"><span data-stu-id="ad131-118">Containerize hello application</span></span>

<span data-ttu-id="ad131-119">Dopo avere creato un [cluster di Service Fabric è in esecuzione in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) si toocreate pronto e distribuire un'applicazione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="ad131-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="ad131-120">toostart in esecuzione l'applicazione in un contenitore, è necessario tooadd **Docker supporto** toohello progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad131-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="ad131-121">Quando si aggiungono **supporto Docker** toohello applicazione, si verifica quanto segue.</span><span class="sxs-lookup"><span data-stu-id="ad131-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="ad131-122">Innanzitutto, un _Dockerfile_ è stato aggiunto il progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="ad131-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="ad131-123">Questo nuovo file viene descritto come immagine contenitore hello è toobe compilato.</span><span class="sxs-lookup"><span data-stu-id="ad131-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="ad131-124">Quindi secondo, con un nuovo _comporre docker_ progetto viene aggiunto toohello soluzione.</span><span class="sxs-lookup"><span data-stu-id="ad131-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="ad131-125">nuovo progetto Hello contiene alcuni docker-comporre i file.</span><span class="sxs-lookup"><span data-stu-id="ad131-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="ad131-126">Comporre docker file possono essere utilizzati toodescribe le modalità di esecuzione contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="ad131-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="ad131-127">Per altre informazioni, vedere [Visual Studio Container Tools][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="ad131-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="ad131-128">Se è hello prima volta che si eseguono le immagini contenitore di Windows nel computer in uso, Docker CE necessario abbassare di immagini di base per i contenitori di hello.</span><span class="sxs-lookup"><span data-stu-id="ad131-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="ad131-129">le immagini di Hello utilizzate in questa esercitazione sono 14 GB.</span><span class="sxs-lookup"><span data-stu-id="ad131-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="ad131-130">Procedo ed eseguo hello seguendo le immagini di base hello toopull comando terminal:</span><span class="sxs-lookup"><span data-stu-id="ad131-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="ad131-131">Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="ad131-131">Add Docker support</span></span>

<span data-ttu-id="ad131-132">Aprire hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad131-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="ad131-133">Pulsante destro del mouse hello **FabrikamFiber.Web** progetto > **Aggiungi** > **Docker supporto**.</span><span class="sxs-lookup"><span data-stu-id="ad131-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="ad131-134">Aggiungere il supporto per SQL</span><span class="sxs-lookup"><span data-stu-id="ad131-134">Add support for SQL</span></span>

<span data-ttu-id="ad131-135">Questa applicazione Usa SQL come provider di dati hello, in modo da un server SQL è un'applicazione hello toorun obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="ad131-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="ad131-136">Fare riferimento a un'immagine del contenitore SQL Server nel file docker-compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="ad131-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="ad131-137">In Visual Studio, aprire **Esplora**, trovare **comporre docker**e i file aperti hello **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="ad131-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="ad131-138">Passare toohello `services:` nodo, aggiungere un nodo denominato `db:` che definisce una voce di SQL Server hello per contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="ad131-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="ad131-139">Per il debug locale è possibile usare un'istanza di SQL Server a scelta, a condizione che sia raggiungibile dall'host.</span><span class="sxs-lookup"><span data-stu-id="ad131-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="ad131-140">**localdb**, tuttavia, non supporta la comunicazione `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="ad131-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="ad131-141">L'esecuzione di SQL Server in un contenitore non consente di rendere persistenti i dati.</span><span class="sxs-lookup"><span data-stu-id="ad131-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="ad131-142">Quando si arresta il contenitore di hello, i dati vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="ad131-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="ad131-143">Non usare questa configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="ad131-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="ad131-144">Passare toohello `fabrikamfiber.web:` nodo e aggiungere un nodo figlio denominato `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="ad131-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="ad131-145">Ciò garantisce che hello `db` avvio del servizio (contenitore di SQL Server hello) prima che l'applicazione web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="ad131-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="ad131-146">Aggiornamento configurazione web hello</span><span class="sxs-lookup"><span data-stu-id="ad131-146">Update hello web config</span></span>

<span data-ttu-id="ad131-147">In hello **FabrikamFiber.Web** del progetto, stringa di connessione di aggiornamento hello in hello **Web. config** file toopoint toohello SQL Server nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="ad131-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="ad131-148">Se si desidera creare un Server SQL diverso durante la compilazione di una versione dell'applicazione web toouse, aggiungere un altro file web.release.config tooyour della stringa connessione.</span><span class="sxs-lookup"><span data-stu-id="ad131-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="ad131-149">Testare il contenitore</span><span class="sxs-lookup"><span data-stu-id="ad131-149">Test your container</span></span>

<span data-ttu-id="ad131-150">Premere **F5** nel contenitore di un'applicazione hello toorun ed eseguire il debug.</span><span class="sxs-lookup"><span data-stu-id="ad131-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="ad131-151">Bordo verrà visualizzata la pagina di avvio definite dell'applicazione utilizzando l'indirizzo IP hello del contenitore hello in rete NAT interna hello (in genere 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="ad131-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="ad131-152">toolearn ulteriori informazioni su debug di applicazioni in contenitori usando Visual Studio 2017, vedere [questo articolo][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="ad131-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![esempio di fabrikam in un contenitore][image-web-preview]

<span data-ttu-id="ad131-154">contenitore Hello è ora pronto toobe compilato e compresso in un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad131-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="ad131-155">Dopo aver creato immagine contenitore hello compilato nel computer, è possibile inviare del Registro di sistema di tooany contenitore ed estrarlo tooany host toorun verso il basso.</span><span class="sxs-lookup"><span data-stu-id="ad131-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="ad131-156">Prepararsi per il cloud hello applicazione hello</span><span class="sxs-lookup"><span data-stu-id="ad131-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="ad131-157">applicazione hello tooget pronta per l'esecuzione nell'infrastruttura di servizio in Azure, è necessario toocomplete due passaggi:</span><span class="sxs-lookup"><span data-stu-id="ad131-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="ad131-158">Esporre porta hello in cui desideriamo tooreach in grado di toobe l'applicazione web in cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ad131-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="ad131-159">Predisporre un database SQL di produzione pronto per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad131-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="ad131-160">Esporre porta hello per app hello</span><span class="sxs-lookup"><span data-stu-id="ad131-160">Expose hello port for hello app</span></span>
<span data-ttu-id="ad131-161">cluster di Service Fabric Hello è stato configurato, è la porta *80* aperta per impostazione predefinita in hello bilanciamento del carico di Azure, che consente di bilanciare cluster toohello di traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="ad131-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="ad131-162">È possibile esporre il contenitore su questa porta tramite il file docker-compose.ym.</span><span class="sxs-lookup"><span data-stu-id="ad131-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="ad131-163">In Visual Studio, aprire **Esplora**, trovare **comporre docker**e i file aperti hello **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="ad131-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="ad131-164">Modificare hello `fabrikamfiber.web:` nodo, aggiungere un nodo figlio denominato `ports:`.</span><span class="sxs-lookup"><span data-stu-id="ad131-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="ad131-165">Aggiungere una voce di stringa `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="ad131-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="ad131-166">Usare un database SQL di produzione</span><span class="sxs-lookup"><span data-stu-id="ad131-166">Use a production SQL database</span></span>
<span data-ttu-id="ad131-167">Durante l'esecuzione nell'ambiente di produzione, è necessario mantenere i dati persistenti nel database.</span><span class="sxs-lookup"><span data-stu-id="ad131-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="ad131-168">Non sono attualmente disponibili dati di permanente di tooguarantee modo in un contenitore, pertanto non è possibile archiviare dati di produzione in SQL Server in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="ad131-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="ad131-169">È consigliabile usare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad131-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="ad131-170">tooset backup ed eseguire un Server gestito di SQL in Azure, visitare hello [Guida introduttiva di Azure SQL Database] [ link-azure-sql] articolo.</span><span class="sxs-lookup"><span data-stu-id="ad131-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="ad131-171">Occorre ricordare che toochange hello connessione stringhe toohello SQL server in hello **web.release.config** file hello **FabrikamFiber.Web** progetto.</span><span class="sxs-lookup"><span data-stu-id="ad131-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="ad131-172">Questa applicazione non funziona correttamente se i database SQL non sono raggiungibili.</span><span class="sxs-lookup"><span data-stu-id="ad131-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="ad131-173">È possibile scegliere toogo-ahead e distribuire un'applicazione hello senza un server SQL.</span><span class="sxs-lookup"><span data-stu-id="ad131-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="ad131-174">Distribuire con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ad131-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="ad131-175">tooset la distribuzione in Visual Studio Team Services, è necessario hello tooinstall [estensione strumenti di distribuzione continua per Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="ad131-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="ad131-176">Questa estensione rende facile toodeploy tooAzure tramite la configurazione di Visual Studio Team Services e ottenere il cluster di Service Fabric tooyour app distribuita.</span><span class="sxs-lookup"><span data-stu-id="ad131-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="ad131-177">tooget avviato, il codice deve essere ospitato in controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="ad131-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="ad131-178">resto Hello di questa sezione presuppone **git** è in uso.</span><span class="sxs-lookup"><span data-stu-id="ad131-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="ad131-179">Configurare un repository VSTS</span><span class="sxs-lookup"><span data-stu-id="ad131-179">Set up a VSTS repo</span></span>
<span data-ttu-id="ad131-180">Nell'angolo in basso a destra di hello di Visual Studio, fare clic su **aggiungere tooSource controllo** > **Git** (o qualsiasi opzione desiderato).</span><span class="sxs-lookup"><span data-stu-id="ad131-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Premere il pulsante controllo origine hello][image-source-control]

<span data-ttu-id="ad131-182">In hello _Team Explorer_ riquadro, premere **pubblicare repository Git**.</span><span class="sxs-lookup"><span data-stu-id="ad131-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="ad131-183">Selezionare il nome dell'archivio VSTS e premere **Repository**.</span><span class="sxs-lookup"><span data-stu-id="ad131-183">Select your VSTS repository name and press **Repository**.</span></span>

![pubblicare tooVSTS repository][image-publish-repo]

<span data-ttu-id="ad131-185">Ora che il codice è sincronizzato con l'archivio del codice sorgente VSTS, è possibile configurare la distribuzione continua e il recapito continuo.</span><span class="sxs-lookup"><span data-stu-id="ad131-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="ad131-186">Configurare il recapito continuo</span><span class="sxs-lookup"><span data-stu-id="ad131-186">Setup continuous delivery</span></span>

<span data-ttu-id="ad131-187">In _Esplora_, hello rapida **soluzione** > **configurare la distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="ad131-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="ad131-188">Selezionare hello sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="ad131-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="ad131-189">Impostare **tipo Host** troppo**Cluster di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="ad131-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="ad131-190">Impostare **Host di destinazione** creato nella sezione precedente hello cluster di toohello service fabric.</span><span class="sxs-lookup"><span data-stu-id="ad131-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="ad131-191">Scegliere un **Registro di sistema contenitore** toopublish nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="ad131-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="ad131-192">Hello utilizzare **modifica** pulsante toocreate del Registro di sistema un contenitore.</span><span class="sxs-lookup"><span data-stu-id="ad131-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="ad131-193">Premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad131-193">Press **OK**.</span></span>

![impostazione dell'integrazione continua di Service Fabric][image-setup-ci]
   
   <span data-ttu-id="ad131-195">Una volta completata la configurazione hello, il contenitore è distribuito tooService dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="ad131-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="ad131-196">Ogni volta che si esegue il push del repository toohello aggiornamenti viene eseguita una nuova compilazione e versione.</span><span class="sxs-lookup"><span data-stu-id="ad131-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ad131-197">Immagini contenitore di compilazione hello necessari circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="ad131-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="ad131-198">cluster Service Fabric toohello Hello prima distribuzione comporta hello base Windows Server Core contenitore immagini toobe scaricato.</span><span class="sxs-lookup"><span data-stu-id="ad131-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="ad131-199">download di Hello accetta toocomplete aggiuntive 5-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="ad131-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="ad131-200">Esplora applicazione Fabrikam Call Center toohello utilizzando url hello del cluster: ad esempio, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="ad131-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="ad131-201">Ora che si dispone di contenitore e di soluzione Fabrikam Call Center hello distribuita, è possibile aprire hello [portale di Azure] [ link-azure-portal] e vedere applicazione hello in esecuzione nell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="ad131-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="ad131-202">un'applicazione hello tootry, aprire un web browser e passare toohello URL del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad131-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad131-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad131-203">Next steps</span></span>

<span data-ttu-id="ad131-204">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="ad131-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ad131-205">Creare un progetto Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad131-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="ad131-206">Distribuire un'applicazione esistente in un contenitore</span><span class="sxs-lookup"><span data-stu-id="ad131-206">Containerize an existing application</span></span>
> * <span data-ttu-id="ad131-207">Configurare l'integrazione continua con Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="ad131-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
