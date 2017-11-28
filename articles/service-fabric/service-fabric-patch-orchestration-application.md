---
title: applicazione di Service Fabric patch orchestrazione aaaAzure | Documenti Microsoft
description: Applicazione tooautomate operativo l'applicazione di sistema in un cluster di Service Fabric patch.
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
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a><span data-ttu-id="a5eda-103">Sistema operativo di Windows hello del cluster di Service Fabric patch</span><span class="sxs-lookup"><span data-stu-id="a5eda-103">Patch hello Windows operating system in your Service Fabric cluster</span></span>

<span data-ttu-id="a5eda-104">un'applicazione Hello patch orchestrazione è un'applicazione Azure Service Fabric che consente di automatizzare l'applicazione di patch in un cluster di Service Fabric in Azure senza tempi di inattività del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-104">hello patch orchestration application is an Azure Service Fabric application that automates operating system patching on a Service Fabric cluster on Azure without downtime.</span></span>

<span data-ttu-id="a5eda-105">app di Hello patch orchestrazione fornisce seguente hello:</span><span class="sxs-lookup"><span data-stu-id="a5eda-105">hello patch orchestration app provides hello following:</span></span>

- <span data-ttu-id="a5eda-106">**Installazione automatica dell'aggiornamento del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="a5eda-106">**Automatic operating system update installation**.</span></span> <span data-ttu-id="a5eda-107">Gli aggiornamenti del sistema operativo vengono scaricati e installati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a5eda-107">Operating system updates are automatically downloaded and installed.</span></span> <span data-ttu-id="a5eda-108">I nodi del cluster vengono riavviati in base alle esigenze senza tempi di inattività del cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-108">Cluster nodes are rebooted as needed without cluster downtime.</span></span>

- <span data-ttu-id="a5eda-109">**Integrazione dell'integrità e l'applicazione di patch compatibile con il cluster**.</span><span class="sxs-lookup"><span data-stu-id="a5eda-109">**Cluster-aware patching and health integration**.</span></span> <span data-ttu-id="a5eda-110">Durante l'applicazione degli aggiornamenti, hello patch orchestrazione app esegue il monitoraggio di integrità hello hello dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-110">While applying updates, hello patch orchestration app monitors hello health of hello cluster nodes.</span></span> <span data-ttu-id="a5eda-111">I nodi del cluster sono aggiornati un nodo alla volta o un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="a5eda-111">Cluster nodes are upgraded one node at a time or one upgrade domain at a time.</span></span> <span data-ttu-id="a5eda-112">Se integrità hello del cluster di hello smette di funzionare a causa di processo di gestione delle patch toohello, l'applicazione di patch è arrestato tooprevent aggravare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-112">If hello health of hello cluster goes down due toohello patching process, patching is stopped tooprevent aggravating hello problem.</span></span>

## <a name="internal-details-of-hello-app"></a><span data-ttu-id="a5eda-113">Dettagli interni dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-113">Internal details of hello app</span></span>

<span data-ttu-id="a5eda-114">app di orchestrazione patch Hello è costituito da hello sottocomponenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5eda-114">hello patch orchestration app is composed of hello following subcomponents:</span></span>

- <span data-ttu-id="a5eda-115">**Coordinator Service**: il servizio con stato è responsabile per:</span><span class="sxs-lookup"><span data-stu-id="a5eda-115">**Coordinator Service**: This stateful service is responsible for:</span></span>
    - <span data-ttu-id="a5eda-116">Coordinare il processo di aggiornamento di Windows hello su intero cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-116">Coordinating hello Windows Update job on hello entire cluster.</span></span>
    - <span data-ttu-id="a5eda-117">Archiviazione del risultato hello delle operazioni completate di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-117">Storing hello result of completed Windows Update operations.</span></span>
- <span data-ttu-id="a5eda-118">**Node Agent Service**: è un servizio senza stato che viene eseguito in tutti i nodi di cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a5eda-118">**Node Agent Service**: This stateless service runs on all Service Fabric cluster nodes.</span></span> <span data-ttu-id="a5eda-119">servizio Hello è responsabile per:</span><span class="sxs-lookup"><span data-stu-id="a5eda-119">hello service is responsible for:</span></span>
    - <span data-ttu-id="a5eda-120">Avvio automatico hello NTService agente nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-120">Bootstrapping hello Node Agent NTService.</span></span>
    - <span data-ttu-id="a5eda-121">Monitoraggio hello NTService agente nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-121">Monitoring hello Node Agent NTService.</span></span>
- <span data-ttu-id="a5eda-122">**Node agent NTService**: questo servizio di Windows NT viene eseguito con un privilegio di livello superiore (SYSTEM).</span><span class="sxs-lookup"><span data-stu-id="a5eda-122">**Node Agent NTService**: This Windows NT service runs at a higher-level privilege (SYSTEM).</span></span> <span data-ttu-id="a5eda-123">Al contrario, hello servizio agente del nodo e il servizio coordinatore hello eseguire in un privilegio di livello inferiore (servizio di rete).</span><span class="sxs-lookup"><span data-stu-id="a5eda-123">In contrast, hello Node Agent Service and hello Coordinator Service run at a lower-level privilege (NETWORK SERVICE).</span></span> <span data-ttu-id="a5eda-124">servizio di Hello è responsabile dell'esecuzione hello seguendo i processi di Windows Update in tutti i nodi del cluster di hello:</span><span class="sxs-lookup"><span data-stu-id="a5eda-124">hello service is responsible for performing hello following Windows Update jobs on all hello cluster nodes:</span></span>
    - <span data-ttu-id="a5eda-125">La disabilitazione di aggiornamento automatico di Windows nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-125">Disabling automatic Windows Update on hello node.</span></span>
    - <span data-ttu-id="a5eda-126">Download e installazione di Windows Update in base a utente hello di criteri toohello ha fornito.</span><span class="sxs-lookup"><span data-stu-id="a5eda-126">Downloading and installing Windows Update according toohello policy hello user has provided.</span></span>
    - <span data-ttu-id="a5eda-127">Il riavvio post macchina hello installazione Windows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-127">Restarting hello machine post Windows Update installation.</span></span>
    - <span data-ttu-id="a5eda-128">Il caricamento dei risultati di hello di toohello gli aggiornamenti di Windows il servizio coordinatore.</span><span class="sxs-lookup"><span data-stu-id="a5eda-128">Uploading hello results of Windows updates toohello Coordinator Service.</span></span>
    - <span data-ttu-id="a5eda-129">Generazione di report sull'integrità in caso di un'operazione non riuscita dopo l'esaurimento di tutti i tentativi.</span><span class="sxs-lookup"><span data-stu-id="a5eda-129">Reporting health reports in case an operation has failed after exhausting all retries.</span></span>

> [!NOTE]
> <span data-ttu-id="a5eda-130">Hello patch orchestrazione app utilizza hello Service Fabric ripristinare toodisable servizio di gestione del sistema o abilitare nodo hello ed eseguire controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="a5eda-130">hello patch orchestration app uses hello Service Fabric repair manager system service toodisable or enable hello node and perform health checks.</span></span> <span data-ttu-id="a5eda-131">attività di correzione Hello creata da hello patch orchestrazione app tracce hello lo stato di avanzamento di Windows Update per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-131">hello repair task created by hello patch orchestration app tracks hello Windows Update progress for each node.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5eda-132">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5eda-132">Prerequisites</span></span>

### <a name="minimum-supported-service-fabric-runtime-version"></a><span data-ttu-id="a5eda-133">Versione minima di runtime di Service Fabric supportata</span><span class="sxs-lookup"><span data-stu-id="a5eda-133">Minimum supported Service Fabric runtime version</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="a5eda-134">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="a5eda-134">Azure clusters</span></span>
<span data-ttu-id="a5eda-135">Hello patch orchestrazione app deve essere eseguito nel cluster di Azure con versione 5.5 versione runtime di Service Fabric o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a5eda-135">hello patch orchestration app must be run on Azure clusters that have Service Fabric runtime version v5.5 or later.</span></span>

#### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="a5eda-136">Cluster locali autonomi</span><span class="sxs-lookup"><span data-stu-id="a5eda-136">Standalone on-premises Clusters</span></span>
<span data-ttu-id="a5eda-137">Hello patch orchestrazione app deve essere eseguito nel cluster autonomo con versione 5.6 versione runtime di Service Fabric o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="a5eda-137">hello patch orchestration app must be run on Standalone clusters that have Service Fabric runtime version v5.6 or later.</span></span>

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a><span data-ttu-id="a5eda-138">Abilitare il servizio di gestione ripristino hello (se non è in esecuzione già)</span><span class="sxs-lookup"><span data-stu-id="a5eda-138">Enable hello repair manager service (if it's not running already)</span></span>

<span data-ttu-id="a5eda-139">app di orchestrazione patch Hello richiede hello repair manager system service toobe abilitata sul cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-139">hello patch orchestration app requires hello repair manager system service toobe enabled on hello cluster.</span></span>

#### <a name="azure-clusters"></a><span data-ttu-id="a5eda-140">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="a5eda-140">Azure clusters</span></span>

<span data-ttu-id="a5eda-141">I cluster di Azure nel livello di durabilità argento hello dispongono hello di ripristinare il servizio di gestione abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a5eda-141">Azure clusters in hello silver durability tier have hello repair manager service enabled by default.</span></span> <span data-ttu-id="a5eda-142">Cluster di Azure nel livello di durabilità gold hello potrebbe oppure potrebbe non disporre di servizio di gestione ripristino hello abilitato, a seconda della creazione di tali cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-142">Azure clusters in hello gold durability tier might or might not have hello repair manager service enabled, depending on when those clusters were created.</span></span> <span data-ttu-id="a5eda-143">Cluster di Azure nel livello di durabilità "Bronze" hello, per impostazione predefinita, non è necessario hello ripristinare il servizio di gestione abilitato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-143">Azure clusters in hello bronze durability tier, by default, do not have hello repair manager service enabled.</span></span> <span data-ttu-id="a5eda-144">Se il servizio di hello è già abilitato, è possibile visualizzarlo in esecuzione nella sezione Servizi di sistema hello in hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a5eda-144">If hello service is already enabled, you can see it running in hello system services section in hello Service Fabric Explorer.</span></span>

##### <a name="azure-portal"></a><span data-ttu-id="a5eda-145">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a5eda-145">Azure portal</span></span>
<span data-ttu-id="a5eda-146">È possibile abilitare Gestione ripristino dal portale di Azure in fase di hello di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-146">You can enable repair manager from Azure portal at hello time of setting up of cluster.</span></span> <span data-ttu-id="a5eda-147">Selezionare `Include Repair Manager` opzione `Add on features` in fase di hello della configurazione del Cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-147">Select `Include Repair Manager` option under `Add on features` at hello time of Cluster configuration.</span></span>
<span data-ttu-id="a5eda-148">![Immagine dell'attivazione del servizio di gestione della riparazione dal portale di Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span><span class="sxs-lookup"><span data-stu-id="a5eda-148">![Image of Enabling Repair Manager from Azure portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)</span></span>

##### <a name="azure-resource-manager-template"></a><span data-ttu-id="a5eda-149">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a5eda-149">Azure Resource Manager template</span></span>
<span data-ttu-id="a5eda-150">In alternativa è possibile utilizzare hello [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello manager di riparazione sui cluster di Service Fabric nuove ed esistenti.</span><span class="sxs-lookup"><span data-stu-id="a5eda-150">Alternatively you can use hello [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello repair manager service on new and existing Service Fabric clusters.</span></span> <span data-ttu-id="a5eda-151">Ottiene il modello di hello per cluster hello che si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a5eda-151">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="a5eda-152">È possibile utilizzare i modelli di esempio hello o creare un modello di gestione risorse personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-152">You can either use hello sample templates or create a custom Resource Manager template.</span></span> 

<span data-ttu-id="a5eda-153">tooenable hello riparazione gestore servizio tramite [modello di Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span><span class="sxs-lookup"><span data-stu-id="a5eda-153">tooenable hello repair manager service using [Azure Resource Manager template](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):</span></span>

1. <span data-ttu-id="a5eda-154">Verificare innanzitutto che hello `apiversion` è troppo`2017-07-01-preview` per hello `Microsoft.ServiceFabric/clusters` risorsa, come illustrato nel seguente frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-154">First check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, as shown in hello following snippet.</span></span> <span data-ttu-id="a5eda-155">Se è diverso, quindi è necessario hello tooupdate `apiVersion` toohello valore `2017-07-01-preview`:</span><span class="sxs-lookup"><span data-stu-id="a5eda-155">If it is different, then you need tooupdate hello `apiVersion` toohello value `2017-07-01-preview`:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="a5eda-156">Ora abilitare il servizio di gestione ripristino hello aggiungendo segue hello `addonFeatures` sezione dopo hello `fabricSettings` sezione:</span><span class="sxs-lookup"><span data-stu-id="a5eda-156">Now enable hello repair manager service by adding hello following `addonFeatures` section after hello `fabricSettings` section:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="a5eda-157">Dopo aver aggiornato il modello di cluster con queste modifiche, applicarli e consentire l'aggiornamento di hello di fine.</span><span class="sxs-lookup"><span data-stu-id="a5eda-157">After you have updated your cluster template with these changes, apply them and let hello upgrade finish.</span></span> <span data-ttu-id="a5eda-158">È ora possibile visualizzare hello manager sistema riparazione in esecuzione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-158">You can now see hello repair manager system service running in your cluster.</span></span> <span data-ttu-id="a5eda-159">Viene chiamato `fabric:/System/RepairManagerService` nella sezione Servizi di sistema hello in hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a5eda-159">It is called `fabric:/System/RepairManagerService` in hello system services section in hello Service Fabric Explorer.</span></span> 

### <a name="standalone-on-premises-clusters"></a><span data-ttu-id="a5eda-160">Cluster locali autonomi</span><span class="sxs-lookup"><span data-stu-id="a5eda-160">Standalone on-premises clusters</span></span>

<span data-ttu-id="a5eda-161">È possibile utilizzare hello [le impostazioni di configurazione per il cluster di Windows autonoma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello manager di riparazione nel cluster di Service Fabric nuove ed esistenti.</span><span class="sxs-lookup"><span data-stu-id="a5eda-161">You can use hello [Configuration settings for standalone Windows cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello repair manager service on new and existing Service Fabric cluster.</span></span>

<span data-ttu-id="a5eda-162">servizio di gestione ripristino hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="a5eda-162">tooenable hello repair manager service:</span></span>

1. <span data-ttu-id="a5eda-163">Verificare innanzitutto che hello `apiversion` in [configurazioni cluster generale](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) è troppo`04-2017` o versione successiva:</span><span class="sxs-lookup"><span data-stu-id="a5eda-163">First check that hello `apiversion` in [General cluster configurations](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) is set too`04-2017` or higher:</span></span>

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. <span data-ttu-id="a5eda-164">Ora abilitare il servizio di gestione ripristino aggiungendo segue hello `addonFeaturres` sezione dopo hello `fabricSettings` sezione come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a5eda-164">Now enable repair manager service by adding hello following `addonFeaturres` section after hello `fabricSettings` section as shown below:</span></span>

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. <span data-ttu-id="a5eda-165">Aggiornare il manifesto del cluster con le modifiche, utilizzando manifesto del cluster aggiornato hello [creare un nuovo cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) o [configurazione del cluster aggiornamento hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span><span class="sxs-lookup"><span data-stu-id="a5eda-165">Update your cluster manifest with these changes, using hello updated cluster manifest [create a new cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) or [upgrade hello cluster configuration](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration).</span></span> <span data-ttu-id="a5eda-166">Una volta cluster hello è in esecuzione con manifesto del cluster aggiornato, è ora possibile visualizzare hello manager sistema riparazione in esecuzione nel cluster, che viene chiamato `fabric:/System/RepairManagerService`, in Esplora Service Fabric hello sezione servizi del sistema.</span><span class="sxs-lookup"><span data-stu-id="a5eda-166">Once hello cluster is running with updated cluster manifest, you can now see hello repair manager system service running in your cluster, which is called `fabric:/System/RepairManagerService`, under system services section in hello Service Fabric explorer.</span></span>

### <a name="disable-automatic-windows-update-on-all-nodes"></a><span data-ttu-id="a5eda-167">Disabilitare la connessione automatica a Windows Update su tutti i nodi</span><span class="sxs-lookup"><span data-stu-id="a5eda-167">Disable automatic Windows Update on all nodes</span></span>

<span data-ttu-id="a5eda-168">Aggiornamenti automatici di Windows potrebbero causare perdita tooavailability perché è possono riavviare più nodi del cluster in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-168">Automatic Windows updates might lead tooavailability loss because multiple cluster nodes can restart at hello same time.</span></span> <span data-ttu-id="a5eda-169">app di orchestrazione patch Hello, per impostazione predefinita, i tentativi toodisable hello automatica di Windows Update in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-169">hello patch orchestration app, by default, tries toodisable hello automatic Windows Update on each cluster node.</span></span> <span data-ttu-id="a5eda-170">Tuttavia, se le impostazioni di hello sono gestite da un amministratore o criteri di gruppo, è consigliabile hello impostazione criteri troppo "notifica prima del Download" in modo esplicito di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-170">However, if hello settings are managed by an administrator or group policy, we recommend setting hello Windows Update policy too“Notify before Download” explicitly.</span></span>

### <a name="optional-enable-azure-diagnostics"></a><span data-ttu-id="a5eda-171">Facoltativo: abilitare Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="a5eda-171">Optional: Enable Azure Diagnostics</span></span>

<span data-ttu-id="a5eda-172">Per i cluster che eseguono la versione di runtime di Service Fabric `5.6.220.9494` e livelli successivi, verranno raccolti i log dell'app di orchestrazione come parte dei log di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a5eda-172">Clusters running Service Fabric runtime version `5.6.220.9494` and above collect patch orchestration app logs as part of Service Fabric logs.</span></span>
<span data-ttu-id="a5eda-173">È possibile ignorare questo passaggio se il cluster è in esecuzione nella versione di runtime di Service Fabric `5.6.220.9494` e nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a5eda-173">You can skip this step if your cluster is running on Service Fabric runtime version `5.6.220.9494` and above.</span></span>

<span data-ttu-id="a5eda-174">Per i cluster che eseguono la versione di runtime Service Fabric minore `5.6.220.9494`, i registri per app di orchestrazione patch hello vengono raccolti in locale in ognuno dei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-174">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs for hello patch orchestration app are collected locally on each of hello cluster nodes.</span></span>
<span data-ttu-id="a5eda-175">È consigliabile configurare il log di diagnostica Azure tooupload da tutti i nodi tooa centrale.</span><span class="sxs-lookup"><span data-stu-id="a5eda-175">We recommend that you configure Azure Diagnostics tooupload logs from all nodes tooa central location.</span></span>

<span data-ttu-id="a5eda-176">Per altre informazioni su come abilitare Diagnostica di Azure, vedere [Raccogliere log con Diagnostica di Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span><span class="sxs-lookup"><span data-stu-id="a5eda-176">For information on enabling Azure Diagnostics, see [Collect logs by using Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).</span></span>

<span data-ttu-id="a5eda-177">Per app di orchestrazione patch hello di registri generati in hello seguente ID di provider predefinito:</span><span class="sxs-lookup"><span data-stu-id="a5eda-177">Logs for hello patch orchestration app are generated on hello following fixed provider IDs:</span></span>

- <span data-ttu-id="a5eda-178">e39b723c-590c-4090-abb0-11e3e6616346</span><span class="sxs-lookup"><span data-stu-id="a5eda-178">e39b723c-590c-4090-abb0-11e3e6616346</span></span>
- <span data-ttu-id="a5eda-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span><span class="sxs-lookup"><span data-stu-id="a5eda-179">fc0028ff-bfdc-499f-80dc-ed922c52c5e9</span></span>
- <span data-ttu-id="a5eda-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span><span class="sxs-lookup"><span data-stu-id="a5eda-180">24afa313-0d3b-4c7c-b485-1047fd964b60</span></span>
- <span data-ttu-id="a5eda-181">05dc046c-60e9-4ef7-965e-91660adffa68</span><span class="sxs-lookup"><span data-stu-id="a5eda-181">05dc046c-60e9-4ef7-965e-91660adffa68</span></span>

<span data-ttu-id="a5eda-182">In Gestione risorse modello goto `EtwEventSourceProviderConfiguration` sezione nel `WadCfg` e aggiungere hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="a5eda-182">In Resource Manager template goto `EtwEventSourceProviderConfiguration` section under `WadCfg` and add hello following entries:</span></span>

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
> <span data-ttu-id="a5eda-183">Se il cluster di Service Fabric con più tipi di nodo, quindi è necessario aggiungere la sezione precedente di hello per hello tutti `WadCfg` sezioni.</span><span class="sxs-lookup"><span data-stu-id="a5eda-183">If your Service Fabric cluster has multiple node types, then hello previous section must be added for all hello `WadCfg` sections.</span></span>

## <a name="download-hello-app-package"></a><span data-ttu-id="a5eda-184">Scaricare il pacchetto di app hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-184">Download hello app package</span></span>

<span data-ttu-id="a5eda-185">Scaricare l'applicazione hello da hello [collegamento per il download](https://go.microsoft.com/fwlink/P/?linkid=849590).</span><span class="sxs-lookup"><span data-stu-id="a5eda-185">Download hello application from hello [download link](https://go.microsoft.com/fwlink/P/?linkid=849590).</span></span>

## <a name="configure-hello-app"></a><span data-ttu-id="a5eda-186">Configurare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-186">Configure hello app</span></span>

<span data-ttu-id="a5eda-187">comportamento dell'app di orchestrazione patch hello Hello può essere configurato toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="a5eda-187">hello behavior of hello patch orchestration app can be configured toomeet your needs.</span></span> <span data-ttu-id="a5eda-188">Eseguire l'override di valori predefiniti di hello passando il parametro applicazione hello durante la creazione dell'applicazione o l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a5eda-188">Override hello default values by passing in hello application parameter during application creation or update.</span></span> <span data-ttu-id="a5eda-189">È possibile specificare i parametri dell'applicazione specificando `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` o `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a5eda-189">Application parameters can be provided by specifying `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` or `New-ServiceFabricApplication` cmdlets.</span></span>

|<span data-ttu-id="a5eda-190">**Parametro**</span><span class="sxs-lookup"><span data-stu-id="a5eda-190">**Parameter**</span></span>        |<span data-ttu-id="a5eda-191">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="a5eda-191">**Type**</span></span>                          | <span data-ttu-id="a5eda-192">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="a5eda-192">**Details**</span></span>|
|:-|-|-|
|<span data-ttu-id="a5eda-193">MaxResultsToCache</span><span class="sxs-lookup"><span data-stu-id="a5eda-193">MaxResultsToCache</span></span>    |<span data-ttu-id="a5eda-194">long</span><span class="sxs-lookup"><span data-stu-id="a5eda-194">Long</span></span>                              | <span data-ttu-id="a5eda-195">Numero massimo di risultati di Windows Update memorizzabili nella cache.</span><span class="sxs-lookup"><span data-stu-id="a5eda-195">Maximum number of Windows Update results, which should be cached.</span></span> <br><span data-ttu-id="a5eda-196">Il valore predefinito è 3000 presumendo che il:</span><span class="sxs-lookup"><span data-stu-id="a5eda-196">Default value is 3000 assuming the:</span></span> <br> <span data-ttu-id="a5eda-197">- Numero di nodi sia 20.</span><span class="sxs-lookup"><span data-stu-id="a5eda-197">- Number of nodes is 20.</span></span> <br> <span data-ttu-id="a5eda-198">- Numero di aggiornamenti eseguiti su un nodo per ogni mese sia pari a cinque.</span><span class="sxs-lookup"><span data-stu-id="a5eda-198">- Number of updates happening on a node per month is five.</span></span> <br> <span data-ttu-id="a5eda-199">- Numero di risultati per ogni operazione sia pari a 10.</span><span class="sxs-lookup"><span data-stu-id="a5eda-199">- Number of results per operation can be 10.</span></span> <br> <span data-ttu-id="a5eda-200">-Risultati per tre mesi hello devono essere archiviati.</span><span class="sxs-lookup"><span data-stu-id="a5eda-200">- Results for hello past three months should be stored.</span></span> |
|<span data-ttu-id="a5eda-201">TaskApprovalPolicy</span><span class="sxs-lookup"><span data-stu-id="a5eda-201">TaskApprovalPolicy</span></span>   |<span data-ttu-id="a5eda-202">Enum</span><span class="sxs-lookup"><span data-stu-id="a5eda-202">Enum</span></span> <br> <span data-ttu-id="a5eda-203">{NodeWise, UpgradeDomainWise}</span><span class="sxs-lookup"><span data-stu-id="a5eda-203">{ NodeWise, UpgradeDomainWise }</span></span>                          |<span data-ttu-id="a5eda-204">TaskApprovalPolicy indica i criteri di hello toobe utilizzato per gli aggiornamenti di Windows hello servizio Coordinator tooinstall tra nodi del cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-204">TaskApprovalPolicy indicates hello policy that is toobe used by hello Coordinator Service tooinstall Windows updates across hello Service Fabric cluster nodes.</span></span><br>                         <span data-ttu-id="a5eda-205">I valori consentiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5eda-205">Allowed values are:</span></span> <br>                                                           <span data-ttu-id="a5eda-206"><b>NodeWise</b>.</span><span class="sxs-lookup"><span data-stu-id="a5eda-206"><b>NodeWise</b>.</span></span> <span data-ttu-id="a5eda-207">Windows Update viene installato un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="a5eda-207">Windows Update is installed one node at a time.</span></span> <br>                                                           <span data-ttu-id="a5eda-208"><b>UpgradeDomainWise</b>.</span><span class="sxs-lookup"><span data-stu-id="a5eda-208"><b>UpgradeDomainWise</b>.</span></span> <span data-ttu-id="a5eda-209">Windows Update viene installato un dominio di aggiornamento alla volta</span><span class="sxs-lookup"><span data-stu-id="a5eda-209">Windows Update is installed one upgrade domain at a time.</span></span> <span data-ttu-id="a5eda-210">(Al massimo hello, tutti i nodi di hello appartenenti tooan dominio di aggiornamento possono andare a Windows Update).</span><span class="sxs-lookup"><span data-stu-id="a5eda-210">(At hello maximum, all hello nodes belonging tooan upgrade domain can go for Windows Update.)</span></span>
|<span data-ttu-id="a5eda-211">LogsDiskQuotaInMB</span><span class="sxs-lookup"><span data-stu-id="a5eda-211">LogsDiskQuotaInMB</span></span>   |<span data-ttu-id="a5eda-212">long</span><span class="sxs-lookup"><span data-stu-id="a5eda-212">Long</span></span>  <br> <span data-ttu-id="a5eda-213">Predefinito: 1024</span><span class="sxs-lookup"><span data-stu-id="a5eda-213">(Default: 1024)</span></span>               |<span data-ttu-id="a5eda-214">Dimensione massima in MB dei log di Patch Orchestration App che è possibile salvare in modo permanente e locale sui nodi.</span><span class="sxs-lookup"><span data-stu-id="a5eda-214">Maximum size of patch orchestration app logs in MB, which can be persisted locally on nodes.</span></span>
| <span data-ttu-id="a5eda-215">WUQuery</span><span class="sxs-lookup"><span data-stu-id="a5eda-215">WUQuery</span></span>               | <span data-ttu-id="a5eda-216">string</span><span class="sxs-lookup"><span data-stu-id="a5eda-216">string</span></span><br><span data-ttu-id="a5eda-217">Impostazione predefinita: "IsInstalled = 0"</span><span class="sxs-lookup"><span data-stu-id="a5eda-217">(Default: "IsInstalled=0")</span></span>                | <span data-ttu-id="a5eda-218">Eseguire una query tooget gli aggiornamenti di Windows.</span><span class="sxs-lookup"><span data-stu-id="a5eda-218">Query tooget Windows updates.</span></span> <span data-ttu-id="a5eda-219">Per altre informazioni, vedere [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a5eda-219">For more information, see [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)</span></span>
| <span data-ttu-id="a5eda-220">InstallWindowsOSOnlyUpdates</span><span class="sxs-lookup"><span data-stu-id="a5eda-220">InstallWindowsOSOnlyUpdates</span></span> | <span data-ttu-id="a5eda-221">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5eda-221">Bool</span></span> <br> <span data-ttu-id="a5eda-222">Predefinito: True</span><span class="sxs-lookup"><span data-stu-id="a5eda-222">(default: True)</span></span>                 | <span data-ttu-id="a5eda-223">Questo flag consente operativo toobe gli aggiornamenti di sistema installato Windows.</span><span class="sxs-lookup"><span data-stu-id="a5eda-223">This flag allows Windows operating system updates toobe installed.</span></span>            |
| <span data-ttu-id="a5eda-224">WUOperationTimeOutInMinutes</span><span class="sxs-lookup"><span data-stu-id="a5eda-224">WUOperationTimeOutInMinutes</span></span> | <span data-ttu-id="a5eda-225">int</span><span class="sxs-lookup"><span data-stu-id="a5eda-225">Int</span></span> <br><span data-ttu-id="a5eda-226">Predefinito: 90</span><span class="sxs-lookup"><span data-stu-id="a5eda-226">(Default: 90)</span></span>                   | <span data-ttu-id="a5eda-227">Specifica il timeout di hello per le operazioni di aggiornamento di Windows (ricerca o scaricare o installare).</span><span class="sxs-lookup"><span data-stu-id="a5eda-227">Specifies hello timeout for any Windows Update operation (search or download or install).</span></span> <span data-ttu-id="a5eda-228">Se l'operazione di hello non viene completata entro hello timeout specificato, che sia interrotto.</span><span class="sxs-lookup"><span data-stu-id="a5eda-228">If hello operation is not completed within hello specified timeout, it is aborted.</span></span>       |
| <span data-ttu-id="a5eda-229">WURescheduleCount</span><span class="sxs-lookup"><span data-stu-id="a5eda-229">WURescheduleCount</span></span>     | <span data-ttu-id="a5eda-230">int</span><span class="sxs-lookup"><span data-stu-id="a5eda-230">Int</span></span> <br> <span data-ttu-id="a5eda-231">Predefinito: 5</span><span class="sxs-lookup"><span data-stu-id="a5eda-231">(Default: 5)</span></span>                  | <span data-ttu-id="a5eda-232">numero massimo di Hello di volte in cui il servizio hello Ripianifica hello Windows update in caso di un'operazione in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="a5eda-232">hello maximum number of times hello service reschedules hello Windows update in case an operation fails persistently.</span></span>          |
| <span data-ttu-id="a5eda-233">WURescheduleTimeInMinutes</span><span class="sxs-lookup"><span data-stu-id="a5eda-233">WURescheduleTimeInMinutes</span></span> | <span data-ttu-id="a5eda-234">int</span><span class="sxs-lookup"><span data-stu-id="a5eda-234">Int</span></span> <br><span data-ttu-id="a5eda-235">Predefinito: 30</span><span class="sxs-lookup"><span data-stu-id="a5eda-235">(Default: 30)</span></span> | <span data-ttu-id="a5eda-236">intervallo di Hello in cui hello servizio Ripianifica l'aggiornamento di Windows hello in caso di errore persiste.</span><span class="sxs-lookup"><span data-stu-id="a5eda-236">hello interval at which hello service reschedules hello Windows update in case failure persists.</span></span> |
| <span data-ttu-id="a5eda-237">WUFrequency</span><span class="sxs-lookup"><span data-stu-id="a5eda-237">WUFrequency</span></span>           | <span data-ttu-id="a5eda-238">Stringa separata da virgole Predefinito: "Weekly, Wednesday, 7:00:00"</span><span class="sxs-lookup"><span data-stu-id="a5eda-238">Comma-separated string (Default: "Weekly, Wednesday, 7:00:00")</span></span>     | <span data-ttu-id="a5eda-239">frequenza di Hello per l'installazione di Windows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-239">hello frequency for installing Windows Update.</span></span> <span data-ttu-id="a5eda-240">Hello formato e i possibili valori sono:</span><span class="sxs-lookup"><span data-stu-id="a5eda-240">hello format and possible values are:</span></span> <br><span data-ttu-id="a5eda-241">-   Monthly, DD,HH:MM:SS, ad esempio, Monthly, 5,12:22:32.</span><span class="sxs-lookup"><span data-stu-id="a5eda-241">-   Monthly, DD,HH:MM:SS, for example, Monthly, 5,12:22:32.</span></span> <br> <span data-ttu-id="a5eda-242">-   Weekly, DAY,HH:MM:SS, ad esempio, Weekly, Tuesday, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="a5eda-242">-   Weekly, DAY,HH:MM:SS, for example, Weekly, Tuesday, 12:22:32.</span></span>  <br> <span data-ttu-id="a5eda-243">-   Daily, HH:MM:SS, ad esempio, Daily, 12:22:32.</span><span class="sxs-lookup"><span data-stu-id="a5eda-243">-   Daily, HH:MM:SS, for example, Daily, 12:22:32.</span></span>  <br> <span data-ttu-id="a5eda-244">- None: indica che non deve essere eseguito Windows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-244">-  None indicates that Windows Update shouldn't be done.</span></span>  <br><br> <span data-ttu-id="a5eda-245">Si noti che tutti gli orari di hello in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="a5eda-245">Note that all hello times are in UTC.</span></span>|
| <span data-ttu-id="a5eda-246">AcceptWindowsUpdateEula</span><span class="sxs-lookup"><span data-stu-id="a5eda-246">AcceptWindowsUpdateEula</span></span> | <span data-ttu-id="a5eda-247">Booleano</span><span class="sxs-lookup"><span data-stu-id="a5eda-247">Bool</span></span> <br><span data-ttu-id="a5eda-248">Predefinito: True</span><span class="sxs-lookup"><span data-stu-id="a5eda-248">(Default: true)</span></span> | <span data-ttu-id="a5eda-249">Impostando questo flag, l'applicazione hello accetta hello contratto di licenza dell'utente finale per Windows Update per conto del proprietario di hello della macchina hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-249">By setting this flag, hello application accepts hello End-User License Agreement for Windows Update on behalf of hello owner of hello machine.</span></span>              |

> [!TIP]
> <span data-ttu-id="a5eda-250">Se si desidera immediatamente toohappen Windows Update, impostare `WUFrequency` toohello relativo tempo di distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a5eda-250">If you want Windows Update toohappen immediately, set `WUFrequency` relative toohello application deployment time.</span></span> <span data-ttu-id="a5eda-251">Ad esempio, si supponga che un'applicazione prova cinque nodi cluster e piano toodeploy hello a circa 17:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="a5eda-251">For example, suppose that you have a five-node test cluster and plan toodeploy hello app at around 5:00 PM UTC.</span></span> <span data-ttu-id="a5eda-252">Se si presuppone che l'aggiornamento dell'applicazione hello o distribuzione richiede 30 minuti hello hello massima, imposta WUFrequency "Giornalieri, 17:30:00."</span><span class="sxs-lookup"><span data-stu-id="a5eda-252">If you assume that hello application upgrade or deployment takes 30 minutes at hello maximum, set hello WUFrequency as "Daily, 17:30:00."</span></span>

## <a name="deploy-hello-app"></a><span data-ttu-id="a5eda-253">Distribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-253">Deploy hello app</span></span>

1. <span data-ttu-id="a5eda-254">Completare tutti i cluster del hello tooprepare hello passaggi preliminari.</span><span class="sxs-lookup"><span data-stu-id="a5eda-254">Finish all hello prerequisite steps tooprepare hello cluster.</span></span>
2. <span data-ttu-id="a5eda-255">Distribuire app di orchestrazione patch hello come qualsiasi altra app Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a5eda-255">Deploy hello patch orchestration app like any other Service Fabric app.</span></span> <span data-ttu-id="a5eda-256">È possibile distribuire l'applicazione hello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5eda-256">You can deploy hello app by using PowerShell.</span></span> <span data-ttu-id="a5eda-257">Seguire i passaggi di hello in [distribuire e rimuovere le applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="a5eda-257">Follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>
3. <span data-ttu-id="a5eda-258">un'applicazione hello tooconfigure in fase di distribuzione, passare hello di hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a5eda-258">tooconfigure hello application at hello time of deployment, pass hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet.</span></span> <span data-ttu-id="a5eda-259">Per praticità, è stato fornito uno script hello Deploy.ps1 insieme a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-259">For your convenience, we’ve provided hello script Deploy.ps1 along with hello application.</span></span> <span data-ttu-id="a5eda-260">script di hello toouse:</span><span class="sxs-lookup"><span data-stu-id="a5eda-260">toouse hello script:</span></span>

    - <span data-ttu-id="a5eda-261">Connettere il cluster di Service Fabric tooa utilizzando `Connect-ServiceFabricCluster`.</span><span class="sxs-lookup"><span data-stu-id="a5eda-261">Connect tooa Service Fabric cluster by using `Connect-ServiceFabricCluster`.</span></span>
    - <span data-ttu-id="a5eda-262">Eseguire lo script di PowerShell di hello Deploy.ps1 con hello appropriato `ApplicationParameter` valore.</span><span class="sxs-lookup"><span data-stu-id="a5eda-262">Execute hello PowerShell script Deploy.ps1 with hello appropriate `ApplicationParameter` value.</span></span>

> [!NOTE]
> <span data-ttu-id="a5eda-263">Consente di mantenere script hello e cartella dell'applicazione hello PatchOrchestrationApplication hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="a5eda-263">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="upgrade-hello-app"></a><span data-ttu-id="a5eda-264">Aggiornare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-264">Upgrade hello app</span></span>

<span data-ttu-id="a5eda-265">tooupgrade un'app di orchestrazione patch esistente tramite PowerShell, seguire i passaggi hello [aggiornamento dell'applicazione di Service Fabric con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span><span class="sxs-lookup"><span data-stu-id="a5eda-265">tooupgrade an existing patch orchestration app by using PowerShell, follow hello steps in [Service Fabric application upgrade using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).</span></span>

## <a name="remove-hello-app"></a><span data-ttu-id="a5eda-266">Rimuovere l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-266">Remove hello app</span></span>

<span data-ttu-id="a5eda-267">un'applicazione hello tooremove, seguire la procedura seguente hello in [distribuire e rimuovere le applicazioni con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span><span class="sxs-lookup"><span data-stu-id="a5eda-267">tooremove hello application, follow hello steps in [Deploy and remove applications using PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).</span></span>

<span data-ttu-id="a5eda-268">Per praticità, è stato fornito uno script hello Undeploy.ps1 insieme a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-268">For your convenience, we've provided hello script Undeploy.ps1 along with hello application.</span></span> <span data-ttu-id="a5eda-269">script di hello toouse:</span><span class="sxs-lookup"><span data-stu-id="a5eda-269">toouse hello script:</span></span>

  - <span data-ttu-id="a5eda-270">Connettere il cluster di Service Fabric tooa utilizzando ```Connect-ServiceFabricCluster```.</span><span class="sxs-lookup"><span data-stu-id="a5eda-270">Connect tooa Service Fabric cluster by using ```Connect-ServiceFabricCluster```.</span></span>

  - <span data-ttu-id="a5eda-271">Esecuzione di script di PowerShell hello Undeploy.ps1.</span><span class="sxs-lookup"><span data-stu-id="a5eda-271">Execute hello PowerShell script Undeploy.ps1.</span></span>

> [!NOTE]
> <span data-ttu-id="a5eda-272">Consente di mantenere script hello e cartella dell'applicazione hello PatchOrchestrationApplication hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="a5eda-272">Keep hello script and hello application folder PatchOrchestrationApplication in hello same directory.</span></span>

## <a name="view-hello-windows-update-results"></a><span data-ttu-id="a5eda-273">Visualizzare i risultati di aggiornamento di Windows hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-273">View hello Windows Update results</span></span>

<span data-ttu-id="a5eda-274">app di orchestrazione patch Hello espone utente toohello di API REST toodisplay hello risultati cronologici.</span><span class="sxs-lookup"><span data-stu-id="a5eda-274">hello patch orchestration app exposes REST APIs toodisplay hello historical results toohello user.</span></span> <span data-ttu-id="a5eda-275">Un esempio di risultato hello JSON:</span><span class="sxs-lookup"><span data-stu-id="a5eda-275">An example of hello result JSON:</span></span>
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
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
<span data-ttu-id="a5eda-276">Se l'aggiornamento non è stato ancora pianificato, il risultato di hello JSON è vuoto.</span><span class="sxs-lookup"><span data-stu-id="a5eda-276">If no update is scheduled yet, hello result JSON is empty.</span></span>

<span data-ttu-id="a5eda-277">Accedi toohello cluster tooquery Windows Update risultati.</span><span class="sxs-lookup"><span data-stu-id="a5eda-277">Log in toohello cluster tooquery Windows Update results.</span></span> <span data-ttu-id="a5eda-278">Trovare l'indirizzo di replica hello per il sito primario di hello di hello servizio Coordinator quindi hit hello URL dal browser hello: http://&lt;REPLICA IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="a5eda-278">Then find out hello replica address for hello primary of hello Coordinator Service, and hit hello URL from hello browser: http://&lt;REPLICA-IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="a5eda-279">endpoint REST Hello per il servizio coordinatore hello dispone di una porta dinamica.</span><span class="sxs-lookup"><span data-stu-id="a5eda-279">hello REST endpoint for hello Coordinator Service has a dynamic port.</span></span> <span data-ttu-id="a5eda-280">toocheck hello URL esatto, fare riferimento toohello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a5eda-280">toocheck hello exact URL, refer toohello Service Fabric Explorer.</span></span> <span data-ttu-id="a5eda-281">Ad esempio, i risultati di hello sono disponibili in `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span><span class="sxs-lookup"><span data-stu-id="a5eda-281">For example, hello results are available at `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.</span></span>

![Immagine dell'endpoint REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


<span data-ttu-id="a5eda-283">Se il proxy inverso hello è abilitata sul cluster hello, è possibile accedere hello URL esterni nonché cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-283">If hello reverse proxy is enabled on hello cluster, you can access hello URL from outside of hello cluster as well.</span></span>
<span data-ttu-id="a5eda-284">endpoint che deve toobe Hello hit è http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span><span class="sxs-lookup"><span data-stu-id="a5eda-284">hello endpoint that needs toobe hit is http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.</span></span>

<span data-ttu-id="a5eda-285">proxy inverso di hello tooenable nel cluster hello, seguire i passaggi hello [inverso in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span><span class="sxs-lookup"><span data-stu-id="a5eda-285">tooenable hello reverse proxy on hello cluster, follow hello steps in [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).</span></span> 

> 
> [!WARNING]
> <span data-ttu-id="a5eda-286">Dopo la configurazione proxy inverso hello, tutti i servizi cluster hello micro che espongono un endpoint HTTP sono indirizzabili da all'esterno del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-286">After hello reverse proxy is configured, all micro services in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>

## <a name="diagnosticshealth-events"></a><span data-ttu-id="a5eda-287">Eventi di diagnostica/integrità</span><span class="sxs-lookup"><span data-stu-id="a5eda-287">Diagnostics/health events</span></span>

### <a name="collect-patch-orchestration-app-logs"></a><span data-ttu-id="a5eda-288">Raccogliere i log di Patch Orchestration App</span><span class="sxs-lookup"><span data-stu-id="a5eda-288">Collect patch orchestration app logs</span></span>

<span data-ttu-id="a5eda-289">Vengono raccolti i log di Patch Orchestration App come parte dei log di Service Fabric dalla versione di runtime `5.6.220.9494` e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a5eda-289">Patch orchestration app logs are collected as part of Service Fabric logs from runtime version `5.6.220.9494` and above.</span></span>
<span data-ttu-id="a5eda-290">Per i cluster che eseguono la versione di runtime Service Fabric minore `5.6.220.9494`, i registri possono essere raccolti utilizzando uno dei seguenti metodi hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-290">For clusters running Service Fabric runtime version less than `5.6.220.9494`, logs can be collected by using one of hello following methods.</span></span>

#### <a name="locally-on-each-node"></a><span data-ttu-id="a5eda-291">In locale in ogni nodo</span><span class="sxs-lookup"><span data-stu-id="a5eda-291">Locally on each node</span></span>

<span data-ttu-id="a5eda-292">I log vengono raccolti localmente su ogni nodo del cluster di Service Fabric se la versione del runtime di Service Fabric è precedente a `5.6.220.9494`.</span><span class="sxs-lookup"><span data-stu-id="a5eda-292">Logs are collected locally on each Service Fabric cluster node if Service Fabric runtime version is less than `5.6.220.9494`.</span></span> <span data-ttu-id="a5eda-293">Hello percorso tooaccess hello viene \[Service Fabric\_installazione\_unità\]:\\PatchOrchestrationApplication\\log.</span><span class="sxs-lookup"><span data-stu-id="a5eda-293">hello location tooaccess hello logs is \[Service Fabric\_Installation\_Drive\]:\\PatchOrchestrationApplication\\logs.</span></span>

<span data-ttu-id="a5eda-294">Ad esempio, se Service Fabric viene installato nell'unità D, percorso hello è d:\\PatchOrchestrationApplication\\log.</span><span class="sxs-lookup"><span data-stu-id="a5eda-294">For example, if Service Fabric is installed on drive D, hello path is D:\\PatchOrchestrationApplication\\logs.</span></span>

#### <a name="central-location"></a><span data-ttu-id="a5eda-295">Posizione centrale</span><span class="sxs-lookup"><span data-stu-id="a5eda-295">Central location</span></span>

<span data-ttu-id="a5eda-296">Se diagnostica Azure è configurata come parte di alcuni passaggi, i registri per app di orchestrazione hello patch sono disponibili in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a5eda-296">If Azure Diagnostics is configured as part of prerequisite steps, logs for hello patch orchestration app are available in Azure Storage.</span></span>

### <a name="health-reports"></a><span data-ttu-id="a5eda-297">Report sull'integrità</span><span class="sxs-lookup"><span data-stu-id="a5eda-297">Health reports</span></span>

<span data-ttu-id="a5eda-298">app di orchestrazione patch Hello pubblica anche rapporti di integrità in base hello servizio Coordinator o hello servizio agente del nodo in hello seguenti casi:</span><span class="sxs-lookup"><span data-stu-id="a5eda-298">hello patch orchestration app also publishes health reports against hello Coordinator Service or hello Node Agent Service in hello following cases:</span></span>

#### <a name="a-windows-update-operation-failed"></a><span data-ttu-id="a5eda-299">Un'operazione di Windows Update ha avuto esito negativo</span><span class="sxs-lookup"><span data-stu-id="a5eda-299">A Windows Update operation failed</span></span>

<span data-ttu-id="a5eda-300">Se un'operazione di aggiornamento di Windows non riesce in un nodo, viene generato un report di integrità su hello servizio agente del nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-300">If a Windows Update operation fails on a node, a health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="a5eda-301">Dettagli del rapporto di stato hello contengono il nome di nodo problematico hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-301">Details of hello health report contain hello problematic node name.</span></span>

<span data-ttu-id="a5eda-302">Dopo l'applicazione di patch è stata completata nel nodo problematico hello, report hello viene automaticamente cancellato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-302">After patching is successfully completed on hello problematic node, hello report is automatically cleared.</span></span>

#### <a name="hello-node-agent-ntservice-is-down"></a><span data-ttu-id="a5eda-303">Hello NTService agente nodo è inattivo</span><span class="sxs-lookup"><span data-stu-id="a5eda-303">hello Node Agent NTService is down</span></span>

<span data-ttu-id="a5eda-304">Se hello NTService agente nodo è attivo in un nodo, viene generato un report di integrità a livello di avviso su hello servizio agente del nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-304">If hello Node Agent NTService is down on a node, a warning-level health report is generated against hello Node Agent Service.</span></span>

#### <a name="hello-repair-manager-service-is-not-enabled"></a><span data-ttu-id="a5eda-305">servizio di gestione di Hello riparazione non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-305">hello repair manager service is not enabled</span></span>

<span data-ttu-id="a5eda-306">Se il servizio di gestione ripristino hello non viene trovato nel cluster hello, viene generato un report di integrità a livello di avviso per il servizio coordinatore hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-306">If hello repair manager service is not found on hello cluster, a warning-level health report is generated for hello Coordinator Service.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="a5eda-307">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="a5eda-307">Frequently asked questions</span></span>

<span data-ttu-id="a5eda-308">D:</span><span class="sxs-lookup"><span data-stu-id="a5eda-308">Q.</span></span> <span data-ttu-id="a5eda-309">**Perché è presente il cluster in uno stato di errore durante l'esecuzione di app di orchestrazione patch hello?**</span><span class="sxs-lookup"><span data-stu-id="a5eda-309">**Why do I see my cluster in an error state when hello patch orchestration app is running?**</span></span>

<span data-ttu-id="a5eda-310">R.</span><span class="sxs-lookup"><span data-stu-id="a5eda-310">A.</span></span> <span data-ttu-id="a5eda-311">Durante il processo di installazione di hello, hello patch orchestrazione app disabilita o riavvia nodi, che possono comportare temporaneamente integrità hello del cluster di hello risulti non disponibile.</span><span class="sxs-lookup"><span data-stu-id="a5eda-311">During hello installation process, hello patch orchestration app disables or restarts nodes, which can temporarily result in hello health of hello cluster going down.</span></span>

<span data-ttu-id="a5eda-312">In base ai criteri di hello per un'applicazione hello, entrambi un nodo può scendere durante un'operazione di gestione delle patch *o* un intero dominio di aggiornamento può scendere contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="a5eda-312">Based on hello policy for hello application, either one node can go down during a patching operation *or* an entire upgrade domain can go down simultaneously.</span></span>

<span data-ttu-id="a5eda-313">Fine hello di installazione dell'aggiornamento di Windows hello, hello nodi vengono riabilitati dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="a5eda-313">By hello end of hello Windows Update installation, hello nodes are reenabled post restart.</span></span>

<span data-ttu-id="a5eda-314">Nell'esempio seguente di hello, cluster hello è verificato un stato di errore tooan temporaneamente perché i due nodi sono inattivi e hello MaxPercentageUnhealthNodes criterio violato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-314">In hello following example, hello cluster went tooan error state temporarily because two nodes were down and hello MaxPercentageUnhealthNodes policy was violated.</span></span> <span data-ttu-id="a5eda-315">Errore di Hello è temporanea fino a quando non è in corso l'applicazione di patch operazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-315">hello error is temporary until hello patching operation is ongoing.</span></span>

![Immagine del cluster non integro](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

<span data-ttu-id="a5eda-317">Se hello problema persiste, consultare la sezione Risoluzione dei problemi toohello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-317">If hello issue persists, refer toohello Troubleshooting section.</span></span>

<span data-ttu-id="a5eda-318">D:</span><span class="sxs-lookup"><span data-stu-id="a5eda-318">Q.</span></span> <span data-ttu-id="a5eda-319">**Patch Orchestration App è in stato di avviso**</span><span class="sxs-lookup"><span data-stu-id="a5eda-319">**Patch orchestration app is in warning state**</span></span>

<span data-ttu-id="a5eda-320">R.</span><span class="sxs-lookup"><span data-stu-id="a5eda-320">A.</span></span> <span data-ttu-id="a5eda-321">Se un rapporto di stato registrato a fronte di un'applicazione hello hello radice causa, controllare toosee.</span><span class="sxs-lookup"><span data-stu-id="a5eda-321">Check toosee if a health report posted against hello application is hello root cause.</span></span> <span data-ttu-id="a5eda-322">Avviso di hello contiene in genere, i dettagli del problema hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-322">Usually, hello warning contains details of hello problem.</span></span> <span data-ttu-id="a5eda-323">Se il problema di hello è temporaneo, un'applicazione hello è previsto tooauto-Ripristina da questo stato.</span><span class="sxs-lookup"><span data-stu-id="a5eda-323">If hello issue is transient, hello application is expected tooauto-recover from this state.</span></span>

<span data-ttu-id="a5eda-324">D:</span><span class="sxs-lookup"><span data-stu-id="a5eda-324">Q.</span></span> <span data-ttu-id="a5eda-325">**Che cosa può fare se il cluster è integro ed è necessario un aggiornamento del sistema operativo urgenti toodo**</span><span class="sxs-lookup"><span data-stu-id="a5eda-325">**What can I do if my cluster is unhealthy and I need toodo an urgent operating system update?**</span></span>

<span data-ttu-id="a5eda-326">R.</span><span class="sxs-lookup"><span data-stu-id="a5eda-326">A.</span></span> <span data-ttu-id="a5eda-327">app di orchestrazione Hello patch non installare gli aggiornamenti mentre il cluster hello è integro.</span><span class="sxs-lookup"><span data-stu-id="a5eda-327">hello patch orchestration app does not install updates while hello cluster is unhealthy.</span></span> <span data-ttu-id="a5eda-328">Provare toobring cluster tooa integro toounblock hello patch orchestrazione app flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a5eda-328">Try toobring your cluster tooa healthy state toounblock hello patch orchestration app workflow.</span></span>

<span data-ttu-id="a5eda-329">D:</span><span class="sxs-lookup"><span data-stu-id="a5eda-329">Q.</span></span> <span data-ttu-id="a5eda-330">**Perché l'applicazione di patch per i cluster richiede molto tempo toorun?**</span><span class="sxs-lookup"><span data-stu-id="a5eda-330">**Why does patching across clusters take so long toorun?**</span></span>

<span data-ttu-id="a5eda-331">R.</span><span class="sxs-lookup"><span data-stu-id="a5eda-331">A.</span></span> <span data-ttu-id="a5eda-332">tempo di Hello necessario dall'app di orchestrazione patch hello dipende principalmente hello seguenti fattori:</span><span class="sxs-lookup"><span data-stu-id="a5eda-332">hello time needed by hello patch orchestration app is mostly dependent on hello following factors:</span></span>

- <span data-ttu-id="a5eda-333">criteri di Hello di hello servizio coordinatore.</span><span class="sxs-lookup"><span data-stu-id="a5eda-333">hello policy of hello Coordinator Service.</span></span> 
  - <span data-ttu-id="a5eda-334">criteri predefiniti, Hello `NodeWise`, comporta l'applicazione di patch solo un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="a5eda-334">hello default policy, `NodeWise`, results in patching only one node at a time.</span></span> <span data-ttu-id="a5eda-335">In particolare nel caso di hello di cluster più grande, è consigliabile utilizzare hello `UpgradeDomainWise` tooachieve criteri più veloce l'applicazione di patch per i cluster.</span><span class="sxs-lookup"><span data-stu-id="a5eda-335">Especially in hello case of bigger clusters, we recommend that you use hello `UpgradeDomainWise` policy tooachieve faster patching across clusters.</span></span>
- <span data-ttu-id="a5eda-336">numero di Hello degli aggiornamenti disponibili per il download e installazione.</span><span class="sxs-lookup"><span data-stu-id="a5eda-336">hello number of updates available for download and installation.</span></span> 
- <span data-ttu-id="a5eda-337">installare un aggiornamento, che non deve superare un paio d'ore Hello toodownload tempo medio necessario.</span><span class="sxs-lookup"><span data-stu-id="a5eda-337">hello average time needed toodownload and install an update, which should not exceed a couple of hours.</span></span>
- <span data-ttu-id="a5eda-338">prestazioni Hello di larghezza di banda di rete e macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-338">hello performance of hello VM and network bandwidth.</span></span>

<span data-ttu-id="a5eda-339">D:</span><span class="sxs-lookup"><span data-stu-id="a5eda-339">Q.</span></span> <span data-ttu-id="a5eda-340">**Motivo per cui è non vengono visualizzati alcuni aggiornamenti in Windows Update risultati ottenuti tramite l'api REST, ma non nella cronologia di Windows Update sul computer hello?**</span><span class="sxs-lookup"><span data-stu-id="a5eda-340">**Why do I see some updates in Windows Update results obtained via REST api's, but not under hello Windows Update history on machine?**</span></span>

<span data-ttu-id="a5eda-341">R.</span><span class="sxs-lookup"><span data-stu-id="a5eda-341">A.</span></span> <span data-ttu-id="a5eda-342">Alcuni aggiornamenti del prodotto è necessario toobe archiviata la cronologia delle rispettive/patch di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a5eda-342">Some product updates need toobe checked in their respective update/patch history.</span></span> <span data-ttu-id="a5eda-343">Ad esempio: gli aggiornamenti di Windows Defender non vengono visualizzati nella cronologia di Windows Update in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a5eda-343">Eg: Windows Defender updates do not show up in Windows Update history on Windows Server 2016.</span></span>

## <a name="disclaimers"></a><span data-ttu-id="a5eda-344">Dichiarazioni di non responsabilità</span><span class="sxs-lookup"><span data-stu-id="a5eda-344">Disclaimers</span></span>

- <span data-ttu-id="a5eda-345">app di Hello patch orchestrazione accetta hello contratto di licenza dell'utente finale di Windows Update per conto di utente hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-345">hello patch orchestration app accepts hello End-User License Agreement of Windows Update on behalf of hello user.</span></span> <span data-ttu-id="a5eda-346">Facoltativamente, hello impostazione può essere disattivata nella configurazione di hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-346">Optionally, hello setting can be turned off in hello configuration of hello application.</span></span>

- <span data-ttu-id="a5eda-347">Hello patch orchestrazione app raccoglie dati di telemetria tootrack utilizzo e delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a5eda-347">hello patch orchestration app collects telemetry tootrack usage and performance.</span></span> <span data-ttu-id="a5eda-348">dati di telemetria dell'applicazione Hello segue l'impostazione di hello dell'impostazione di telemetria del runtime di Service Fabric hello (che è attivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="a5eda-348">hello application’s telemetry follows hello setting of hello Service Fabric runtime’s telemetry setting (which is on by default).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a5eda-349">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a5eda-349">Troubleshooting</span></span>

### <a name="a-node-is-not-coming-back-tooup-state"></a><span data-ttu-id="a5eda-350">Un nodo non tornerà tooup stato</span><span class="sxs-lookup"><span data-stu-id="a5eda-350">A node is not coming back tooup state</span></span>

<span data-ttu-id="a5eda-351">**nodo Hello potrebbe essere bloccata in uno stato di disattivazione perché**:</span><span class="sxs-lookup"><span data-stu-id="a5eda-351">**hello node might be stuck in a disabling state because**:</span></span>

<span data-ttu-id="a5eda-352">Un controllo di sicurezza è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="a5eda-352">A safety check is pending.</span></span> <span data-ttu-id="a5eda-353">tooremedy questa situazione, verificare che siano disponibili sufficienti nodi in uno stato integro.</span><span class="sxs-lookup"><span data-stu-id="a5eda-353">tooremedy this situation, ensure that enough nodes are available in a healthy state.</span></span>

<span data-ttu-id="a5eda-354">**nodo Hello potrebbe essere bloccata in uno stato disabilitato perché**:</span><span class="sxs-lookup"><span data-stu-id="a5eda-354">**hello node might be stuck in a disabled state because**:</span></span>

- <span data-ttu-id="a5eda-355">nodo Hello è stata disabilitata manualmente.</span><span class="sxs-lookup"><span data-stu-id="a5eda-355">hello node was disabled manually.</span></span>
- <span data-ttu-id="a5eda-356">nodo Hello è stata disabilitata a causa di processo di tooan dell'infrastruttura di Azure in corso.</span><span class="sxs-lookup"><span data-stu-id="a5eda-356">hello node was disabled due tooan ongoing Azure infrastructure job.</span></span>
- <span data-ttu-id="a5eda-357">nodo Hello è stata disabilitata temporaneamente dal nodo di hello patch orchestrazione app toopatch hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-357">hello node was disabled temporarily by hello patch orchestration app toopatch hello node.</span></span>

<span data-ttu-id="a5eda-358">**Hello nodo potrebbe essere bloccato in uno stato inattivo perché**:</span><span class="sxs-lookup"><span data-stu-id="a5eda-358">**hello node might be stuck in a down state because**:</span></span>

- <span data-ttu-id="a5eda-359">nodo Hello è stato inserito manualmente in uno stato inattivo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-359">hello node was put in a down state manually.</span></span>
- <span data-ttu-id="a5eda-360">nodo Hello è in fase di riavvio (che potrebbe essere attivato da hello patch orchestrazione app).</span><span class="sxs-lookup"><span data-stu-id="a5eda-360">hello node is undergoing a restart (which might be triggered by hello patch orchestration app).</span></span>
- <span data-ttu-id="a5eda-361">nodo Hello è inattivo a causa di tooa difettoso VM o computer o rete problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="a5eda-361">hello node is down due tooa faulty VM or machine or network connectivity issues.</span></span>

### <a name="updates-were-skipped-on-some-nodes"></a><span data-ttu-id="a5eda-362">Gli aggiornamenti sono stati ignorati in alcuni nodi</span><span class="sxs-lookup"><span data-stu-id="a5eda-362">Updates were skipped on some nodes</span></span>

<span data-ttu-id="a5eda-363">app di orchestrazione patch Hello tenta tooinstall un aggiornamento in base toohello riprogrammazione criterio di Windows.</span><span class="sxs-lookup"><span data-stu-id="a5eda-363">hello patch orchestration app tries tooinstall a Windows update according toohello rescheduling policy.</span></span> <span data-ttu-id="a5eda-364">servizio Hello tenta nodo hello toorecover e ignorare i criteri di applicazione di hello aggiornamento secondo toohello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-364">hello service tries toorecover hello node and skip hello update according toohello application policy.</span></span>

<span data-ttu-id="a5eda-365">In tal caso, viene generato un report di integrità a livello di avviso su hello servizio agente del nodo.</span><span class="sxs-lookup"><span data-stu-id="a5eda-365">In such a case, a warning-level health report is generated against hello Node Agent Service.</span></span> <span data-ttu-id="a5eda-366">il risultato di Hello di Windows Update contiene anche motivo possibile: hello errore hello.</span><span class="sxs-lookup"><span data-stu-id="a5eda-366">hello result for Windows Update also contains hello possible reason for hello failure.</span></span>

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a><span data-ttu-id="a5eda-367">integrità Hello del cluster di hello passa tooerror durante l'installazione dell'aggiornamento hello</span><span class="sxs-lookup"><span data-stu-id="a5eda-367">hello health of hello cluster goes tooerror while hello update installs</span></span>

<span data-ttu-id="a5eda-368">Un aggiornamento di Windows non corretto può compromettere l'integrità di hello di un'applicazione o del cluster in un nodo particolare o di un dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a5eda-368">A faulty Windows update can bring down hello health of an application or cluster on a particular node or upgrade domain.</span></span> <span data-ttu-id="a5eda-369">Hello patch orchestrazione app interrompe un'operazione di aggiornamento di Windows successive fino a cluster hello è integro nuovamente.</span><span class="sxs-lookup"><span data-stu-id="a5eda-369">hello patch orchestration app discontinues any subsequent Windows Update operation until hello cluster is healthy again.</span></span>

<span data-ttu-id="a5eda-370">Un amministratore deve intervenire e determinare perché un'applicazione hello o il cluster è diventato non integro scadenza tooWindows Update.</span><span class="sxs-lookup"><span data-stu-id="a5eda-370">An administrator must intervene and determine why hello application or cluster became unhealthy due tooWindows Update.</span></span>

## <a name="release-notes-"></a><span data-ttu-id="a5eda-371">Note sulla versione:</span><span class="sxs-lookup"><span data-stu-id="a5eda-371">Release Notes :</span></span>

### <a name="version-110"></a><span data-ttu-id="a5eda-372">Versione 1.1.0</span><span class="sxs-lookup"><span data-stu-id="a5eda-372">Version 1.1.0</span></span>
- <span data-ttu-id="a5eda-373">Versione pubblica</span><span class="sxs-lookup"><span data-stu-id="a5eda-373">Public release</span></span>

### <a name="version-111"></a><span data-ttu-id="a5eda-374">Versione 1.1.1</span><span class="sxs-lookup"><span data-stu-id="a5eda-374">Version 1.1.1</span></span>
- <span data-ttu-id="a5eda-375">Correzione di un bug in SetupEntryPoint di NodeAgentService che ha impedito l'installazione di NodeAgentNTService.</span><span class="sxs-lookup"><span data-stu-id="a5eda-375">Fixed a bug in SetupEntryPoint of NodeAgentService that prevented installation of NodeAgentNTService.</span></span>

### <a name="version-120-latest"></a><span data-ttu-id="a5eda-376">Versione 1.2.0 (versione più recente)</span><span class="sxs-lookup"><span data-stu-id="a5eda-376">Version 1.2.0 (Latest)</span></span>

- <span data-ttu-id="a5eda-377">Correzioni di bug nel flusso di lavoro di riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="a5eda-377">Bug fixes around system restart workflow.</span></span>
- <span data-ttu-id="a5eda-378">Correzione di bug nella creazione di attività RM a causa di controllo di integrità toowhich durante la preparazione delle attività di ripristino si verificava come previsto.</span><span class="sxs-lookup"><span data-stu-id="a5eda-378">Bug fix in creation of RM tasks due toowhich health check during preparing repair tasks wasn't happening as expected.</span></span>
- <span data-ttu-id="a5eda-379">Hello modificato la modalità di avvio del servizio windows POANodeSvc toodelayed automatico.</span><span class="sxs-lookup"><span data-stu-id="a5eda-379">Changed hello startup mode for windows service POANodeSvc from auto toodelayed-auto.</span></span>
