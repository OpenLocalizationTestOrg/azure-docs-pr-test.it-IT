---
title: Raccogliere log con Diagnostica di Azure | Microsoft Docs
description: Questo articolo illustra come configurare Diagnostica di Azure per raccogliere log da un cluster di Service Fabric in esecuzione in Azure.
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="1839d-103">Raccogliere log con Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="1839d-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1839d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="1839d-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="1839d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="1839d-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="1839d-106">Quando si esegue un cluster Azure Service Fabric, è consigliabile raccogliere i log da tutti i nodi in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="1839d-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="1839d-107">Il salvataggio dei log in una posizione centrale semplifica l'analisi e la risoluzione di eventuali problemi nel cluster o nelle applicazioni e nei servizi in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1839d-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="1839d-108">Un modo per caricare e raccogliere i log consiste nell'usare l'estensione Diagnostica di Azure, che consente di caricare i log di archiviazione di Azure, Azure Application Insights o Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="1839d-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="1839d-109">I log non sono utili direttamente nell'archiviazione o in Hub eventi,</span><span class="sxs-lookup"><span data-stu-id="1839d-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="1839d-110">ma è possibile usare un processo esterno per leggere gli eventi dalla risorsa di archiviazione e inserirli in un prodotto come [Log Analytics](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.</span><span class="sxs-lookup"><span data-stu-id="1839d-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="1839d-111">In [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) è integrato un servizio completo di analisi e di ricerca dei log.</span><span class="sxs-lookup"><span data-stu-id="1839d-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1839d-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1839d-112">Prerequisites</span></span>
<span data-ttu-id="1839d-113">Questi strumenti vengono usati per eseguire alcune operazioni nel documento:</span><span class="sxs-lookup"><span data-stu-id="1839d-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="1839d-114">[Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata ai Servizi cloud di Azure, include alcune informazioni ed esempi utili)</span><span class="sxs-lookup"><span data-stu-id="1839d-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="1839d-115">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1839d-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="1839d-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1839d-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="1839d-117">Client di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1839d-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="1839d-118">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1839d-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="1839d-119">Origini di log da raccogliere</span><span class="sxs-lookup"><span data-stu-id="1839d-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="1839d-120">**Log di Service Fabric:** generati dalla piattaforma in canali Event Tracing for Windows (ETW) ed EventSource standard.</span><span class="sxs-lookup"><span data-stu-id="1839d-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="1839d-121">I log possono essere di diversi tipi:</span><span class="sxs-lookup"><span data-stu-id="1839d-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="1839d-122">Eventi operativi: log relativi a operazioni eseguite dalla piattaforma Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1839d-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="1839d-123">Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1839d-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="1839d-124">Eventi del modello di programmazione Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="1839d-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="1839d-125">Eventi relativi al modello di programmazione Reliable Services</span><span class="sxs-lookup"><span data-stu-id="1839d-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="1839d-126">**Eventi dell'applicazione:** eventi generati dal codice del servizio e scritti mediante la classe helper EventSource disponibile nei modelli di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1839d-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="1839d-127">Per altre informazioni su come scrivere i log dall'applicazione, vedere [Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="1839d-128">Distribuire l'estensione Diagnostica</span><span class="sxs-lookup"><span data-stu-id="1839d-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="1839d-129">Il primo passaggio per la raccolta dei log consiste nel distribuire l'estensione Diagnostica in ogni VM del cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1839d-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="1839d-130">Questa estensione raccoglie i log in ogni VM e li carica nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="1839d-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="1839d-131">La procedura varia a seconda che si usi il portale di Azure oppure Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1839d-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="1839d-132">Anche i passaggi variano se la distribuzione fa parte della creazione del cluster o è relativa a un cluster già esistente.</span><span class="sxs-lookup"><span data-stu-id="1839d-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="1839d-133">Ecco la procedura per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="1839d-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="1839d-134">Distribuire l’estensione Diagnostica come parte della creazione di cluster tramite il portale</span><span class="sxs-lookup"><span data-stu-id="1839d-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="1839d-135">Per distribuire l'estensione Diagnostica nelle VM del cluster come parte della creazione del cluster, si usa il pannello Impostazioni di diagnostica illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="1839d-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="1839d-136">Per abilitare la raccolta di eventi Reliable Actors o Reliable Services, verificare che l'opzione Diagnostica sia impostata su **Sì**, che corrisponde all'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1839d-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="1839d-137">Dopo aver creato il cluster, non è possibile modificare questa impostazione tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="1839d-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Impostazioni di diagnostica di Azure nel portale per la creazione del cluster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="1839d-139">Il team di Supporto di Azure *necessita* dei log di supporto per gestire eventuali richieste di supporto create dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1839d-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="1839d-140">I log vengono raccolti in tempo reale e archiviati in uno degli account di archiviazione creati nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1839d-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="1839d-141">Le impostazioni di diagnostica configurano gli eventi a livello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1839d-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="1839d-142">Sono inclusi gli eventi [Reliable Actors](service-fabric-reliable-actors-diagnostics.md), [Reliable Services](service-fabric-reliable-services-diagnostics.md) e alcuni eventi di Service Fabric a livello di sistema da archiviare in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1839d-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="1839d-143">Gli eventi possono essere ottenuti dall'account di archiviazione da prodotti come [ElasticSearch](https://www.elastic.co/guide/index.html) o da un processo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1839d-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="1839d-144">Attualmente non è possibile filtrare o eliminare gli eventi inviati alla tabella.</span><span class="sxs-lookup"><span data-stu-id="1839d-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="1839d-145">Se non si implementa un processo per rimuovere gli eventi dalla tabella, le dimensioni della tabella continueranno ad aumentare.</span><span class="sxs-lookup"><span data-stu-id="1839d-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="1839d-146">Quando si crea un cluster con il portale, è consigliabile scaricare il modello **prima di fare clic su OK** per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="1839d-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="1839d-147">Per informazioni dettagliate, vedere [Configurare un cluster di Service Fabric usando un modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="1839d-148">Il modello è necessario per apportare modifiche in un secondo momento perché non è possibile apportare alcune modifiche tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="1839d-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="1839d-149">È possibile esportare i modelli dal portale attenendosi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1839d-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="1839d-150">Tuttavia, questi modelli possono risultare più difficili da usare poiché potrebbero contenere valori Null in cui mancano informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="1839d-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="1839d-151">Aprire il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1839d-151">Open your resource group.</span></span>
2. <span data-ttu-id="1839d-152">Selezionare **Impostazioni** per visualizzare il pannello Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1839d-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="1839d-153">Selezionare **Distribuzioni** per visualizzare il pannello Cronologia distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="1839d-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="1839d-154">Selezionare una distribuzione per visualizzare i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="1839d-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="1839d-155">Selezionare **Esporta modello** per visualizzare il pannello Modello.</span><span class="sxs-lookup"><span data-stu-id="1839d-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="1839d-156">Selezionare **Salva su file** per esportare un file con estensione zip contenente i file del modello, dei parametri e di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1839d-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="1839d-157">Dopo aver esportato i file, è necessario apportare una modifica.</span><span class="sxs-lookup"><span data-stu-id="1839d-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="1839d-158">Modificare il file parameters.json e rimuovere l'elemento **adminPassword**.</span><span class="sxs-lookup"><span data-stu-id="1839d-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="1839d-159">In questo modo viene richiesta la password quando viene eseguito lo script di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1839d-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="1839d-160">Quando si esegue lo script di distribuzione, è necessario correggere i valori dei parametri Null.</span><span class="sxs-lookup"><span data-stu-id="1839d-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="1839d-161">Per usare il modello scaricato per aggiornare una configurazione:</span><span class="sxs-lookup"><span data-stu-id="1839d-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="1839d-162">Estrarre il contenuto in una cartella nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="1839d-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="1839d-163">Modificare il contenuto in modo da riflettere la nuova configurazione.</span><span class="sxs-lookup"><span data-stu-id="1839d-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="1839d-164">Avviare PowerShell e passare alla cartella in cui è stato estratto il contenuto.</span><span class="sxs-lookup"><span data-stu-id="1839d-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="1839d-165">Eseguire **deploy.ps1** e immettere ID sottoscrizione, nome del gruppo di risorse (usare lo stesso nome per aggiornare la configurazione) e un nome di distribuzione univoco.</span><span class="sxs-lookup"><span data-stu-id="1839d-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="1839d-166">Distribuire l’estensione Diagnostica come parte della creazione di cluster tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1839d-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="1839d-167">Per creare un cluster tramite Resource Manager, è necessario aggiungere il file JSON di configurazione di Diagnostica al modello di Resource Manager di tipo cluster completo prima di creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="1839d-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="1839d-168">Gli esempi relativi ai modelli di Gestione risorse includono un modello di cluster con 5 VM con aggiunta della configurazione di Diagnostica,</span><span class="sxs-lookup"><span data-stu-id="1839d-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="1839d-169">disponibile nella raccolta di esempi di Azure nella pagina relativa all'[esempio di modello di Resource Manager di cluster con cinque nodi con Diagnostica](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="1839d-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="1839d-170">Per visualizzare l'impostazione di Diagnostica nel modello di Resource Manager, aprire il file azuredeploy.json e cercare **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="1839d-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="1839d-171">Per creare un cluster con questo modello, è sufficiente selezionare il pulsante di **distribuzione in Azure** disponibile nel collegamento precedente.</span><span class="sxs-lookup"><span data-stu-id="1839d-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="1839d-172">In alternativa, è possibile scaricare l'esempio di Resource Manager, modificarlo e creare un cluster con il modello modificato mediante il comando `New-AzureRmResourceGroupDeployment` in una finestra di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1839d-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="1839d-173">Per i parametri passati al comando, vedere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="1839d-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="1839d-174">Per informazioni dettagliate sulla distribuzione di un gruppo di risorse con PowerShell, vedere l'articolo su come [distribuire un gruppo di risorse con un modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="1839d-175">Distribuire l'estensione Diagnostica in un cluster esistente</span><span class="sxs-lookup"><span data-stu-id="1839d-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="1839d-176">Se in un cluster esistente non è stata distribuita l'estensione Diagnostica o se si vuole modificare una configurazione esistente, è possibile aggiungerla o aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="1839d-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="1839d-177">Modificare il modello di Resource Manager usato per creare il cluster esistente o scaricare il modello dal portale come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1839d-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="1839d-178">Modificare il file template.json eseguendo le attività seguenti.</span><span class="sxs-lookup"><span data-stu-id="1839d-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="1839d-179">Aggiungere una nuova risorsa di archiviazione al modello nella sezione risorse.</span><span class="sxs-lookup"><span data-stu-id="1839d-179">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="1839d-180">Aggiungere quindi alla sezione parametri subito dopo le definizioni dell'account di archiviazione, tra `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="1839d-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="1839d-181">Sostituire il testo segnaposto *storage account name goes here* con il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1839d-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="1839d-182">Aggiornare quindi la sezione `VirtualMachineProfile` del file template.json aggiungendo quanto segue all'interno della matrice delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="1839d-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="1839d-183">Assicurarsi di aggiungere una virgola all'inizio o alla fine, a seconda del punto di inserimento.</span><span class="sxs-lookup"><span data-stu-id="1839d-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="1839d-184">Dopo aver modificato il file template.json come descritto, pubblicare nuovamente il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1839d-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="1839d-185">Se il modello è stato esportato, eseguire il file deploy.ps1 per pubblicarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="1839d-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="1839d-186">Dopo la distribuzione, assicurarsi che il valore di **ProvisioningState** sia **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="1839d-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="1839d-187">Aggiornare i dati di diagnostica per raccogliere eventi di integrità e di caricamento</span><span class="sxs-lookup"><span data-stu-id="1839d-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="1839d-188">A partire dalla versione 5.4 di Service Fabric è possibile raccogliere gli eventi di metrica di integrità e caricamento.</span><span class="sxs-lookup"><span data-stu-id="1839d-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="1839d-189">Questi riflettono gli eventi generati dal sistema o dal codice usando le API di creazione di report di integrità o caricamento, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="1839d-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="1839d-190">Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento.</span><span class="sxs-lookup"><span data-stu-id="1839d-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="1839d-191">Per visualizzare tali eventi nel visualizzatore eventi di diagnostica di Visual Studio, aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" all'elenco di provider ETW.</span><span class="sxs-lookup"><span data-stu-id="1839d-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="1839d-192">Per raccogliere gli eventi, modificare il modello di Resource Manager includendo quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1839d-192">To collect the events, modify the resource manager template to include</span></span>

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="1839d-193">Aggiornare Diagnostica per raccogliere e caricare log da nuovi canali EventSource</span><span class="sxs-lookup"><span data-stu-id="1839d-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="1839d-194">Per aggiornare Diagnostica in modo da raccogliere log da nuovi canali EventSource che rappresentano una nuova applicazione da distribuire, eseguire gli stessi passaggi illustrati nella [sezione precedente](#deploywadarm) per la configurazione di Diagnostica per un cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="1839d-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="1839d-195">Aggiornare la sezione `EtwEventSourceProviderConfiguration` nel file template.json per aggiungere voci per i nuovi canali EventSource prima di applicare l'aggiornamento della configurazione tramite il comando `New-AzureRmResourceGroupDeployment` di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1839d-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="1839d-196">Il nome dell'origine evento è definito come parte del codice del file ServiceEventSource.cs generato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1839d-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="1839d-197">Ad esempio, se l'origine evento è denominato My Eventsource, aggiungere il codice seguente per inserire gli eventi da My Eventsource in una tabella denominata MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="1839d-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="1839d-198">Per raccogliere i contatori delle prestazioni o i log eventi, modificare il modello di Resource Manager tramite gli esempi forniti in [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante i modelli di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1839d-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1839d-199">Pubblicare di nuovo il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1839d-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1839d-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1839d-200">Next steps</span></span>
<span data-ttu-id="1839d-201">Per informazioni più dettagliate sugli eventi da esaminare durante la risoluzione dei problemi, vedere gli eventi di diagnostica emessi per [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) e [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="1839d-202">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="1839d-202">Related articles</span></span>
* [<span data-ttu-id="1839d-203">Informazioni su come raccogliere i contatori delle prestazioni o i log mediante l'estensione Diagnostica</span><span class="sxs-lookup"><span data-stu-id="1839d-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1839d-204">Soluzione Service Fabric in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1839d-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

