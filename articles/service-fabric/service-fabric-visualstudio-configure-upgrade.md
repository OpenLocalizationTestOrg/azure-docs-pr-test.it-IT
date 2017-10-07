---
title: aggiornamento di hello aaaConfigure di un'applicazione di Service Fabric | Documenti Microsoft
description: Informazioni su come tooconfigure hello impostazioni per l'aggiornamento di un'applicazione di Service Fabric con Microsoft Visual Studio.
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
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="bc15c-103">Configurare l'aggiornamento hello di un'applicazione di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc15c-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="bc15c-104">Visual Studio tools per Azure Service Fabric forniscono supporto per l'aggiornamento per la pubblicazione toolocal o dei cluster remoti.</span><span class="sxs-lookup"><span data-stu-id="bc15c-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="bc15c-105">Esistono tre scenari in cui si desidera tooupgrade la versione più recente tooa di applicazione non sostituisce un'applicazione hello durante i test e debug:</span><span class="sxs-lookup"><span data-stu-id="bc15c-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="bc15c-106">Dati dell'applicazione non venga persi durante l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="bc15c-107">Disponibilità resta alta in modo non qualsiasi interruzione del servizio durante l'aggiornamento di hello, se non esistono che sufficienti le istanze del servizio distribuiti in domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bc15c-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="bc15c-108">Durante l'aggiornamento, possono essere eseguiti test in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc15c-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="bc15c-109">Parametri necessari tooupgrade</span><span class="sxs-lookup"><span data-stu-id="bc15c-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="bc15c-110">È possibile scegliere tra due tipi di distribuzione: normale o aggiornata.</span><span class="sxs-lookup"><span data-stu-id="bc15c-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="bc15c-111">Una distribuzione normale Cancella i dati nel cluster hello e informazioni sulla distribuzione precedente distribuzione di un aggiornamento mantiene il.</span><span class="sxs-lookup"><span data-stu-id="bc15c-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="bc15c-112">Quando si aggiorna un'applicazione di Service Fabric in Visual Studio, è necessario tooprovide parametri di aggiornamento dell'applicazione e i criteri di controllo di integrità.</span><span class="sxs-lookup"><span data-stu-id="bc15c-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="bc15c-113">Aggiornamento dell'applicazione i parametri consentono di controllare l'aggiornamento di hello, mentre i criteri di controllo di integrità determinano se l'aggiornamento di hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="bc15c-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="bc15c-114">Vedere l'articolo relativo all' [aggiornamento di un'applicazione di Service Fabric e i parametri di aggiornamento](service-fabric-application-upgrade-parameters.md) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="bc15c-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="bc15c-115">Sono disponibili tre modalità di aggiornamento: *Monitored*, *UnmonitoredAuto* e *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="bc15c-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="bc15c-116">Un aggiornamento di monitoraggio consente di automatizzare l'aggiornamento di hello e applicazione controllo di integrità.</span><span class="sxs-lookup"><span data-stu-id="bc15c-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="bc15c-117">Un aggiornamento UnmonitoredAuto consente di automatizzare l'aggiornamento di hello, ma ignora hello verifica integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc15c-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="bc15c-118">Quando si esegue un aggiornamento UnmonitoredManual, è necessario toomanually aggiornare ogni dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bc15c-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="bc15c-119">Ogni modalità di aggiornamento richiede diversi set di parametri.</span><span class="sxs-lookup"><span data-stu-id="bc15c-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="bc15c-120">Vedere [parametri di aggiornamento dell'applicazione](service-fabric-application-upgrade-parameters.md) toolearn ulteriori informazioni sulle opzioni di aggiornamento disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="bc15c-121">Aggiornamento di un'applicazione di Infrastruttura di servizi in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc15c-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="bc15c-122">Se si utilizza tooupgrade strumenti di Visual Studio Service Fabric hello un'applicazione di Service Fabric, specificare un toobe processo pubblica un aggiornamento anziché una distribuzione normale controllando hello **l'aggiornamento di un'applicazione hello** controllare casella.</span><span class="sxs-lookup"><span data-stu-id="bc15c-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="bc15c-123">parametri di aggiornamento hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="bc15c-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="bc15c-124">Fare clic su hello **impostazioni** pulsante Avanti toohello casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="bc15c-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="bc15c-125">Hello **modifica parametri aggiornamento** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bc15c-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="bc15c-126">Hello **modifica parametri aggiornamento** la finestra di dialogo supporta la modalità aggiornamento hello monitorati, UnmonitoredAuto e UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="bc15c-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="bc15c-127">Selezionare la modalità di aggiornamento hello toouse desiderati e quindi compilare griglia parametro hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="bc15c-128">Ogni parametro ha valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="bc15c-128">Each parameter has default values.</span></span> <span data-ttu-id="bc15c-129">parametro facoltativo Hello *DefaultServiceTypeHealthPolicy* accetta un input di tabella hash.</span><span class="sxs-lookup"><span data-stu-id="bc15c-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="bc15c-130">Di seguito è riportato un esempio di hello input formato della tabella hash per *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="bc15c-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="bc15c-131">*ServiceTypeHealthPolicyMap* è un altro parametro facoltativo che accetta un input di tabella hash in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="bc15c-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="bc15c-132">Ecco un esempio reale:</span><span class="sxs-lookup"><span data-stu-id="bc15c-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="bc15c-133">Se si seleziona la modalità di aggiornamento UnmonitoredManual, è necessario avviare un toocontinue console PowerShell manualmente e completare hello processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bc15c-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="bc15c-134">Fare riferimento troppo[aggiornamento dell'applicazione di Service Fabric: argomenti avanzati](service-fabric-application-upgrade-advanced.md) toolearn manuale aggiornare works.</span><span class="sxs-lookup"><span data-stu-id="bc15c-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="bc15c-135">Aggiornare un'applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc15c-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="bc15c-136">È possibile utilizzare i cmdlet di PowerShell tooupgrade un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bc15c-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="bc15c-137">Per informazioni dettagliate, vedere [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) e [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc15c-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="bc15c-138">Specificare un criterio di controllo di integrità nel file manifesto dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bc15c-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="bc15c-139">Ogni servizio in un'applicazione di Service Fabric può avere i propri parametri di criteri di integrità che eseguono l'override di valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="bc15c-140">È possibile fornire i valori di parametro nel file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="bc15c-141">Hello esempio seguente viene illustrato come tooapply salute univoca controllare criteri per ogni servizio nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bc15c-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="bc15c-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc15c-142">Next steps</span></span>
<span data-ttu-id="bc15c-143">Per ulteriori informazioni sulla distribuzione di un'applicazione, vedere [Distribuire un'applicazione esistente in Infrastruttura di servizi di Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="bc15c-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>