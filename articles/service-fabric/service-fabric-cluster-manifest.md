---
title: Configurare un cluster autonomo di Azure Service Fabric | Microsoft Docs
description: Informazioni su come configurare un cluster di Service Fabric autonomo o privato.
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="ba6a1-103">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="ba6a1-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="ba6a1-104">Questo articolo descrive come configurare un cluster di Service Fabric autonomo usando il file ***ClusterConfig.JSON***.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="ba6a1-105">Questo file può essere usato per specificare informazioni quali i nodi di Service Fabric e i relativi indirizzi IP, i vari tipi di nodi nel cluster, le configurazioni di sicurezza e la topologia di rete in termini di domini di errore/aggiornamento per il cluster autonomo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="ba6a1-106">Quando si [scarica un pacchetto autonomo di Service Fabric](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), alcuni campioni del file ClusterConfig.JSON vengono scaricati sul computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="ba6a1-107">I campioni i cui nomi contengono *DevCluster* aiuteranno a creare un cluster con tutti e tre i nodi nello stesso computer, ad esempio nodi logici.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="ba6a1-108">Almeno uno di questi nodi deve essere contrassegnato come primario.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="ba6a1-109">Questo cluster è utile per un ambiente di sviluppo o test e non è supportato come cluster di produzione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="ba6a1-110">I campioni i cui nomi contengono *MultiMachine* aiuteranno a creare un cluster di qualità di produzione, in cui ogni nodo si trova in un computer separato.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="ba6a1-111">*ClusterConfig.Unsecure.DevCluster.JSON* e *ClusterConfig.Unsecure.MultiMachine.JSON* mostrano rispettivamente come creare cluster senza protezione per test e produzione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="ba6a1-112">*ClusterConfig.Windows.DevCluster.JSON* e *ClusterConfig.Windows.MultiMachine.JSON* mostrano come creare cluster di test o produzione protetti tramite [protezione di Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="ba6a1-113">*ClusterConfig.X509.DevCluster.JSON* e *ClusterConfig.X509.MultiMachine.JSON* mostrano come creare cluster di test o produzione protetti tramite [protezione basata su certificato X509](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="ba6a1-114">Verranno esaminate ora le diverse sezioni di un file ***ClusterConfig.JSON***, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="ba6a1-115">Configurazioni generali del cluster</span><span class="sxs-lookup"><span data-stu-id="ba6a1-115">General cluster configurations</span></span>
<span data-ttu-id="ba6a1-116">Questa sezione tratta in modo ampio le configurazioni specifiche dei cluster, come illustrato nel frammento di codice JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="ba6a1-117">È possibile attribuire qualsiasi nome descrittivo al cluster di Service Fabric assegnandolo alla variabile **name**.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="ba6a1-118">**clusterConfigurationVersion** rappresenta il numero di versione del cluster; è possibile aggiornarlo ogni volta che si aggiorna il cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="ba6a1-119">Tuttavia, è necessario mantenere il valore predefinito per **apiVersion**.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="ba6a1-120">Nodi del cluster</span><span class="sxs-lookup"><span data-stu-id="ba6a1-120">Nodes on the cluster</span></span>
<span data-ttu-id="ba6a1-121">È possibile configurare i nodi nel cluster di Service Fabric tramite la sezione **nodes** , come illustrato nel frammento seguente.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

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

<span data-ttu-id="ba6a1-122">Un cluster Service Fabric deve contenere almeno 3 nodi.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="ba6a1-123">È possibile aggiungere più nodi a questa sezione in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="ba6a1-124">La tabella seguente illustra le impostazioni di configurazione per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="ba6a1-125">**Configurazione nodo**</span><span class="sxs-lookup"><span data-stu-id="ba6a1-125">**Node configuration**</span></span> | <span data-ttu-id="ba6a1-126">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ba6a1-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ba6a1-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="ba6a1-127">nodeName</span></span> |<span data-ttu-id="ba6a1-128">È possibile assegnare qualsiasi nome descrittivo al nodo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="ba6a1-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="ba6a1-129">iPAddress</span></span> |<span data-ttu-id="ba6a1-130">Trovare l'indirizzo IP del nodo aprendo una finestra di comando e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="ba6a1-131">Prendere nota dell'indirizzo IPV4 e assegnarlo alla variabile **iPAddress** .</span><span class="sxs-lookup"><span data-stu-id="ba6a1-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="ba6a1-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="ba6a1-132">nodeTypeRef</span></span> |<span data-ttu-id="ba6a1-133">È possibile assegnare un tipo diverso a ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="ba6a1-134">I [tipi di nodo](#nodetypes) sono definiti nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="ba6a1-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="ba6a1-135">faultDomain</span></span> |<span data-ttu-id="ba6a1-136">I domini di errore consentono agli amministratori del cluster di definire i nodi fisici su cui è probabile che si verifichino contemporaneamente degli errori a causa di dipendenze fisiche condivise.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="ba6a1-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="ba6a1-137">upgradeDomain</span></span> |<span data-ttu-id="ba6a1-138">I domini di aggiornamento descrivono set di nodi che vengono arrestati per gli aggiornamenti di Service Fabric quasi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="ba6a1-139">È possibile scegliere i nodi da assegnare a determinati domini di aggiornamento perché non sono limitati da eventuali requisiti fisici.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="ba6a1-140">Proprietà del cluster</span><span class="sxs-lookup"><span data-stu-id="ba6a1-140">Cluster properties</span></span>
<span data-ttu-id="ba6a1-141">La sezione **properties** in ClusterConfig.JSON viene usata per configurare il cluster come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="ba6a1-142">Affidabilità</span><span class="sxs-lookup"><span data-stu-id="ba6a1-142">Reliability</span></span>
<span data-ttu-id="ba6a1-143">Il concetto di **reliabilityLevel** definisce il numero di repliche o istanze dei servizi di sistema di Service Fabric eseguibili nei nodi primari del cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="ba6a1-144">Determina l'affidabilità di questi servizi e quindi del cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="ba6a1-145">Il valore viene calcolato dal sistema in fase di creazione e di aggiornamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="ba6a1-146">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="ba6a1-146">Diagnostics</span></span>
<span data-ttu-id="ba6a1-147">La sezione **diagnosticsStore** consente di configurare i parametri per consentire la diagnostica e la risoluzione degli errori di nodi o cluster, come illustrato nel frammento riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="ba6a1-148">**metadata** descrive la diagnostica del cluster e può essere impostata in base alla configurazione in uso.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="ba6a1-149">Queste variabili consentono di raccogliere log di traccia ETW, dump di arresto anomalo e contatori delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="ba6a1-150">Per altre informazioni sui log di traccia ETW, leggere gli articoli [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) e [Traccia ETW](https://msdn.microsoft.com/library/ms751538.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="ba6a1-151">Tutti i log che includono [dump di arresto anomalo del sistema](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) e [contatori delle prestazioni](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) possono essere indirizzati alla cartella **connectionString** nel computer.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="ba6a1-152">È anche possibile usare *AzureStorage* per l'archiviazione della diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="ba6a1-153">Per un frammento di esempio, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="ba6a1-154">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="ba6a1-154">Security</span></span>
<span data-ttu-id="ba6a1-155">La sezione **security** è necessaria per la protezione di un cluster di Service Fabric autonomo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="ba6a1-156">Il frammento seguente mostra una parte di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="ba6a1-157">**metadata** descrive il cluster protetto e può essere impostata in base alla configurazione in uso.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="ba6a1-158">**ClusterCredentialType** e **ServerCredentialType** determinano il tipo di protezione che verrà implementata dal cluster e dai nodi.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="ba6a1-159">È possibile impostarle su *X509* per una protezione basata su certificato o su *Windows* per una protezione basata su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="ba6a1-160">Il resto della sezione **security** sarà basato sul tipo di protezione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="ba6a1-161">Leggere l'articolo [Proteggere il cluster Windows autonomo con i certificati](service-fabric-windows-cluster-x509-security.md) o [Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows](service-fabric-windows-cluster-windows-security.md) per informazioni su come compilare il resto della sezione **security**.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="ba6a1-162">Tipi di nodi</span><span class="sxs-lookup"><span data-stu-id="ba6a1-162">Node Types</span></span>
<span data-ttu-id="ba6a1-163">La sezione **nodeTypes** descrive il tipo dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="ba6a1-164">Per ogni cluster deve essere specificato almeno un tipo di nodo, come illustrato nel frammento riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

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

<span data-ttu-id="ba6a1-165">**name** è il nome descrittivo per questo tipo di nodo particolare.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="ba6a1-166">Per creare un nodo di questo tipo, assegnare il nome descrittivo alla variabile **nodeTypeRef** per tale nodo, come indicato [sopra](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="ba6a1-167">Per ogni tipo di nodo, definire gli endpoint di connessione che verranno usati.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="ba6a1-168">È possibile scegliere qualsiasi numero di porta per gli endpoint di connessione, purché non entrino in conflitto con altri endpoint in questo cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="ba6a1-169">In un cluster multinodo saranno presenti uno o più nodi primari (ad esempio **isPrimary** impostato su *true*), in base a [**reliabilityLevel**](#reliability).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="ba6a1-170">Per informazioni su **nodeTypes** e **reliabilityLevel** e per sapere quali sono i tipi di nodo primari e non primari, vedere [Considerazioni sulla pianificazione della capacità del cluster Service Fabric](service-fabric-cluster-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="ba6a1-171">Endpoint usati per configurare i tipi di nodi</span><span class="sxs-lookup"><span data-stu-id="ba6a1-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="ba6a1-172">*clientConnectionEndpointPort* è la porta usata dal client per connettersi al cluster quando si usano le API del client.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="ba6a1-173">*clusterConnectionEndpointPort* è la porta in cui i nodi di comunicano tra loro.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="ba6a1-174">*leaseDriverEndpointPort* è la porta usata dal driver di lease del cluster per scoprire se i nodi sono ancora attivi.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="ba6a1-175">*serviceConnectionEndpointPort* è la porta usata da applicazioni e servizi distribuiti in un nodo, per comunicare con il client di Service Fabric in quel determinato nodo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="ba6a1-176">*httpGatewayEndpointPort* è la porta usata da Service Fabric Explorer per connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="ba6a1-177">Le porte *ephemeralPorts* eseguono l'override delle [porte dinamiche usate dal sistema operativo](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="ba6a1-178">Service Fabric userà una parte di queste porte dell'applicazione, mentre le rimanenti saranno a disposizione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="ba6a1-179">Inoltre eseguirà il mapping di questo intervallo nell'intervallo presente nel sistema operativo, quindi per tutti gli scopi è possibile usare gli intervalli forniti nei file JSON campione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="ba6a1-180">È necessario assicurarsi che la differenza tra la porta iniziale e la porta finale sia almeno 255.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="ba6a1-181">Questo intervallo è condiviso con il sistema operativo e possono quindi verificarsi dei conflitti se la differenza è troppo bassa.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="ba6a1-182">Per visualizzare l'intervallo di porte dinamiche configurato, eseguire il comando `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="ba6a1-183">*applicationPorts* sono le porte che verranno usate dalle applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="ba6a1-184">L'intervallo di porte dell'applicazione deve essere abbastanza grande da soddisfare il requisito di endpoint delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="ba6a1-185">Questo intervallo deve essere esclusivo dall'intervallo di porte dinamico del computer, ad esempio l'intervallo *ephemeralPorts* impostato nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="ba6a1-186">Service Fabric le userà tutte le volte che servono nuove porte, inoltre si occuperà di aprire i relativi firewall.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="ba6a1-187">*reverseProxyEndpointPort* è un endpoint proxy inverso facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="ba6a1-188">Per altri dettagli vedere [Proxy inverso di Service Fabric](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="ba6a1-189">Impostazioni log</span><span class="sxs-lookup"><span data-stu-id="ba6a1-189">Log Settings</span></span>
<span data-ttu-id="ba6a1-190">La sezione **fabricSettings** consente di impostare le directory radice per i log e i dati di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="ba6a1-191">È possibile personalizzarle solo durante la creazione del cluster iniziale.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="ba6a1-192">Per un frammento di esempio di questa sezione, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="ba6a1-193">Si consiglia di usare un'unità non del sistema operativo come FabricDataRoot e FabricLogRoot, poiché risulta più affidabile in caso di arresto anomalo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="ba6a1-194">Si noti che se si personalizza solo la radice dei dati, la radice del log verrà inserita un livello sotto la radice dei dati.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="ba6a1-195">Impostazioni di Reliable Services con stato</span><span class="sxs-lookup"><span data-stu-id="ba6a1-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="ba6a1-196">La sezione **KtlLogger** consente di impostare le impostazioni di configurazione globali per Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="ba6a1-197">Per altre informazioni su queste impostazioni leggere [Configurazione dei servizi Reliable Services con stato](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="ba6a1-198">L'esempio seguente illustra come modificare il log delle transazioni condiviso creato per eseguire il backup di eventuali raccolte affidabili per i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="ba6a1-199">Funzionalità aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ba6a1-199">Add-on features</span></span>
<span data-ttu-id="ba6a1-200">Per configurare le funzioni aggiuntive l'impostazione di apiVersion deve essere '04-2017' o versione successiva ed è necessario configurare addonFeatures:</span><span class="sxs-lookup"><span data-stu-id="ba6a1-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="ba6a1-201">Supporto dei contenitori</span><span class="sxs-lookup"><span data-stu-id="ba6a1-201">Container support</span></span>
<span data-ttu-id="ba6a1-202">Per abilitare il supporto dei contenitori sia per il contenitore di Windows Server che per il contenitore di Hyper-V per i cluster autonomi, deve essere attivata la funzionalità aggiuntiva 'DnsService'.</span><span class="sxs-lookup"><span data-stu-id="ba6a1-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ba6a1-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba6a1-203">Next steps</span></span>
<span data-ttu-id="ba6a1-204">Dopo aver completato la configurazione di un file ClusterConfig.JSON in base alla configurazione del cluster autonomo, è possibile distribuire il cluster seguendo l'articolo [Creare un cluster di Service Fabric autonomo](service-fabric-cluster-creation-for-windows-server.md) e quindi proseguire per la [Visualizzazione del cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ba6a1-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

