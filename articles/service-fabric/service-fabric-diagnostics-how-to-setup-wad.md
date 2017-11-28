---
title: aaaCollect log tramite diagnostica Azure | Documenti Microsoft
description: In questo articolo viene descritto come tooset di diagnostica Azure toocollect log da un cluster di Service Fabric in esecuzione in Azure.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="2614a-103">Raccogliere log con Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="2614a-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2614a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2614a-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="2614a-105">Linux</span><span class="sxs-lookup"><span data-stu-id="2614a-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="2614a-106">Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="2614a-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="2614a-107">La presenza di log hello in una posizione centrale consente di analizzare e risolvere i problemi del cluster, o problemi in applicazioni hello e servizi in esecuzione in tale cluster.</span><span class="sxs-lookup"><span data-stu-id="2614a-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="2614a-108">Tooupload un modo e raccogliere i log è toouse hello l'estensione diagnostica Azure, quali caricamenti registra tooAzure archiviazione, Azure Application Insights o hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2614a-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="2614a-109">i registri di Hello non sono utili direttamente nell'archiviazione o negli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2614a-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="2614a-110">Ma è possibile utilizzare gli eventi di hello tooread un processo esterno dall'archivio e inserirli in un prodotto, ad esempio [Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.</span><span class="sxs-lookup"><span data-stu-id="2614a-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="2614a-111">In [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) è integrato un servizio completo di analisi e di ricerca dei log.</span><span class="sxs-lookup"><span data-stu-id="2614a-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2614a-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2614a-112">Prerequisites</span></span>
<span data-ttu-id="2614a-113">Utilizzare questi strumenti tooperform alcune delle operazioni di hello in questo documento:</span><span class="sxs-lookup"><span data-stu-id="2614a-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="2614a-114">[Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata tooAzure servizi Cloud, ma con informazioni ed esempi)</span><span class="sxs-lookup"><span data-stu-id="2614a-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="2614a-115">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="2614a-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="2614a-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2614a-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="2614a-117">Client di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2614a-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="2614a-118">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2614a-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="2614a-119">Origini di log che è possibile toocollect</span><span class="sxs-lookup"><span data-stu-id="2614a-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="2614a-120">**I log di Service Fabric**: generato dai hello piattaforma toostandard traccia eventi per Windows (ETW) ed EventSource canali.</span><span class="sxs-lookup"><span data-stu-id="2614a-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="2614a-121">I log possono essere di diversi tipi:</span><span class="sxs-lookup"><span data-stu-id="2614a-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="2614a-122">Gli eventi operativi: log per operazioni che hello Service Fabric piattaforma esegue.</span><span class="sxs-lookup"><span data-stu-id="2614a-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="2614a-123">Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2614a-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="2614a-124">Eventi del modello di programmazione Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2614a-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="2614a-125">Eventi relativi al modello di programmazione Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2614a-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="2614a-126">**Gli eventi dell'applicazione**: gli eventi generati dal codice del servizio e scritte usando classe helper di EventSource hello fornito nei modelli di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="2614a-127">Per ulteriori informazioni sulla modalità di registrazione toowrite dall'applicazione, vedere [Monitor e diagnosticare i servizi in una configurazione di sviluppo locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="2614a-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="2614a-128">Distribuire l'estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="2614a-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="2614a-129">Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="2614a-130">Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="2614a-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="2614a-131">passaggi di Hello variano leggermente in base che si utilizzi hello portale di Azure o Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2614a-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="2614a-132">procedura di Hello anche varia a seconda che la distribuzione di hello fa parte della creazione del cluster o per un cluster che esiste già.</span><span class="sxs-lookup"><span data-stu-id="2614a-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="2614a-133">Esaminiamo i passaggi di hello per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="2614a-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="2614a-134">Distribuire l'estensione di diagnostica hello come parte della creazione del cluster tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="2614a-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="2614a-135">toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, utilizzare pannello impostazioni di diagnostica hello mostrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="2614a-136">tooenable Reliable Actors o servizi affidabili raccolta degli eventi, assicurarsi che la diagnostica sia impostata troppo**su** (hello l'impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="2614a-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="2614a-137">Dopo aver creato il cluster hello, è possibile modificare queste impostazioni mediante il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Impostazioni di diagnostica di Azure nel portale di hello per la creazione del cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="2614a-139">salve team di supporto tecnico di Azure *richiede* supporto registra toohelp risolvere tutte le richieste di supporto che si creano.</span><span class="sxs-lookup"><span data-stu-id="2614a-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="2614a-140">Questi log vengono raccolti in tempo reale e vengono archiviati in uno degli account di archiviazione hello creato nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="2614a-141">le impostazioni di diagnostica Hello configurano gli eventi a livello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="2614a-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="2614a-142">Questi eventi includono [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventi, [servizi affidabili](service-fabric-reliable-services-diagnostics.md) eventi e alcuni toobe gli eventi di Service Fabric a livello di sistema archiviati in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2614a-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="2614a-143">I prodotti, ad esempio [Elasticsearch](https://www.elastic.co/guide/index.html) o un processo personalizzato è possibile ottenere gli eventi di hello dall'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="2614a-144">Non è presente alcun modo toofilter o pulitura hello gli eventi inviati toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="2614a-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="2614a-145">Se si non implementa un tooremove di elaborare gli eventi dalla tabella hello, tabella hello continuerà toogrow.</span><span class="sxs-lookup"><span data-stu-id="2614a-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="2614a-146">Quando si crea un cluster tramite il portale di hello, si consiglia di scaricare il modello di hello **prima di scegliere OK** cluster hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2614a-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="2614a-147">Per informazioni dettagliate, vedere troppo[configurazione di un cluster di Service Fabric utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2614a-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="2614a-148">È necessario toomake modifiche al modello hello in un secondo momento, poiché non è possibile apportare alcune modifiche tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="2614a-149">È possibile esportare i modelli dal portale hello utilizzando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2614a-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="2614a-150">Tuttavia, questi modelli possono essere più difficile toouse perché potrebbe contengono valori null che mancano informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="2614a-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="2614a-151">Aprire il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2614a-151">Open your resource group.</span></span>
2. <span data-ttu-id="2614a-152">Selezionare **impostazioni** toodisplay hello impostazioni del pannello.</span><span class="sxs-lookup"><span data-stu-id="2614a-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="2614a-153">Selezionare **distribuzioni** pannello della cronologia di distribuzione hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="2614a-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="2614a-154">Selezionare i dettagli hello toodisplay distribuzione su distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="2614a-155">Selezionare **Esporta modello** Pannello di toodisplay hello modello.</span><span class="sxs-lookup"><span data-stu-id="2614a-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="2614a-156">Selezionare **salvare toofile** tooexport un file con estensione zip che contiene il modello di hello, parametro e i file di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2614a-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="2614a-157">Dopo aver esportato il file hello, è necessario toomake una modifica.</span><span class="sxs-lookup"><span data-stu-id="2614a-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="2614a-158">Modificare il file parameters.json hello e rimuovere hello **adminPassword** elemento.</span><span class="sxs-lookup"><span data-stu-id="2614a-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="2614a-159">In questo modo la richiesta hello password durante l'esecuzione di script di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="2614a-160">Quando si esegue lo script di distribuzione hello, potrebbe essere toofix valori di parametro null.</span><span class="sxs-lookup"><span data-stu-id="2614a-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="2614a-161">hello toouse scaricati tooupdate modello una configurazione:</span><span class="sxs-lookup"><span data-stu-id="2614a-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="2614a-162">Estrarre la cartella di tooa hello contenuto nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="2614a-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="2614a-163">Modificare hello contenuto tooreflect hello nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="2614a-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="2614a-164">Avviare PowerShell e modificare toohello cartella in cui è stato estratto il contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="2614a-165">Eseguire **deploy.ps1** e compilare hello sottoscrizione ID, nome del gruppo di risorse hello (utilizzare hello stessa configurazione del nome tooupdate hello) e un nome univoco di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2614a-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="2614a-166">Distribuire l'estensione di diagnostica hello come parte della creazione del cluster usando Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="2614a-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="2614a-167">toocreate un cluster usando Gestione risorse, è necessario tooadd hello diagnostica JSON toohello completo del cluster di gestione delle risorse modello di configurazione prima di creare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="2614a-168">Offriamo un modello di gestione risorse di esempio 5-VM cluster con configurazione di diagnostica aggiunti tooit come parte di esempi di gestione delle risorse modello.</span><span class="sxs-lookup"><span data-stu-id="2614a-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="2614a-169">È possibile visualizzarlo in questa posizione nella raccolta di esempi di Azure hello: [cluster cinque nodi con il modello di gestione risorse diagnostica esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="2614a-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="2614a-170">impostazione di diagnostica hello toosee nel modello di gestione risorse di hello, file azuredeploy.json aprire hello e cercare **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="2614a-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="2614a-171">un cluster utilizzando questo modello, seleziona hello toocreate **distribuire tooAzure** pulsante disponibile all'indirizzo collegamento precedente hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="2614a-172">In alternativa, è possibile scaricare Gestione risorse: esempio hello, apportare le modifiche tooit e creare un cluster con modello modificato hello utilizzando hello `New-AzureRmResourceGroupDeployment` comando in una finestra di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="2614a-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="2614a-173">Vedere hello seguente codice per i parametri di hello che viene passato nel comando toohello.</span><span class="sxs-lookup"><span data-stu-id="2614a-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="2614a-174">Per informazioni dettagliate sul modo in cui raggruppare toodeploy una risorsa tramite PowerShell, vedere l'articolo hello [distribuire un gruppo di risorse con il modello di gestione risorse di Azure hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2614a-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="2614a-175">Distribuire cluster esistente tooan estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="2614a-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="2614a-176">Se si dispone di un cluster esistente che non dispone di diagnostica distribuita o se si desidera toomodify una configurazione esistente, è possibile aggiungere o aggiornare.</span><span class="sxs-lookup"><span data-stu-id="2614a-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="2614a-177">Modificare modello di gestione risorse hello cluster esistente di hello toocreate usato o scaricare il modello di hello dal portale hello come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2614a-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="2614a-178">Modificare il file di template.json hello eseguendo hello seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="2614a-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="2614a-179">Aggiungere un nuovo modello toohello risorse di archiviazione aggiungendo toohello sezione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="2614a-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="2614a-180">Successivamente, aggiungere parametri toohello sezione subito dopo le definizioni account di archiviazione hello, tra `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="2614a-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="2614a-181">Sostituire il testo segnaposto hello *nome account di archiviazione qui* con nome hello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2614a-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="2614a-182">Quindi, aggiornare hello `VirtualMachineProfile` sezione del file template.json hello aggiungendo hello seguente codice all'interno della matrice estensioni hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="2614a-183">Essere tooadd che una virgola all'inizio di hello o alla fine di hello, a seconda di dove viene inserito.</span><span class="sxs-lookup"><span data-stu-id="2614a-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="2614a-184">Dopo aver modificato il file template.json hello come descritto, è possibile ripubblicare il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="2614a-185">Se è stato esportato il modello di hello, l'esecuzione del file di deploy.ps1 hello Ripubblica modello hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="2614a-186">Dopo la distribuzione, assicurarsi che il valore di **ProvisioningState** sia **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="2614a-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="2614a-187">Aggiornare gli eventi di integrità e carico toocollect diagnostica</span><span class="sxs-lookup"><span data-stu-id="2614a-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="2614a-188">A partire dalla versione di hello 5.4 di Service Fabric, gli eventi di metrica di integrità e carico sono disponibili per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="2614a-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="2614a-189">Questi eventi riflettono gli eventi generati dal sistema hello o il codice tramite integrità hello o caricare le API di creazione di report, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="2614a-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="2614a-190">Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento.</span><span class="sxs-lookup"><span data-stu-id="2614a-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="2614a-191">tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" toohello elenco dei provider ETW.</span><span class="sxs-lookup"><span data-stu-id="2614a-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="2614a-192">eventi di hello toocollect, modificare hello resource manager modello tooinclude</span><span class="sxs-lookup"><span data-stu-id="2614a-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="2614a-193">Aggiornare toocollect diagnostica e caricare i log dei nuovi canali EventSource</span><span class="sxs-lookup"><span data-stu-id="2614a-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="2614a-194">log di toocollect tooupdate diagnostica da nuovi canali EventSource che rappresentano una nuova applicazione che è quasi toodeploy, eseguire hello stessi passaggi come hello [precedente sezione](#deploywadarm) per l'installazione di diagnostica per un oggetto esistente cluster.</span><span class="sxs-lookup"><span data-stu-id="2614a-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="2614a-195">Aggiornare hello `EtwEventSourceProviderConfiguration` sezione nelle voci di hello template.json file tooadd per hello nuovi EventSource canali prima di applicare la configurazione hello aggiornare utilizzando hello `New-AzureRmResourceGroupDeployment` comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2614a-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="2614a-196">nome di Hello dell'origine evento hello è definito come parte del codice nel file di Visual Studio generati ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="2614a-197">Ad esempio, se l'origine eventi è denominato My Eventsource, aggiungere hello dopo gli eventi di codice tooplace hello da My Eventsource in una tabella denominata MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="2614a-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="2614a-198">i contatori delle prestazioni toocollect o nei registri eventi, è possibile modificare il modello di gestione risorse di hello usando hello esempi forniti in [creare una macchina virtuale Windows con monitoraggio e diagnostica utilizzando un modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2614a-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2614a-199">Quindi, pubblicare di nuovo il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="2614a-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2614a-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2614a-200">Next steps</span></span>
<span data-ttu-id="2614a-201">toounderstand in dettaglio gli eventi che è necessario cercare la risoluzione dei problemi, vedere gli eventi di diagnostica hello generati per [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [servizi affidabili](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2614a-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="2614a-202">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="2614a-202">Related articles</span></span>
* [<span data-ttu-id="2614a-203">Informazioni su come i contatori delle prestazioni toocollect o i registri tramite hello estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="2614a-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2614a-204">Soluzione Service Fabric in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2614a-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

