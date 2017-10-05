---
title: Aggregazione di eventi di Azure Service Fabric con Diagnostica di Microsoft Azure | Microsoft Docs
description: Informazioni sull'aggregazione e la raccolta di eventi con Diagnostica di Microsoft Azure per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 5773361fdec4cb8ee54fa2856f6aa969d5dac4e9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="31cc0-103">Aggregazione e raccolta di eventi con Diagnostica di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="31cc0-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="31cc0-104">Windows</span><span class="sxs-lookup"><span data-stu-id="31cc0-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="31cc0-105">Linux</span><span class="sxs-lookup"><span data-stu-id="31cc0-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="31cc0-106">Quando si esegue un cluster Azure Service Fabric, è consigliabile raccogliere i log da tutti i nodi in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="31cc0-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="31cc0-107">Il salvataggio dei log in una posizione centrale semplifica l'analisi e la risoluzione di eventuali problemi nel cluster o nelle applicazioni e nei servizi in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="31cc0-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="31cc0-108">Un modo per caricare e raccogliere i log consiste nell'usare l'estensione Diagnostica di Microsoft Azure, che carica i log in Archiviazione di Azure e offre anche la possibilità di inviarli ad Azure Application Insights o Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="31cc0-108">One way to upload and collect logs is to use the Windows Azure Diagnostics (WAD) extension, which uploads logs to Azure Storage, and also has the option to send logs to Azure Application Insights or Event Hubs.</span></span> <span data-ttu-id="31cc0-109">È anche possibile usare un processo esterno per leggere gli eventi dalla risorsa di archiviazione e inserirli in una piattaforma di analisi come [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.</span><span class="sxs-lookup"><span data-stu-id="31cc0-109">You can also use an external process to read the events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31cc0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31cc0-110">Prerequisites</span></span>
<span data-ttu-id="31cc0-111">Per eseguire alcune delle operazioni descritte in questo documento vengono usati gli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="31cc0-111">These tools are used to perform some of the operations in this document:</span></span>

* <span data-ttu-id="31cc0-112">[Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata ai Servizi cloud di Azure, include alcune informazioni ed esempi utili)</span><span class="sxs-lookup"><span data-stu-id="31cc0-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="31cc0-113">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="31cc0-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="31cc0-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31cc0-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="31cc0-115">Client di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31cc0-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="31cc0-116">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="31cc0-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="31cc0-117">Origini di log ed eventi</span><span class="sxs-lookup"><span data-stu-id="31cc0-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="31cc0-118">Eventi della piattaforma Service Fabric</span><span class="sxs-lookup"><span data-stu-id="31cc0-118">Service Fabric platform events</span></span>
<span data-ttu-id="31cc0-119">Come illustrato in [questo articolo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric offre alcuni canali di registrazione predefiniti. Tra questi, i canali seguenti sono facilmente configurabili con Diagnostica di Microsoft Azure per inviare i dati di monitoraggio e diagnostica a una tabella di archiviazione o un'altra posizione.</span><span class="sxs-lookup"><span data-stu-id="31cc0-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which the following channels are easily configured with WAD to send monitoring and diagnostics data to a storage table or elsewhere:</span></span>
  * <span data-ttu-id="31cc0-120">Eventi operativi: operazioni generali eseguite dalla piattaforma Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="31cc0-120">Operational events: higher-level operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="31cc0-121">Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="31cc0-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="31cc0-122">Questi eventi vengono generati come log di Event Tracing for Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="31cc0-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="31cc0-123">Eventi del modello di programmazione Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="31cc0-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="31cc0-124">Eventi relativi al modello di programmazione Reliable Services</span><span class="sxs-lookup"><span data-stu-id="31cc0-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="31cc0-125">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="31cc0-125">Application events</span></span>
 <span data-ttu-id="31cc0-126">Eventi generati dal codice delle applicazioni e dei servizi e scritti con la classe helper EventSource disponibile nei modelli di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31cc0-126">Events emitted from your applications' and services' code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="31cc0-127">Per altre informazioni su come scrivere log EventSource dall'applicazione, vedere [Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-127">For more information on how to write EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="31cc0-128">Distribuire l'estensione Diagnostica</span><span class="sxs-lookup"><span data-stu-id="31cc0-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="31cc0-129">Il primo passaggio per la raccolta dei log consiste nel distribuire l'estensione Diagnostica in ogni VM del cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="31cc0-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="31cc0-130">Questa estensione raccoglie i log in ogni VM e li carica nell'account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="31cc0-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="31cc0-131">La procedura varia a seconda che si usi il portale di Azure oppure Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31cc0-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="31cc0-132">Anche i passaggi variano se la distribuzione fa parte della creazione del cluster o è relativa a un cluster già esistente.</span><span class="sxs-lookup"><span data-stu-id="31cc0-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="31cc0-133">Ecco la procedura per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="31cc0-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="31cc0-134">Distribuire l'estensione Diagnostica nell'ambito della creazione del cluster tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31cc0-134">Deploy the Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="31cc0-135">Per distribuire l'estensione Diagnostica nelle VM del cluster nell'ambito della creazione del cluster, si usa il pannello delle impostazioni di diagnostica illustrato nell'immagine seguente. Verificare che l'opzione Diagnostica sia impostata su **Sì** (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="31cc0-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image - ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="31cc0-136">Dopo aver creato il cluster, non è possibile modificare questa impostazione tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="31cc0-136">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Impostazioni di diagnostica di Azure nel portale per la creazione del cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="31cc0-138">Quando si crea un cluster con il portale, è consigliabile scaricare il modello **prima di fare clic su OK** per creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="31cc0-138">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="31cc0-139">Per informazioni dettagliate, vedere [Configurare un cluster di Service Fabric usando un modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-139">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="31cc0-140">Il modello è necessario per apportare modifiche in un secondo momento perché non è possibile apportare alcune modifiche tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="31cc0-140">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="31cc0-141">Distribuire l’estensione Diagnostica come parte della creazione di cluster tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="31cc0-141">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="31cc0-142">Per creare un cluster tramite Resource Manager, è necessario aggiungere il file JSON di configurazione di Diagnostica al modello di Resource Manager di tipo cluster completo prima di creare il cluster.</span><span class="sxs-lookup"><span data-stu-id="31cc0-142">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="31cc0-143">Gli esempi relativi ai modelli di Gestione risorse includono un modello di cluster con 5 VM con aggiunta della configurazione di Diagnostica,</span><span class="sxs-lookup"><span data-stu-id="31cc0-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="31cc0-144">disponibile nella raccolta di esempi di Azure nella pagina relativa all'[esempio di modello di Resource Manager di cluster con cinque nodi con Diagnostica](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="31cc0-144">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="31cc0-145">Per visualizzare l'impostazione di Diagnostica nel modello di Resource Manager, aprire il file azuredeploy.json e cercare **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="31cc0-145">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="31cc0-146">Per creare un cluster con questo modello, è sufficiente selezionare il pulsante di **distribuzione in Azure** disponibile nel collegamento precedente.</span><span class="sxs-lookup"><span data-stu-id="31cc0-146">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="31cc0-147">In alternativa, è possibile scaricare l'esempio di Resource Manager, modificarlo e creare un cluster con il modello modificato mediante il comando `New-AzureRmResourceGroupDeployment` in una finestra di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31cc0-147">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="31cc0-148">Per i parametri passati al comando, vedere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="31cc0-148">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="31cc0-149">Per informazioni dettagliate sulla distribuzione di un gruppo di risorse con PowerShell, vedere l'articolo su come [distribuire un gruppo di risorse con un modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-149">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="31cc0-150">Distribuire l'estensione Diagnostica in un cluster esistente</span><span class="sxs-lookup"><span data-stu-id="31cc0-150">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="31cc0-151">Se in un cluster esistente non è stata distribuita l'estensione Diagnostica o se si vuole modificare una configurazione esistente, è possibile aggiungerla o aggiornarla.</span><span class="sxs-lookup"><span data-stu-id="31cc0-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="31cc0-152">Modificare il modello di Resource Manager usato per creare il cluster esistente o scaricare il modello dal portale come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="31cc0-152">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="31cc0-153">Modificare il file template.json eseguendo le attività seguenti.</span><span class="sxs-lookup"><span data-stu-id="31cc0-153">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="31cc0-154">Aggiungere una nuova risorsa di archiviazione al modello nella sezione risorse.</span><span class="sxs-lookup"><span data-stu-id="31cc0-154">Add a new storage resource to the template by adding to the resources section.</span></span>

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

 <span data-ttu-id="31cc0-155">Aggiungere quindi alla sezione parametri subito dopo le definizioni dell'account di archiviazione, tra `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="31cc0-155">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="31cc0-156">Sostituire il testo segnaposto *storage account name goes here* con il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31cc0-156">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

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
<span data-ttu-id="31cc0-157">Aggiornare quindi la sezione `VirtualMachineProfile` del file template.json aggiungendo quanto segue all'interno della matrice delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="31cc0-157">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="31cc0-158">Assicurarsi di aggiungere una virgola all'inizio o alla fine, a seconda del punto di inserimento.</span><span class="sxs-lookup"><span data-stu-id="31cc0-158">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="31cc0-159">Dopo aver modificato il file template.json come descritto, pubblicare nuovamente il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31cc0-159">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="31cc0-160">Se il modello è stato esportato, eseguire il file deploy.ps1 per pubblicarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="31cc0-160">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="31cc0-161">Dopo la distribuzione, assicurarsi che il valore di **ProvisioningState** sia **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="31cc0-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="31cc0-162">Raccogliere gli eventi di integrità e di caricamento</span><span class="sxs-lookup"><span data-stu-id="31cc0-162">Collect health and load events</span></span>

<span data-ttu-id="31cc0-163">A partire dalla versione 5.4 di Service Fabric è possibile raccogliere gli eventi di metrica di integrità e caricamento.</span><span class="sxs-lookup"><span data-stu-id="31cc0-163">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="31cc0-164">Questi riflettono gli eventi generati dal sistema o dal codice usando le API di creazione di report di integrità o caricamento, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="31cc0-164">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="31cc0-165">Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento.</span><span class="sxs-lookup"><span data-stu-id="31cc0-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="31cc0-166">Per visualizzare tali eventi nel visualizzatore eventi di diagnostica di Visual Studio, aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" all'elenco di provider ETW.</span><span class="sxs-lookup"><span data-stu-id="31cc0-166">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="31cc0-167">Per raccogliere gli eventi, modificare il modello di Resource Manager in modo da includere</span><span class="sxs-lookup"><span data-stu-id="31cc0-167">To collect the events, modify the Resource Manager template to include</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="31cc0-168">Raccogliere eventi del proxy inverso</span><span class="sxs-lookup"><span data-stu-id="31cc0-168">Collect reverse proxy events</span></span>

<span data-ttu-id="31cc0-169">A partire dalla versione 5.7 di Service Fabric, è possibile raccogliere gli eventi del [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-169">Starting with the 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="31cc0-170">Il proxy inverso emette eventi in due canali, uno dei quali contiene gli eventi di errore corrispondenti agli errori di elaborazione delle richieste e l'altro contiene gli eventi dettagliati relativi a tutte le richieste elaborate nel proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="31cc0-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and the other one containing verbose events about all the requests processed at the reverse proxy.</span></span> 

1. <span data-ttu-id="31cc0-171">Raccogliere gli eventi di errore: per visualizzare questi eventi nel visualizzatore eventi di diagnostica di Visual Studio, aggiungere "Microsoft-ServiceFabric:4:0x4000000000000010" all'elenco di provider ETW.</span><span class="sxs-lookup"><span data-stu-id="31cc0-171">Collect error events: To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" to the list of ETW providers.</span></span>
<span data-ttu-id="31cc0-172">Per raccogliere gli eventi dai cluster di Azure, modificare il modello di Resource Manager in modo da includere</span><span class="sxs-lookup"><span data-stu-id="31cc0-172">To collect the events from Azure clusters, modify the Resource Manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="31cc0-173">Raccogliere tutti gli eventi di elaborazione delle richieste: nel visualizzatore eventi di diagnostica di Visual Studio aggiornare la voce Microsoft-ServiceFabric nell'elenco di provider ETW modificandola in "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="31cc0-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update the Microsoft-ServiceFabric entry in the ETW provider list to "Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="31cc0-174">Per i cluster di Azure Service Fabric, modificare il modello di Resource Manager in modo da includere</span><span class="sxs-lookup"><span data-stu-id="31cc0-174">For Azure Service Fabric clusters, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="31cc0-175">È consigliabile abilitare la raccolta degli eventi in modo sensato da questo canale, in quanto raccoglie tutto il traffico attraverso il proxy inverso e può consumare rapidamente la capacità di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31cc0-175">It is recommended to judiciously enable collecting events from this channel as this collects all traffic through the reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="31cc0-176">Per i cluster di Azure Service Fabric, vengono raccolti gli eventi da tutti i nodi, che vengono aggregati in SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="31cc0-176">For Azure Service Fabric clusters, the events from all the nodes are collected and aggregated in the SystemEventTable.</span></span>
<span data-ttu-id="31cc0-177">Per informazioni dettagliate sulla risoluzione dei problemi relativi agli eventi del proxy inverso, vedere la [guida alla diagnostica dei problemi relativi al proxy inverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-177">For detailed troubleshooting of the reverse proxy events, refer the [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="31cc0-178">Eseguire la raccolta dai nuovi canali EventSource</span><span class="sxs-lookup"><span data-stu-id="31cc0-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="31cc0-179">Per aggiornare Diagnostica in modo da raccogliere log da nuovi canali EventSource che rappresentano una nuova applicazione da distribuire, eseguire gli stessi passaggi descritti in precedenza per la configurazione di Diagnostica per un cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="31cc0-179">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as previously described for the setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="31cc0-180">Aggiornare la sezione `EtwEventSourceProviderConfiguration` nel file template.json per aggiungere voci per i nuovi canali EventSource prima di applicare l'aggiornamento della configurazione tramite il comando `New-AzureRmResourceGroupDeployment` di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31cc0-180">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="31cc0-181">Il nome dell'origine evento è definito come parte del codice del file ServiceEventSource.cs generato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31cc0-181">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="31cc0-182">Ad esempio, se l'origine evento è denominato My Eventsource, aggiungere il codice seguente per inserire gli eventi da My Eventsource in una tabella denominata MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="31cc0-182">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="31cc0-183">Per raccogliere i contatori delle prestazioni o i log eventi, modificare il modello di Resource Manager tramite gli esempi forniti in [Creare una macchina virtuale Windows con monitoraggio e diagnostica mediante i modelli di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31cc0-183">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="31cc0-184">Pubblicare di nuovo il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31cc0-184">Then, republish the Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="31cc0-185">Raccogliere i contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="31cc0-185">Collect Performance Counters</span></span>

<span data-ttu-id="31cc0-186">Per raccogliere metriche delle prestazioni dal cluster, aggiungere i contatori delle prestazioni a "WadCfg > DiagnosticMonitorConfiguration" nel modello di Resource Manager per il cluster.</span><span class="sxs-lookup"><span data-stu-id="31cc0-186">To collect performance metrics from your cluster, add the performance counters to your "WadCfg > DiagnosticMonitorConfiguration" in the Resource Manager template for your cluster.</span></span> <span data-ttu-id="31cc0-187">Per informazioni sui contatori delle prestazioni che è consigliabile raccogliere, vedere l'articolo relativo ai [contatori delle prestazioni in Service Fabric](service-fabric-diagnostics-event-generation-perf.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="31cc0-188">Di seguito, ad esempio, si imposta un contatore delle prestazioni con campionamento ogni 15 secondi e trasferimento nella tabella di archiviazione appropriata ogni minuto. La frequenza di campionamento può essere modificata seguendo il formato "PT\<tempo>\<unità>"; PT3M, ad esempio, determinerà il campionamento a intervalli di tre minuti.</span><span class="sxs-lookup"><span data-stu-id="31cc0-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows the format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred to the appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="31cc0-189">Se si usa un sink di Application Insights, come descritto nella sezione di seguito, e si vuole che queste metriche vengano visualizzate in Application Insights, aggiungere il nome del sink nella sezione "sinks" illustrata sopra.</span><span class="sxs-lookup"><span data-stu-id="31cc0-189">If you are using an Application Insights sink, as described in the section below, and want these metrics to show up in Application Insights, then make sure to add the sink name in the "sinks" section as shown above.</span></span> <span data-ttu-id="31cc0-190">Valutare inoltre la possibilità di creare una tabella separata in cui inviare i contatori delle prestazioni, per non esaurire lo spazio a disposizione dei dati provenienti dagli altri canali di registrazione che sono stati abilitati.</span><span class="sxs-lookup"><span data-stu-id="31cc0-190">Additionally, consider creating a separate table to send your Performance Counters to, so they don't crowd out the data coming from the other logging channels you have enabled.</span></span>


## <a name="send-logs-to-application-insights"></a><span data-ttu-id="31cc0-191">Inviare i log ad Application Insights</span><span class="sxs-lookup"><span data-stu-id="31cc0-191">Send logs to Application Insights</span></span>

<span data-ttu-id="31cc0-192">L'invio dei dati di monitoraggio e diagnostica ad Application Insights può essere eseguito nell'ambito della configurazione di Diagnostica di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="31cc0-192">Sending monitoring and diagnostics data to Application Insights (AI) can be done as part of the WAD configuration.</span></span> <span data-ttu-id="31cc0-193">Se si decide di usare Application Insights per l'analisi e la visualizzazione degli eventi, vedere [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione di eventi con Application Insights) per configurare un sink di Application Insights in "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="31cc0-193">If you decide to use AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) to set up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="31cc0-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31cc0-194">Next steps</span></span>

<span data-ttu-id="31cc0-195">Dopo aver configurato correttamente Diagnostica di Azure, sarà possibile visualizzare i dati nelle tabelle di archiviazione dai log EventSource ed ETW.</span><span class="sxs-lookup"><span data-stu-id="31cc0-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from the ETW and EventSource logs.</span></span> <span data-ttu-id="31cc0-196">Se si sceglie di usare OMS, Kibana o qualsiasi altra piattaforma di analisi e visualizzazione dati non configurata direttamente nel modello di Resource Manager, assicurarsi di configurare la piattaforma scelta per la lettura dei dati da queste tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="31cc0-196">If you choose to use OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in the Resource Manager template, make sure to set up the platform of your choice to read in the data from these storage tables.</span></span> <span data-ttu-id="31cc0-197">Questa operazione in OMS è relativamente semplice ed è illustrata nell'articolo relativo all'[analisi di eventi e log tramite OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="31cc0-198">Application Insights è un caso particolare sotto questo aspetto, perché può essere configurato nell'ambito della configurazione dell'estensione Diagnostica. Se si sceglie di usare Application Insights, vedere l'[articolo appropriato](service-fabric-diagnostics-event-analysis-appinsights.md).</span><span class="sxs-lookup"><span data-stu-id="31cc0-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of the Diagnostics extension configuration, so refer to the [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose to use AI.</span></span>

>[!NOTE]
><span data-ttu-id="31cc0-199">Attualmente non è possibile filtrare o eliminare gli eventi inviati alla tabella.</span><span class="sxs-lookup"><span data-stu-id="31cc0-199">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="31cc0-200">Se non si implementa un processo per rimuovere gli eventi dalla tabella, le dimensioni della tabella continueranno ad aumentare.</span><span class="sxs-lookup"><span data-stu-id="31cc0-200">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span> <span data-ttu-id="31cc0-201">È attualmente disponibile un esempio di servizio di eliminazione dati in esecuzione nel [watchdog di esempio](https://github.com/Azure-Samples/service-fabric-watchdog-service). È consigliabile scriverne uno personalizzato, a meno che non esista un motivo valido per archiviare i log per un intervallo di tempo superiore a 30 o 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="31cc0-201">Currently, there is an example of a data grooming service running in the [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you to store logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="31cc0-202">Informazioni su come raccogliere i contatori delle prestazioni o i log mediante l'estensione Diagnostica</span><span class="sxs-lookup"><span data-stu-id="31cc0-202">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="31cc0-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione di eventi con Application Insights)</span><span class="sxs-lookup"><span data-stu-id="31cc0-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)</span></span>
* <span data-ttu-id="31cc0-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione di eventi con OMS)</span><span class="sxs-lookup"><span data-stu-id="31cc0-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md)</span></span>