---
title: Configurare l'aggiornamento di un'applicazione di Service Fabric | Documentazione Microsoft
description: Informazioni su come configurare le impostazioni per l'aggiornamento di un'applicazione di Infrastruttura di servizi con Microsoft Visual Studio.
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="d8080-103">Configurare l'aggiornamento di un'applicazione di Infrastruttura di servizi in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8080-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="d8080-104">Gli strumenti di Visual Studio per Service Fabric di Azure forniscono supporto per l'aggiornamento per la pubblicazione nei cluster locali o remoti.</span><span class="sxs-lookup"><span data-stu-id="d8080-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="d8080-105">Esistono tre scenari in cui è consigliabile eseguire l'aggiornamento dell'applicazione a una versione più recente anziché sostituirla durante il test e il debug:</span><span class="sxs-lookup"><span data-stu-id="d8080-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="d8080-106">I dati dell'applicazione non vengono persi durante l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d8080-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="d8080-107">Si garantisce una disponibilità elevata continua per evitare ogni tipo di interruzione del servizio durante l'aggiornamento in presenza di sufficienti istanze del servizio distribuite nei domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d8080-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="d8080-108">Durante l'aggiornamento, possono essere eseguiti test in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8080-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="d8080-109">Parametri necessari per l'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="d8080-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="d8080-110">È possibile scegliere tra due tipi di distribuzione: normale o aggiornata.</span><span class="sxs-lookup"><span data-stu-id="d8080-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="d8080-111">Una distribuzione regolare cancella qualsiasi informazione di distribuzioni precedenti e i dati nel cluster, mentre una distribuzione di un aggiornamento li conserva.</span><span class="sxs-lookup"><span data-stu-id="d8080-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="d8080-112">Quando si aggiorna un'applicazione di Infrastruttura di servizi in Visual Studio, è necessario fornire parametri di aggiornamento dell’applicazione e criteri per il controllo dell’integrità.</span><span class="sxs-lookup"><span data-stu-id="d8080-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="d8080-113">I parametri di aggiornamento dell'applicazione consentono di controllare l'aggiornamento, mentre i criteri di controllo dell'integrità determinano se l'aggiornamento è avvenuto correttamente.</span><span class="sxs-lookup"><span data-stu-id="d8080-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="d8080-114">Vedere l'articolo relativo all' [aggiornamento di un'applicazione di Service Fabric e i parametri di aggiornamento](service-fabric-application-upgrade-parameters.md) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="d8080-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="d8080-115">Sono disponibili tre modalità di aggiornamento: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="d8080-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="d8080-116">Un aggiornamento Monitored consente di automatizzare l'aggiornamento e il controllo dell'integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8080-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="d8080-117">Un aggiornamento UnmonitoredAuto consente di automatizzare l'aggiornamento, ma ignorando il controllo dell'integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8080-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="d8080-118">Quando si esegue un aggiornamento UnmonitoredManual è necessario aggiornare manualmente ogni dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d8080-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="d8080-119">Ogni modalità di aggiornamento richiede diversi set di parametri.</span><span class="sxs-lookup"><span data-stu-id="d8080-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="d8080-120">Vedere [Parametri di aggiornamento di un'applicazione](service-fabric-application-upgrade-parameters.md) per conoscere le opzioni di aggiornamento disponibili.</span><span class="sxs-lookup"><span data-stu-id="d8080-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="d8080-121">Aggiornamento di un'applicazione di Infrastruttura di servizi in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8080-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="d8080-122">Se si utilizzano gli strumenti di Service Fabric di Visual Studio per aggiornare un'applicazione di Service Fabric, è possibile specificare un processo di pubblicazione come aggiornamento anziché distribuzione normale selezionando la casella di controllo **Aggiorna applicazione** .</span><span class="sxs-lookup"><span data-stu-id="d8080-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="d8080-123">Per configurare i parametri di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="d8080-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="d8080-124">Fare clic sul pulsante **Impostazioni** accanto alla casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="d8080-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="d8080-125">La finestra di dialogo **Edit Upgrade Parameters** verrà visualizzata.</span><span class="sxs-lookup"><span data-stu-id="d8080-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="d8080-126">La finestra di dialogo **Edit Upgrade Parameters** supporta le modalità di aggiornamento Monitored, UnmonitoredAuto e UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="d8080-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="d8080-127">Selezionare la modalità di aggiornamento che si desidera usare, quindi compilare la griglia dei parametri.</span><span class="sxs-lookup"><span data-stu-id="d8080-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="d8080-128">Ogni parametro ha valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="d8080-128">Each parameter has default values.</span></span> <span data-ttu-id="d8080-129">Il parametro facoltativo *DefaultServiceTypeHealthPolicy* accetta un input di tabella hash.</span><span class="sxs-lookup"><span data-stu-id="d8080-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="d8080-130">Di seguito è riportato un esempio del formato di input di tabella hash per *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="d8080-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="d8080-131">*ServiceTypeHealthPolicyMap* è un altro parametro facoltativo che accetta un input di tabella hash nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="d8080-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="d8080-132">Ecco un esempio reale:</span><span class="sxs-lookup"><span data-stu-id="d8080-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="d8080-133">Se si seleziona la modalità di aggiornamento UnmonitoredManual, è necessario avviare manualmente una console di PowerShell per continuare il processo di aggiornamento e completarlo.</span><span class="sxs-lookup"><span data-stu-id="d8080-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="d8080-134">Fare riferimento a [Aggiornamento di un'applicazione di infrastruttura di servizi: argomenti avanzati](service-fabric-application-upgrade-advanced.md) per scoprire come funziona l'aggiornamento manuale.</span><span class="sxs-lookup"><span data-stu-id="d8080-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="d8080-135">Aggiornare un'applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8080-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="d8080-136">È possibile utilizzare i cmdlet PowerShell per aggiornare un'applicazione di Infrastruttura di servizi.</span><span class="sxs-lookup"><span data-stu-id="d8080-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="d8080-137">Per informazioni dettagliate, vedere [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8080-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="d8080-138">Specificare un criterio di controllo dell'integrità nel file manifesto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d8080-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="d8080-139">Ogni servizio in un'applicazione di Infrastruttura di servizi può disporre di propri parametri di criteri di integrità che sostituiscono i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="d8080-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="d8080-140">È possibile fornire questi valori di parametro nel file manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8080-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="d8080-141">Nell'esempio seguente viene illustrato come applicare un criterio di controllo di integrità univoco per ogni servizio nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d8080-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="d8080-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8080-142">Next steps</span></span>
<span data-ttu-id="d8080-143">Per ulteriori informazioni sulla distribuzione di un'applicazione, vedere [Distribuire un'applicazione esistente in Infrastruttura di servizi di Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8080-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>