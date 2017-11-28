---
title: Creare un cluster autonomo di Azure Service Fabric | Documentazione Microsoft
description: Creare un cluster di Azure Service Fabric su qualsiasi macchina (fisica o virtuale) che esegue Windows Server, sia locale che nel cloud.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="3c880-103">Creare un cluster autonomo in esecuzione su Windows Server</span><span class="sxs-lookup"><span data-stu-id="3c880-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="3c880-104">Azure Service Fabric consente di creare cluster Service Fabric su qualsiasi macchina virtuale o computer che esegue Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3c880-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="3c880-105">In questo modo è possibile distribuire ed eseguire applicazioni di Service Fabric in qualsiasi ambiente che contenga un set di computer Windows Server interconnessi, in locale o con qualsiasi provider di cloud.</span><span class="sxs-lookup"><span data-stu-id="3c880-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="3c880-106">Service Fabric offre un pacchetto di installazione per la creazione di cluster di Service Fabric, denominato pacchetto autonomo per Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3c880-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="3c880-107">Questo articolo illustra la procedura di creazione di un cluster autonomo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3c880-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3c880-108">Questo pacchetto autonomo di Windows Server è disponibile in commercio e può essere usato per distribuzioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="3c880-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="3c880-109">Il pacchetto può contenere nuove funzionalità di Service Fabric in "Anteprima".</span><span class="sxs-lookup"><span data-stu-id="3c880-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="3c880-110">Scorrere verso il basso fino alla sezione "[Funzionalità di anteprima incluse in questo pacchetto](#previewfeatures_anchor)".</span><span class="sxs-lookup"><span data-stu-id="3c880-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="3c880-111">per visualizzare l'elenco delle funzionalità in anteprima.</span><span class="sxs-lookup"><span data-stu-id="3c880-111">section for the list of the preview features.</span></span> <span data-ttu-id="3c880-112">È possibile [scaricare una copia del contratto di licenza](http://go.microsoft.com/fwlink/?LinkID=733084) ora.</span><span class="sxs-lookup"><span data-stu-id="3c880-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="3c880-113">Ottenere supporto per il pacchetto Service Fabric per Windows Server</span><span class="sxs-lookup"><span data-stu-id="3c880-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="3c880-114">Porre domande alla community sul pacchetto autonomo Service Fabric per Windows Server nel [forum di Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="3c880-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="3c880-115">Aprire un ticket per ottenere il [supporto professionale per Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="3c880-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="3c880-116">Altre informazioni sul supporto professionale Microsoft sono disponibili [qui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="3c880-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="3c880-117">È possibile anche ottenere supporto per questo pacchetto come parte del [Supporto tecnico Microsoft Premier](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="3c880-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="3c880-118">Per altre informazioni vedere [Opzioni di supporto di Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="3c880-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="3c880-119">Per raccogliere log a scopo di supporto, eseguire l'[agente di raccolta log autonomo di Service Fabric](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="3c880-120">Scaricare il pacchetto Service Fabric per Windows Server</span><span class="sxs-lookup"><span data-stu-id="3c880-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="3c880-121">Per creare il cluster usare il pacchetto Service Fabric per Windows Server (Windows Server 2012 R2 e versioni successive) disponibile qui:</span><span class="sxs-lookup"><span data-stu-id="3c880-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="3c880-122">
[Collegamento per il download - Pacchetto autonomo di Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="3c880-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="3c880-123">Informazioni dettagliate sul contenuto del pacchetto sono disponibili [qui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="3c880-124">Il pacchetto di runtime di Service Fabric viene scaricato automaticamente al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="3c880-125">Se si esegue la distribuzione da un computer non connesso a Internet, scaricare il pacchetto di runtime fuori banda da qui:</span><span class="sxs-lookup"><span data-stu-id="3c880-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="3c880-126">
[Collegamento per il download - Runtime di Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="3c880-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="3c880-127">Trovare esempi di configurazione di cluster autonomi in:</span><span class="sxs-lookup"><span data-stu-id="3c880-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="3c880-128">
[Esempi di configurazione di cluster autonomi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="3c880-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="3c880-129">Creare il cluster</span><span class="sxs-lookup"><span data-stu-id="3c880-129">Create the cluster</span></span>
<span data-ttu-id="3c880-130">Service Fabric può essere distribuito in un cluster di sviluppo macchine usando il file *ClusterConfig.Unsecure.DevCluster.json* file incluso negli [esempi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="3c880-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="3c880-131">Decomprimere il pacchetto autonomo nella macchina, copiare il file di configurazione di esempio nella macchina locale, quindi eseguire lo script *CreateServiceFabricCluster.ps1* tramite una sessione di PowerShell come amministratore, dalla cartella del pacchetto autonomo:</span><span class="sxs-lookup"><span data-stu-id="3c880-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="3c880-132">Passaggio 1A: creare un cluster di sviluppo locale non protetto</span><span class="sxs-lookup"><span data-stu-id="3c880-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="3c880-133">Per informazioni dettagliate sulla risoluzione dei problemi, vedere la sezione Configurazione dell'ambiente in [Pianificare e preparare la distribuzione del cluster](service-fabric-cluster-standalone-deployment-preparation.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="3c880-134">Al termine dell'esecuzione degli scenari di sviluppo è possibile rimuovere il cluster Service Fabric dalla macchina facendo riferimento alla procedura della sezione "[Rimuovere un cluster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="3c880-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="3c880-135">Passaggio 1B: creare un cluster con più macchine</span><span class="sxs-lookup"><span data-stu-id="3c880-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="3c880-136">Dopo avere eseguito i passaggi di pianificazione e preparazione illustrati nel collegamento seguente, si è pronti per creare il cluster di produzione usando il file di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="3c880-137">
[Pianificare e preparare la distribuzione del cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="3c880-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="3c880-138">Convalidare il file di configurazione scritto eseguendo lo script *TestConfiguration.ps1* nella cartella del pacchetto autonomo:</span><span class="sxs-lookup"><span data-stu-id="3c880-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="3c880-139">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3c880-139">You should see output like below.</span></span> <span data-ttu-id="3c880-140">Se nel campo in basso "Passed" viene restituito un valore "True", sono stati superati i controlli di integrità ed è possibile distribuire il cluster in base alla configurazione di input.</span><span class="sxs-lookup"><span data-stu-id="3c880-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="3c880-141">Creare il cluster: eseguire lo script *CreateServiceFabricCluster.ps1* per la distribuzione del cluster Service Fabric in ogni computer nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="3c880-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="3c880-142">Le tracce di distribuzione vengono scritte nella VM o nel computer in cui è stato eseguito lo script PowerShell CreateServiceFabricCluster.ps1.</span><span class="sxs-lookup"><span data-stu-id="3c880-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="3c880-143">Sono disponibili nella sottocartella DeploymentTraces all'interno della directory da cui è stato eseguito lo script.</span><span class="sxs-lookup"><span data-stu-id="3c880-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="3c880-144">Per verificare se Service Fabric è stato distribuito correttamente in un computer, individuare i file installati nella directory FabricDataRoot, come descritto in dettaglio nella sezione FabricSetting del file di configurazione del cluster. Per impostazione predefinita la directory è c:\ProgramData\SF.</span><span class="sxs-lookup"><span data-stu-id="3c880-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="3c880-145">I processi FabricHost.exe e Fabric.exe possono essere visualizzati in esecuzione in Gestione attività.</span><span class="sxs-lookup"><span data-stu-id="3c880-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="3c880-146">Passaggio 1C: Creare un cluster offline (non connesso a Internet)</span><span class="sxs-lookup"><span data-stu-id="3c880-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="3c880-147">Il pacchetto di runtime di Service Fabric viene scaricato automaticamente al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="3c880-148">Quando si distribuisce un cluster a computer non connessi a Internet è necessario scaricare il pacchetto di runtime di Service Fabric separatamente e specificare il percorso del pacchetto al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="3c880-149">Il pacchetto di runtime può essere scaricato separatamente da un altro computer connesso a Internet in [Collegamento per il download - Service Fabric Runtime (Runtime di Service Fabric) - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="3c880-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="3c880-150">Copiare il pacchetto di runtime nella posizione da cui si intende distribuire il cluster offline eseguendo `CreateServiceFabricCluster.ps1` con il parametro `-FabricRuntimePackagePath` incluso, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3c880-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="3c880-151">dove `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` sono rispettivamente i percorsi per la configurazione del cluster e per il file di runtime con estensione cab.</span><span class="sxs-lookup"><span data-stu-id="3c880-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="3c880-152">Passaggio 2: connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="3c880-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="3c880-153">Per connettersi a un cluster protetto, vedere la sezione relativa alla [connessione di Service Fabric a un cluster protetto](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="3c880-154">Per connettersi a un cluster non protetto, eseguire il seguente comando di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c880-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="3c880-155">Esempio:</span><span class="sxs-lookup"><span data-stu-id="3c880-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="3c880-156">Passaggio 3: Visualizzare Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3c880-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="3c880-157">È ora possibile connettersi al cluster con Service Fabric Explorer direttamente da uno dei computer con http://localhost:19080/Explorer/index.html o in modalità remota con http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="3c880-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="3c880-158">Aggiungere e rimuovere ruoli</span><span class="sxs-lookup"><span data-stu-id="3c880-158">Add and remove nodes</span></span>
<span data-ttu-id="3c880-159">È possibile aggiungere o rimuovere nodi nel cluster di Service Fabric autonomo al variare delle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="3c880-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="3c880-160">Per i passaggi dettagliati, leggere le informazioni su [aggiunta e rimozione di nodi in un cluster Service Fabric autonomo](service-fabric-cluster-windows-server-add-remove-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="3c880-161">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="3c880-161">Remove a cluster</span></span>
<span data-ttu-id="3c880-162">Per rimuovere un cluster, eseguire lo script *RemoveServiceFabricCluster.ps1* di Powershell dalla cartella del pacchetto e passare il percorso del file di configurazione JSON.</span><span class="sxs-lookup"><span data-stu-id="3c880-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="3c880-163">Se necessario, è anche possibile specificare un percorso per il log del processo di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="3c880-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="3c880-164">Questo script può essere eseguito su qualsiasi macchina con accesso amministrativo a tutte le macchine elencate come nodi nel file di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="3c880-165">La macchina in cui viene eseguito lo script non deve necessariamente far parte del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="3c880-166">Dati di telemetria raccolti e come rifiutarli esplicitamente</span><span class="sxs-lookup"><span data-stu-id="3c880-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="3c880-167">Per impostazione predefinita, il prodotto raccoglie i dati di telemetria sull'utilizzo di Service Fabric per migliorarlo.</span><span class="sxs-lookup"><span data-stu-id="3c880-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="3c880-168">Best Practice Analyzer, che viene eseguito durante la configurazione, controlla la connettività a [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="3c880-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="3c880-169">Se non è raggiungibile, la configurazione non riesce, a meno che non si rifiutino esplicitamente i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="3c880-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="3c880-170">La pipeline di telemetria cerca di caricare i dati seguenti in [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="3c880-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="3c880-171">Si tratta di un tentativo di caricamento che non influisce sulla funzionalità del cluster.</span><span class="sxs-lookup"><span data-stu-id="3c880-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="3c880-172">I dati di telemetria vengono inviati solo dal nodo che esegue la gestione failover primaria.</span><span class="sxs-lookup"><span data-stu-id="3c880-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="3c880-173">Nessun altro nodo invia dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="3c880-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="3c880-174">La telemetria è costituita dagli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c880-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="3c880-175">Numero di servizi</span><span class="sxs-lookup"><span data-stu-id="3c880-175">Number of services</span></span>
* <span data-ttu-id="3c880-176">Numero di elementi ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="3c880-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="3c880-177">Numero di elementi Applications</span><span class="sxs-lookup"><span data-stu-id="3c880-177">Number of Applications</span></span>
* <span data-ttu-id="3c880-178">Numero di elementi ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="3c880-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="3c880-179">Numero di elementi FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="3c880-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="3c880-180">Numero di elementi InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="3c880-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="3c880-181">Numero di elementi UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="3c880-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="3c880-182">Numero di elementi Replicas</span><span class="sxs-lookup"><span data-stu-id="3c880-182">Number of Replicas</span></span>
* <span data-ttu-id="3c880-183">Numero di elementi InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="3c880-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="3c880-184">Numero di elementi StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="3c880-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="3c880-185">Numero di elementi OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="3c880-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="3c880-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="3c880-186">CommonQueueLength</span></span>
* <span data-ttu-id="3c880-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="3c880-187">QueryQueueLength</span></span>
* <span data-ttu-id="3c880-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="3c880-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="3c880-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="3c880-189">CommitQueueLength</span></span>
* <span data-ttu-id="3c880-190">Numero di elementi Nodes</span><span class="sxs-lookup"><span data-stu-id="3c880-190">Number of Nodes</span></span>
* <span data-ttu-id="3c880-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="3c880-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="3c880-192">ClusterId: GUID generato casualmente per ogni cluster</span><span class="sxs-lookup"><span data-stu-id="3c880-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="3c880-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="3c880-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="3c880-194">Indirizzo IP della macchina virtuale o del computer da cui vengono caricati i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="3c880-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="3c880-195">Per disabilitare la telemetria, aggiungere quanto segue all'elemento *properties* nel file di configurazione del cluster *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="3c880-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="3c880-196">Funzionalità di anteprima incluse in questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="3c880-196">Preview features included in this package</span></span>
<span data-ttu-id="3c880-197">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="3c880-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="3c880-198">A partire dalla nuova [versione GA del cluster autonomo per Windows Server (versione 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/) è possibile aggiornare il cluster per le versioni future, manualmente o automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3c880-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="3c880-199">Per informazioni dettagliate, vedere [Aggiornare il cluster autonomo di Service Fabric in Windows Server](service-fabric-cluster-upgrade-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="3c880-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3c880-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c880-200">Next steps</span></span>
* [<span data-ttu-id="3c880-201">Distribuire e rimuovere applicazioni con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c880-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="3c880-202">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="3c880-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="3c880-203">Aggiungere o rimuovere nodi in un cluster di Service Fabric autonomo</span><span class="sxs-lookup"><span data-stu-id="3c880-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="3c880-204">Aggiornare il cluster autonomo di Service Fabric in Windows Server</span><span class="sxs-lookup"><span data-stu-id="3c880-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="3c880-205">Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="3c880-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="3c880-206">Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows</span><span class="sxs-lookup"><span data-stu-id="3c880-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="3c880-207">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="3c880-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
