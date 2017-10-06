---
title: aaaAdd o rimuovere nodi tooa autonomo cluster di Service Fabric | Documenti Microsoft
description: "Informazioni su come tooadd o rimuovere nodi tooan Azure Service Fabric cluster in un computer fisico o macchina virtuale che esegue Windows Server, che può essere locale o in qualsiasi cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="b577b-103">Aggiungere o rimuovere nodi tooa autonomo Service Fabric cluster che esegue Windows Server</span><span class="sxs-lookup"><span data-stu-id="b577b-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="b577b-104">Dopo aver [creato il cluster di Service Fabric autonomo nei computer Windows Server](service-fabric-cluster-creation-for-windows-server.md), possono modificare le esigenze aziendali e potrebbe essere necessario tooadd o rimuovere nodi tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="b577b-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="b577b-105">Questo articolo fornisce i passaggi dettagliati tooachieve questo.</span><span class="sxs-lookup"><span data-stu-id="b577b-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="b577b-106">Si noti che la funzionalità di aggiunta o rimozione di nodi non è supportata nei cluster di sviluppo locali.</span><span class="sxs-lookup"><span data-stu-id="b577b-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="b577b-107">Aggiungere nodi tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="b577b-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="b577b-108">Preparazione hello VM/macchina da tooadd tooyour cluster seguendo i passaggi di hello indicati in hello [hello Prepara computer prerequisiti hello toomeet per la distribuzione di cluster](service-fabric-cluster-creation-for-windows-server.md) sezione</span><span class="sxs-lookup"><span data-stu-id="b577b-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="b577b-109">Identificare il dominio di errore e dominio di aggiornamento si corso tooadd la macchina virtuale/macchina</span><span class="sxs-lookup"><span data-stu-id="b577b-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="b577b-110">Desktop remoto (RDP) nella macchina virtuale o computer che si desidera che il cluster di toohello tooadd hello</span><span class="sxs-lookup"><span data-stu-id="b577b-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="b577b-111">Copia o [download del pacchetto autonomo hello per Service Fabric per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/macchina e decomprimere il pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="b577b-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="b577b-112">Esecuzione di Powershell con privilegi elevati e passare toohello percorso del pacchetto decompresso hello</span><span class="sxs-lookup"><span data-stu-id="b577b-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="b577b-113">Eseguire hello *AddNode.ps1* script con i parametri di hello che descrivono hello nuovo nodo tooadd.</span><span class="sxs-lookup"><span data-stu-id="b577b-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="b577b-114">esempio Hello seguente aggiunge un nuovo nodo denominato VM5, con il tipo NodeType0 e un indirizzo IP, 182.17.34.52 in UD1 e fd: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="b577b-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="b577b-115">Hello *ExistingClusterConnectionEndPoint* è già un endpoint della connessione per un nodo nel cluster esistente hello, che può essere l'indirizzo IP hello del *qualsiasi* nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b577b-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="b577b-116">Al termine dell'esecuzione dello script hello, è possibile verificare se è stato aggiunto il nuovo nodo di hello eseguendo hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b577b-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="b577b-117">tooensure la coerenza tra i diversi nodi cluster hello, è necessario avviare un aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b577b-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="b577b-118">Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello file di configurazione più recente e aggiungere hello appena aggiunta nodo troppo sezione "Nodi".</span><span class="sxs-lookup"><span data-stu-id="b577b-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="b577b-119">È inoltre consigliabile tooalways hanno hello configurazione più recente del cluster disponibile in caso di hello che è necessario un cluster con hello tooredploy stessa configurazione.</span><span class="sxs-lookup"><span data-stu-id="b577b-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="b577b-120">Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b577b-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b577b-121">È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b577b-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b577b-122">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b577b-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="b577b-123">Aggiunta di nodi tooclusters configurato con la sicurezza di Windows utilizzando l'account</span><span class="sxs-lookup"><span data-stu-id="b577b-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="b577b-124">Per i cluster configurati con un account del servizio gestito del gruppo (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx) è possibile aggiungere un nuovo nodo con un aggiornamento della configurazione:</span><span class="sxs-lookup"><span data-stu-id="b577b-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="b577b-125">Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) in uno dei nodi esistenti hello tooget hello file di configurazione più recente e aggiungere i dettagli sul nuovo nodo hello desiderato tooadd nella sezione dei nodi"hello".</span><span class="sxs-lookup"><span data-stu-id="b577b-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="b577b-126">Verificare che il nuovo nodo hello fa parte di hello stesso account gestito di gruppo.</span><span class="sxs-lookup"><span data-stu-id="b577b-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="b577b-127">Questo account deve essere un account Administrator su tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="b577b-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="b577b-128">Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b577b-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="b577b-129">È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b577b-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b577b-130">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b577b-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="b577b-131">Aggiungere cluster tooyour tipi di nodo</span><span class="sxs-lookup"><span data-stu-id="b577b-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="b577b-132">In ordine tooadd un nuovo tipo di nodo, modificare il configurazione tooinclude hello nuovo tipo di nodo nella sezione "NodeTypes" in "Proprietà" e iniziare una configurazione di eseguire l'aggiornamento utilizzando [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b577b-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="b577b-133">Una volta completato l'aggiornamento di hello, è possibile aggiungere nuovo cluster di nodi tooyour con questo tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="b577b-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="b577b-134">Rimuovere nodi dal cluster</span><span class="sxs-lookup"><span data-stu-id="b577b-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="b577b-135">Un nodo può essere rimosso da un cluster con un aggiornamento della configurazione, nel seguente modo hello:</span><span class="sxs-lookup"><span data-stu-id="b577b-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="b577b-136">Eseguire [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) file di configurazione più recente di tooget hello e *rimuovere* nodo hello dalla sezione "Nodi".</span><span class="sxs-lookup"><span data-stu-id="b577b-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="b577b-137">Aggiungere "NodesToBeRemoved" hello parametro troppo "configurazione" sezione all'interno di sezione "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="b577b-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="b577b-138">Hello "value" deve essere un elenco separato da virgole di nomi di nodo di nodi che devono toobe rimosso.</span><span class="sxs-lookup"><span data-stu-id="b577b-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="b577b-139">Eseguire [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) aggiornamento hello toobegin.</span><span class="sxs-lookup"><span data-stu-id="b577b-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="b577b-140">È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b577b-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="b577b-141">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b577b-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="b577b-142">È possibile che con la rimozione di nodi vengano avviati più aggiornamenti in sequenza.</span><span class="sxs-lookup"><span data-stu-id="b577b-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="b577b-143">Alcuni nodi sono contrassegnati con `IsSeedNode=”true”` tag e può essere identificato tramite l'esecuzione di query cluster hello manifesto utilizzando `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="b577b-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="b577b-144">La rimozione di tali nodi può richiedere più tempo rispetto ad altri poiché dispongono di nodi seme hello toobe spostati in tali scenari.</span><span class="sxs-lookup"><span data-stu-id="b577b-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="b577b-145">cluster Hello devono mantenere un minimo di 3 nodi di tipo di nodo primario.</span><span class="sxs-lookup"><span data-stu-id="b577b-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="b577b-146">Rimuovere i tipi di nodi dal cluster</span><span class="sxs-lookup"><span data-stu-id="b577b-146">Remove node types from your cluster</span></span>
<span data-ttu-id="b577b-147">Prima di rimuovere un tipo di nodo, verificare se sono presenti nodi che fanno riferimento a tipo di nodo hello.</span><span class="sxs-lookup"><span data-stu-id="b577b-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="b577b-148">Rimuovere questi nodi prima di rimuovere il tipo di nodo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="b577b-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="b577b-149">Dopo aver rimosso tutti i nodi corrispondenti, è possibile rimuovere hello NodeType dalla configurazione del cluster hello e una configurazione di iniziare l'aggiornamento utilizzando [inizio ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="b577b-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="b577b-150">Sostituire i nodi primari del cluster</span><span class="sxs-lookup"><span data-stu-id="b577b-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="b577b-151">sostituzione di Hello dei nodi primari deve essere un nodo eseguito dopo l'altro, invece di rimuovere e quindi aggiungere in batch.</span><span class="sxs-lookup"><span data-stu-id="b577b-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b577b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b577b-152">Next steps</span></span>
* [<span data-ttu-id="b577b-153">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="b577b-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="b577b-154">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="b577b-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="b577b-155">Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="b577b-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

