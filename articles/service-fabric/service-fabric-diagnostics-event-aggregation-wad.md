---
title: Aggregazione evento dei servizi dell'infrastruttura con diagnostica di Windows Azure aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="7ee59-103">Aggregazione e raccolta di eventi con Diagnostica di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7ee59-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ee59-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7ee59-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="7ee59-105">Linux</span><span class="sxs-lookup"><span data-stu-id="7ee59-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="7ee59-106">Quando si esegue un cluster di Azure Service Fabric, è un log di hello buona toocollect da tutti i nodi di hello in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="7ee59-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="7ee59-107">La presenza di log hello in una posizione centrale consente di analizzare e risolvere i problemi del cluster, o problemi in applicazioni hello e servizi in esecuzione in tale cluster.</span><span class="sxs-lookup"><span data-stu-id="7ee59-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="7ee59-108">Tooupload un modo e raccogliere i log è toouse estensione di Windows Azure di diagnostica hello, che consente di caricare i log tooAzure archiviazione e dispone inoltre di hello opzione toosend registri tooAzure Application Insights o hub eventi.</span><span class="sxs-lookup"><span data-stu-id="7ee59-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="7ee59-109">È inoltre possibile utilizzare gli eventi di hello tooread un processo esterno dall'archivio e inserirle in un prodotto di piattaforma di analisi, ad esempio [OMS Log Analitica](../log-analytics/log-analytics-service-fabric.md) o un'altra soluzione di analisi di log.</span><span class="sxs-lookup"><span data-stu-id="7ee59-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ee59-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7ee59-110">Prerequisites</span></span>
<span data-ttu-id="7ee59-111">Questi strumenti sono tooperform usate alcune delle operazioni di hello in questo documento:</span><span class="sxs-lookup"><span data-stu-id="7ee59-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="7ee59-112">[Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (correlata tooAzure servizi Cloud, ma con informazioni ed esempi)</span><span class="sxs-lookup"><span data-stu-id="7ee59-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="7ee59-113">Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7ee59-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7ee59-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ee59-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="7ee59-115">Client di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ee59-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="7ee59-116">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ee59-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="7ee59-117">Origini di log ed eventi</span><span class="sxs-lookup"><span data-stu-id="7ee59-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="7ee59-118">Eventi della piattaforma Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ee59-118">Service Fabric platform events</span></span>
<span data-ttu-id="7ee59-119">Come descritto in [questo articolo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric set di con alcuni canali di registrazione della casella, di cui hello seguenti canali sono facili da configurare con WAD toosend monitoraggio e diagnostica tooa archiviazione tabella dati o in altre posizioni:</span><span class="sxs-lookup"><span data-stu-id="7ee59-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="7ee59-120">Gli eventi operativi: le operazioni di alto livello che hello Service Fabric piattaforma esegue.</span><span class="sxs-lookup"><span data-stu-id="7ee59-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="7ee59-121">Gli esempi includono la creazione di applicazioni e servizi, le modifiche allo stato dei nodi e informazioni sull'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7ee59-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="7ee59-122">Questi eventi vengono generati come log di Event Tracing for Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="7ee59-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="7ee59-123">Eventi del modello di programmazione Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="7ee59-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="7ee59-124">Eventi relativi al modello di programmazione Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7ee59-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="7ee59-125">Eventi dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7ee59-125">Application events</span></span>
 <span data-ttu-id="7ee59-126">Gli eventi generati dal codice delle applicazioni e dei servizi e scritto utilizzando una classe helper di EventSource hello fornito in hello modelli di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ee59-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="7ee59-127">Per ulteriori informazioni sulla modalità di registrazione toowrite EventSource dall'applicazione, vedere [Monitor e diagnosticare i servizi in una configurazione di sviluppo locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="7ee59-128">Distribuire l'estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="7ee59-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="7ee59-129">Hello primo passaggio per la raccolta di log è l'estensione di diagnostica toodeploy hello in ognuna delle macchine virtuali di hello in cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="7ee59-130">Hello estensione di diagnostica raccoglie i log in ogni macchina virtuale e li carica toohello account di archiviazione specificato.</span><span class="sxs-lookup"><span data-stu-id="7ee59-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="7ee59-131">passaggi di Hello variano leggermente in base che si utilizzi hello portale di Azure o Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee59-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="7ee59-132">procedura di Hello anche varia a seconda che la distribuzione di hello fa parte della creazione del cluster o per un cluster che esiste già.</span><span class="sxs-lookup"><span data-stu-id="7ee59-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="7ee59-133">Esaminiamo i passaggi di hello per ogni scenario.</span><span class="sxs-lookup"><span data-stu-id="7ee59-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="7ee59-134">Distribuire l'estensione di diagnostica hello come parte della creazione del cluster tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7ee59-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="7ee59-135">toodeploy hello diagnostica estensione toohello macchine virtuali in cluster hello come parte della creazione del cluster, utilizzare pannello impostazioni di diagnostica hello illustrato nell'esempio hello immagine, assicurarsi che la diagnostica è troppo**su** (hello l'impostazione predefinita) .</span><span class="sxs-lookup"><span data-stu-id="7ee59-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="7ee59-136">Dopo aver creato il cluster hello, è possibile modificare queste impostazioni mediante il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Impostazioni di diagnostica di Azure nel portale di hello per la creazione del cluster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="7ee59-138">Quando si crea un cluster tramite il portale di hello, si consiglia di scaricare il modello di hello **prima di scegliere OK** cluster hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ee59-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="7ee59-139">Per informazioni dettagliate, vedere troppo[configurazione di un cluster di Service Fabric utilizzando un modello di gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="7ee59-140">È necessario toomake modifiche al modello hello in un secondo momento, poiché non è possibile apportare alcune modifiche tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="7ee59-141">Distribuire l'estensione di diagnostica hello come parte della creazione del cluster usando Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7ee59-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="7ee59-142">toocreate un cluster usando Gestione risorse, è necessario tooadd hello diagnostica JSON toohello completo del cluster di gestione delle risorse modello di configurazione prima di creare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="7ee59-143">Offriamo un modello di gestione risorse di esempio 5-VM cluster con configurazione di diagnostica aggiunti tooit come parte di esempi di gestione delle risorse modello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="7ee59-144">È possibile visualizzarlo in questa posizione nella raccolta di esempi di Azure hello: [cluster cinque nodi con il modello di gestione risorse diagnostica esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="7ee59-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="7ee59-145">impostazione di diagnostica hello toosee nel modello di gestione risorse di hello, file azuredeploy.json aprire hello e cercare **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="7ee59-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="7ee59-146">un cluster utilizzando questo modello, seleziona hello toocreate **distribuire tooAzure** pulsante disponibile all'indirizzo collegamento precedente hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="7ee59-147">In alternativa, è possibile scaricare Gestione risorse: esempio hello, apportare le modifiche tooit e creare un cluster con modello modificato hello utilizzando hello `New-AzureRmResourceGroupDeployment` comando in una finestra di PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee59-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="7ee59-148">Vedere hello seguente codice per i parametri di hello che viene passato nel comando toohello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="7ee59-149">Per informazioni dettagliate sul modo in cui raggruppare toodeploy una risorsa tramite PowerShell, vedere l'articolo hello [distribuire un gruppo di risorse con il modello di gestione risorse di Azure hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="7ee59-150">Distribuire cluster esistente tooan estensione diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="7ee59-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="7ee59-151">Se si dispone di un cluster esistente che non dispone di diagnostica distribuita o se si desidera toomodify una configurazione esistente, è possibile aggiungere o aggiornare.</span><span class="sxs-lookup"><span data-stu-id="7ee59-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="7ee59-152">Modificare modello di gestione risorse hello cluster esistente di hello toocreate usato o scaricare il modello di hello dal portale hello come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7ee59-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="7ee59-153">Modificare il file di template.json hello eseguendo hello seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="7ee59-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="7ee59-154">Aggiungere un nuovo modello toohello risorse di archiviazione aggiungendo toohello sezione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="7ee59-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="7ee59-155">Successivamente, aggiungere parametri toohello sezione subito dopo le definizioni account di archiviazione hello, tra `supportLogStorageAccountName` e `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="7ee59-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="7ee59-156">Sostituire il testo segnaposto hello *nome account di archiviazione qui* con nome hello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7ee59-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="7ee59-157">Quindi, aggiornare hello `VirtualMachineProfile` sezione del file template.json hello aggiungendo hello seguente codice all'interno della matrice estensioni hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="7ee59-158">Essere tooadd che una virgola all'inizio di hello o alla fine di hello, a seconda di dove viene inserito.</span><span class="sxs-lookup"><span data-stu-id="7ee59-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="7ee59-159">Dopo aver modificato il file template.json hello come descritto, è possibile ripubblicare il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="7ee59-160">Se è stato esportato il modello di hello, l'esecuzione del file di deploy.ps1 hello Ripubblica modello hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="7ee59-161">Dopo la distribuzione, assicurarsi che il valore di **ProvisioningState** sia **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="7ee59-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="7ee59-162">Raccogliere gli eventi di integrità e di caricamento</span><span class="sxs-lookup"><span data-stu-id="7ee59-162">Collect health and load events</span></span>

<span data-ttu-id="7ee59-163">A partire dalla versione di hello 5.4 di Service Fabric, gli eventi di metrica di integrità e carico sono disponibili per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="7ee59-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="7ee59-164">Questi eventi riflettono gli eventi generati dal sistema hello o il codice tramite integrità hello o caricare le API di creazione di report, ad esempio [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee59-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="7ee59-165">Ciò consente l'aggregazione e la visualizzazione dell'integrità del sistema nel tempo, nonché la generazione di avvisi in base a eventi di integrità o di caricamento.</span><span class="sxs-lookup"><span data-stu-id="7ee59-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="7ee59-166">tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000008" toohello elenco dei provider ETW.</span><span class="sxs-lookup"><span data-stu-id="7ee59-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="7ee59-167">eventi di hello toocollect, modificare hello Gestione risorse modello tooinclude</span><span class="sxs-lookup"><span data-stu-id="7ee59-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="7ee59-168">Raccogliere eventi del proxy inverso</span><span class="sxs-lookup"><span data-stu-id="7ee59-168">Collect reverse proxy events</span></span>

<span data-ttu-id="7ee59-169">A partire dalla versione di hello 5.7 dell'infrastruttura di servizio, [proxy inverso](service-fabric-reverseproxy.md) eventi sono disponibili per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="7ee59-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="7ee59-170">Proxy inverso genera eventi in due canali, un errore che contiene gli eventi che riflettono richiedere gli errori di elaborazione e altro contenente gli eventi dettagliati su tutte le richieste di hello elaborati nel proxy inverso hello hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="7ee59-171">Raccolta eventi di errore: tooview questi eventi nel Visualizzatore eventi di diagnostica di Visual Studio aggiungere "Microsoft-ServiceFabric:4:0x4000000000000010" toohello elenco dei provider ETW.</span><span class="sxs-lookup"><span data-stu-id="7ee59-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="7ee59-172">gli eventi di hello toocollect dal cluster di Azure, modificare hello Gestione risorse modello tooinclude</span><span class="sxs-lookup"><span data-stu-id="7ee59-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="7ee59-173">Raccogliere tutti gli eventi di elaborazione della richiesta: Visualizzatore eventi diagnostica In Visual Studio, aggiornamento voce hello Microsoft ServiceFabric hello elenco di provider ETW troppo "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="7ee59-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="7ee59-174">Per i cluster di Azure Service Fabric, modificare hello resource manager modello tooinclude</span><span class="sxs-lookup"><span data-stu-id="7ee59-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="7ee59-175">È consigliabile toojudiciously Abilita raccolta degli eventi da questo canale in quanto consente di raccogliere tutto il traffico tramite proxy inverso hello e può utilizzare rapidamente capacità di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7ee59-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="7ee59-176">Per i cluster di Azure Service Fabric, gli eventi di hello da tutti i nodi di hello vengono raccolti e aggregati in hello SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="7ee59-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="7ee59-177">Per risoluzione dei problemi degli eventi di proxy inverso hello dettagliata, fare riferimento hello [Guida di diagnostica proxy inverso](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="7ee59-178">Eseguire la raccolta dai nuovi canali EventSource</span><span class="sxs-lookup"><span data-stu-id="7ee59-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="7ee59-179">log di toocollect tooupdate diagnostica da nuovi canali EventSource che rappresentano una nuova applicazione che è quasi toodeploy, eseguire hello stessi passaggi come descritto in precedenza per l'installazione di hello di diagnostica per un cluster esistente.</span><span class="sxs-lookup"><span data-stu-id="7ee59-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="7ee59-180">Aggiornare hello `EtwEventSourceProviderConfiguration` sezione nelle voci di hello template.json file tooadd per hello nuovi EventSource canali prima di applicare la configurazione hello aggiornare utilizzando hello `New-AzureRmResourceGroupDeployment` comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ee59-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="7ee59-181">nome di Hello dell'origine evento hello è definito come parte del codice nel file di Visual Studio generati ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="7ee59-182">Ad esempio, se l'origine eventi è denominato My Eventsource, aggiungere hello dopo gli eventi di codice tooplace hello da My Eventsource in una tabella denominata MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="7ee59-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="7ee59-183">i contatori delle prestazioni toocollect o nei registri eventi, è possibile modificare il modello di gestione risorse di hello usando hello esempi forniti in [creare una macchina virtuale Windows con monitoraggio e diagnostica utilizzando un modello di gestione risorse di Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ee59-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7ee59-184">Quindi, pubblicare di nuovo il modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="7ee59-185">Raccogliere i contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7ee59-185">Collect Performance Counters</span></span>

<span data-ttu-id="7ee59-186">le metriche delle prestazioni toocollect dal cluster, aggiungere tooyour di contatori delle prestazioni di hello "WadCfg > DiagnosticMonitorConfiguration" nel modello di gestione risorse di hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7ee59-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="7ee59-187">Per informazioni sui contatori delle prestazioni che è consigliabile raccogliere, vedere l'articolo relativo ai [contatori delle prestazioni in Service Fabric](service-fabric-diagnostics-event-generation-perf.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="7ee59-188">Ad esempio, di seguito viene impostato un contatore di prestazioni, campionato ogni 15 secondi (questo comportamento può essere modificato e segue hello formato di "PT\<ora >\<unità >", ad esempio, PT3M sarebbe esempio a intervalli di tre minuti) e trasferiti toohello tabella di archiviazione appropriato ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="7ee59-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="7ee59-189">Se si utilizza un sink di Application Insights, come descritto nella seguente sezione hello e si desidera tooshow queste metriche in Application Insights, assicurarsi che nome di sink hello tooadd della sezione "sink" hello come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7ee59-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="7ee59-190">Inoltre, è consigliabile creare toosend una tabella separata i contatori delle prestazioni, in modo che non troppi out hello hello di dati provenienti da altri canali di registrazione è stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="7ee59-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="7ee59-191">Trasmissione registra informazioni dettagliate tooApplication</span><span class="sxs-lookup"><span data-stu-id="7ee59-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="7ee59-192">L'invio di dati di monitoraggio e diagnostica tooApplication Insights (AI) può essere eseguita come parte della configurazione di WAD hello.</span><span class="sxs-lookup"><span data-stu-id="7ee59-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="7ee59-193">Se si decide di toouse per la visualizzazione e analisi degli eventi, leggere [analisi degli eventi e la visualizzazione con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset un sink AI come parte del "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="7ee59-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ee59-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ee59-194">Next steps</span></span>

<span data-ttu-id="7ee59-195">Dopo aver configurato correttamente diagnostica Windows Azure, verranno visualizzati dati nelle tabelle di archiviazione da hello ETW e i registri di EventSource.</span><span class="sxs-lookup"><span data-stu-id="7ee59-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="7ee59-196">Se si sceglie toouse OMS, Kibana o qualsiasi altra dati analitica e la visualizzazione piattaforma che non viene configurata direttamente nel modello di gestione risorse di hello, apportare tooset che compongono la piattaforma hello di tooread la scelta hello dati da tali tabelle di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7ee59-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="7ee59-197">Questa operazione in OMS è relativamente semplice ed è illustrata nell'articolo relativo all'[analisi di eventi e log tramite OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="7ee59-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="7ee59-198">Application Insights è un po' di un caso speciale in questo senso, poiché può essere configurato come parte della configurazione dell'estensione diagnostica hello, fare riferimento toohello [appropriato](service-fabric-diagnostics-event-analysis-appinsights.md) se si sceglie toouse AI.</span><span class="sxs-lookup"><span data-stu-id="7ee59-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="7ee59-199">Non è presente alcun modo toofilter o pulitura hello gli eventi inviati toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="7ee59-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="7ee59-200">Se si non implementa un tooremove di elaborare gli eventi dalla tabella hello, tabella hello continuerà toogrow.</span><span class="sxs-lookup"><span data-stu-id="7ee59-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="7ee59-201">Attualmente è disponibile un esempio di un servizio di pulitura di dati in esecuzione in hello [esempio Watchdog](https://github.com/Azure-Samples/service-fabric-watchdog-service), è consigliabile scrivere uno per se stessi, a meno che non vi è un buon motivo per l'utente registri toostore oltre a un intervallo di 30 o 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="7ee59-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="7ee59-202">Informazioni su come i contatori delle prestazioni toocollect o i registri tramite hello estensione di diagnostica</span><span class="sxs-lookup"><span data-stu-id="7ee59-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="7ee59-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione degli eventi con Application Insights)</span><span class="sxs-lookup"><span data-stu-id="7ee59-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)</span></span>
* <span data-ttu-id="7ee59-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione di eventi con OMS)</span><span class="sxs-lookup"><span data-stu-id="7ee59-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md)</span></span>