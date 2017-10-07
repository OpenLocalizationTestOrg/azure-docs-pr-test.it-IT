---
title: aaaManage le applicazioni in Visual Studio | Documenti Microsoft
description: Utilizzare toocreate di Visual Studio, sviluppare, pacchetto, distribuzione e debug di applicazioni di Service Fabric e ai servizi.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="f3efb-103">Utilizzare Visual Studio toosimplify scrittura e la gestione delle applicazioni di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="f3efb-104">È possibile gestire le applicazioni e i servizi di Service Fabric di Azure tramite Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3efb-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="f3efb-105">Dopo aver [configurare l'ambiente di sviluppo](service-fabric-get-started.md), è possibile utilizzare applicazioni di Service Fabric toocreate Visual Studio, aggiungere registro servizi o di pacchetto e distribuire le applicazioni del cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="f3efb-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="f3efb-106">Distribuire l'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="f3efb-107">Per impostazione predefinita, la distribuzione di un'applicazione combina hello in una semplice operazione come segue:</span><span class="sxs-lookup"><span data-stu-id="f3efb-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="f3efb-108">Creazione pacchetto di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f3efb-108">Creating hello application package</span></span>
2. <span data-ttu-id="f3efb-109">Archivio di immagini di caricamento hello applicazione pacchetto toohello</span><span class="sxs-lookup"><span data-stu-id="f3efb-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="f3efb-110">Registrazione del tipo di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="f3efb-110">Registering hello application type</span></span>
4. <span data-ttu-id="f3efb-111">Rimozione delle eventuali istanze dell'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f3efb-111">Removing any running application instances</span></span>
5. <span data-ttu-id="f3efb-112">Creazione di un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f3efb-112">Creating an application instance</span></span>

<span data-ttu-id="f3efb-113">In Visual Studio, premere **F5** distribuisce l'applicazione e collegare le istanze dell'applicazione hello debugger tooall.</span><span class="sxs-lookup"><span data-stu-id="f3efb-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="f3efb-114">È possibile utilizzare **Ctrl + F5** toodeploy un'applicazione senza debug oppure è possibile pubblicare tooa locale o remota del cluster tramite hello profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="f3efb-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="f3efb-115">Per ulteriori informazioni, vedere [pubblicare un cluster remoto tooa delle applicazioni con Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f3efb-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="f3efb-116">Modalità di debug applicazione</span><span class="sxs-lookup"><span data-stu-id="f3efb-116">Application Debug Mode</span></span>
<span data-ttu-id="f3efb-117">Visual Studio forniscono una proprietà denominata **modalità di Debug dell'applicazione**, che controlla la modalità di distribuzione di applicazioni di Visual studi toohandle come parte di debug.</span><span class="sxs-lookup"><span data-stu-id="f3efb-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="f3efb-118">hello tooset proprietà modalità di Debug dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f3efb-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="f3efb-119">In hello Service Fabric del progetto dell'applicazione (*. sfproj) dal menu di scelta rapida scegliere **proprietà** (o premere hello **F4** chiave).</span><span class="sxs-lookup"><span data-stu-id="f3efb-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="f3efb-120">In hello **proprietà** finestra, hello set **modalità di Debug dell'applicazione** proprietà.</span><span class="sxs-lookup"><span data-stu-id="f3efb-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Impostare la proprietà Modalità di debug applicazione][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="f3efb-122">Modalità di debug dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f3efb-122">Application Debug Modes</span></span>

1. <span data-ttu-id="f3efb-123">**Aggiornare applicazione** questa modalità consente modifiche tooquickly ed eseguire il debug del codice e supporta la modifica di file web statici durante il debug.</span><span class="sxs-lookup"><span data-stu-id="f3efb-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="f3efb-124">Questa modalità funziona solo se il cluster di sviluppo locale è in [modalità a 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="f3efb-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="f3efb-125">**Rimuovere l'applicazione** cause hello toobe applicazione rimossi quando termina la sessione di debug hello.</span><span class="sxs-lookup"><span data-stu-id="f3efb-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="f3efb-126">**L'aggiornamento automatico** applicazione hello continua toorun quando termina la sessione di debug hello.</span><span class="sxs-lookup"><span data-stu-id="f3efb-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="f3efb-127">Hello successiva sessione di debug verrà considerato distribuzione hello un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="f3efb-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="f3efb-128">processo di aggiornamento Hello mantiene tutti i dati immessi in una sessione di debug precedente.</span><span class="sxs-lookup"><span data-stu-id="f3efb-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="f3efb-129">**Applicazione di mantenere** mantiene applicazione hello in esecuzione in cluster hello quando hello debug sessione termina.</span><span class="sxs-lookup"><span data-stu-id="f3efb-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="f3efb-130">Hello inizio hello successiva sessione di debug, un'applicazione hello verrà rimossi.</span><span class="sxs-lookup"><span data-stu-id="f3efb-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="f3efb-131">Per **l'aggiornamento automatico** i dati vengono conservati applicando la funzionalità di aggiornamento dell'applicazione hello di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f3efb-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="f3efb-132">Per altre informazioni sull'aggiornamento delle applicazioni e su come è possibile eseguire un aggiornamento in un ambiente reale, vedere [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="f3efb-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="f3efb-133">Aggiungere un tooyour servizio applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="f3efb-134">È possibile aggiungere nuovi servizi tooyour applicazione tooextend relativa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f3efb-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="f3efb-135">tooensure servizio hello viene incluso nel pacchetto dell'applicazione, aggiungere il servizio di hello tramite hello **nuovo Service Fabric...**  voce di menu.</span><span class="sxs-lookup"><span data-stu-id="f3efb-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Aggiungere un nuovo servizio di Service Fabric][newservice]

<span data-ttu-id="f3efb-137">Selezionare un'applicazione di Service Fabric progetto tipo tooadd tooyour e specificare un nome per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="f3efb-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="f3efb-138">Vedere [scelta di un framework per il servizio](service-fabric-choose-framework.md) toohelp si decide quale servizio digitare toouse.</span><span class="sxs-lookup"><span data-stu-id="f3efb-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Selezionare un'applicazione tooyour tooadd tipo di Service Fabric servizio progetto][addserviceproject]

<span data-ttu-id="f3efb-140">nuovo servizio Hello viene aggiunto tooyour soluzione e il pacchetto di applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="f3efb-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="f3efb-141">riferimenti al servizio Hello e un'istanza del servizio predefinito sarà manifesto dell'applicazione toohello aggiunto, causando hello servizio toobe creata e avviata hello successivo che si distribuisce un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3efb-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![nuovo servizio Hello viene aggiunto il manifesto di applicazione tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="f3efb-143">Creazione del pacchetto per l'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-143">Package your Service Fabric application</span></span>
<span data-ttu-id="f3efb-144">un'applicazione hello toodeploy e il cluster tooa services, è necessario toocreate un pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3efb-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="f3efb-145">Consente di organizzare i pacchetti Hello manifesto dell'applicazione hello, i manifesti del servizio e altri file necessari in un layout specifico.</span><span class="sxs-lookup"><span data-stu-id="f3efb-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="f3efb-146">Visual Studio configura e gestisce i pacchetti hello nella cartella del progetto dell'applicazione hello, nella directory 'pkg' hello.</span><span class="sxs-lookup"><span data-stu-id="f3efb-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="f3efb-147">Fare clic su **pacchetto** da hello **applicazione** Crea menu di scelta rapida o aggiornamenti hello pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3efb-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="f3efb-148">Rimuovere applicazioni e tipi di applicazione con Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f3efb-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="f3efb-149">È possibile eseguire le operazioni di Gestione cluster di base dall'interno Visual Studio Cloud Explorer, che è possibile avviare da hello usando **vista** menu.</span><span class="sxs-lookup"><span data-stu-id="f3efb-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="f3efb-150">È ad esempio possibile eliminare applicazioni e annullare il provisioning di tipi di applicazione in cluster locali o remoti.</span><span class="sxs-lookup"><span data-stu-id="f3efb-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Rimuovere un'applicazione][removeapplication]

> [!TIP]
> <span data-ttu-id="f3efb-152">Per funzionalità di gestione dei cluster più avanzate, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f3efb-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="f3efb-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3efb-153">Next steps</span></span>
* [<span data-ttu-id="f3efb-154">Modello di applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="f3efb-155">Distribuzione di un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="f3efb-156">Gestione dei parametri dell'applicazione per più ambienti</span><span class="sxs-lookup"><span data-stu-id="f3efb-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="f3efb-157">Debug dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="f3efb-158">Visualizzazione del cluster con l’explorer di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3efb-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png