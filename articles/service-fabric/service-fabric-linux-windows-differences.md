---
title: aaaAzure Service Fabric le differenze tra Linux e Windows | Documenti Microsoft
description: Differenze tra hello Azure Service Fabric Preview in Linux e Azure Service Fabric in Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="bba70-103">Differenze tra Service Fabric in Linux (anteprima) e in Windows (disponibile a livello generale)</span><span class="sxs-lookup"><span data-stu-id="bba70-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="bba70-104">Poiché Service Fabric in Linux è un'anteprima, alcune funzionalità sono supportate in Windows, ma non ancora in Linux.</span><span class="sxs-lookup"><span data-stu-id="bba70-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="bba70-105">Infine, il set di funzionalità hello saranno in parità quando Service Fabric in Linux diventa disponibile.</span><span class="sxs-lookup"><span data-stu-id="bba70-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="bba70-106">Con le versioni future, questo gap di funzionalità verrà ridotto.</span><span class="sxs-lookup"><span data-stu-id="bba70-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="bba70-107">Hello seguenti esistono differenze tra le versioni disponibili più recenti di hello (vale a dire tra la versione 5.6 in Windows e la versione 5.5 in Linux):</span><span class="sxs-lookup"><span data-stu-id="bba70-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="bba70-108">Reliable Collections e Reliable Stateful Services</span><span class="sxs-lookup"><span data-stu-id="bba70-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="bba70-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="bba70-109">ReverseProxy</span></span> 
* <span data-ttu-id="bba70-110">Programma di installazione autonomo</span><span class="sxs-lookup"><span data-stu-id="bba70-110">Standalone installer</span></span> 
* <span data-ttu-id="bba70-111">Convalida XML Schema per i file manifesto</span><span class="sxs-lookup"><span data-stu-id="bba70-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="bba70-112">Reindirizzamento della console</span><span class="sxs-lookup"><span data-stu-id="bba70-112">Console redirection</span></span> 
* <span data-ttu-id="bba70-113">Hello errore Analysis Service (/FAs)</span><span class="sxs-lookup"><span data-stu-id="bba70-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="bba70-114">Docker Compose e driver di volume e registrazione per i contenitori</span><span class="sxs-lookup"><span data-stu-id="bba70-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="bba70-115">Governance delle risorse per contenitori e servizi</span><span class="sxs-lookup"><span data-stu-id="bba70-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="bba70-116">Servizio DNS</span><span class="sxs-lookup"><span data-stu-id="bba70-116">DNS service</span></span>
* <span data-ttu-id="bba70-117">Supporto di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bba70-117">Azure Active Directory support</span></span>
* <span data-ttu-id="bba70-118">Comandi dell'interfaccia della riga di comando equivalenti ad alcuni comandi di Powershell</span><span class="sxs-lookup"><span data-stu-id="bba70-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="bba70-119">Solo un subset di comandi di Powershell può essere eseguito su un cluster Linux (in formato espanso nella sezione successiva hello).</span><span class="sxs-lookup"><span data-stu-id="bba70-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="bba70-120">Il reindirizzamento della console non è supportato nei cluster di produzione, nemmeno in Windows.</span><span class="sxs-lookup"><span data-stu-id="bba70-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="bba70-121">Anche gli strumenti di sviluppo presentano differenze tra Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="bba70-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="bba70-122">VisualStudio, Powershell, VSTS e ETW vengono usati in Windows mentre Yeoman, Eclipse, Jenkins, e LTTng vengono usati in Linux.</span><span class="sxs-lookup"><span data-stu-id="bba70-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="bba70-123">Cmdlet di Powershell che non funzionano in un cluster di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="bba70-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="bba70-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="bba70-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="bba70-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="bba70-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="bba70-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="bba70-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="bba70-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="bba70-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="bba70-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="bba70-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="bba70-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="bba70-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="bba70-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="bba70-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="bba70-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="bba70-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="bba70-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="bba70-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="bba70-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="bba70-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="bba70-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="bba70-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="bba70-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="bba70-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="bba70-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="bba70-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="bba70-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="bba70-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="bba70-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="bba70-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="bba70-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="bba70-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="bba70-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="bba70-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="bba70-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="bba70-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="bba70-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="bba70-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="bba70-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="bba70-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="bba70-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="bba70-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="bba70-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="bba70-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="bba70-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="bba70-146">Cmd</span></span>
* <span data-ttu-id="bba70-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="bba70-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="bba70-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="bba70-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="bba70-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="bba70-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="bba70-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="bba70-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="bba70-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="bba70-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="bba70-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="bba70-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="bba70-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="bba70-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="bba70-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="bba70-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="bba70-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="bba70-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="bba70-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="bba70-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="bba70-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="bba70-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="bba70-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="bba70-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="bba70-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="bba70-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="bba70-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="bba70-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="bba70-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="bba70-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="bba70-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="bba70-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="bba70-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="bba70-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="bba70-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="bba70-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="bba70-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="bba70-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="bba70-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="bba70-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="bba70-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="bba70-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="bba70-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="bba70-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="bba70-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="bba70-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bba70-177">Next steps</span></span>
* [<span data-ttu-id="bba70-178">Preparare l'ambiente di sviluppo in Linux</span><span class="sxs-lookup"><span data-stu-id="bba70-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="bba70-179">Preparare l'ambiente di sviluppo in OSX</span><span class="sxs-lookup"><span data-stu-id="bba70-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="bba70-180">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="bba70-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="bba70-181">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse)</span><span class="sxs-lookup"><span data-stu-id="bba70-181">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="bba70-182">Creare la prima applicazione CSharp in Linux</span><span class="sxs-lookup"><span data-stu-id="bba70-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="bba70-183">Utilizzare le applicazioni di hello servizio infrastruttura CLI toomanage</span><span class="sxs-lookup"><span data-stu-id="bba70-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
