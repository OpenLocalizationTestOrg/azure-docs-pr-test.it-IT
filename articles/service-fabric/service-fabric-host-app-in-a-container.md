---
title: Distribuire un'applicazione .NET in un contenitore in Azure Service Fabric | Microsoft Docs
description: Viene illustrato come creare un pacchetto di un'applicazione .NET in Visual Studio in un contenitore Docker. La nuova app "contenitore" viene quindi distribuita in un cluster di Service Fabric.
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
ms.openlocfilehash: 484db494e7975df950543d19bf841a4df7cdd139
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-to-azure-service-fabric"></a><span data-ttu-id="c94ec-104">Distribuire un'applicazione .NET in un contenitore Windows in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c94ec-104">Deploy a .NET application in a Windows container to Azure Service Fabric</span></span>

<span data-ttu-id="c94ec-105">Questa esercitazione illustra come distribuire un'applicazione ASP.NET esistente in un contenitore Windows in Azure.</span><span class="sxs-lookup"><span data-stu-id="c94ec-105">This tutorial shows you how to deploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="c94ec-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="c94ec-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c94ec-107">Creare un progetto Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c94ec-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="c94ec-108">Distribuire un'applicazione esistente in un contenitore</span><span class="sxs-lookup"><span data-stu-id="c94ec-108">Containerize an existing application</span></span>
> * <span data-ttu-id="c94ec-109">Configurare l'integrazione continua con Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="c94ec-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c94ec-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c94ec-110">Prerequisites</span></span>

1. <span data-ttu-id="c94ec-111">Installare [Docker CE per Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) in modo da poter eseguire i contenitori in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c94ec-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="c94ec-112">Acquisire familiarità con le informazioni riportate nella [Guida introduttiva ai contenitori di Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="c94ec-112">Familiarize yourself with the [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="c94ec-113">Scaricare l'applicazione di esempio [Fabrikam Fiber CallCenter][link-fabrikam-github].</span><span class="sxs-lookup"><span data-stu-id="c94ec-113">Download the [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="c94ec-114">Installare [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="c94ec-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="c94ec-115">Installare l'[estensione Strumenti di recapito continuo per Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="c94ec-115">Install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="c94ec-116">Creare una [sottoscrizione di Azure][link-azure-subscription] e un [account di Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="c94ec-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="c94ec-117">Creare un cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="c94ec-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-the-application"></a><span data-ttu-id="c94ec-118">Distribuire l'applicazione in un contenitore</span><span class="sxs-lookup"><span data-stu-id="c94ec-118">Containerize the application</span></span>

<span data-ttu-id="c94ec-119">Un [cluster di Service Fabric è ora in esecuzione in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) e si è pronti quindi per creare e distribuire un'applicazione in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready to create and deploy a containerized application.</span></span> <span data-ttu-id="c94ec-120">Per avviare l'esecuzione dell'applicazione in un contenitore, è necessario aggiungere il **supporto per Docker** al progetto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c94ec-120">To start running our application in a container, we need to add **Docker Support** to the project in Visual Studio.</span></span> <span data-ttu-id="c94ec-121">Quando si aggiunge il **supporto per Docker** all'applicazione, si verifica quanto segue.</span><span class="sxs-lookup"><span data-stu-id="c94ec-121">When you add **Docker support** to the application, two things happen.</span></span> <span data-ttu-id="c94ec-122">Per prima cosa, un _Dockerfile_ viene aggiunto al progetto.</span><span class="sxs-lookup"><span data-stu-id="c94ec-122">First, a _Dockerfile_ is added to the project.</span></span> <span data-ttu-id="c94ec-123">Questo nuovo file descrive il modo in cui l'immagine del contenitore deve essere compilata.</span><span class="sxs-lookup"><span data-stu-id="c94ec-123">This new file describes how the container image is to be built.</span></span> <span data-ttu-id="c94ec-124">In secondo luogo, alla soluzione viene aggiunto un nuovo progetto _docker-compose_.</span><span class="sxs-lookup"><span data-stu-id="c94ec-124">Then second, a new _docker-compose_ project is added to the solution.</span></span> <span data-ttu-id="c94ec-125">Il nuovo progetto contiene alcuni file docker-compose.</span><span class="sxs-lookup"><span data-stu-id="c94ec-125">The new project contains a few docker-compose files.</span></span> <span data-ttu-id="c94ec-126">I file docker-compose possono essere usati per descrivere le modalità di esecuzione del contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-126">Docker-compose files can be used to describe how the container is run.</span></span>

<span data-ttu-id="c94ec-127">Per altre informazioni, vedere [Visual Studio Container Tools][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="c94ec-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="c94ec-128">Se questa è la prima volta che si eseguono immagini del contenitori Windows sul computer in uso, è necessario che Docker CE ottenga le immagini di base per i contenitori.</span><span class="sxs-lookup"><span data-stu-id="c94ec-128">If it is the first time you are running Windows container images on your computer, Docker CE must pull down the base images for your containers.</span></span> <span data-ttu-id="c94ec-129">Le immagini usate in questa esercitazione sono pari a 14 GB.</span><span class="sxs-lookup"><span data-stu-id="c94ec-129">The images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="c94ec-130">Procedere ed eseguire il comando seguente per ottenere le immagini di base:</span><span class="sxs-lookup"><span data-stu-id="c94ec-130">Go ahead and run the following terminal command to pull the base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="c94ec-131">Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="c94ec-131">Add Docker support</span></span>

<span data-ttu-id="c94ec-132">Aprire il file [FabrikamFiber.CallCenter.sln][link-fabrikam-github] in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c94ec-132">Open the [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="c94ec-133">Fare clic con il pulsante destro del mouse sul progetto **FabrikamFiber.Web** > **Aggiungi** > **Supporto Docker**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-133">Right-click the **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="c94ec-134">Aggiungere il supporto per SQL</span><span class="sxs-lookup"><span data-stu-id="c94ec-134">Add support for SQL</span></span>

<span data-ttu-id="c94ec-135">Questa applicazione usa SQL come provider di dati, motivo per cui per eseguire l'applicazione è necessaria un'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c94ec-135">This application uses SQL as the data provider, so a SQL server is required to run the application.</span></span> <span data-ttu-id="c94ec-136">Fare riferimento a un'immagine del contenitore SQL Server nel file docker-compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="c94ec-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="c94ec-137">In Visual Studio aprire **Esplora soluzioni**, trovare **docker-compose** e aprire il file **docker-compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="c94ec-138">Passare al nodo `services:` e aggiungere un nodo chiamato `db:` che definisce la voce di SQL Server per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-138">Navigate to the `services:` node, add a node named `db:` that defines the SQL Server entry for the container.</span></span>

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
><span data-ttu-id="c94ec-139">Per il debug locale è possibile usare un'istanza di SQL Server a scelta, a condizione che sia raggiungibile dall'host.</span><span class="sxs-lookup"><span data-stu-id="c94ec-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="c94ec-140">**localdb**, tuttavia, non supporta la comunicazione `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="c94ec-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="c94ec-141">L'esecuzione di SQL Server in un contenitore non consente di rendere persistenti i dati.</span><span class="sxs-lookup"><span data-stu-id="c94ec-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="c94ec-142">Quando si arresta il contenitore, i dati vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="c94ec-142">When the container stops, your data is erased.</span></span> <span data-ttu-id="c94ec-143">Non usare questa configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="c94ec-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="c94ec-144">Passare al nodo `fabrikamfiber.web:` e aggiungere un nodo figlio di nome `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="c94ec-144">Navigate to the `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="c94ec-145">Il questo modo si assicura che il servizio `db` (il contenitore SQL Server) venga avviato prima dell'applicazione Web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="c94ec-145">This ensures that the `db` service (the SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-the-web-config"></a><span data-ttu-id="c94ec-146">Aggiornare il file di configurazione Web</span><span class="sxs-lookup"><span data-stu-id="c94ec-146">Update the web config</span></span>

<span data-ttu-id="c94ec-147">Tornare al progetto **FabrikamFiber.Web** e aggiornare la stringa di connessione nel file **web.config** in modo che punti all'istanza di SQL Server nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-147">Back in the **FabrikamFiber.Web** project, update the connection string in the **web.config** file, to point to the SQL Server in the container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="c94ec-148">Se si desidera usare un'istanza di SQL Server diversa durante la creazione di una compilazione di rilascio dell'applicazione Web, aggiungere un'altra stringa di connessione al file web.release.config.</span><span class="sxs-lookup"><span data-stu-id="c94ec-148">If you want to use a different SQL Server when building a release build of your web application, add another connection string to your web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="c94ec-149">Testare il contenitore</span><span class="sxs-lookup"><span data-stu-id="c94ec-149">Test your container</span></span>

<span data-ttu-id="c94ec-150">Premere **F5** per eseguire l'applicazione ed eseguirne il debug nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-150">Press **F5** to run and debug the application in your container.</span></span>

<span data-ttu-id="c94ec-151">Edge apre la pagina di avvio definita dell'applicazione usando l'indirizzo IP del contenitore nella rete NAT interna (in genere 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="c94ec-151">Edge opens your application's defined launch page using the IP address of the container on the internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="c94ec-152">Per altre informazioni sul debug delle applicazioni nei contenitori mediante Visual Studio 2017, vedere [questo articolo][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="c94ec-152">To learn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![esempio di fabrikam in un contenitore][image-web-preview]

<span data-ttu-id="c94ec-154">Il contenitore è ora pronto per la compilazione e l'inserimento come pacchetto in un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-154">The container is now ready to be built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="c94ec-155">Dopo aver creato l'immagine del contenitore sul computer, è possibile eseguirne il push in qualsiasi registro contenitori e quindi estrarla in qualsiasi host per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c94ec-155">Once you have the container image built on your machine, you can push it to any container registry and pull it down to any host to run.</span></span>

## <a name="get-the-application-ready-for-the-cloud"></a><span data-ttu-id="c94ec-156">Preparazione l'applicazione per il cloud</span><span class="sxs-lookup"><span data-stu-id="c94ec-156">Get the application ready for the cloud</span></span>

<span data-ttu-id="c94ec-157">Per preparare l'applicazione per l'esecuzione in Service Fabric di Azure, è necessario completare due passaggi:</span><span class="sxs-lookup"><span data-stu-id="c94ec-157">To get the application ready for running in Service Fabric in Azure, we need to complete two steps:</span></span>

1. <span data-ttu-id="c94ec-158">Esporre la porta in cui si vuole poter raggiungere l'applicazione Web nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-158">Expose the port where we want to be able to reach our web application in the Service Fabric cluster.</span></span>
2. <span data-ttu-id="c94ec-159">Predisporre un database SQL di produzione pronto per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c94ec-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-the-port-for-the-app"></a><span data-ttu-id="c94ec-160">Esporre la porta per l'app</span><span class="sxs-lookup"><span data-stu-id="c94ec-160">Expose the port for the app</span></span>
<span data-ttu-id="c94ec-161">Il cluster di Service Fabric configurato presenta la porta *80* aperta per impostazione predefinita in Azure Load Balancer, che consente di bilanciare il traffico in ingresso nel cluster.</span><span class="sxs-lookup"><span data-stu-id="c94ec-161">The Service Fabric cluster we have configured, has port *80* open by default in the Azure Load Balancer, that balances incoming traffic to the cluster.</span></span> <span data-ttu-id="c94ec-162">È possibile esporre il contenitore su questa porta tramite il file docker-compose.ym.</span><span class="sxs-lookup"><span data-stu-id="c94ec-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="c94ec-163">In Visual Studio aprire **Esplora soluzioni**, trovare **docker-compose** e aprire il file **docker-compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="c94ec-164">Modificare il nodo `fabrikamfiber.web:` e aggiungere un nodo figlio denominato `ports:`.</span><span class="sxs-lookup"><span data-stu-id="c94ec-164">Modify the `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="c94ec-165">Aggiungere una voce di stringa `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="c94ec-165">Add a string entry `- "80:80"`.</span></span>

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

### <a name="use-a-production-sql-database"></a><span data-ttu-id="c94ec-166">Usare un database SQL di produzione</span><span class="sxs-lookup"><span data-stu-id="c94ec-166">Use a production SQL database</span></span>
<span data-ttu-id="c94ec-167">Durante l'esecuzione nell'ambiente di produzione, è necessario mantenere i dati persistenti nel database.</span><span class="sxs-lookup"><span data-stu-id="c94ec-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="c94ec-168">Al momento non c'è modo di garantire la persistenza dei dati in un contenitore, pertanto non è possibile archiviare i dati di produzione in SQL Server in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-168">There is currently no way to guarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="c94ec-169">È consigliabile usare un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="c94ec-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="c94ec-170">Per configurare ed eseguire un SQL Server gestito in Azure, consultare l'articolo [Documentazione sul database SQL di Azure][link-azure-sql].</span><span class="sxs-lookup"><span data-stu-id="c94ec-170">To set up and run a managed SQL Server in Azure, visit the [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="c94ec-171">Ricordarsi di modificare le stringhe di connessione a SQL Server nel file **web.release.config**all'interno del progetto **FabrikamFiber.Web**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-171">Remember to change the connection strings to the SQL server in the **web.release.config** file in the **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="c94ec-172">Questa applicazione non funziona correttamente se i database SQL non sono raggiungibili.</span><span class="sxs-lookup"><span data-stu-id="c94ec-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="c94ec-173">È possibile proseguire e distribuire l'applicazione senza un server SQL.</span><span class="sxs-lookup"><span data-stu-id="c94ec-173">You can choose to go ahead and deploy the application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="c94ec-174">Distribuire con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c94ec-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="c94ec-175">Per configurare la distribuzione con Visual Studio Team Services, è necessario installare l'[estensione Strumenti di recapito continuo per Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="c94ec-175">To set up deployment using Visual Studio Team Services, you need to install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="c94ec-176">Questa estensione facilita la distribuzione in Azure mediante la configurazione di Visual Studio Team Services e consente di distribuire l'app nel cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-176">This extension makes it easy to deploy to Azure by configuring Visual Studio Team Services and get your app deployed to your Service Fabric cluster.</span></span>

<span data-ttu-id="c94ec-177">Per iniziare, il codice deve essere ospitato nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="c94ec-177">To get started, your code must be hosted in source control.</span></span> <span data-ttu-id="c94ec-178">Nella restante parte della sezione si presuppone l'uso di **git**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-178">The rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="c94ec-179">Configurare un repository VSTS</span><span class="sxs-lookup"><span data-stu-id="c94ec-179">Set up a VSTS repo</span></span>
<span data-ttu-id="c94ec-180">Nell'angolo inferiore destro di Visual Studio fare clic su **Aggiungi al controllo del codice sorgente** > **Git** (o su qualsiasi opzione desiderata).</span><span class="sxs-lookup"><span data-stu-id="c94ec-180">At the bottom-right corner of Visual Studio, click **Add to Source Control** > **Git** (or whichever option you prefer).</span></span>

![fare clic sul pulsante del controllo del codice sorgente][image-source-control]

<span data-ttu-id="c94ec-182">Nel riquadro _Team Explorer_ premere **Pubblica repository GIT**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-182">In the _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="c94ec-183">Selezionare il nome dell'archivio VSTS e premere **Repository**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-183">Select your VSTS repository name and press **Repository**.</span></span>

![pubblicazione dell'archivio in VSTS][image-publish-repo]

<span data-ttu-id="c94ec-185">Ora che il codice è sincronizzato con l'archivio del codice sorgente VSTS, è possibile configurare la distribuzione continua e il recapito continuo.</span><span class="sxs-lookup"><span data-stu-id="c94ec-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="c94ec-186">Configurare il recapito continuo</span><span class="sxs-lookup"><span data-stu-id="c94ec-186">Setup continuous delivery</span></span>

<span data-ttu-id="c94ec-187">In _Esplora soluzioni_ fare clic con il pulsante destro del mouse sulla **soluzione** > **Configura recapito continuo**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-187">In _Solution Explorer_, right-click the **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="c94ec-188">Selezionare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c94ec-188">Select the Azure Subscription.</span></span>

<span data-ttu-id="c94ec-189">Impostare **Tipo host** su **Cluster di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-189">Set **Host Type** to **Service Fabric Cluster**.</span></span>

<span data-ttu-id="c94ec-190">Impostare **Target Host** (Host di destinazione) sul cluster di Service Fabric creato nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="c94ec-190">Set **Target Host** to the service fabric cluster you created in the previous section.</span></span>

<span data-ttu-id="c94ec-191">Scegliere un **Registro contenitori** in cui pubblicare il contenitore.</span><span class="sxs-lookup"><span data-stu-id="c94ec-191">Choose a **Container Registry** to publish your container to.</span></span>

>[!TIP]
><span data-ttu-id="c94ec-192">Usare il pulsante **Modifica** per creare un registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="c94ec-192">Use the **Edit** button to create a container registry.</span></span>

<span data-ttu-id="c94ec-193">Premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="c94ec-193">Press **OK**.</span></span>

![impostazione dell'integrazione continua di Service Fabric][image-setup-ci]
   
   <span data-ttu-id="c94ec-195">Dopo aver completato la configurazione, il contenitore viene distribuito in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-195">Once the configuration is completed, your container is deployed to Service Fabric.</span></span> <span data-ttu-id="c94ec-196">Ogni volta che si esegue il push degli aggiornamenti nel repository viene eseguita una nuova compilazione e una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="c94ec-196">Whenever you push updates to the repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c94ec-197">La compilazione delle immagini di contenitore richiede circa 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="c94ec-197">Building the container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="c94ec-198">La prima distribuzione nel cluster di Service Fabric comporta il download delle immagini del contenitore di base di Windows Server Core.</span><span class="sxs-lookup"><span data-stu-id="c94ec-198">The first deployment to the Service Fabric cluster causes the base Windows Server Core container images to be downloaded.</span></span> <span data-ttu-id="c94ec-199">Il completamento del download richiede altri 5-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="c94ec-199">The download takes additional 5-10 minutes to complete.</span></span>

<span data-ttu-id="c94ec-200">Passare all'applicazione Fabrikam Call Center usando l'URL del cluster: ad esempio *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="c94ec-200">Browse to the Fabrikam Call Center application using the url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="c94ec-201">Dopo aver inserito la soluzione Fabrikam Call in un pacchetto e averla distribuita, è possibile aprire il [portale di Azure ][link-azure-portal] e visualizzare l'applicazione in esecuzione in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-201">Now that you have containerized and deployed the Fabrikam Call Center solution, you can open the [Azure portal][link-azure-portal] and see the application running in Service Fabric.</span></span> <span data-ttu-id="c94ec-202">Per verificare l'applicazione, aprire un Web browser e passare all'URL del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c94ec-202">To try the application, open a web browser and go to the URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c94ec-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c94ec-203">Next steps</span></span>

<span data-ttu-id="c94ec-204">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="c94ec-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c94ec-205">Creare un progetto Docker in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c94ec-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="c94ec-206">Distribuire un'applicazione esistente in un contenitore</span><span class="sxs-lookup"><span data-stu-id="c94ec-206">Containerize an existing application</span></span>
> * <span data-ttu-id="c94ec-207">Configurare l'integrazione continua con Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="c94ec-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance to the next tutorial to learn how to bind a custom SSL certificate to it.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md)

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
