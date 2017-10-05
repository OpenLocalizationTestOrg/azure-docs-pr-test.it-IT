---
title: Configurare un cluster autonomo di Azure Service Fabric | Microsoft Docs
description: "Creare un cluster di sviluppo autonomo con tre nodi in esecuzione nello stesso computer. Al termine della configurazione sarà possibile creare un cluster costituito da più macchine virtuali."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="bdbd8-104">Creare il primo cluster autonomo di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bdbd8-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="bdbd8-105">È possibile creare un cluster autonomo di Service Fabric su qualsiasi macchina virtuale o computer che esegua Windows Server 2012 R2 o Windows Server 2016, locale o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="bdbd8-106">Questa guida introduttiva consente di creare un cluster di sviluppo autonomo in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="bdbd8-107">Al termine si ottiene un cluster di tre nodi in esecuzione in un singolo computer nel quale è possibile distribuire app.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bdbd8-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="bdbd8-108">Before you begin</span></span>
<span data-ttu-id="bdbd8-109">Service Fabric offre un pacchetto di installazione per la creazione di cluster di Service Fabric autonomi.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="bdbd8-110">[Scaricare il pacchetto di installazione](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="bdbd8-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="bdbd8-111">Decomprimere il pacchetto di installazione in una cartella nel computer o nella macchina virtuale in cui si configura il cluster di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="bdbd8-112">Il contenuto del pacchetto di installazione è descritto nei dettagli [qui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="bdbd8-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="bdbd8-113">L'amministratore del cluster che distribuisce e configura il cluster deve avere privilegi di amministratore nel computer.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="bdbd8-114">Non è possibile installare Service Fabric in un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="bdbd8-115">Convalidare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="bdbd8-115">Validate the environment</span></span>
<span data-ttu-id="bdbd8-116">Lo script *TestConfiguration.ps1* nel pacchetto autonomo viene usato come Best Practices Analyzer per verificare se un cluster possa essere distribuito in un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="bdbd8-117">La [preparazione della distribuzione](service-fabric-cluster-standalone-deployment-preparation.md) elenca i prerequisiti e i requisiti dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="bdbd8-118">Eseguire lo script per verificare se è possibile creare il cluster di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="bdbd8-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="bdbd8-119">Creare il cluster</span><span class="sxs-lookup"><span data-stu-id="bdbd8-119">Create the cluster</span></span>
<span data-ttu-id="bdbd8-120">Con il pacchetto di installazione vengono installati diversi file di esempio per la configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="bdbd8-121">*ClusterConfig.Unsecure.DevCluster.json* è la configurazione del cluster più semplice: un cluster non sicuro, con tre nodi in esecuzione in un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="bdbd8-122">Altri file di configurazione descrivono cluster con una o più macchine virtuali protetti con la sicurezza di Windows o certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="bdbd8-123">Non è necessario modificare le impostazioni di configurazione predefinite per questa esercitazione, ma è consigliabile esaminare il file di configurazione per acquisire familiarità con le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="bdbd8-124">La sezione **nodes** descrive i tre nodi nel cluster, indicando nome, indirizzo IP, [tipo di nodo, dominio di errore e dominio di aggiornamento](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="bdbd8-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="bdbd8-125">La sezione **properties** definisce le impostazioni per [sicurezza, livello di affidabilità, raccolta di dati di diagnostica e tipi di nodi ](service-fabric-cluster-manifest.md#cluster-properties) del cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="bdbd8-126">Questo cluster è senza protezione.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-126">This cluster is unsecure.</span></span>  <span data-ttu-id="bdbd8-127">Chiunque si può connettere in modo anonimo ed eseguire operazioni di gestione. È quindi necessario proteggere sempre i cluster di produzione usando certificati X.509 o la sicurezza di Windows.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="bdbd8-128">La sicurezza viene configurata solo in fase di creazione del cluster e non è possibile abilitare la sicurezza dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="bdbd8-129">Vedere [Proteggere un cluster](service-fabric-cluster-security.md) per altre informazioni sulla sicurezza dei cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="bdbd8-130">Per creare il cluster di sviluppo con tre nodi, eseguire lo script *CreateServiceFabricCluster.ps1* da una sessione amministratore di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bdbd8-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="bdbd8-131">Il pacchetto di runtime di Service Fabric viene scaricato e installato automaticamente al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="bdbd8-132">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="bdbd8-132">Connect to the cluster</span></span>
<span data-ttu-id="bdbd8-133">Il cluster di sviluppo di tre nodi è ora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="bdbd8-134">Il modulo ServiceFabric di PowerShell viene installato con il runtime.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="bdbd8-135">È possibile verificare che il cluster sia in esecuzione dallo stesso computer o da un computer remoto con il runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="bdbd8-136">Il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) stabilisce una connessione al cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="bdbd8-137">Per altri esempi di connessione a un cluster, vedere [Connettersi a un cluster sicuro](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bdbd8-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="bdbd8-138">Dopo la connessione al cluster, usare il cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) per visualizzare un elenco dei nodi presenti nel cluster e informazioni di stato per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="bdbd8-139">**HealthState** deve essere *OK* per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="bdbd8-140">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="bdbd8-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="bdbd8-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) rappresenta un ottimo strumento per la visualizzazione del cluster e la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="bdbd8-142">Service Fabric Explorer è un servizio in esecuzione nel cluster, cui si accede tramite un browser passando a [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="bdbd8-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="bdbd8-143">Il dashboard del cluster offre una panoramica del cluster, incluso un riepilogo dell'integrità delle applicazioni e dei nodi.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="bdbd8-144">La visualizzazione dei nodi mostra il layout fisico del cluster.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="bdbd8-145">Per un determinato nodo, è possibile esaminare le applicazioni con il codice distribuito in quel nodo.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="bdbd8-147">Rimuovere il cluster</span><span class="sxs-lookup"><span data-stu-id="bdbd8-147">Remove the cluster</span></span>
<span data-ttu-id="bdbd8-148">Per rimuovere un cluster, eseguire lo script *RemoveServiceFabricCluster.ps1* di Powershell dalla cartella del pacchetto e passare il percorso del file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="bdbd8-149">Se necessario, è anche possibile specificare un percorso per il log del processo di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="bdbd8-150">Per rimuovere il runtime di Service Fabric dal computer, eseguire lo script di PowerShell seguente dalla cartella del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="bdbd8-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bdbd8-151">Next steps</span></span>
<span data-ttu-id="bdbd8-152">Ora che è stato configurato un cluster di sviluppo autonomo, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdbd8-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="bdbd8-153">[Configurare un cluster autonomo con più computer](service-fabric-cluster-creation-for-windows-server.md) e abilitare la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bdbd8-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="bdbd8-154">Distribuire le app tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdbd8-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
