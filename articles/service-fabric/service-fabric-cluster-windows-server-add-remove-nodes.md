---
title: Aggiungere o rimuovere nodi in un cluster di Service Fabric autonomo | Documentazione Microsoft
description: Informazioni su come aggiungere o rimuovere nodi in un cluster di Azure Service Fabric su una macchina fisica o virtuale che esegue Windows Server in locale o nel cloud.
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
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="84c36-103">Aggiungere o rimuovere nodi in un cluster di Service Fabric autonomo eseguito in Windows Server</span><span class="sxs-lookup"><span data-stu-id="84c36-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="84c36-104">Dopo la [creazione del cluster autonomo di Service Fabric in computer Windows Server](service-fabric-cluster-creation-for-windows-server.md) le esigenze aziendali possono cambiare e richiedere l'aggiunta o la rimozione di più nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="84c36-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="84c36-105">Questo articolo riporta i passaggi dettagliati per ottenere questo risultato.</span><span class="sxs-lookup"><span data-stu-id="84c36-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="84c36-106">Si noti che la funzionalità di aggiunta o rimozione di nodi non è supportata nei cluster di sviluppo locali.</span><span class="sxs-lookup"><span data-stu-id="84c36-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="84c36-107">Aggiungere nodi al cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="84c36-108">Preparare la VM o il computer che si vuole aggiungere al cluster seguendo i passaggi illustrati nella sezione [Preparare i computer con i prerequisiti per la distribuzione del cluster](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="84c36-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="84c36-109">Pianificare a quale dominio di errore e dominio di aggiornamento si aggiungerà il computer o la VM</span><span class="sxs-lookup"><span data-stu-id="84c36-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="84c36-110">Creare una connessione Desktop remoto (RDP) con il computer o la VM da aggiungere al cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="84c36-111">Copiare o [scaricare il pacchetto autonomo di Service Fabric per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) nel computer o nella VM e decomprimerlo</span><span class="sxs-lookup"><span data-stu-id="84c36-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="84c36-112">Eseguire PowerShell con privilegi elevati e passare alla posizione del pacchetto decompresso</span><span class="sxs-lookup"><span data-stu-id="84c36-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="84c36-113">Eseguire lo script *AddNode.ps1* con i parametri che descrivono il nuovo nodo da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="84c36-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="84c36-114">L'esempio seguente aggiunge in UD1 e fd:/dc1/r0 un nuovo nodo denominato VM5 con tipo NodeType0 e indirizzo IP 182.17.34.52.</span><span class="sxs-lookup"><span data-stu-id="84c36-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="84c36-115">*ExistingClusterConnectionEndPoint* è un endpoint di connessione per un nodo già presente nel cluster esistente e può corrispondere all'indirizzo IP di *qualsiasi* nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="84c36-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="84c36-116">Al termine dell'esecuzione dello script è possibile eseguire il cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) per verificare se il nuovo nodo è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="84c36-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="84c36-117">Per garantire la coerenza tra i diversi nodi del cluster è necessario avviare un aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="84c36-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="84c36-118">Eseguire [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) per ottenere il file di configurazione più recente e includere il nodo appena aggiunto nella sezione "Nodes".</span><span class="sxs-lookup"><span data-stu-id="84c36-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="84c36-119">È anche consigliabile avere sempre a disposizione la configurazione cluster più recente in caso fosse necessario ridistribuire un cluster con la stessa configurazione.</span><span class="sxs-lookup"><span data-stu-id="84c36-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="84c36-120">Eseguire [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) per avviare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="84c36-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="84c36-121">È possibile monitorare lo stato dell'aggiornamento in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84c36-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84c36-122">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84c36-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="84c36-123">Aggiungere nodi a cluster configurati con la protezione di Windows mediante gMSA</span><span class="sxs-lookup"><span data-stu-id="84c36-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="84c36-124">Per i cluster configurati con un account del servizio gestito del gruppo (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx) è possibile aggiungere un nuovo nodo con un aggiornamento della configurazione:</span><span class="sxs-lookup"><span data-stu-id="84c36-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="84c36-125">Eseguire [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) su uno dei nodi esistenti per ottenere il file di configurazione più recente e includere nella sezione "Nodes" i dettagli relativi al nuovo nodo da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="84c36-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="84c36-126">Verificare che il nuovo nodo appartenga allo stesso account gestito del gruppo.</span><span class="sxs-lookup"><span data-stu-id="84c36-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="84c36-127">Questo account deve essere un account Administrator su tutti i computer.</span><span class="sxs-lookup"><span data-stu-id="84c36-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="84c36-128">Eseguire [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) per avviare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="84c36-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="84c36-129">È possibile monitorare lo stato dell'aggiornamento in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84c36-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84c36-130">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84c36-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="84c36-131">Aggiungere tipi di nodi al cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-131">Add node types to your cluster</span></span>
<span data-ttu-id="84c36-132">Per aggiungere un nuovo tipo di nodo modificare la configurazione, includere il nuovo tipo di nodo nella sezione "NodeTypes" in "Properties" e avviare un aggiornamento della configurazione usando [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84c36-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="84c36-133">Dopo aver completato l'aggiornamento, è possibile aggiungere al cluster nuovi nodi con questo tipo di nodo.</span><span class="sxs-lookup"><span data-stu-id="84c36-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="84c36-134">Rimuovere nodi dal cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="84c36-135">È possibile rimuovere un nodo da un cluster mediante un aggiornamento della configurazione, con le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="84c36-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="84c36-136">Eseguire [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) per ottenere il file di configurazione più recente e quindi *remove* per rimuovere il nodo dalla sezione "Nodes".</span><span class="sxs-lookup"><span data-stu-id="84c36-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="84c36-137">Aggiungere il parametro "NodesToBeRemoved" alla sezione "Setup" inclusa nella sezione "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="84c36-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="84c36-138">"value" deve essere un elenco separato da virgole contenente i nomi dei nodi da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="84c36-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

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
2. <span data-ttu-id="84c36-139">Eseguire [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) per avviare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="84c36-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="84c36-140">È possibile monitorare lo stato dell'aggiornamento in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84c36-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84c36-141">In alternativa è possibile eseguire [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84c36-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="84c36-142">È possibile che con la rimozione di nodi vengano avviati più aggiornamenti in sequenza.</span><span class="sxs-lookup"><span data-stu-id="84c36-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="84c36-143">Alcuni nodi sono contrassegnati con il tag `IsSeedNode=”true”` e possono essere identificati mediante query nel manifesto del cluster usando `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="84c36-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="84c36-144">La rimozione di tali nodi può richiedere più tempo perché comporta lo spostamento dei nodi di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="84c36-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="84c36-145">Il cluster deve mantenere almeno 3 nodi di tipo primario.</span><span class="sxs-lookup"><span data-stu-id="84c36-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="84c36-146">Rimuovere i tipi di nodi dal cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-146">Remove node types from your cluster</span></span>
<span data-ttu-id="84c36-147">Prima di rimuovere un tipo di nodo, verificare se sono presenti nodi che fanno riferimento al tipo di nodo stesso.</span><span class="sxs-lookup"><span data-stu-id="84c36-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="84c36-148">Rimuovere tali nodi prima di rimuovere il tipo di nodo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="84c36-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="84c36-149">Dopo aver rimosso tutti i nodi corrispondenti, è possibile rimuovere il tipo di nodo (NodeType) dalla configurazione del cluster e avviare un aggiornamento della configurazione mediante [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84c36-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="84c36-150">Sostituire i nodi primari del cluster</span><span class="sxs-lookup"><span data-stu-id="84c36-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="84c36-151">La sostituzione dei nodi primari deve essere eseguita un nodo alla volta, anziché eseguire la rimozione e l'aggiunta in batch.</span><span class="sxs-lookup"><span data-stu-id="84c36-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="84c36-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84c36-152">Next steps</span></span>
* [<span data-ttu-id="84c36-153">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="84c36-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="84c36-154">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="84c36-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="84c36-155">Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="84c36-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

