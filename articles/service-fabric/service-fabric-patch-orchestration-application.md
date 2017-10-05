---
title: Patch Orchestration Application di Azure Service Fabric | Microsoft Docs
description: Applicazione per automatizzare l'applicazione di patch ai sistemi operativi in un cluster di Service Fabric.
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="ca09e-103">Applicare patch al sistema operativo Windows nel cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ca09e-103">Patch the Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="ca09e-104">Patch Orchestration Application è un'applicazione Azure Service Fabric che automatizza l'applicazione di patch nei sistemi operativi in un cluster di Service Fabric in Azure senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="ca09e-104">The patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="ca09e-105">Patch Orchestration Application offre quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ca09e-105">The patch orchestration app provides the following:</span></span>

- <span data-ttu-id="ca09e-106">**Installazione automatica dell'aggiornamento del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="ca09e-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="ca09e-107">Gli aggiornamenti del sistema operativo vengono scaricati e installati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="ca09e-108">I nodi del cluster vengono riavviati in base alle esigenze senza tempi di inattività del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="ca09e-109">**Integrazione dell'integrità e l'applicazione di patch compatibile con il cluster**.</span><span class="sxs-lookup"><span data-stu-id="ca09e-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="ca09e-110">Durante l'applicazione degli aggiornamenti, Patch Orchestration Application esegue il monitoraggio dell'integrità dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-110">While applying updates, the patch orchestration app monitors the health of the cluster nodes.</span></span> <span data-ttu-id="ca09e-111">I nodi del cluster sono aggiornati un nodo alla volta o un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="ca09e-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="ca09e-112">Se l'integrità del cluster si arresta a causa del processo di applicazione di patch, l'applicazione di patch viene interrotta per impedire l'aggravarsi del problema.</span><span class="sxs-lookup"><span data-stu-id="ca09e-112">If the health of the cluster goes down due to the patching process, patching is stopped to prevent aggravating the problem.</span></span>

## <a name="internal-details-of-the-app"></a><span data-ttu-id="ca09e-113">Dettagli interni dell'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-113">Internal details of the app</span></span>

<span data-ttu-id="ca09e-114">Patch Orchestration Application è costituita dai sottocomponenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca09e-114">The patch orchestration app is composed of the following subcomponents:</span></span>

- <span data-ttu-id="ca09e-115">**Coordinator Service**: il servizio con stato è responsabile per:</span><span class="sxs-lookup"><span data-stu-id="ca09e-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="ca09e-116">Il coordinamento del processo di Windows Update nell'intero cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-116">Coordinating the Windows Update job on the entire cluster.</span></span>
    - <span data-ttu-id="ca09e-117">L'archiviazione del risultato delle operazioni completate di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-117">Storing the result of completed Windows Update operations.</span></span>
- <span data-ttu-id="ca09e-118">**Node Agent Service**: è un servizio senza stato che viene eseguito in tutti i nodi di cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca09e-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="ca09e-119">Il servizio è responsabile per:</span><span class="sxs-lookup"><span data-stu-id="ca09e-119">The service is responsible for:</span></span>
    - <span data-ttu-id="ca09e-120">Il bootstrap del Node Agent NTService.</span><span class="sxs-lookup"><span data-stu-id="ca09e-120">Bootstrapping the Node Agent NTService.</span></span>
    - <span data-ttu-id="ca09e-121">Il monitoraggio di Node Agent NTService</span><span class="sxs-lookup"><span data-stu-id="ca09e-121">Monitoring the Node Agent NTService.</span></span>
- <span data-ttu-id="ca09e-122">**Node agent NTService**: questo servizio di Windows NT viene eseguito con un privilegio di livello superiore (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="ca09e-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="ca09e-123">Il Node Agent Service e il Coordinator Service vengono invece eseguiti con un privilegio di livello inferiore (NETWORK SERVICE).</span><span class="sxs-lookup"><span data-stu-id="ca09e-123">In contrast, the Node Agent Service and the Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="ca09e-124">Il servizio è responsabile dell'esecuzione dei seguenti processi di Windows Update in tutti i nodi del cluster:</span><span class="sxs-lookup"><span data-stu-id="ca09e-124">The service is responsible for performing the following Windows Update jobs on all the cluster nodes:</span></span>
    - <span data-ttu-id="ca09e-125">Disabilitazione della connessione automatica a Windows Update nel nodo.</span><span class="sxs-lookup"><span data-stu-id="ca09e-125">Disabling automatic Windows Update on the node.</span></span>
    - <span data-ttu-id="ca09e-126">Download e installazione di Windows Update in base al criterio fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-126">Downloading and installing Windows Update according to the policy the user has provided.</span></span>
    - <span data-ttu-id="ca09e-127">Riavvio della macchina dopo l'installazione di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-127">Restarting the machine post Windows Update installation.</span></span>
    - <span data-ttu-id="ca09e-128">Caricamento dei risultati di Windows Update nel Coordinator Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-128">Uploading the results of Windows updates to the Coordinator Service.</span></span>
    - <span data-ttu-id="ca09e-129">Generazione di report sull'integrità in caso di un'operazione non riuscita dopo l'esaurimento di tutti i tentativi.</span><span class="sxs-lookup"><span data-stu-id="ca09e-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="ca09e-130">Patch Orchestration App usa il sistema di servizio di gestione della riparazione di Service Fabric per disabilitare o abilitare il nodo ed eseguire i controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="ca09e-130">The patch orchestration app uses the Service Fabric repair manager system service to disable or enable the node and perform health checks.</span></span> <span data-ttu-id="ca09e-131">L'attività di riparazione creata da Patch Orchestration App tiene traccia dell'avanzamento di Windows Update per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="ca09e-131">The repair task created by the patch orchestration app tracks the Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca09e-132">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ca09e-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="ca09e-133">Versione minima di runtime di Service Fabric supportata</span><span class="sxs-lookup"><span data-stu-id="ca09e-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ca09e-134">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="ca09e-134">Azure clusters</span></span>
<span data-ttu-id="ca09e-135">Patch Orchestration App deve essere eseguita nei cluster di Azure con versione di runtime di Service Fabric 5.5 o successive.</span><span class="sxs-lookup"><span data-stu-id="ca09e-135">The patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ca09e-136">Cluster locali autonomi</span><span class="sxs-lookup"><span data-stu-id="ca09e-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="ca09e-137">Patch Orchestration App deve essere eseguita nei cluster autonomi con versione di runtime di Service Fabric 5.6 o successive.</span><span class="sxs-lookup"><span data-stu-id="ca09e-137">The patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="ca09e-138">Abilitare il servizio di gestione della riparazione (se non è già in esecuzione)</span><span class="sxs-lookup"><span data-stu-id="ca09e-138">Enable the repair manager service (if it's not running already)</span></span>

<span data-ttu-id="ca09e-139">Patch Orchestration App richiede che il servizio del sistema di gestione della riparazione sia abilitato nel cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-139">The patch orchestration app requires the repair manager system service to be enabled on the cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="ca09e-140">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="ca09e-140">Azure clusters</span></span>

<span data-ttu-id="ca09e-141">I cluster di Azure al livello di durabilità silver hanno il servizio di gestione della riparazione abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ca09e-141">Azure clusters in the silver durability tier have the repair manager service enabled by default.</span></span> <span data-ttu-id="ca09e-142">I cluster di Azure al livello di durabilità gold potrebbero avere o non avere il servizio di gestione della riparazione abilitato, a seconda relativa data di creazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-142">Azure clusters in the gold durability tier might or might not have the repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="ca09e-143">I cluster di Azure al livello di durabilità bronze, per impostazione predefinita, non hanno il servizio di gestione della riparazione abilitato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-143">Azure clusters in the bronze durability tier, by default, do not have the repair manager service enabled.</span></span> <span data-ttu-id="ca09e-144">Se il servizio è già abilitato, è possibile vederlo in esecuzione nella sezione relativa ai servizi del sistema in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ca09e-144">If the service is already enabled, you can see it running in the system services section in the Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="ca09e-145">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ca09e-145">Azure portal</span></span>
<span data-ttu-id="ca09e-146">È possibile abilitare il servizio di gestione della riparazione dal portale di Azure al momento della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-146">You can enable repair manager from Azure portal at the time of setting up of cluster.</span></span> <span data-ttu-id="ca09e-147">Selezionare l'opzione `Include Repair Manager` in `Add on features` al momento della configurazione del Cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-147">Select `Include Repair Manager` option under `Add on features` at the time of Cluster configuration.</span></span>
<span data-ttu-id="ca09e-148">![Immagine dell'attivazione del servizio di gestione della riparazione dal portale di Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="ca09e-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="ca09e-149">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ca09e-149">Azure Resource Manager template</span></span>
<span data-ttu-id="ca09e-150">In alternativa, è possibile usare il [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) per abilitare il servizio di gestione della riparazione nei cluster nuovi ed esistenti di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca09e-150">Alternatively you can use the [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) to enable the repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="ca09e-151">Ottenere il modello per il cluster che si vuole distribuire.</span><span class="sxs-lookup"><span data-stu-id="ca09e-151">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="ca09e-152">È possibile usare i modelli di esempio o creare un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca09e-152">You can either use the sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="ca09e-153">Per abilitare il servizio di gestione della riparazione tramite il [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="ca09e-153">To enable the repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="ca09e-154">Verificare prima che il `apiversion` sia impostato su `2017-07-01-preview` per la risorsa `Microsoft.ServiceFabric/clusters` come illustrato nel frammento riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ca09e-154">First check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, as shown in the following snippet.</span></span> <span data-ttu-id="ca09e-155">Se il valore è diverso, è necessario aggiornare `apiVersion` a `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="ca09e-155">If it is different, then you need to update the `apiVersion` to the value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="ca09e-156">A questo punto, abilitare il servizio di gestione della riparazione aggiungendo la sezione seguente `addonFeatures` dopo la sezione `fabricSettings`:</span><span class="sxs-lookup"><span data-stu-id="ca09e-156">Now enable the repair manager service by adding the following `addonFeatures` section after the `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ca09e-157">Dopo aver aggiornato il modello del cluster con queste modifiche, applicarle e consentire la conclusione dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ca09e-157">After you have updated your cluster template with these changes, apply them and let the upgrade finish.</span></span> <span data-ttu-id="ca09e-158">È ora possibile vedere il servizio del sistema di gestione della riparazione in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-158">You can now see the repair manager system service running in your cluster.</span></span> <span data-ttu-id="ca09e-159">Viene chiamato `fabric:/System/RepairManagerService` nella sezione relativa ai servizi del sistema in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ca09e-159">It is called `fabric:/System/RepairManagerService` in the system services section in the Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="ca09e-160">Cluster locali autonomi</span><span class="sxs-lookup"><span data-stu-id="ca09e-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="ca09e-161">È possibile usare le [Impostazioni di configurazione per un cluster autonomo in Windows](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) per abilitare il servizio di gestione della riparazione nei cluster di Service Fabric nuovi ed esistenti.</span><span class="sxs-lookup"><span data-stu-id="ca09e-161">You can use the [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) to enable the repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="ca09e-162">Per abilitare il servizio di gestione della riparazione:</span><span class="sxs-lookup"><span data-stu-id="ca09e-162">To enable the repair manager service:</span></span>

1. <span data-ttu-id="ca09e-163">In primo luogo, verificare che `apiversion` in [Configurazioni generali del cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) sia impostato su `04-2017` o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="ca09e-163">First check that the `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set to `04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="ca09e-164">A questo punto abilitare il servizio di gestione della riparazione aggiungendo la sezione seguente `addonFeaturres` dopo la sezione `fabricSettings`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ca09e-164">Now enable repair manager service by adding the following `addonFeaturres` section after the `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="ca09e-165">Aggiornare il manifesto del cluster con queste modifiche usando il manifesto del cluster aggiornato [Creare un cluster autonomo in esecuzione su Windows Server](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) o [Aggiornare il cluster autonomo di Azure Service Fabric in Windows Server](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="ca09e-165">Update your cluster manifest with these changes, using the updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade the cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="ca09e-166">Quando il cluster è in esecuzione con il manifesto del cluster aggiornato, è possibile vedere il servizio del sistema di gestione della riparazione in esecuzione nel cluster, denominato `fabric:/System/RepairManagerService`, nella sezione relativa ai servizi del sistema in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ca09e-166">Once the cluster is running with updated cluster manifest, you can now see the repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in the Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="ca09e-167">Disabilitare la connessione automatica a Windows Update su tutti i nodi</span><span class="sxs-lookup"><span data-stu-id="ca09e-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="ca09e-168">Gli aggiornamenti automatici di Windows potrebbero causare la perdita di disponibilità perché più nodi del cluster possono riavviarsi nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="ca09e-168">Automatic Windows updates might lead to availability loss because multiple cluster nodes can restart at the same time.</span></span> <span data-ttu-id="ca09e-169">Patch Orchestration App, per impostazione predefinita, tenta di disabilitare la connessione automatica a Windows Update su ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-169">The patch orchestration app, by default, tries to disable the automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="ca09e-170">Tuttavia, nel caso in cui le impostazioni vengano gestite da un amministratore o dai criteri di gruppo, è consigliabile impostare i criteri di Windows Update sulla notifica prima del download in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="ca09e-170">However, if the settings are managed by an administrator or group policy, we recommend setting the Windows Update policy to “Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="ca09e-171">Facoltativo: abilitare Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="ca09e-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="ca09e-172">Per i cluster che eseguono la versione di runtime di Service Fabric `5.6.220.9494` e livelli successivi, verranno raccolti i log dell'app di orchestrazione come parte dei log di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca09e-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="ca09e-173">È possibile ignorare questo passaggio se il cluster è in esecuzione nella versione di runtime di Service Fabric `5.6.220.9494` e nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ca09e-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="ca09e-174">Per i cluster che eseguono la versione di runtime di Service Fabric precedente a `5.6.220.9494`, i log per l'app di orchestrazione delle patch vengono raccolti localmente su ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for the patch orchestration app are collected locally on each of the cluster nodes.</span></span>
<span data-ttu-id="ca09e-175">Si consiglia di configurare Diagnostica di Azure per caricare i log da tutti i nodi in una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="ca09e-175">We recommend that you configure Azure Diagnostics to upload logs from all nodes to a central location.</span></span>

<span data-ttu-id="ca09e-176">Per altre informazioni su come abilitare Diagnostica di Azure, vedere [Raccogliere log con Diagnostica di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="ca09e-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="ca09e-177">I log per Patch Orchestration App sono generati nei seguenti ID dei provider stabiliti:</span><span class="sxs-lookup"><span data-stu-id="ca09e-177">Logs for the patch orchestration app are generated on the following fixed provider IDs:</span></span>

- <span data-ttu-id="ca09e-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="ca09e-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="ca09e-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="ca09e-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="ca09e-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="ca09e-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="ca09e-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="ca09e-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="ca09e-182">Nel modello di Resource Manager passare alla sezione `EtwEventSourceProviderConfiguration` in `WadCfg` e aggiungere le seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="ca09e-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add the following entries:</span></span>

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> <span data-ttu-id="ca09e-183">Se il cluster di Service Fabric ha più tipi di nodo, è necessario aggiungere la sezione precedente per tutte le sezioni `WadCfg`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-183">If your Service Fabric cluster has multiple node types, then the previous section must be added for all the `WadCfg` sections.</span></span>

## <a name="download-the-app-package"></a><span data-ttu-id="ca09e-184">Scaricare il pacchetto dell'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-184">Download the app package</span></span>

<span data-ttu-id="ca09e-185">Scaricare l'applicazione dal [collegamento di download](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="ca09e-185">Download the application from the [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-the-app"></a><span data-ttu-id="ca09e-186">Configurare l'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-186">Configure the app</span></span>

<span data-ttu-id="ca09e-187">Il comportamento di Patch Orchestration App può essere configurato per soddisfare le esigenze.</span><span class="sxs-lookup"><span data-stu-id="ca09e-187">The behavior of the patch orchestration app can be configured to meet your needs.</span></span> <span data-ttu-id="ca09e-188">Eseguire l'override dei valori predefiniti passando il parametro dell'applicazione durante la creazione o l'aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-188">Override the default values by passing in the application parameter during application creation or update.</span></span> <span data-ttu-id="ca09e-189">È possibile fornire i parametri dell'applicazione specificando `ApplicationParameter` ai cmdlet `Start-ServiceFabricApplicationUpgrade` o `New-ServiceFabricApplication`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-189">Application parameters can be provided by specifying `ApplicationParameter` to the `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="ca09e-190">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="ca09e-190">**Parameter**</span></span>        |<span data-ttu-id="ca09e-191">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="ca09e-191">**Type**</span></span>                          | <span data-ttu-id="ca09e-192">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="ca09e-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="ca09e-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="ca09e-193">MaxResultsToCache</span></span>    |<span data-ttu-id="ca09e-194">long</span><span class="sxs-lookup"><span data-stu-id="ca09e-194">Long</span></span>                              | <span data-ttu-id="ca09e-195">Numero massimo di risultati di Windows Update memorizzabili nella cache.</span><span class="sxs-lookup"><span data-stu-id="ca09e-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="ca09e-196">Il valore predefinito è 3000 presumendo che il:</span><span class="sxs-lookup"><span data-stu-id="ca09e-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="ca09e-197">- Numero di nodi sia 20.</span><span class="sxs-lookup"><span data-stu-id="ca09e-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="ca09e-198">- Numero di aggiornamenti eseguiti su un nodo per ogni mese sia pari a cinque.</span><span class="sxs-lookup"><span data-stu-id="ca09e-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="ca09e-199">- Numero di risultati per ogni operazione sia pari a 10.</span><span class="sxs-lookup"><span data-stu-id="ca09e-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="ca09e-200">- I risultati per gli ultimi tre mesi debbano essere archiviati.</span><span class="sxs-lookup"><span data-stu-id="ca09e-200">- Results for the past three months should be stored.</span></span> |
|<span data-ttu-id="ca09e-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="ca09e-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="ca09e-202">Enum</span><span class="sxs-lookup"><span data-stu-id="ca09e-202">Enum</span></span> <br> <span data-ttu-id="ca09e-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="ca09e-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="ca09e-204">TaskApprovalPolicy indica i criteri che devono essere usati dal Coordinator Service per installare gli aggiornamenti di Windows Update nei nodi del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca09e-204">TaskApprovalPolicy indicates the policy that is to be used by the Coordinator Service to install Windows updates across the Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="ca09e-205">I valori consentiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca09e-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="ca09e-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="ca09e-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="ca09e-207">Windows Update viene installato un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="ca09e-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="ca09e-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="ca09e-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="ca09e-209">Windows Update viene installato un dominio di aggiornamento alla volta</span><span class="sxs-lookup"><span data-stu-id="ca09e-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="ca09e-210">(al massimo, tutti i nodi appartenenti a un dominio di aggiornamento possono passare per Windows Update).</span><span class="sxs-lookup"><span data-stu-id="ca09e-210">(At the maximum, all the nodes belonging to an upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="ca09e-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="ca09e-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="ca09e-212">long</span><span class="sxs-lookup"><span data-stu-id="ca09e-212">Long</span></span>  <br> <span data-ttu-id="ca09e-213">Predefinito: 1024</span><span class="sxs-lookup"><span data-stu-id="ca09e-213">(Default: 1024)</span></span>               |<span data-ttu-id="ca09e-214">Dimensione massima in MB dei log di Patch Orchestration App che è possibile salvare in modo permanente e locale sui nodi.</span><span class="sxs-lookup"><span data-stu-id="ca09e-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="ca09e-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="ca09e-215">WUQuery</span></span>               | <span data-ttu-id="ca09e-216">string</span><span class="sxs-lookup"><span data-stu-id="ca09e-216">string</span></span><br><span data-ttu-id="ca09e-217">Impostazione predefinita: "IsInstalled = 0"</span><span class="sxs-lookup"><span data-stu-id="ca09e-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="ca09e-218">Eseguire una query per ottenere gli aggiornamenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="ca09e-218">Query to get Windows updates.</span></span> <span data-ttu-id="ca09e-219">Per altre informazioni, vedere [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="ca09e-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="ca09e-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="ca09e-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="ca09e-221">Booleano</span><span class="sxs-lookup"><span data-stu-id="ca09e-221">Bool</span></span> <br> <span data-ttu-id="ca09e-222">Predefinito: True</span><span class="sxs-lookup"><span data-stu-id="ca09e-222">(default: True)</span></span>                 | <span data-ttu-id="ca09e-223">Questo flag consente l'installazione degli aggiornamenti del sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="ca09e-223">This flag allows Windows operating system updates to be installed.</span></span>            |
| <span data-ttu-id="ca09e-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="ca09e-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="ca09e-225">int</span><span class="sxs-lookup"><span data-stu-id="ca09e-225">Int</span></span> <br><span data-ttu-id="ca09e-226">Predefinito: 90</span><span class="sxs-lookup"><span data-stu-id="ca09e-226">(Default: 90)</span></span>                   | <span data-ttu-id="ca09e-227">Specifica il timeout per qualsiasi operazione di Windows Update (ricerca, download o installazione).</span><span class="sxs-lookup"><span data-stu-id="ca09e-227">Specifies the timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="ca09e-228">L'operazione viene interrotta se non viene completata entro il timeout specificato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-228">If the operation is not completed within the specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="ca09e-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="ca09e-229">WURescheduleCount</span></span>     | <span data-ttu-id="ca09e-230">int</span><span class="sxs-lookup"><span data-stu-id="ca09e-230">Int</span></span> <br> <span data-ttu-id="ca09e-231">Predefinito: 5</span><span class="sxs-lookup"><span data-stu-id="ca09e-231">(Default: 5)</span></span>                  | <span data-ttu-id="ca09e-232">Il numero massimo di volte in cui il servizio ripianifica l'aggiornamento di Windows quando un'operazione continua ad avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ca09e-232">The maximum number of times the service reschedules the Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="ca09e-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="ca09e-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="ca09e-234">int</span><span class="sxs-lookup"><span data-stu-id="ca09e-234">Int</span></span> <br><span data-ttu-id="ca09e-235">Predefinito: 30</span><span class="sxs-lookup"><span data-stu-id="ca09e-235">(Default: 30)</span></span> | <span data-ttu-id="ca09e-236">L'intervallo con cui il servizio ripianifica l'aggiornamento di Windows se il problema persiste.</span><span class="sxs-lookup"><span data-stu-id="ca09e-236">The interval at which the service reschedules the Windows update in case failure persists.</span></span> |
| <span data-ttu-id="ca09e-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="ca09e-237">WUFrequency</span></span>           | <span data-ttu-id="ca09e-238">Stringa separata da virgole Predefinito: "Weekly, Wednesday, 7:00:00"</span><span class="sxs-lookup"><span data-stu-id="ca09e-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="ca09e-239">La frequenza di installazione di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-239">The frequency for installing Windows Update.</span></span> <span data-ttu-id="ca09e-240">Il formato e i valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="ca09e-240">The format and possible values are:</span></span> <br><span data-ttu-id="ca09e-241">-   Monthly, DD,HH:MM:SS, ad esempio, Monthly, 5,12:22:32.</span><span class="sxs-lookup"><span data-stu-id="ca09e-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="ca09e-242">-   Weekly, DAY,HH:MM:SS, ad esempio, Weekly, Tuesday, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="ca09e-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="ca09e-243">-   Daily, HH:MM:SS, ad esempio, Daily, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="ca09e-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="ca09e-244">- None: indica che non deve essere eseguito Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="ca09e-245">SI noti che tutti gli orari sono in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="ca09e-245">Note that all the times are in UTC.</span></span>|
| <span data-ttu-id="ca09e-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="ca09e-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="ca09e-247">Booleano</span><span class="sxs-lookup"><span data-stu-id="ca09e-247">Bool</span></span> <br><span data-ttu-id="ca09e-248">Predefinito: True</span><span class="sxs-lookup"><span data-stu-id="ca09e-248">(Default: true)</span></span> | <span data-ttu-id="ca09e-249">Impostando questo flag, l'applicazione accetta il contratto di licenza dell'utente finale per Windows Update per conto del proprietario della macchina.</span><span class="sxs-lookup"><span data-stu-id="ca09e-249">By setting this flag, the application accepts the End-User License Agreement for Windows Update on behalf of the owner of the machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="ca09e-250">Se si desidera che Windows Update venga eseguito immediatamente, impostare `WUFrequency` in relazione al tempo di distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-250">If you want Windows Update to happen immediately, set `WUFrequency` relative to the application deployment time.</span></span> <span data-ttu-id="ca09e-251">Ad esempio, si supponga di disporre di un cluster di test a cinque nodi e si prevede di distribuire l'app all'incirca alle 17:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="ca09e-251">For example, suppose that you have a five-node test cluster and plan to deploy the app at around 5:00 PM UTC.</span></span> <span data-ttu-id="ca09e-252">Se si presuppone che l'aggiornamento o la distribuzione dell'applicazione richiedano un massimo di 30 minuti, impostare il WUFrequency su "Daily, 17:30:00".</span><span class="sxs-lookup"><span data-stu-id="ca09e-252">If you assume that the application upgrade or deployment takes 30 minutes at the maximum, set the WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-the-app"></a><span data-ttu-id="ca09e-253">Distribuire l'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-253">Deploy the app</span></span>

1. <span data-ttu-id="ca09e-254">Completare tutti i passaggi preliminari per preparare il cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-254">Finish all the prerequisite steps to prepare the cluster.</span></span>
2. <span data-ttu-id="ca09e-255">Distribuire Patch Orchestration App come qualsiasi altra app di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca09e-255">Deploy the patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="ca09e-256">È possibile distribuire l'app tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca09e-256">You can deploy the app by using PowerShell.</span></span> <span data-ttu-id="ca09e-257">Seguire la procedura in [Distribuire e rimuovere applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="ca09e-257">Follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="ca09e-258">Per configurare l'applicazione al momento della distribuzione, passare `ApplicationParamater` al cmdlet `New-ServiceFabricApplication`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-258">To configure the application at the time of deployment, pass the `ApplicationParamater` to the `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="ca09e-259">Per praticità, è stato fornito lo script Deploy.ps1 insieme all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-259">For your convenience, we’ve provided the script Deploy.ps1 along with the application.</span></span> <span data-ttu-id="ca09e-260">Per usare lo script:</span><span class="sxs-lookup"><span data-stu-id="ca09e-260">To use the script:</span></span>

    - <span data-ttu-id="ca09e-261">Connettersi a un cluster di Service Fabric tramite `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-261">Connect to a Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="ca09e-262">Eseguire lo script Deploy.ps1 di PowerShell con il valore `ApplicationParameter` appropriato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-262">Execute the PowerShell script Deploy.ps1 with the appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="ca09e-263">Mantenere lo script e la cartella dell'applicazione PatchOrchestrationApplication nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="ca09e-263">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="upgrade-the-app"></a><span data-ttu-id="ca09e-264">Aggiornare l'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-264">Upgrade the app</span></span>

<span data-ttu-id="ca09e-265">Per aggiornare una Patch Orchestration App esistente tramite PowerShell, seguire la procedura in [Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="ca09e-265">To upgrade an existing patch orchestration app by using PowerShell, follow the steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-the-app"></a><span data-ttu-id="ca09e-266">Rimuovere l'app</span><span class="sxs-lookup"><span data-stu-id="ca09e-266">Remove the app</span></span>

<span data-ttu-id="ca09e-267">Per rimuovere l'applicazione, seguire la procedura in [Distribuire e rimuovere applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="ca09e-267">To remove the application, follow the steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="ca09e-268">Per praticità, è stato fornito lo script Undeploy.ps1 insieme all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-268">For your convenience, we've provided the script Undeploy.ps1 along with the application.</span></span> <span data-ttu-id="ca09e-269">Per usare lo script:</span><span class="sxs-lookup"><span data-stu-id="ca09e-269">To use the script:</span></span>

  - <span data-ttu-id="ca09e-270">Connettersi a un cluster di Service Fabric tramite ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="ca09e-270">Connect to a Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="ca09e-271">Eseguire lo script Undeploy.ps1 di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca09e-271">Execute the PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="ca09e-272">Mantenere lo script e la cartella dell'applicazione PatchOrchestrationApplication nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="ca09e-272">Keep the script and the application folder PatchOrchestrationApplication in the same directory.</span></span>

## <a name="view-the-windows-update-results"></a><span data-ttu-id="ca09e-273">Visualizzare i risultati di Windows Update</span><span class="sxs-lookup"><span data-stu-id="ca09e-273">View the Windows Update results</span></span>

<span data-ttu-id="ca09e-274">Patch Orchestration Application espone l'API REST per visualizzare i risultati cronologici all'utente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-274">The patch orchestration app exposes REST APIs to display the historical results to the user.</span></span> <span data-ttu-id="ca09e-275">Un esempio del file JSON dei risultati:</span><span class="sxs-lookup"><span data-stu-id="ca09e-275">An example of the result JSON:</span></span>
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
<span data-ttu-id="ca09e-276">Se non è stato ancora pianificato alcun aggiornamento, il file JSON dei risultati è vuoto.</span><span class="sxs-lookup"><span data-stu-id="ca09e-276">If no update is scheduled yet, the result JSON is empty.</span></span>

<span data-ttu-id="ca09e-277">Accedere al cluster per eseguire la query sui risultati di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-277">Log in to the cluster to query Windows Update results.</span></span> <span data-ttu-id="ca09e-278">Trovare quindi l'indirizzo della replica per il primario del Coordinator Service e raggiungere l'URL dal browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="ca09e-278">Then find out the replica address for the primary of the Coordinator Service, and hit the URL from the browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ca09e-279">L'endpoint REST per Coordinator Service dispone di una porta dinamica.</span><span class="sxs-lookup"><span data-stu-id="ca09e-279">The REST endpoint for the Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="ca09e-280">Per controllare l'URL esatto, fare riferimento a Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="ca09e-280">To check the exact URL, refer to the Service Fabric Explorer.</span></span> <span data-ttu-id="ca09e-281">Ad esempio, i risultati sono disponibili in `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-281">For example, the results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Immagine dell'endpoint REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="ca09e-283">Nel caso in cui il proxy inverso sia abilitato nel cluster, l'utente può accedere all'URL anche dall'esterno del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-283">If the reverse proxy is enabled on the cluster, you can access the URL from outside of the cluster as well.</span></span>
<span data-ttu-id="ca09e-284">L'endpoint da scegliere è: http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="ca09e-284">The endpoint that needs to be hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="ca09e-285">Per abilitare il proxy inverso nel cluster, seguire la procedura in [Proxy inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="ca09e-285">To enable the reverse proxy on the cluster, follow the steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="ca09e-286">Dopo aver configurato il proxy inverso, tutti i microservizi nel cluster che espongono un endpoint HTTP sono indirizzabili dall'esterno del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-286">After the reverse proxy is configured, all micro services in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="ca09e-287">Eventi di diagnostica/integrità</span><span class="sxs-lookup"><span data-stu-id="ca09e-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="ca09e-288">Raccogliere i log di Patch Orchestration App</span><span class="sxs-lookup"><span data-stu-id="ca09e-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="ca09e-289">Vengono raccolti i log di Patch Orchestration App come parte dei log di Service Fabric dalla versione di runtime `5.6.220.9494` e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="ca09e-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="ca09e-290">Per i cluster che eseguono la versione di runtime di Service Fabric inferiore a `5.6.220.9494`, i log possono essere raccolti usando uno dei metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ca09e-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of the following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="ca09e-291">In locale in ogni nodo</span><span class="sxs-lookup"><span data-stu-id="ca09e-291">Locally on each node</span></span>

<span data-ttu-id="ca09e-292">I log vengono raccolti localmente su ogni nodo del cluster di Service Fabric se la versione del runtime di Service Fabric è precedente a `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="ca09e-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="ca09e-293">Il percorso per accedere ai log è \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="ca09e-293">The location to access the logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="ca09e-294">Ad esempio, se Service Fabric è installato nell'unità D, il percorso è D:\\PatchOrchestrationApplication\\logs.</span><span class="sxs-lookup"><span data-stu-id="ca09e-294">For example, if Service Fabric is installed on drive D, the path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="ca09e-295">Posizione centrale</span><span class="sxs-lookup"><span data-stu-id="ca09e-295">Central location</span></span>

<span data-ttu-id="ca09e-296">Se Diagnostica di Azure viene configurata come parte dei passaggi preliminari, i log per Patch Orchestration App sono disponibili in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ca09e-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for the patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="ca09e-297">Report sull'integrità</span><span class="sxs-lookup"><span data-stu-id="ca09e-297">Health reports</span></span>

<span data-ttu-id="ca09e-298">Patch Orchestration App pubblica anche i report sull'integrità per il Coordinator Service o il Node Agent Service nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca09e-298">The patch orchestration app also publishes health reports against the Coordinator Service or the Node Agent Service in the following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="ca09e-299">Un'operazione di Windows Update ha avuto esito negativo</span><span class="sxs-lookup"><span data-stu-id="ca09e-299">A Windows Update operation failed</span></span>

<span data-ttu-id="ca09e-300">Se un'operazione di Windows Update ha esito negativo in un nodo, viene generato un report sull'integrità del Node Agent Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-300">If a Windows Update operation fails on a node, a health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="ca09e-301">I dettagli del report sull'integrità contengono il nome del nodo problematico.</span><span class="sxs-lookup"><span data-stu-id="ca09e-301">Details of the health report contain the problematic node name.</span></span>

<span data-ttu-id="ca09e-302">Il report viene cancellato automaticamente dopo che viene completata correttamente l'applicazione delle patch nel nodo problematico.</span><span class="sxs-lookup"><span data-stu-id="ca09e-302">After patching is successfully completed on the problematic node, the report is automatically cleared.</span></span>

#### <a name="the-node-agent-ntservice-is-down"></a><span data-ttu-id="ca09e-303">Il Node Agent NTService è inattivo</span><span class="sxs-lookup"><span data-stu-id="ca09e-303">The Node Agent NTService is down</span></span>

<span data-ttu-id="ca09e-304">Se il Node Agent NTService è inattivo in un nodo, viene generato un report sull'integrità dei livelli di avviso per il Node Agent Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-304">If the Node Agent NTService is down on a node, a warning-level health report is generated against the Node Agent Service.</span></span>

#### <a name="the-repair-manager-service-is-not-enabled"></a><span data-ttu-id="ca09e-305">Il servizio di gestione della riparazione non è abilitato</span><span class="sxs-lookup"><span data-stu-id="ca09e-305">The repair manager service is not enabled</span></span>

<span data-ttu-id="ca09e-306">Se il servizio di gestione della riparazione non viene individuato nel cluster, viene generato un report sull'integrità dei livelli di avviso per il Coordinator Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-306">If the repair manager service is not found on the cluster, a warning-level health report is generated for the Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ca09e-307">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ca09e-307">Frequently asked questions</span></span>

<span data-ttu-id="ca09e-308">D:</span><span class="sxs-lookup"><span data-stu-id="ca09e-308">Q.</span></span> <span data-ttu-id="ca09e-309">**Perché il cluster è in uno stato di errore quando Patch Orchestration App è in esecuzione?**</span><span class="sxs-lookup"><span data-stu-id="ca09e-309">**Why do I see my cluster in an error state when the patch orchestration app is running?**</span></span>

<span data-ttu-id="ca09e-310">R.</span><span class="sxs-lookup"><span data-stu-id="ca09e-310">A.</span></span> <span data-ttu-id="ca09e-311">Durante il processo di installazione, Patch Orchestration App disabilita o riavvia i nodi, il che può comportare temporaneamente la violazione dell'integrità del cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-311">During the installation process, the patch orchestration app disables or restarts nodes, which can temporarily result in the health of the cluster going down.</span></span>

<span data-ttu-id="ca09e-312">A seconda dei criteri impostati per l'applicazione, durante un'operazione di applicazione di patch è possibile che diventi non disponibile un singolo nodo *oppure* un intero dominio di aggiornamento simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-312">Based on the policy for the application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="ca09e-313">Al termine dell'installazione di Windows Update, i nodi vengono abilitati di nuovo dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="ca09e-313">By the end of the Windows Update installation, the nodes are reenabled post restart.</span></span>

<span data-ttu-id="ca09e-314">Nell'esempio seguente, il cluster è passato temporaneamente a uno stato di errore perché i due nodi sono stati resi inattivi e il criterio MaxPercentageUnhealthNodes è stato violato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-314">In the following example, the cluster went to an error state temporarily because two nodes were down and the MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="ca09e-315">L'errore è temporaneo fino a quando l'operazione di aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="ca09e-315">The error is temporary until the patching operation is ongoing.</span></span>

![Immagine del cluster non integro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="ca09e-317">Se il problema persiste, fare riferimento alla sezione relativa alla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ca09e-317">If the issue persists, refer to the Troubleshooting section.</span></span>

<span data-ttu-id="ca09e-318">D:</span><span class="sxs-lookup"><span data-stu-id="ca09e-318">Q.</span></span> <span data-ttu-id="ca09e-319">**Patch Orchestration App è in stato di avviso**</span><span class="sxs-lookup"><span data-stu-id="ca09e-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="ca09e-320">R.</span><span class="sxs-lookup"><span data-stu-id="ca09e-320">A.</span></span> <span data-ttu-id="ca09e-321">Verificare se la causa principale è un report sull'integrità inviato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-321">Check to see if a health report posted against the application is the root cause.</span></span> <span data-ttu-id="ca09e-322">L'avviso in genere contiene i dettagli del problema.</span><span class="sxs-lookup"><span data-stu-id="ca09e-322">Usually, the warning contains details of the problem.</span></span> <span data-ttu-id="ca09e-323">Se il problema è temporaneo, è previsto il ripristino automatico dell'applicazione da questo stato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-323">If the issue is transient, the application is expected to auto-recover from this state.</span></span>

<span data-ttu-id="ca09e-324">D:</span><span class="sxs-lookup"><span data-stu-id="ca09e-324">Q.</span></span> <span data-ttu-id="ca09e-325">**Che cosa è possibile fare se il cluster non è integro ed è necessario eseguire un aggiornamento del sistema operativo?**</span><span class="sxs-lookup"><span data-stu-id="ca09e-325">**What can I do if my cluster is unhealthy and I need to do an urgent operating system update?**</span></span>

<span data-ttu-id="ca09e-326">R.</span><span class="sxs-lookup"><span data-stu-id="ca09e-326">A.</span></span> <span data-ttu-id="ca09e-327">Patch Orchestration App non installa gli aggiornamenti mentre il cluster non è in uno stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="ca09e-327">The patch orchestration app does not install updates while the cluster is unhealthy.</span></span> <span data-ttu-id="ca09e-328">Provare a portare il cluster in uno stato di integrità per sbloccare il flusso di lavoro di Patch Orchestration App.</span><span class="sxs-lookup"><span data-stu-id="ca09e-328">Try to bring your cluster to a healthy state to unblock the patch orchestration app workflow.</span></span>

<span data-ttu-id="ca09e-329">D:</span><span class="sxs-lookup"><span data-stu-id="ca09e-329">Q.</span></span> <span data-ttu-id="ca09e-330">**Perché l'applicazione di patch nei cluster richiede molto tempo?**</span><span class="sxs-lookup"><span data-stu-id="ca09e-330">**Why does patching across clusters take so long to run?**</span></span>

<span data-ttu-id="ca09e-331">R.</span><span class="sxs-lookup"><span data-stu-id="ca09e-331">A.</span></span> <span data-ttu-id="ca09e-332">Il tempo impiegato da Patch Orchestration App dipende principalmente dai seguenti fattori:</span><span class="sxs-lookup"><span data-stu-id="ca09e-332">The time needed by the patch orchestration app is mostly dependent on the following factors:</span></span>

- <span data-ttu-id="ca09e-333">I criteri del Coordinator Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-333">The policy of the Coordinator Service.</span></span> 
  - <span data-ttu-id="ca09e-334">I criteri predefiniti, `NodeWise`, comportano l'applicazione di patch solo un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="ca09e-334">The default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="ca09e-335">In particolare nel caso di cluster più grandi, è consigliabile usare i criteri `UpgradeDomainWise` per ottenere un'applicazione più rapida delle patch nei cluster.</span><span class="sxs-lookup"><span data-stu-id="ca09e-335">Especially in the case of bigger clusters, we recommend that you use the `UpgradeDomainWise` policy to achieve faster patching across clusters.</span></span>
- <span data-ttu-id="ca09e-336">Il numero di aggiornamenti disponibili per il download e l'installazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-336">The number of updates available for download and installation.</span></span> 
- <span data-ttu-id="ca09e-337">Il tempo medio necessario per scaricare e installare un aggiornamento, che non deve superare un paio d'ore.</span><span class="sxs-lookup"><span data-stu-id="ca09e-337">The average time needed to download and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="ca09e-338">Le prestazioni della VM e la larghezza di banda della rete.</span><span class="sxs-lookup"><span data-stu-id="ca09e-338">The performance of the VM and network bandwidth.</span></span>

<span data-ttu-id="ca09e-339">D:</span><span class="sxs-lookup"><span data-stu-id="ca09e-339">Q.</span></span> <span data-ttu-id="ca09e-340">**Qual è il motivo per cui vengono visualizzati alcuni aggiornamenti nei risultati di Windows Update ottenuti tramite l'API REST, ma non nella cronologia di Windows Update sul computer?**</span><span class="sxs-lookup"><span data-stu-id="ca09e-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under the Windows Update history on machine?**</span></span>

<span data-ttu-id="ca09e-341">R.</span><span class="sxs-lookup"><span data-stu-id="ca09e-341">A.</span></span> <span data-ttu-id="ca09e-342">Alcuni aggiornamenti del prodotto devono essere archiviati nella rispettiva cronologia patch/di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ca09e-342">Some product updates need to be checked in their respective update/patch history.</span></span> <span data-ttu-id="ca09e-343">Ad esempio: gli aggiornamenti di Windows Defender non vengono visualizzati nella cronologia di Windows Update in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ca09e-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="ca09e-344">Dichiarazioni di non responsabilità</span><span class="sxs-lookup"><span data-stu-id="ca09e-344">Disclaimers</span></span>

- <span data-ttu-id="ca09e-345">Patch Orchestration App accetta il contratto licenza di Windows Update per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-345">The patch orchestration app accepts the End-User License Agreement of Windows Update on behalf of the user.</span></span> <span data-ttu-id="ca09e-346">Facoltativamente, l'impostazione può essere disattivata nella configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-346">Optionally, the setting can be turned off in the configuration of the application.</span></span>

- <span data-ttu-id="ca09e-347">Patch Orchestration App raccoglie i dati di telemetria per tenere traccia dell'uso e delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ca09e-347">The patch orchestration app collects telemetry to track usage and performance.</span></span> <span data-ttu-id="ca09e-348">I dati di telemetria dell'applicazione seguono l'impostazione dei dati di telemetria del runtime di Service Fabric (attiva per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="ca09e-348">The application’s telemetry follows the setting of the Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ca09e-349">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ca09e-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-to-up-state"></a><span data-ttu-id="ca09e-350">Un nodo non torna allo stato attivo</span><span class="sxs-lookup"><span data-stu-id="ca09e-350">A node is not coming back to up state</span></span>

<span data-ttu-id="ca09e-351">**Il nodo potrebbe essere bloccato in uno stato di disattivazione perché**:</span><span class="sxs-lookup"><span data-stu-id="ca09e-351">**The node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="ca09e-352">Un controllo di sicurezza è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="ca09e-352">A safety check is pending.</span></span> <span data-ttu-id="ca09e-353">Per risolvere questo problema, assicurarsi che siano disponibili sufficienti nodi in uno stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="ca09e-353">To remedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="ca09e-354">**Il nodo potrebbe essere bloccato in uno stato di disattivazione perché**:</span><span class="sxs-lookup"><span data-stu-id="ca09e-354">**The node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="ca09e-355">Il nodo è stato disabilitato manualmente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-355">The node was disabled manually.</span></span>
- <span data-ttu-id="ca09e-356">Il nodo è stato disabilitato a causa di un processo dell'infrastruttura di Azure in corso.</span><span class="sxs-lookup"><span data-stu-id="ca09e-356">The node was disabled due to an ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="ca09e-357">Il nodo è stato disabilitato temporaneamente da Patch Orchestration App per applicare le patch al nodo.</span><span class="sxs-lookup"><span data-stu-id="ca09e-357">The node was disabled temporarily by the patch orchestration app to patch the node.</span></span>

<span data-ttu-id="ca09e-358">**Il nodo potrebbe essere bloccato in uno stato inattivo perché**:</span><span class="sxs-lookup"><span data-stu-id="ca09e-358">**The node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="ca09e-359">Il nodo è stato impostato su uno stato inattivo manualmente.</span><span class="sxs-lookup"><span data-stu-id="ca09e-359">The node was put in a down state manually.</span></span>
- <span data-ttu-id="ca09e-360">Il nodo è in fase di riavvio (che è possibile che venga avviato da Patch Orchestration App).</span><span class="sxs-lookup"><span data-stu-id="ca09e-360">The node is undergoing a restart (which might be triggered by the patch orchestration app).</span></span>
- <span data-ttu-id="ca09e-361">Il nodo è inattivo a causa di problemi relativi a una rete o macchina o macchina virtuale difettosa.</span><span class="sxs-lookup"><span data-stu-id="ca09e-361">The node is down due to a faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="ca09e-362">Gli aggiornamenti sono stati ignorati in alcuni nodi</span><span class="sxs-lookup"><span data-stu-id="ca09e-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="ca09e-363">Patch Orchestration App tenta di installare un aggiornamento di Windows in base ai criteri di ripianificazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-363">The patch orchestration app tries to install a Windows update according to the rescheduling policy.</span></span> <span data-ttu-id="ca09e-364">Il servizio tenta di recuperare il nodo e di ignorare l'aggiornamento in base ai criteri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca09e-364">The service tries to recover the node and skip the update according to the application policy.</span></span>

<span data-ttu-id="ca09e-365">In questo caso, viene generato un report sull'integrità dei livelli di avviso per Node Agent Service.</span><span class="sxs-lookup"><span data-stu-id="ca09e-365">In such a case, a warning-level health report is generated against the Node Agent Service.</span></span> <span data-ttu-id="ca09e-366">Il risultato di Windows Update contiene anche la possibile causa dell'errore.</span><span class="sxs-lookup"><span data-stu-id="ca09e-366">The result for Windows Update also contains the possible reason for the failure.</span></span>

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a><span data-ttu-id="ca09e-367">L'integrità del cluster passa nello stato di errore durante l'installazione dell'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="ca09e-367">The health of the cluster goes to error while the update installs</span></span>

<span data-ttu-id="ca09e-368">Un aggiornamento difettoso di Windows può compromettere l'integrità di un'applicazione o di un cluster in un nodo particolare o in un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ca09e-368">A faulty Windows update can bring down the health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="ca09e-369">Patch Orchestration App interrompe qualsiasi successiva operazione di aggiornamento di Windows fino a quando il cluster è di nuovo integro.</span><span class="sxs-lookup"><span data-stu-id="ca09e-369">The patch orchestration app discontinues any subsequent Windows Update operation until the cluster is healthy again.</span></span>

<span data-ttu-id="ca09e-370">Un amministratore deve intervenire e stabilire perché l'applicazione o il cluster è diventato non integro a causa di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="ca09e-370">An administrator must intervene and determine why the application or cluster became unhealthy due to Windows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="ca09e-371">Note sulla versione:</span><span class="sxs-lookup"><span data-stu-id="ca09e-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="ca09e-372">Versione 1.1.0</span><span class="sxs-lookup"><span data-stu-id="ca09e-372">Version 1.1.0</span></span>
- <span data-ttu-id="ca09e-373">Versione pubblica</span><span class="sxs-lookup"><span data-stu-id="ca09e-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="ca09e-374">Versione 1.1.1</span><span class="sxs-lookup"><span data-stu-id="ca09e-374">Version 1.1.1</span></span>
- <span data-ttu-id="ca09e-375">Correzione di un bug in SetupEntryPoint di NodeAgentService che ha impedito l'installazione di NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="ca09e-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="ca09e-376">Versione 1.2.0 (versione più recente)</span><span class="sxs-lookup"><span data-stu-id="ca09e-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="ca09e-377">Correzioni di bug nel flusso di lavoro di riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="ca09e-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="ca09e-378">Correzione di bug nella creazione di attività RM a causa delle quali il controllo dell'integrità durante la preparazione delle attività di ripristino non ha avuto luogo come previsto.</span><span class="sxs-lookup"><span data-stu-id="ca09e-378">Bug fix in creation of RM tasks due to which health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="ca09e-379">Modificata la modalità di avvio per il servizio di windows POANodeSvc da automatico ad automatico ritardato.</span><span class="sxs-lookup"><span data-stu-id="ca09e-379">Changed the startup mode for windows service POANodeSvc from auto to delayed-auto.</span></span>
