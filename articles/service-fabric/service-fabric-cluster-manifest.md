---
title: aaaConfigure il cluster di Azure Service Fabric autonomo | Documenti Microsoft
description: Informazioni su come tooconfigure autonomo o un cluster di Service Fabric privato.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="4aef1-103">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="4aef1-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="4aef1-104">In questo articolo viene descritto come un cluster di Service Fabric autonomo tramite tooconfigure hello ***Clusterconfig*** file.</span><span class="sxs-lookup"><span data-stu-id="4aef1-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="4aef1-105">È possibile utilizzare queste informazioni toospecify file, ad esempio nodi di Service Fabric hello e i relativi indirizzi IP, i diversi tipi di nodi nel cluster hello, configurazioni di sicurezza hello, nonché la topologia di rete hello in termini di domini di errore, aggiornamento, l'autonomo cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="4aef1-106">Quando si [download del pacchetto Service Fabric autonomo hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alcuni esempi di file Clusterconfig hello sono computer di lavoro tooyour scaricato.</span><span class="sxs-lookup"><span data-stu-id="4aef1-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="4aef1-107">esempi di Hello con *DevCluster* nei relativi nomi consente di creare un cluster con tutti i tre nodi hello stesso computer, ad esempio nodi logici.</span><span class="sxs-lookup"><span data-stu-id="4aef1-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="4aef1-108">Almeno uno di questi nodi deve essere contrassegnato come primario.</span><span class="sxs-lookup"><span data-stu-id="4aef1-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="4aef1-109">Questo cluster è utile per un ambiente di sviluppo o test e non è supportato come cluster di produzione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="4aef1-110">esempi di Hello con *MultiMachine* nei relativi nomi, consente di creare un cluster di qualità di produzione, con ogni nodo in un computer separato.</span><span class="sxs-lookup"><span data-stu-id="4aef1-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="4aef1-111">*ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* Mostra come toocreate un test non protetto o produzione cluster rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="4aef1-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="4aef1-112">*ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* Mostra come cluster di test o produzione toocreate, protetti tramite [la sicurezza di Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="4aef1-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="4aef1-113">*ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* Mostra come cluster di test o produzione toocreate, protetti tramite [X509 sicurezza basata sui certificati](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="4aef1-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="4aef1-114">Ora verrà esaminata hello diverse sezioni di un ***Clusterconfig*** file come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="4aef1-115">Configurazioni generali del cluster</span><span class="sxs-lookup"><span data-stu-id="4aef1-115">General cluster configurations</span></span>
<span data-ttu-id="4aef1-116">Questo articolo descrive hello ampie specifiche configurazioni dei cluster, come illustrato nel frammento di codice JSON hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="4aef1-117">È possibile assegnare i cluster di Service Fabric tooyour qualsiasi nome descrittivo assegnandole toohello **nome** variabile.</span><span class="sxs-lookup"><span data-stu-id="4aef1-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="4aef1-118">Hello **clusterConfigurationVersion** è il numero di versione hello del cluster; è necessario aumentare ogni volta che si esegue l'aggiornamento del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4aef1-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="4aef1-119">È tuttavia consigliabile lasciare hello **apiVersion** toohello predefinita.</span><span class="sxs-lookup"><span data-stu-id="4aef1-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="4aef1-120">Nodi cluster hello</span><span class="sxs-lookup"><span data-stu-id="4aef1-120">Nodes on hello cluster</span></span>
<span data-ttu-id="4aef1-121">È possibile configurare i nodi di hello nel cluster di Service Fabric utilizzando hello **nodi** sezione come hello seguente mostra.</span><span class="sxs-lookup"><span data-stu-id="4aef1-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="4aef1-122">Un cluster Service Fabric deve contenere almeno 3 nodi.</span><span class="sxs-lookup"><span data-stu-id="4aef1-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="4aef1-123">È possibile aggiungere una sezione di toothis più nodi in base all'impostazione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="4aef1-124">Hello nella tabella seguente vengono illustrate le impostazioni di configurazione hello per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="4aef1-125">**Configurazione nodo**</span><span class="sxs-lookup"><span data-stu-id="4aef1-125">**Node configuration**</span></span> | <span data-ttu-id="4aef1-126">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="4aef1-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4aef1-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="4aef1-127">nodeName</span></span> |<span data-ttu-id="4aef1-128">È possibile assegnare qualsiasi nodo toohello nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="4aef1-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="4aef1-129">iPAddress</span></span> |<span data-ttu-id="4aef1-130">Trovare l'indirizzo IP di hello del nodo, aprire una finestra di comando e digitare `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="4aef1-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="4aef1-131">Prendere nota di indirizzo IPV4 hello e assegnarlo toohello **iPAddress** variabile.</span><span class="sxs-lookup"><span data-stu-id="4aef1-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="4aef1-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="4aef1-132">nodeTypeRef</span></span> |<span data-ttu-id="4aef1-133">È possibile assegnare un tipo diverso a ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="4aef1-134">Hello [tipi di nodo](#nodetypes) definiti nella sezione hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="4aef1-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="4aef1-135">faultDomain</span></span> |<span data-ttu-id="4aef1-136">Errore domini Abilita amministratori toodefine hello fisici nodi del cluster che potrebbero non riuscire in hello stesso tempo a causa di dipendenze fisico tooshared.</span><span class="sxs-lookup"><span data-stu-id="4aef1-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="4aef1-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="4aef1-137">upgradeDomain</span></span> |<span data-ttu-id="4aef1-138">Domini di aggiornamento vengono descritti i set di nodi che vengono arrestati per Service Fabric aggiornato su hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="4aef1-139">È possibile scegliere quali toowhich tooassign nodi domini di aggiornamento, poiché non sono limitate dalle eventuali requisiti fisici.</span><span class="sxs-lookup"><span data-stu-id="4aef1-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="4aef1-140">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="4aef1-140">Cluster properties</span></span>
<span data-ttu-id="4aef1-141">Hello **proprietà** sezione hello Clusterconfig è cluster hello tooconfigure usati come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="4aef1-142">Affidabilità</span><span class="sxs-lookup"><span data-stu-id="4aef1-142">Reliability</span></span>
<span data-ttu-id="4aef1-143">il concetto di Hello di **reliabilityLevel** definisce il numero di hello di repliche o istanze di servizi di sistema di Service Fabric hello che è possono eseguire sui nodi primari di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="4aef1-144">Determina l'affidabilità di hello di questi servizi e pertanto hello cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="4aef1-145">il valore di Hello è calcolata dal sistema hello in fase di creazione e l'aggiornamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="4aef1-146">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="4aef1-146">Diagnostics</span></span>
<span data-ttu-id="4aef1-147">Hello **diagnosticsStore** sezione consente di diagnostica di tooenable parametri tooconfigure e nodo di risoluzione dei problemi o errori del cluster, come illustrato nel seguente frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="4aef1-148">Hello **metadati** è una descrizione di diagnostica del cluster e può essere impostata in base all'impostazione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="4aef1-149">Queste variabili consentono di raccogliere log di traccia ETW, dump di arresto anomalo e contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="4aef1-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="4aef1-150">Per altre informazioni sui log di traccia ETW, leggere gli articoli [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Traccia ETW](https://msdn.microsoft.com/library/ms751538.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aef1-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="4aef1-151">Tutti i log inclusi [dump di arresto anomalo](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [i contatori delle prestazioni](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) può essere indirizzato toohello **connectionString** cartella nel computer.</span><span class="sxs-lookup"><span data-stu-id="4aef1-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="4aef1-152">È anche possibile usare *AzureStorage* per l'archiviazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="4aef1-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="4aef1-153">Per un frammento di esempio, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="4aef1-154">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="4aef1-154">Security</span></span>
<span data-ttu-id="4aef1-155">Hello **sicurezza** sezione è necessaria per un cluster di Service Fabric autonomo sicura.</span><span class="sxs-lookup"><span data-stu-id="4aef1-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="4aef1-156">Hello frammento di codice seguente viene illustrata una parte di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="4aef1-157">Hello **metadati** è una descrizione del cluster protetto e può essere impostata in base all'impostazione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="4aef1-158">Hello **ClusterCredentialType** e **ServerCredentialType** determinare il tipo di hello di sicurezza che consente di implementare cluster hello e nodi hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="4aef1-159">Possono essere impostati tooeither *X509* per una sicurezza basata sui certificati o *Windows* per una protezione basata su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4aef1-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="4aef1-160">Hello rest di hello **sicurezza** sezione si baserà sul tipo hello di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="4aef1-161">Lettura [sicurezza basata sui certificati in un cluster autonomo](service-fabric-windows-cluster-x509-security.md) o [la sicurezza di Windows in un cluster autonomo](service-fabric-windows-cluster-windows-security.md) per informazioni su come toofill out hello rest di hello **sicurezza**sezione.</span><span class="sxs-lookup"><span data-stu-id="4aef1-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="4aef1-162">Tipi di nodi</span><span class="sxs-lookup"><span data-stu-id="4aef1-162">Node Types</span></span>
<span data-ttu-id="4aef1-163">Hello **nodeTypes** sezione descrive il tipo di hello dei nodi di hello con il cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="4aef1-164">Come illustrato nel seguente frammento di hello, è necessario specificare il tipo di almeno un nodo per un cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="4aef1-165">Hello **nome** hello nome descrittivo per questo tipo di nodo specifico.</span><span class="sxs-lookup"><span data-stu-id="4aef1-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="4aef1-166">toocreate un nodo di questo tipo di nodo, assegnare il nome descrittivo di toohello **proprietà nodeTypeRef** variabile per il nodo, come indicato in [sopra](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="4aef1-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="4aef1-167">Per ogni tipo di nodo, definire l'endpoint della connessione hello che verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4aef1-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="4aef1-168">È possibile scegliere qualsiasi numero di porta per gli endpoint di connessione, purché non entrino in conflitto con altri endpoint in questo cluster.</span><span class="sxs-lookup"><span data-stu-id="4aef1-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="4aef1-169">In un cluster a più nodi, saranno presenti uno o più nodi principali (ad esempio **isPrimary** impostare troppo*true*), a seconda di hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="4aef1-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="4aef1-170">Lettura [considerazioni sulla pianificazione della capacità di Service Fabric cluster](service-fabric-cluster-capacity.md) per informazioni su **nodeTypes** e **reliabilityLevel**, tooknow le primario e hello e tipi di nodo non primario.</span><span class="sxs-lookup"><span data-stu-id="4aef1-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="4aef1-171">Gli endpoint utilizzati tipi di nodo hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="4aef1-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="4aef1-172">*clientConnectionEndpointPort* hello porta utilizzato dal cluster toohello tooconnect di hello client, quando si utilizza l'API client hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="4aef1-173">*clusterConnectionEndpointPort* hello porta in cui i nodi di hello comunicano tra loro.</span><span class="sxs-lookup"><span data-stu-id="4aef1-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="4aef1-174">*leaseDriverEndpointPort* hello porta utilizzata dal hello cluster lease driver toofind out se i nodi di hello sono ancora attivi.</span><span class="sxs-lookup"><span data-stu-id="4aef1-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="4aef1-175">*serviceConnectionEndpointPort* è porta hello utilizzata dalle applicazioni hello e i servizi distribuiti in un nodo, toocommunicate con client di Service Fabric hello in quel determinato nodo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="4aef1-176">*httpGatewayEndpointPort* hello porta utilizzato dal cluster toohello tooconnect di hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4aef1-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="4aef1-177">*ephemeralPorts* override hello [porte dinamiche utilizzate dal sistema operativo hello](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="4aef1-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="4aef1-178">Service Fabric utilizzerà una parte di queste porte dell'applicazione e hello rimanenti saranno disponibili per hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="4aef1-179">Presente nel sistema operativo, hello questo intervallo toohello esistente intervallo eseguirà il mapping anche per tutti gli scopi, è possibile utilizzare intervalli hello dati nei file JSON di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="4aef1-180">È necessario che la differenza hello tra inizio hello e porte finali hello sia almeno 255 toomake.</span><span class="sxs-lookup"><span data-stu-id="4aef1-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="4aef1-181">Se questa differenza è troppo bassa, poiché questo intervallo è condiviso con sistema operativo hello, che potrebbero verificarsi conflitti.</span><span class="sxs-lookup"><span data-stu-id="4aef1-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="4aef1-182">Visualizzare l'intervallo di porte dinamiche hello configurato eseguendo `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="4aef1-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="4aef1-183">*applicationPorts* sono porte hello che verranno utilizzate dalle applicazioni di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="4aef1-184">intervallo di porte applicazione Hello deve essere sufficientemente grande toocover requisito di endpoint hello delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4aef1-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="4aef1-185">Questo intervallo deve essere esclusivo dall'intervallo di porte dinamiche hello computer hello, vale a dire hello *ephemeralPorts* intervallo come set di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="4aef1-186">Service Fabric utilizzeranno queste ogni volta che nuove porte sono necessari, nonché occuperà di apertura firewall hello per queste porte.</span><span class="sxs-lookup"><span data-stu-id="4aef1-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="4aef1-187">*reverseProxyEndpointPort* è un endpoint proxy inverso facoltativo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="4aef1-188">Per altri dettagli vedere [Proxy inverso di Service Fabric](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="4aef1-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="4aef1-189">Impostazioni log</span><span class="sxs-lookup"><span data-stu-id="4aef1-189">Log Settings</span></span>
<span data-ttu-id="4aef1-190">Hello **fabricSettings** sezione consente di directory radice di hello tooset per dati di Service Fabric hello e di log.</span><span class="sxs-lookup"><span data-stu-id="4aef1-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="4aef1-191">È possibile personalizzare queste solo durante la creazione iniziale del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="4aef1-192">Per un frammento di esempio di questa sezione, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="4aef1-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="4aef1-193">È consigliabile usare un'unità non del sistema operativo come hello FabricDataRoot e FabricLogRoot poiché fornisce maggiore affidabilità rispetto degli arresti anomali del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="4aef1-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="4aef1-194">Si noti che se si personalizza solo radice dei dati di hello, quindi radice log hello verrà inserito un livello inferiore radice dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="4aef1-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="4aef1-195">Impostazioni di Reliable Services con stato</span><span class="sxs-lookup"><span data-stu-id="4aef1-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="4aef1-196">Hello **KtlLogger** sezione consente di impostazioni di configurazione globali hello tooset per servizi affidabili.</span><span class="sxs-lookup"><span data-stu-id="4aef1-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="4aef1-197">Per altre informazioni su queste impostazioni leggere [Configurazione dei servizi Reliable Services con stato](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="4aef1-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="4aef1-198">esempio Hello riportato di seguito viene illustrata la toochange hello hello condiviso log delle transazioni che ottiene creazione tooback raccolte affidabile per i servizi con stati.</span><span class="sxs-lookup"><span data-stu-id="4aef1-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="4aef1-199">Funzionalità aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4aef1-199">Add-on features</span></span>
<span data-ttu-id="4aef1-200">le funzioni aggiuntive tooconfigure, hello apiVersion deve essere configurato come ' 04-2017' o versione successiva e addonFeatures deve toobe configurato:</span><span class="sxs-lookup"><span data-stu-id="4aef1-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="4aef1-201">Supporto dei contenitori</span><span class="sxs-lookup"><span data-stu-id="4aef1-201">Container support</span></span>
<span data-ttu-id="4aef1-202">supporto del contenitore tooenable per contenitore di windows server e il contenitore di hyper-v per i cluster autonomo, funzionalità di componente aggiuntivo 'DnsService' hello deve toobe abilitato.</span><span class="sxs-lookup"><span data-stu-id="4aef1-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4aef1-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4aef1-203">Next steps</span></span>
<span data-ttu-id="4aef1-204">Dopo aver creato un file Clusterconfig completo configurato per l'installazione del cluster autonomo, è possibile distribuire il cluster dal seguente hello [creare un cluster di Service Fabric autonomo](service-fabric-cluster-creation-for-windows-server.md) e quindi procedere troppo[visualizzazione cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4aef1-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

