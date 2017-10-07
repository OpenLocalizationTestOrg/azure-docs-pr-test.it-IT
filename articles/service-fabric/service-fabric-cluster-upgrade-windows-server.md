---
title: aaaUpgrade autonoma Azure Service Fabric del cluster in Windows Server | Documenti Microsoft
description: "Aggiornare il codice di Azure Service Fabric hello e/o di configurazione che esegue un cluster di Service Fabric autonomo, inclusa l'impostazione di modalità di aggiornamento di cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="96a04-103">Aggiornare il cluster autonomo di Azure Service Fabric in Windows Server</span><span class="sxs-lookup"><span data-stu-id="96a04-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96a04-104">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="96a04-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="96a04-105">Cluster autonomo</span><span class="sxs-lookup"><span data-stu-id="96a04-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="96a04-106">Per qualsiasi sistema moderna, hello possibilità tooupgrade è un successo a lungo termine toohello chiave del prodotto.</span><span class="sxs-lookup"><span data-stu-id="96a04-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="96a04-107">Un cluster di Azure Service Fabric è una risorsa di cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="96a04-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="96a04-108">Questo articolo descrive come è possibile assicurarsi che cluster hello viene sempre eseguito versioni supportate di codice dell'infrastruttura di servizio e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="96a04-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="96a04-109">Versione di Service Fabric hello di controllo che esegue il cluster</span><span class="sxs-lookup"><span data-stu-id="96a04-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="96a04-110">tooset Aggiorna toodownload il cluster di Service Fabric quando Microsoft rilascia una nuova versione, set hello **fabricClusterAutoupgradeEnabled** tootrue di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="96a04-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="96a04-111">una versione supportata di Service Fabric che si desidera il toobe cluster sul set hello tooselect **fabricClusterAutoupgradeEnabled** toofalse di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="96a04-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="96a04-112">Verificare che il cluster esegua sempre una versione di Service Fabric supportata.</span><span class="sxs-lookup"><span data-stu-id="96a04-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="96a04-113">Quando Microsoft annuncia versione hello di una nuova versione di Service Fabric, la versione precedente di hello viene contrassegnata per la fine del supporto dopo un minimo di 60 giorni dalla data di hello annuncio hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="96a04-114">Le nuove versioni vengono annunciate [sul blog del team di Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="96a04-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="96a04-115">nuova versione di Hello è toochoose disponibili a questo punto.</span><span class="sxs-lookup"><span data-stu-id="96a04-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="96a04-116">È possibile aggiornare la nuova versione di toohello cluster solo se si utilizza una configurazione di nodi di stile di produzione, in cui ogni nodo di Service Fabric è allocato in una macchina virtuale o fisico separato.</span><span class="sxs-lookup"><span data-stu-id="96a04-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="96a04-117">Se si dispone di un cluster di sviluppo, più di un nodo di Service Fabric in cui è in un unico computer fisico o macchina virtuale, è necessario creare nuovamente il cluster hello con la nuova versione di hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="96a04-118">Due flussi di lavoro distinti è possibile aggiornare la versione più recente di toohello cluster o una versione supportata di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="96a04-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="96a04-119">Un flusso di lavoro è per i cluster con versione più recente di connettività toodownload hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96a04-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="96a04-120">Hello altro flusso di lavoro è per i cluster che non dispone di connettività toodownload hello Service Fabric più recente.</span><span class="sxs-lookup"><span data-stu-id="96a04-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="96a04-121">Aggiornare i cluster con configurazione e il codice più recente di connettività toodownload hello</span><span class="sxs-lookup"><span data-stu-id="96a04-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="96a04-122">Utilizzare la versione di tooa supportato cluster tooupgrade questi passaggi se i nodi del cluster dispongono di connettività Internet troppo[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="96a04-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="96a04-123">Per i cluster che dispone della connettività troppo[http://download.microsoft.com](http://download.microsoft.com), Microsoft controlla periodicamente per la disponibilità di nuove versioni di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="96a04-124">Quando una nuova versione di Service Fabric è disponibile, il pacchetto di hello venga scaricato localmente toohello cluster e il provisioning per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="96a04-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="96a04-125">Inoltre, cliente di hello tooinform di questa nuova versione, sistema hello Mostra cluster esplicita integrità di un avviso è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="96a04-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="96a04-126">"supporto della versione [versione #] cluster corrente hello termina [Date]".</span><span class="sxs-lookup"><span data-stu-id="96a04-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="96a04-127">Dopo che il cluster hello è in esecuzione la versione più recente di hello, avviso hello è stata risolta.</span><span class="sxs-lookup"><span data-stu-id="96a04-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="96a04-128">Flusso di lavoro per l'aggiornamento del cluster</span><span class="sxs-lookup"><span data-stu-id="96a04-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="96a04-129">Dopo aver visualizzato l'avviso di integrità del cluster di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="96a04-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="96a04-130">Connettere il cluster di toohello da qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="96a04-131">macchina Hello che questo script viene eseguito in non è una parte del cluster hello toobe.</span><span class="sxs-lookup"><span data-stu-id="96a04-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="96a04-132">Ottenere l'elenco di hello delle versioni di Service Fabric che è possibile eseguire l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="96a04-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="96a04-133">È necessario ottenere un toothis simili di output:</span><span class="sxs-lookup"><span data-stu-id="96a04-133">You should get an output similar toothis:</span></span>

    ![ottenere versioni di Fabric][getfabversions]
3. <span data-ttu-id="96a04-135">Avviare una versione di cluster tooan aggiornamento disponibile tramite il [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) cmd di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96a04-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="96a04-136">toomonitor hello lo stato di avanzamento dell'aggiornamento di hello, è possibile utilizzare Service Fabric Explorer o hello esecuzione comando di Windows PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="96a04-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="96a04-137">Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="96a04-138">criteri di integrità personalizzato toospecify per hello **inizio ServiceFabricClusterUpgrade** command, vedere la documentazione per [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a04-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="96a04-139">Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, avviare nuovamente l'aggiornamento di hello hello seguente procedura come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="96a04-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="96a04-140">Aggiornare i cluster che presentano <U>nessuna connettività</u> codice più recente di toodownload hello e la configurazione</span><span class="sxs-lookup"><span data-stu-id="96a04-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="96a04-141">Utilizzare la versione di tooa supportato cluster tooupgrade questi passaggi se i nodi del cluster non dispongono di connettività Internet troppo[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="96a04-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="96a04-142">Se si utilizza un cluster che non è connesso toohello Internet, sarà necessario toolearn toomonitor hello Service Fabric team blog su una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="96a04-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="96a04-143">sistema di Hello non viene visualizzato un tooalert di avviso di integrità del cluster di una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="96a04-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="96a04-144">Confronto tra provisioning automatico e provisioning manuale</span><span class="sxs-lookup"><span data-stu-id="96a04-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="96a04-145">tooenable il download automatico e la registrazione per la versione del codice più recente hello, configurare l'aggiornamento dell'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="96a04-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="96a04-146">Fare riferimento toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt all'interno di hello [pacchetto autonomo](service-fabric-cluster-standalone-package-contents.md) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="96a04-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="96a04-147">Per un processo manuale, istruzioni hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="96a04-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="96a04-148">Modificare il hello tooset configurazione di cluster seguendo toofalse proprietà prima di avviare un aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="96a04-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="96a04-149">Fare riferimento troppo[cmd PS inizio ServiceFabricClusterConfigurationUpgrade ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) per informazioni dettagliate sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="96a04-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="96a04-150">Verificare che tooupdate 'clusterConfigurationVersion' nel file JSON prima di iniziare l'aggiornamento della configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="96a04-151">Flusso di lavoro per l'aggiornamento del cluster</span><span class="sxs-lookup"><span data-stu-id="96a04-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="96a04-152">Eseguire Get-ServiceFabricClusterUpgrade da uno dei nodi cluster hello hello e prendere nota di hello TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="96a04-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="96a04-153">Seguente hello esecuzione da un toolist computer connesso internet tutti aggiornare le versioni compatibili con la versione corrente di hello e scaricare hello pacchetto dai collegamenti di download associati hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="96a04-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="96a04-154">Connettere il cluster di toohello da qualsiasi computer che dispone di amministratore accesso tooall hello computer elencati come nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="96a04-155">macchina Hello che questo script viene eseguito in non è una parte del cluster di hello toobe</span><span class="sxs-lookup"><span data-stu-id="96a04-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="96a04-156">Copiare il pacchetto scaricato hello nell'archivio di immagini cluster hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="96a04-157">Registrare il pacchetto copiato hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="96a04-158">Avviare una versione di cluster tooan aggiornamento disponibile.</span><span class="sxs-lookup"><span data-stu-id="96a04-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="96a04-159">È possibile monitorare lo stato di avanzamento hello dell'aggiornamento hello in Service Fabric Explorer o è possibile eseguire il comando PowerShell seguente hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="96a04-160">Se non vengono soddisfatti i criteri di integrità del cluster di hello, viene eseguito il rollback di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="96a04-161">criteri di integrità personalizzato toospecify per hello **inizio ServiceFabricClusterUpgrade** command, vedere la documentazione di hello per [inizio ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="96a04-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="96a04-162">Dopo aver risolto i problemi di hello che ha comportato il rollback di hello, avviare nuovamente l'aggiornamento di hello hello seguente procedura come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="96a04-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="96a04-163">Aggiorna la configurazione del cluster hello</span><span class="sxs-lookup"><span data-stu-id="96a04-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="96a04-164">Prima di iniziare l'aggiornamento della configurazione hello, è possibile testare il nuovo json di configurazione del cluster eseguendo uno script di powershell hello in pacchetto autonomo hello.</span><span class="sxs-lookup"><span data-stu-id="96a04-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="96a04-165">oppure</span><span class="sxs-lookup"><span data-stu-id="96a04-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="96a04-166">Alcune configurazioni non possono essere aggiornate, ad esempio gli endpoint, il nome del cluster, l'IP del nodo e così via. Questo test hello nuovo cluster configurazione json rispetto hello precedente e generano errori nella finestra di Powershell hello se è presente alcun problema.</span><span class="sxs-lookup"><span data-stu-id="96a04-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="96a04-167">l'aggiornamento della configurazione cluster hello tooupgrade, eseguire **inizio ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="96a04-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="96a04-168">l'aggiornamento della configurazione Hello è elaborato aggiornamento del dominio dal dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="96a04-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="96a04-169">Aggiornamento della configurazione del certificato del cluster</span><span class="sxs-lookup"><span data-stu-id="96a04-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="96a04-170">Il certificato del cluster viene utilizzato per l'autenticazione tra i nodi del cluster, in modo rollover del certificato hello deve essere eseguita con prestare particolare attenzione perché verrà bloccata la comunicazione hello tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="96a04-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="96a04-171">Tecnicamente, sono supportate tre opzioni:</span><span class="sxs-lookup"><span data-stu-id="96a04-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="96a04-172">Aggiornamento singolo certificato: percorso di aggiornamento hello ' certificato (primaria) -> B certificato (primaria) -> C certificato (primaria) ->... '.</span><span class="sxs-lookup"><span data-stu-id="96a04-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="96a04-173">Double aggiornamento certificati: percorso di aggiornamento hello ' certificato -> (principale) del certificato (primaria) e B (secondario) -> B certificato (primaria) -> B certificato (primaria) e C (secondario) -> C certificato (primaria) ->... '.</span><span class="sxs-lookup"><span data-stu-id="96a04-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="96a04-174">Aggiornamento del tipo di certificato: configurazione dei certificati basati su identificazione personale <-> configurazione dei certificati basati su CommonName.</span><span class="sxs-lookup"><span data-stu-id="96a04-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="96a04-175">Ad esempio, identificazione personale del certificato A (primario) e identificazione personale B (secondario) -> CommonName del certificato C.</span><span class="sxs-lookup"><span data-stu-id="96a04-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="96a04-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96a04-176">Next steps</span></span>
* <span data-ttu-id="96a04-177">Informazioni su come toocustomize alcuni [impostazioni cluster di Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="96a04-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="96a04-178">Informazioni su come troppo[aumentare e ridurre il cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="96a04-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="96a04-179">Informazioni su come eseguire [aggiornamenti dell'applicazione](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="96a04-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
