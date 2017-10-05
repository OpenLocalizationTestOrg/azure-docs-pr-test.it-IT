---
title: Aggiornare un cluster autonomo di Azure Service Fabric in Windows Server | Microsoft Docs
description: "Aggiornare il codice di Azure Service Fabric e/o della configurazione che esegue un cluster autonomo di Service Fabric e impostare la modalità di aggiornamento del cluster."
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
ms.openlocfilehash: ac40775ca62362a32184207857a0b965a798e135
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="27249-103">Aggiornare il cluster autonomo di Azure Service Fabric in Windows Server</span><span class="sxs-lookup"><span data-stu-id="27249-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27249-104">Cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="27249-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="27249-105">Cluster autonomo</span><span class="sxs-lookup"><span data-stu-id="27249-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="27249-106">La possibilità di aggiornare un sistema moderno è fondamentale per il successo a lungo termine del prodotto.</span><span class="sxs-lookup"><span data-stu-id="27249-106">For any modern system, the ability to upgrade is a key to the long-term success of your product.</span></span> <span data-ttu-id="27249-107">Un cluster di Azure Service Fabric è una risorsa di cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="27249-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="27249-108">Questo articolo descrive in che modo è possibile verificare che il cluster esegua sempre versioni supportate del codice e delle configurazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="27249-108">This article describes how you can make sure that the cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-the-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="27249-109">Controllare la versione di Service Fabric eseguita nel cluster</span><span class="sxs-lookup"><span data-stu-id="27249-109">Control the Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="27249-110">Per impostare il cluster per il download di aggiornamenti di Service Fabric quando Microsoft rilascia una nuova versione, impostare la configurazione cluster **fabricClusterAutoupgradeEnabled** su true.</span><span class="sxs-lookup"><span data-stu-id="27249-110">To set your cluster to download updates of Service Fabric when Microsoft releases a new version, set the **fabricClusterAutoupgradeEnabled** cluster configuration to true.</span></span> <span data-ttu-id="27249-111">Per selezionare una versione supportata di Service Fabric per il cluster, impostare la configurazione cluster **fabricClusterAutoupgradeEnabled** su false.</span><span class="sxs-lookup"><span data-stu-id="27249-111">To select a supported version of Service Fabric that you want your cluster to be on, set the **fabricClusterAutoupgradeEnabled** cluster configuration to false.</span></span>

> [!NOTE]
> <span data-ttu-id="27249-112">Verificare che il cluster esegua sempre una versione di Service Fabric supportata.</span><span class="sxs-lookup"><span data-stu-id="27249-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="27249-113">Quando Microsoft annuncia il rilascio di una nuova versione di Service Fabric, viene segnalato il termine del periodo di supporto per la versione precedente dopo un minimo di 60 giorni dalla data dell'annuncio.</span><span class="sxs-lookup"><span data-stu-id="27249-113">When Microsoft announces the release of a new version of Service Fabric, the previous version is marked for end of support after a minimum of 60 days from the date of the announcement.</span></span> <span data-ttu-id="27249-114">Le nuove versioni vengono annunciate nel [blog del team di Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="27249-114">New releases are announced [on the Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="27249-115">A questo punto è possibile scegliere la nuova versione.</span><span class="sxs-lookup"><span data-stu-id="27249-115">The new release is available to choose at that point.</span></span>
>
>

<span data-ttu-id="27249-116">È possibile aggiornare il cluster alla nuova versione solo se si usa una configurazione del nodo di tipo produzione, in cui ogni nodo di Service Fabric viene allocato in una macchina virtuale o fisica separata.</span><span class="sxs-lookup"><span data-stu-id="27249-116">You can upgrade your cluster to the new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="27249-117">Se si usa un cluster di sviluppo in cui sono presenti più nodi di Service Fabric in un'unica macchina virtuale o computer fisico, è necessario creare di nuovo il cluster con la nuova versione.</span><span class="sxs-lookup"><span data-stu-id="27249-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create the cluster with the new version.</span></span>

<span data-ttu-id="27249-118">Due flussi di lavoro distinti possono aggiornare il cluster alla versione di Service Fabric più recente o a una versione supportata.</span><span class="sxs-lookup"><span data-stu-id="27249-118">Two distinct workflows can upgrade your cluster to the latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="27249-119">Un flusso di lavoro è per i cluster con connettività che scaricano automaticamente la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="27249-119">One workflow is for clusters that have connectivity to download the latest version automatically.</span></span> <span data-ttu-id="27249-120">L'altro flusso di lavoro è per i cluster senza connettività che quindi non scaricano la versione più recente di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="27249-120">The other workflow is for clusters that do not have connectivity to download the latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="27249-121">Aggiornare i cluster con la connettività per scaricare il codice e la configurazione più recenti</span><span class="sxs-lookup"><span data-stu-id="27249-121">Upgrade clusters that have connectivity to download the latest code and configuration</span></span>
<span data-ttu-id="27249-122">Seguire questa procedura per aggiornare il cluster a una versione supportata se i nodi del cluster hanno la connettività Internet a [http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27249-122">Use these steps to upgrade your cluster to a supported version if your cluster nodes have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="27249-123">Per i cluster che hanno la connettività a [http://download.microsoft.com](http://download.microsoft.com), Microsoft verifica periodicamente la disponibilità di nuove versioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="27249-123">For clusters that have connectivity to [http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for the availability of new Service Fabric versions.</span></span>

<span data-ttu-id="27249-124">Quando è disponibile una nuova versione di Service Fabric, il pacchetto viene scaricato localmente nel cluster e ne viene eseguito il provisioning per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="27249-124">When a new Service Fabric version is available, the package is downloaded locally to the cluster and provisioned for upgrade.</span></span> <span data-ttu-id="27249-125">Inoltre, per informare il cliente di questa nuova versione, il sistema visualizza un avviso esplicito di integrità del cluster simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="27249-125">Additionally, to inform the customer of this new version, the system shows an explicit cluster health warning that's similar to the following:</span></span>

<span data-ttu-id="27249-126">"Il supporto per la versione corrente del cluster [versione] termina il [Data]."</span><span class="sxs-lookup"><span data-stu-id="27249-126">“The current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="27249-127">Quando il cluster inizia a eseguire la versione più recente, l'avviso non viene più visualizzato.</span><span class="sxs-lookup"><span data-stu-id="27249-127">After the cluster is running the latest version, the warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="27249-128">Flusso di lavoro per l'aggiornamento del cluster</span><span class="sxs-lookup"><span data-stu-id="27249-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="27249-129">Quando viene visualizzato l'avviso di integrità del cluster, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="27249-129">After you see the cluster health warning, do the following:</span></span>

1. <span data-ttu-id="27249-130">Connettersi al cluster da qualsiasi macchina con accesso amministrativo a tutte le macchine elencate come nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="27249-130">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="27249-131">La macchina in cui viene eseguito lo script non deve necessariamente far parte del cluster.</span><span class="sxs-lookup"><span data-stu-id="27249-131">The machine that this script is run on does not have to be part of the cluster.</span></span>

    ```powershell

    ###### connect to the secure cluster using certs
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

2. <span data-ttu-id="27249-132">Ottenere l'elenco delle versioni di Service Fabric a cui è possibile eseguire l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="27249-132">Get the list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="27249-133">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="27249-133">You should get an output similar to this:</span></span>

    ![ottenere versioni di Fabric][getfabversions]
3. <span data-ttu-id="27249-135">Avviare un aggiornamento del cluster a una versione disponibile usando il comando [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27249-135">Start a cluster upgrade to an available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="27249-136">Per monitorare lo stato di avanzamento dell'aggiornamento, è possibile usare Service Fabric Explorer o eseguire il comando di Windows PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="27249-136">To monitor the progress of the upgrade, you can use Service Fabric Explorer or run the following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="27249-137">Se i criteri di integrità del cluster non vengono soddisfatti, viene eseguito il rollback dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="27249-137">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="27249-138">Per specificare criteri di integrità personalizzati per il comando **Start-ServiceFabricClusterUpgrade**, vedere la documentazione relativa a [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="27249-138">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="27249-139">Dopo aver risolto i problemi che hanno determinato il ripristino dello stato precedente, avviare di nuovo l'aggiornamento ripetendo la procedura descritta prima.</span><span class="sxs-lookup"><span data-stu-id="27249-139">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-to-download-the-latest-code-and-configuration"></a><span data-ttu-id="27249-140">Aggiornare i cluster <U>senza la connettività</u> per scaricare il codice e la configurazione più recenti</span><span class="sxs-lookup"><span data-stu-id="27249-140">Upgrade clusters that have <U>no connectivity</u> to download the latest code and configuration</span></span>
<span data-ttu-id="27249-141">Seguire questa procedura per aggiornare il cluster a una versione supportata se i nodi del cluster non hanno la connettività Internet a [http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27249-141">Use these steps to upgrade your cluster to a supported version if your cluster nodes do not have Internet connectivity to [http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="27249-142">Se si esegue un cluster non connesso a Internet, è necessario monitorare il blog del team di Service Fabric per informazioni sulla nuova versione.</span><span class="sxs-lookup"><span data-stu-id="27249-142">If you are running a cluster that is not connected to the Internet, you will have to monitor the Service Fabric team blog to learn about a new release.</span></span> <span data-ttu-id="27249-143">Il sistema non visualizza alcun avviso di integrità del cluster per informare l'utente di una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="27249-143">The system does not show a cluster health warning to alert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="27249-144">Confronto tra provisioning automatico e provisioning manuale</span><span class="sxs-lookup"><span data-stu-id="27249-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="27249-145">Per consentire il download e la registrazione automatici per la versione più recente del codice, impostare il servizio di aggiornamento di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="27249-145">To enable automatic downloading and registration for the latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="27249-146">Per istruzioni, vedere Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt nel [pacchetto autonomo](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="27249-146">Refer to the Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside the [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="27249-147">Per il processo manuale, seguire le istruzioni riportate di seguito.</span><span class="sxs-lookup"><span data-stu-id="27249-147">For manual process, follow the instructions below.</span></span>

<span data-ttu-id="27249-148">Modificare la configurazione del cluster per impostare la proprietà seguente su false prima di avviare un aggiornamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="27249-148">Modify your cluster configuration to set the following property to false before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="27249-149">Per informazioni dettagliate sull'utilizzo, fare riferimento a [Start-ServiceFabricClusterConfigurationUpgrade PS cmd (File CMD di PowerShell Start-ServiceFabricClusterConfigurationUpgrade)](https://msdn.microsoft.com/en-us/library/mt788302.aspx).</span><span class="sxs-lookup"><span data-stu-id="27249-149">Refer to [Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="27249-150">Prima di avviare l'aggiornamento della configurazione, verificare di aggiornare "clusterConfigurationVersion" nel file JSON.</span><span class="sxs-lookup"><span data-stu-id="27249-150">Make sure to update 'clusterConfigurationVersion' in your JSON before you start the configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="27249-151">Flusso di lavoro per l'aggiornamento del cluster</span><span class="sxs-lookup"><span data-stu-id="27249-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="27249-152">Eseguire Get-ServiceFabricClusterUpgrade da uno dei nodi del cluster e annotare il valore di TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="27249-152">Run Get-ServiceFabricClusterUpgrade from one of the nodes in the cluster and note the TargetCodeVersion.</span></span>
2. <span data-ttu-id="27249-153">Eseguire il comando seguente da un computer connesso a Internet per elencare tutte le versioni compatibili di l'aggiornamento con la versione corrente e scaricare il pacchetto corrispondente dai collegamenti di download associati.</span><span class="sxs-lookup"><span data-stu-id="27249-153">Run the following from an internet connected machine to list all upgrade compatible versions with the current version and download the corresponding package from the associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="27249-154">Connettersi al cluster da qualsiasi macchina con accesso amministrativo a tutte le macchine elencate come nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="27249-154">Connect to the cluster from any machine that has administrator access to all the machines that are listed as nodes in the cluster.</span></span> <span data-ttu-id="27249-155">La macchina in cui viene eseguito lo script non deve necessariamente far parte del cluster</span><span class="sxs-lookup"><span data-stu-id="27249-155">The machine that this script is run on does not have to be part of the cluster</span></span>

    ```powershell

   ###### Get the list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file including the path to it> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="27249-156">Copiare il pacchetto scaricato nell'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="27249-156">Copy the downloaded package into the cluster image store.</span></span>

5. <span data-ttu-id="27249-157">Registrare il pacchetto copiato.</span><span class="sxs-lookup"><span data-stu-id="27249-157">Register the copied package.</span></span>

    ```powershell

    ###### Get the list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of the .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="27249-158">Avviare un aggiornamento del cluster a una versione disponibile.</span><span class="sxs-lookup"><span data-stu-id="27249-158">Start a cluster upgrade to an available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="27249-159">È possibile monitorare lo stato di avanzamento dell'aggiornamento in Service Fabric Explorer oppure è possibile eseguire questo comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27249-159">You can monitor the progress of the upgrade on Service Fabric Explorer, or you can run the following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="27249-160">Se i criteri di integrità del cluster non vengono soddisfatti, viene eseguito il rollback dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="27249-160">If the cluster health policies are not met, the upgrade is rolled back.</span></span> <span data-ttu-id="27249-161">Per specificare criteri di integrità personalizzati per il comando **Start-ServiceFabricClusterUpgrade**, vedere la documentazione relativa a [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="27249-161">To specify custom health policies for the **Start-ServiceFabricClusterUpgrade** command, see the documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="27249-162">Dopo aver risolto i problemi che hanno determinato il ripristino dello stato precedente, avviare di nuovo l'aggiornamento ripetendo la procedura descritta prima.</span><span class="sxs-lookup"><span data-stu-id="27249-162">After you fix the issues that resulted in the rollback, initiate the upgrade again by following the same steps as previously described.</span></span>


## <a name="upgrade-the-cluster-configuration"></a><span data-ttu-id="27249-163">Aggiornare la configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="27249-163">Upgrade the cluster configuration</span></span>
<span data-ttu-id="27249-164">Prima di avviare l'aggiornamento della configurazione, è possibile testare il nuovo file JSON di configurazione cluster eseguendo lo script di PowerShell nel pacchetto autonomo.</span><span class="sxs-lookup"><span data-stu-id="27249-164">Before you initiate the configuration upgrade, you can test your new cluster configuration json by running the powershell script in the standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File>

```
<span data-ttu-id="27249-165">oppure</span><span class="sxs-lookup"><span data-stu-id="27249-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path to the new Configuration File> -OldClusterConfigFilePath <Path to the old Configuration File> -FabricRuntimePackagePath <Path to the .cab file which you want to test the configuration against>

```

<span data-ttu-id="27249-166">Alcune configurazioni non possono essere aggiornate, ad esempio gli endpoint, il nome del cluster, l'IP del nodo e così via. Il nuovo file JSON di configurazione cluster verrà testato confrontandolo con quello precedente e, in caso di problemi, verranno generati errori nella finestra di Powershell.</span><span class="sxs-lookup"><span data-stu-id="27249-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test the new cluster configuration json against the old one and throw errors in the Powershell window if there is any issue.</span></span>

<span data-ttu-id="27249-167">Per aggiornare la configurazione del cluster, eseguire **Start-ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="27249-167">To upgrade the cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="27249-168">L'aggiornamento della configurazione viene eseguito per dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="27249-168">The configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="27249-169">Aggiornamento della configurazione del certificato del cluster</span><span class="sxs-lookup"><span data-stu-id="27249-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="27249-170">Il certificato del cluster viene usato per l'autenticazione tra i nodi del cluster; il rollover del certificato deve quindi essere eseguito con particolare attenzione perché un eventuale errore bloccherà la comunicazione tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="27249-170">Cluster certificate is used for authentication between cluster nodes, so the certificate roll over should be performed with extra caution because failure will block the communication among cluster nodes.</span></span>  
<span data-ttu-id="27249-171">Tecnicamente, sono supportate tre opzioni:</span><span class="sxs-lookup"><span data-stu-id="27249-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="27249-172">Aggiornamento certificato singolo: il percorso di aggiornamento è 'Certificato (primario)-> Certificato B (primario)-> Certificato C (primario)->...'.</span><span class="sxs-lookup"><span data-stu-id="27249-172">Single certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="27249-173">Aggiornamento certificato doppio: il percorso di aggiornamento è "Certificato A (primario) -> Certificato A (primario) e B (secondario) -> Certificato B (primario) -> Certificato B (primario) e C (secondario) -> Certificato C (primario) -> ...".</span><span class="sxs-lookup"><span data-stu-id="27249-173">Double certificate upgrade: The upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="27249-174">Aggiornamento del tipo di certificato: configurazione dei certificati basati su identificazione personale <-> configurazione dei certificati basati su CommonName.</span><span class="sxs-lookup"><span data-stu-id="27249-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="27249-175">Ad esempio, identificazione personale del certificato A (primario) e identificazione personale B (secondario) -> CommonName del certificato C.</span><span class="sxs-lookup"><span data-stu-id="27249-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="27249-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27249-176">Next steps</span></span>
* <span data-ttu-id="27249-177">Informazioni su come personalizzare alcune [impostazioni dei cluster di Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="27249-177">Learn how to customize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="27249-178">Informazioni su come [aumentare o ridurre le istanze del cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="27249-178">Learn how to [scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="27249-179">Informazioni su come eseguire [aggiornamenti dell'applicazione](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="27249-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
