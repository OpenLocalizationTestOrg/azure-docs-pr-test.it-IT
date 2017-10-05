---
title: Gestire le applicazioni in Visual Studio | Microsoft Docs
description: "Usare Visual Studio per creare, sviluppare, creare pacchetti, distribuire ed effettuare il debug di applicazioni dell’infrastruttura di servizi e di servizi."
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
ms.openlocfilehash: 3f6a47a15b74a7ceb6504b2834be62e76ab70bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="bea2a-103">Usare Visual Studio per semplificare la scrittura e la gestione delle applicazioni dell’infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="bea2a-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="bea2a-104">È possibile gestire le applicazioni e i servizi di Service Fabric di Azure tramite Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bea2a-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="bea2a-105">Dopo aver [configurato l'ambiente di sviluppo](service-fabric-get-started.md), è infatti possibile usare Visual Studio per creare applicazioni di Service Fabric, aggiungere servizi o creare i pacchetti, registrare e distribuire le applicazioni nel cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="bea2a-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="bea2a-106">Distribuire l'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="bea2a-107">Per impostazione predefinita, la distribuzione di un'applicazione combina in un'unica operazione i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bea2a-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="bea2a-108">Creazione del pacchetto applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-108">Creating the application package</span></span>
2. <span data-ttu-id="bea2a-109">Caricamento del pacchetto applicazione in Image Store</span><span class="sxs-lookup"><span data-stu-id="bea2a-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="bea2a-110">Registrazione del tipo di applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-110">Registering the application type</span></span>
4. <span data-ttu-id="bea2a-111">Rimozione delle eventuali istanze dell'applicazione in esecuzione</span><span class="sxs-lookup"><span data-stu-id="bea2a-111">Removing any running application instances</span></span>
5. <span data-ttu-id="bea2a-112">Creazione di un'istanza dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-112">Creating an application instance</span></span>

<span data-ttu-id="bea2a-113">In Visual Studio se si preme **F5** l'applicazione viene distribuita e il debugger viene allegato a tutte le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea2a-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="bea2a-114">È possibile utilizzare **Ctrl + F5** per distribuire un'applicazione senza il debug, o pubblicare in un cluster locale o remoto mediante il profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="bea2a-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="bea2a-115">Per altre informazioni, consultare [Pubblicare un'applicazione in un cluster remoto mediante Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bea2a-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="bea2a-116">Modalità di debug applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-116">Application Debug Mode</span></span>
<span data-ttu-id="bea2a-117">Visual Studio include la proprietà **Modalità di debug applicazione** che controlla la modalità di distribuzione dell'applicazione nel contesto del debug.</span><span class="sxs-lookup"><span data-stu-id="bea2a-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="bea2a-118">Per impostare la proprietà Modalità di debug applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-118">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="bea2a-119">Nel menu di scelta rapida del progetto applicazione Service Fabric (*.sfproj) scegliere **Proprietà** (o premere **F4**).</span><span class="sxs-lookup"><span data-stu-id="bea2a-119">On the Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="bea2a-120">Nella finestra **Proprietà** impostare la proprietà **Modalità di debug applicazione**.</span><span class="sxs-lookup"><span data-stu-id="bea2a-120">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Impostare la proprietà Modalità di debug applicazione][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="bea2a-122">Modalità di debug dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="bea2a-122">Application Debug Modes</span></span>

1. <span data-ttu-id="bea2a-123">**Aggiorna l'applicazione**: questa modalità consente di modificare rapidamente il codice e di eseguirne il debug e supporta la modifica dei file Web statici durante il debug.</span><span class="sxs-lookup"><span data-stu-id="bea2a-123">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="bea2a-124">Questa modalità funziona solo se il cluster di sviluppo locale è in [modalità a 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="bea2a-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="bea2a-125">**Rimuovi applicazione** fa sì che l'applicazione venga rimossa al termine della sessione di debug.</span><span class="sxs-lookup"><span data-stu-id="bea2a-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="bea2a-126">**Aggiornamento automatico**: l'applicazione resta in esecuzione al termine della sessione di debug.</span><span class="sxs-lookup"><span data-stu-id="bea2a-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="bea2a-127">La sessione di debug successiva considera la distribuzione come un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bea2a-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="bea2a-128">Il processo di aggiornamento mantiene tutti i dati immessi in una sessione di debug precedente.</span><span class="sxs-lookup"><span data-stu-id="bea2a-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="bea2a-129">**Mantieni l'applicazione**: l'applicazione resta in esecuzione nel cluster al termine della sessione di debug.</span><span class="sxs-lookup"><span data-stu-id="bea2a-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="bea2a-130">All'inizio della sessione di debug successiva, l'applicazione viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="bea2a-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="bea2a-131">Con l'opzione **Aggiornamento automatico** i dati vengono mantenuti applicando le funzionalità di aggiornamento dell'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bea2a-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="bea2a-132">Per altre informazioni sull'aggiornamento delle applicazioni e su come è possibile eseguire un aggiornamento in un ambiente reale, vedere [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="bea2a-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="bea2a-133">Aggiungere un servizio all'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="bea2a-134">È possibile aggiungere nuovi servizi all'applicazione per estenderne le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bea2a-134">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="bea2a-135">Per essere certi che il servizio venga incluso nel pacchetto applicazione, aggiungere il servizio usando la voce di menu **New Fabric Service** .</span><span class="sxs-lookup"><span data-stu-id="bea2a-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Aggiungere un nuovo servizio di Service Fabric][newservice]

<span data-ttu-id="bea2a-137">Selezionare un tipo di progetto di Service Fabric da aggiungere all'applicazione e specificare un nome per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bea2a-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="bea2a-138">Per decidere più facilmente quale tipo di servizio usare, vedere [Scelta di un framework per il servizio](service-fabric-choose-framework.md) .</span><span class="sxs-lookup"><span data-stu-id="bea2a-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Selezionare un tipo di progetto di servizio Service Fabric da aggiungere all'applicazione][addserviceproject]

<span data-ttu-id="bea2a-140">Il nuovo servizio viene aggiunto alla soluzione e al pacchetto dell'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="bea2a-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="bea2a-141">I riferimenti e un'istanza del servizio predefinita vengono aggiunti al manifesto dell'applicazione, in modo che il servizio venga creato e avviato alla successiva distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea2a-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![Il nuovo servizio viene aggiunto al manifesto dell'applicazione][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="bea2a-143">Creazione del pacchetto per l'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-143">Package your Service Fabric application</span></span>
<span data-ttu-id="bea2a-144">Per distribuire l'applicazione e i relativi servizi in un cluster, è necessario creare un pacchetto dell’applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea2a-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="bea2a-145">Il pacchetto organizza il manifesto dell'applicazione, i manifesti dei servizi e gli altri file necessari in un layout specifico.</span><span class="sxs-lookup"><span data-stu-id="bea2a-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="bea2a-146">Visual Studio imposta e gestisce il pacchetto nella cartella del progetto dell'applicazione, nella cartella "pkg".</span><span class="sxs-lookup"><span data-stu-id="bea2a-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="bea2a-147">Facendo clic su **Pacchetto** dal menu di scelta rapida **Applicazione** il pacchetto dell'applicazione viene creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="bea2a-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="bea2a-148">Rimuovere applicazioni e tipi di applicazione con Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="bea2a-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="bea2a-149">In Visual Studio è possibile eseguire operazioni di gestione dei cluster di base con Cloud Explorer, che può essere avviato dal menu **Visualizza** .</span><span class="sxs-lookup"><span data-stu-id="bea2a-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="bea2a-150">È ad esempio possibile eliminare applicazioni e annullare il provisioning di tipi di applicazione in cluster locali o remoti.</span><span class="sxs-lookup"><span data-stu-id="bea2a-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Rimuovere un'applicazione][removeapplication]

> [!TIP]
> <span data-ttu-id="bea2a-152">Per funzionalità di gestione dei cluster più avanzate, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bea2a-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="bea2a-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bea2a-153">Next steps</span></span>
* [<span data-ttu-id="bea2a-154">Modello di applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="bea2a-155">Distribuzione di un'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="bea2a-156">Gestione dei parametri dell'applicazione per più ambienti</span><span class="sxs-lookup"><span data-stu-id="bea2a-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="bea2a-157">Debug dell'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="bea2a-158">Visualizzazione del cluster con l’explorer di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bea2a-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png