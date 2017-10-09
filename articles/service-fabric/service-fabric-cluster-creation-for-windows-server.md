---
title: un cluster di Azure Service Fabric autonomo aaaCreate | Documenti Microsoft
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
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="6f5b5-103">Creare un cluster autonomo in esecuzione su Windows Server</span><span class="sxs-lookup"><span data-stu-id="6f5b5-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="6f5b5-104">È possibile utilizzare cluster di Service Fabric toocreate Azure Service Fabric in macchine virtuali o computer che eseguono Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="6f5b5-105">In questo modo è possibile distribuire ed eseguire applicazioni di Service Fabric in qualsiasi ambiente che contenga un set di computer Windows Server interconnessi, in locale o con qualsiasi provider di cloud.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="6f5b5-106">Service Fabric fornisce un toocreate pacchetto di installazione che cluster di Service Fabric chiamato pacchetto di Windows Server autonomo hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="6f5b5-107">In questo articolo vengono illustrati i passaggi hello per la creazione di un cluster di Service Fabric autonomo.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5b5-108">Questo pacchetto autonomo di Windows Server è disponibile in commercio e può essere usato per distribuzioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="6f5b5-109">Il pacchetto può contenere nuove funzionalità di Service Fabric in "Anteprima".</span><span class="sxs-lookup"><span data-stu-id="6f5b5-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="6f5b5-110">Scorrere verso il basso troppo"[funzionalità incluse in questo pacchetto di anteprima](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="6f5b5-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="6f5b5-111">sezione elenco hello delle funzionalità di anteprima hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="6f5b5-112">È possibile [scaricare una copia del contratto di licenza hello](http://go.microsoft.com/fwlink/?LinkID=733084) ora.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="6f5b5-113">Ottenere supporto per il pacchetto di Service Fabric per Windows Server hello</span><span class="sxs-lookup"><span data-stu-id="6f5b5-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="6f5b5-114">Chiedi community hello pacchetto autonomo di hello Service Fabric per Windows Server in hello [forum di Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="6f5b5-115">Aprire un ticket per ottenere il [supporto professionale per Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="6f5b5-116">Altre informazioni sul supporto professionale Microsoft sono disponibili [qui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="6f5b5-117">È possibile anche ottenere supporto per questo pacchetto come parte del [Supporto tecnico Microsoft Premier](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="6f5b5-118">Per altre informazioni vedere [Opzioni di supporto di Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="6f5b5-119">i registri toocollect per scopi di supporto, Esegui hello [servizio Fabric autonomo Log collector](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="6f5b5-120">Scaricare il pacchetto di Service Fabric per Windows Server hello</span><span class="sxs-lookup"><span data-stu-id="6f5b5-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="6f5b5-121">cluster hello toocreate, utilizzare un pacchetto di Service Fabric per Windows Server hello (Windows Server 2012 R2 e versioni successive) disponibili qui:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="6f5b5-122">
[Collegamento per il download - Pacchetto autonomo di Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="6f5b5-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="6f5b5-123">Trovare i dettagli sul contenuto del pacchetto di hello [qui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="6f5b5-124">pacchetto di runtime di Service Fabric Hello viene scaricato automaticamente al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="6f5b5-125">Se la distribuzione da un computer non connessi toohello internet, scaricare il pacchetto di runtime hello fuori banda da qui:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="6f5b5-126">
[Collegamento per il download - Runtime di Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="6f5b5-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="6f5b5-127">Trovare esempi di configurazione di cluster autonomi in:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="6f5b5-128">
[Esempi di configurazione di cluster autonomi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="6f5b5-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="6f5b5-129">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="6f5b5-129">Create hello cluster</span></span>
<span data-ttu-id="6f5b5-130">Service Fabric può essere il cluster di sviluppo di una macchina tooa distribuito tramite hello *ClusterConfig.Unsecure.DevCluster.json* i file inclusi in [esempi](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="6f5b5-131">Decomprimere macchina tooyour pacchetto di hello autonoma, copia hello esempio config file toohello locale, quindi esecuzione hello *CreateServiceFabricCluster.ps1* uno script tramite una sessione di PowerShell amministratore dal hello autonomo cartella del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="6f5b5-132">Passaggio 1A: creare un cluster di sviluppo locale non protetto</span><span class="sxs-lookup"><span data-stu-id="6f5b5-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="6f5b5-133">Vedere hello sezione di configurazione dell'ambiente alla [pianificare e preparare la distribuzione di cluster](service-fabric-cluster-standalone-deployment-preparation.md) dettagli della risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="6f5b5-134">Se si sono terminato in esecuzione gli scenari di sviluppo, è possibile rimuovere il cluster di Service Fabric hello dalla macchina di hello riferendosi toosteps nella sezione "[rimuovere un cluster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="6f5b5-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="6f5b5-135">Passaggio 1B: creare un cluster con più macchine</span><span class="sxs-lookup"><span data-stu-id="6f5b5-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="6f5b5-136">Dopo che sono già state completate tramite pianificazione hello e passaggi di preparazione dettagliate in hello di sotto di collegamento, si è pronti a toocreate il cluster di produzione usando il file di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="6f5b5-137">
[Pianificare e preparare la distribuzione del cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="6f5b5-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="6f5b5-138">Convalidare il file di configurazione hello è stato scritto eseguendo hello *TestConfiguration.ps1* script dalla cartella del pacchetto autonomo hello:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="6f5b5-139">Verrà visualizzato un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-139">You should see output like below.</span></span> <span data-ttu-id="6f5b5-140">Se il campo inferiore hello "Superato" viene restituito come "True", i controlli di integrità sono stati superati e cluster hello Cerca toobe distribuibile in base alla configurazione di input hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="6f5b5-141">Creare il cluster hello: eseguire hello *CreateServiceFabricCluster.ps1* cluster di Service Fabric hello toodeploy script in ogni computer nella configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="6f5b5-142">Tracce di distribuzione vengono scritte toohello macchine Virtuali/computer in cui è stato eseguito uno script di PowerShell CreateServiceFabricCluster.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="6f5b5-143">Questi sono disponibili nella sottocartella hello DeploymentTraces, basato su nella directory hello da quale hello è stato eseguito uno script.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="6f5b5-144">toosee se Service Fabric è stato distribuito correttamente tooa computer, trovare i file hello installato nella directory FabricDataRoot hello, come descritto in dettaglio nel file di configurazione del cluster hello sezione FabricSettings (per impostazione predefinita c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="6f5b5-145">I processi FabricHost.exe e Fabric.exe possono essere visualizzati in esecuzione in Gestione attività.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="6f5b5-146">Passaggio 1C: Creare un cluster offline (non connesso a Internet)</span><span class="sxs-lookup"><span data-stu-id="6f5b5-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="6f5b5-147">pacchetto di runtime di Service Fabric Hello viene scaricato automaticamente al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="6f5b5-148">Quando la distribuzione di un cluster di toomachines non connessi toohello internet, è necessario hello toodownload Service Fabric runtime pacchetto separatamente e fornire hello percorso tooit al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="6f5b5-149">possono essere scaricati separatamente mediante Hello runtime package, da un altro computer connesso toohello internet, in [collegamento Download - Runtime dell'infrastruttura del servizio - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="6f5b5-150">Copiare hello runtime pacchetto toowhere la distribuzione di cluster non in linea di hello da e creare il cluster hello eseguendo `CreateServiceFabricCluster.ps1` con hello `-FabricRuntimePackagePath` parametro incluso, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="6f5b5-151">dove `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` sono rispettivamente di configurazione del cluster toohello percorsi hello e file CAB di runtime hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="6f5b5-152">Passaggio 2: Connettere il cluster di toohello</span><span class="sxs-lookup"><span data-stu-id="6f5b5-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="6f5b5-153">cluster sicuro tooa tooconnect, vedere [Service fabric connettersi cluster toosecure](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="6f5b5-154">tooconnect tooan non sicuri cluster, eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="6f5b5-155">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="6f5b5-156">Passaggio 3: Visualizzare Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="6f5b5-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="6f5b5-157">Ora è possibile collegare toohello cluster con Service Fabric Explorer direttamente da uno dei computer hello http://localhost:19080/Explorer/index.html o in modalità remota con http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="6f5b5-158">Aggiungere e rimuovere ruoli</span><span class="sxs-lookup"><span data-stu-id="6f5b5-158">Add and remove nodes</span></span>
<span data-ttu-id="6f5b5-159">È possibile aggiungere o rimuovere i cluster di Service Fabric autonomo tooyour nodi come variare delle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="6f5b5-160">Vedere [aggiungere o rimuovere nodi tooa Service Fabric autonomo cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) per i passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="6f5b5-161">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="6f5b5-161">Remove a cluster</span></span>
<span data-ttu-id="6f5b5-162">tooremove un cluster, eseguire hello *RemoveServiceFabricCluster.ps1* dalla cartella del pacchetto hello e passare nel file di configurazione JSON toohello percorso hello uno script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="6f5b5-163">È facoltativamente possibile specificare un percorso per il log di hello di eliminazione hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="6f5b5-164">Questo script può essere eseguito su qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi nel file di configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="6f5b5-165">macchina Hello che questo script viene eseguito in non è una parte del cluster hello toobe.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="6f5b5-166">Dati di telemetria raccolti e come tooopt esplicitamente</span><span class="sxs-lookup"><span data-stu-id="6f5b5-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="6f5b5-167">Per impostazione predefinita, prodotto hello raccoglie dati di telemetria del prodotto hello Service Fabric utilizzo tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="6f5b5-168">Hello Best Practice Analyzer che viene eseguita come parte dell'installazione di hello verifica la presenza di connettività troppo[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="6f5b5-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="6f5b5-169">Se non è raggiungibile, il programma di installazione di hello ha esito negativo a meno che non è rifiutare esplicitamente i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="6f5b5-170">pipeline di dati di telemetria Hello tenta hello tooupload segue dati troppo[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="6f5b5-171">È un principio del best effort caricamento e non ha alcun impatto sulla funzionalità di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="6f5b5-172">dati di telemetria Hello viene inviato solo dal nodo hello che viene eseguito hello failover manager primario.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="6f5b5-173">Nessun altro nodo invia dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="6f5b5-174">telemetria Hello è costituita dai seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="6f5b5-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="6f5b5-175">Numero di servizi</span><span class="sxs-lookup"><span data-stu-id="6f5b5-175">Number of services</span></span>
* <span data-ttu-id="6f5b5-176">Numero di elementi ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="6f5b5-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="6f5b5-177">Numero di elementi Applications</span><span class="sxs-lookup"><span data-stu-id="6f5b5-177">Number of Applications</span></span>
* <span data-ttu-id="6f5b5-178">Numero di elementi ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="6f5b5-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="6f5b5-179">Numero di elementi FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6f5b5-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="6f5b5-180">Numero di elementi InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6f5b5-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="6f5b5-181">Numero di elementi UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="6f5b5-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="6f5b5-182">Numero di elementi Replicas</span><span class="sxs-lookup"><span data-stu-id="6f5b5-182">Number of Replicas</span></span>
* <span data-ttu-id="6f5b5-183">Numero di elementi InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="6f5b5-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="6f5b5-184">Numero di elementi StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="6f5b5-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="6f5b5-185">Numero di elementi OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="6f5b5-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="6f5b5-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="6f5b5-186">CommonQueueLength</span></span>
* <span data-ttu-id="6f5b5-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="6f5b5-187">QueryQueueLength</span></span>
* <span data-ttu-id="6f5b5-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="6f5b5-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="6f5b5-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="6f5b5-189">CommitQueueLength</span></span>
* <span data-ttu-id="6f5b5-190">Numero di elementi Nodes</span><span class="sxs-lookup"><span data-stu-id="6f5b5-190">Number of Nodes</span></span>
* <span data-ttu-id="6f5b5-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="6f5b5-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="6f5b5-192">ClusterId: GUID generato casualmente per ogni cluster</span><span class="sxs-lookup"><span data-stu-id="6f5b5-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="6f5b5-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="6f5b5-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="6f5b5-194">Indirizzo IP di macchina virtuale hello o computer dal quale hello vengono caricati dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="6f5b5-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="6f5b5-195">dati di telemetria toodisable, aggiungere il seguente troppo di hello*proprietà* nella configurazione del cluster: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="6f5b5-196">Funzionalità di anteprima incluse in questo pacchetto</span><span class="sxs-lookup"><span data-stu-id="6f5b5-196">Preview features included in this package</span></span>
<span data-ttu-id="6f5b5-197">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="6f5b5-198">A partire da hello nuovo [versione GA di cluster autonomi hello per Windows Server (versione 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), è possibile aggiornare le versioni di toofuture cluster, manualmente o automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="6f5b5-199">Fare riferimento troppo[aggiornare una versione di cluster di Service Fabric autonomo](service-fabric-cluster-upgrade-windows-server.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6f5b5-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6f5b5-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f5b5-200">Next steps</span></span>
* [<span data-ttu-id="6f5b5-201">Distribuire e rimuovere applicazioni con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f5b5-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="6f5b5-202">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="6f5b5-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="6f5b5-203">Aggiungere o rimuovere nodi tooa autonoma dell'infrastruttura del servizio cluster</span><span class="sxs-lookup"><span data-stu-id="6f5b5-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="6f5b5-204">Aggiornare il cluster autonomo di Service Fabric in Windows Server</span><span class="sxs-lookup"><span data-stu-id="6f5b5-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="6f5b5-205">Creare un cluster di Service Fabric autonomo con VM di Azure che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="6f5b5-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="6f5b5-206">Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows</span><span class="sxs-lookup"><span data-stu-id="6f5b5-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="6f5b5-207">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="6f5b5-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
