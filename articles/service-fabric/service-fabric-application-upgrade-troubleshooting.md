---
title: Risoluzione dei problemi di aggiornamento delle applicazioni | Documentazione Microsoft
description: Questo articolo descrive alcuni problemi comuni relativi all'aggiornamento di un'applicazione di Service Fabric e come risolverli.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="1142c-103">Risolvere i problemi relativi agli aggiornamenti delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="1142c-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="1142c-104">Questo articolo descrive alcuni dei problemi comuni relativi all'aggiornamento di un'applicazione di Azure Service Fabric e come risolverli.</span><span class="sxs-lookup"><span data-stu-id="1142c-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="1142c-105">Risolvere i problemi relativi all'aggiornamento di un'applicazione non riuscito</span><span class="sxs-lookup"><span data-stu-id="1142c-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="1142c-106">Se un aggiornamento ha esito negativo, l'output del comando **Get-ServiceFabricApplicationUpgrade** contiene alcune informazioni aggiuntive per il debug dell'errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="1142c-107">L'elenco seguente specifica come si possono usare le informazioni aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="1142c-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="1142c-108">Identificare il tipo di errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-108">Identify the failure type.</span></span>
2. <span data-ttu-id="1142c-109">Identificare la causa dell'errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="1142c-110">Isolare uno o più componenti che hanno causato l'errore per altre indagini.</span><span class="sxs-lookup"><span data-stu-id="1142c-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="1142c-111">Queste informazioni sono disponibili nel momento in cui Service Fabric rileva l'errore, indipendentemente dal fatto che la proprietà **FailureAction** sia impostata per il rollback o la sospensione dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1142c-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="1142c-112">Identificare il tipo di errore</span><span class="sxs-lookup"><span data-stu-id="1142c-112">Identify the failure type</span></span>
<span data-ttu-id="1142c-113">Nell'output di **Get-ServiceFabricApplicationUpgrade** l'elemento **FailureTimestampUtc** identifica il timestamp (in UTC) in corrispondenza del quale Service Fabric ha rilevato un errore di aggiornamento ed è stata attivata la proprietà **FailureAction**.</span><span class="sxs-lookup"><span data-stu-id="1142c-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="1142c-114">**FailureReason** identifica una delle tre possibili cause generali dell'errore:</span><span class="sxs-lookup"><span data-stu-id="1142c-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="1142c-115">UpgradeDomainTimeout: indica che uno specifico dominio di aggiornamento ha impiegato troppo tempo per il completamento e il valore di **UpgradeDomainTimeout** è scaduto.</span><span class="sxs-lookup"><span data-stu-id="1142c-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="1142c-116">OverallUpgradeTimeout: indica che l'aggiornamento globale ha impiegato troppo tempo per il completamento e il valore di **UpgradeTimeout** è scaduto.</span><span class="sxs-lookup"><span data-stu-id="1142c-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="1142c-117">HealthCheck: indica che, dopo l'aggiornamento di un dominio di aggiornamento, l'applicazione è rimasta in uno stato non integro secondo i criteri di integrità specificati e il valore di **HealthCheckRetryTimeout** è scaduto.</span><span class="sxs-lookup"><span data-stu-id="1142c-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="1142c-118">Queste voci sono visualizzate nell'output se l'aggiornamento ha esito negativo e viene avviato il rollback.</span><span class="sxs-lookup"><span data-stu-id="1142c-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="1142c-119">A seconda del tipo di errore sono visualizzate informazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1142c-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="1142c-120">Analizzare i timeout di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="1142c-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="1142c-121">Gli errori di timeout di aggiornamento si verificano più comunemente a causa di problemi di disponibilità dei servizi.</span><span class="sxs-lookup"><span data-stu-id="1142c-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="1142c-122">L'output che segue questo paragrafo è tipico di aggiornamenti in cui le repliche o le istanze dei servizi non si avviano nella nuova versione del codice.</span><span class="sxs-lookup"><span data-stu-id="1142c-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="1142c-123">Il campo **UpgradeDomainProgressAtFailure** acquisisce uno snapshot di eventuali processi di aggiornamento in sospeso al momento dell'errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="1142c-124">In questo esempio l'aggiornamento non è riuscito nel dominio di aggiornamento *MYUD1* e due partizioni (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) sono state bloccate.</span><span class="sxs-lookup"><span data-stu-id="1142c-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="1142c-125">Le partizioni sono state bloccate perché il runtime non è stato in grado di posizionare le repliche primarie (*WaitForPrimaryPlacement*) nei nodi di destinazione *Node1* e *Node4*.</span><span class="sxs-lookup"><span data-stu-id="1142c-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="1142c-126">È possibile usare il comando **Get-ServiceFabricNode** per verificare che questi due nodi siano contenuti nel dominio di aggiornamento *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="1142c-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="1142c-127">Il valore di *UpgradePhase* è *PostUpgradeSafetyCheck*, a indicare che questi controlli di sicurezza vengono eseguiti al termine dell'aggiornamento di tutti i nodi del dominio di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1142c-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="1142c-128">Tutte queste informazioni indicano un possibile problema con la nuova versione del codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="1142c-129">I problemi più comuni sono rappresentati da errori di servizi nell'apertura o nell'innalzamento di livello a percorsi di codice primari.</span><span class="sxs-lookup"><span data-stu-id="1142c-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="1142c-130">Se il valore di *UpgradePhase* è *PreUpgradeSafetyCheck*, si sono verificati problemi durante la preparazione del dominio di aggiornamento prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1142c-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="1142c-131">I problemi più comuni in questo caso sono errori di servizi nella chiusura o nell'abbassamento di livello da percorsi di codice primari.</span><span class="sxs-lookup"><span data-stu-id="1142c-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="1142c-132">Il valore corrente di **UpgradeState** è *RollingBackCompleted*, pertanto l'aggiornamento originale deve essere stato eseguito con la proprietà **FailureAction** impostata per il rollback ed è stato eseguito automaticamente il rollback dell'aggiornamento al momento dell'errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="1142c-133">Se l'aggiornamento originale fosse stato eseguito con la proprietà **FailureAction**impostata per l'azione manuale, si sarebbe attivato lo stato di sospensione dell'aggiornamento per consentire il debug attivo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="1142c-134">Analizzare gli errori di controllo dell'integrità</span><span class="sxs-lookup"><span data-stu-id="1142c-134">Investigate health check failures</span></span>
<span data-ttu-id="1142c-135">Gli errori di controllo dell'integrità possono essere attivati da vari problemi che possono verificarsi dopo l'aggiornamento di tutti i nodi di un dominio di aggiornamento e dopo aver superato tutti i controlli di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1142c-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="1142c-136">L'output che segue questo paragrafo è tipico di un errore di aggiornamento causato da controlli di integrità non riusciti.</span><span class="sxs-lookup"><span data-stu-id="1142c-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="1142c-137">Il campo **UnhealthyEvaluations** acquisisce uno snapshot dei controlli di integrità non riusciti al momento dell'aggiornamento in base ai [criteri di integrità](service-fabric-health-introduction.md)specificati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1142c-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="1142c-138">Per analizzare gli errori dei controlli di integrità è prima necessario conoscere il modello di integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1142c-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="1142c-139">Anche senza questa conoscenza approfondita è comunque possibile osservare che due servizi risultano non integri: *fabric:/DemoApp/Svc3* e *fabric:/DemoApp/Svc2*, insieme ai report sugli errori di integrità, in questo caso "InjectedFault".</span><span class="sxs-lookup"><span data-stu-id="1142c-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="1142c-140">In questo esempio risultano non integri 2 servizi su 4, quindi al di sotto dell'obiettivo predefinito di non integrità pari a 0% (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="1142c-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="1142c-141">L'aggiornamento è stato sospeso contestualmente all'errore grazie all'impostazione di **FailureAction** per l'azione manuale all'avvio dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1142c-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="1142c-142">Questa modalità consente di analizzare il sistema nello stato di errore prima di eseguire altre azioni.</span><span class="sxs-lookup"><span data-stu-id="1142c-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="1142c-143">Eseguire il ripristino da un aggiornamento sospeso</span><span class="sxs-lookup"><span data-stu-id="1142c-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="1142c-144">Con la proprietà **FailureAction**impostata per il rollback, non è necessario alcun ripristino in quanto l'aggiornamento esegue automaticamente il rollback in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="1142c-145">Con una proprietà **FailureAction**impostata per l'azione manuale invece sono disponibili diverse opzioni di ripristino:</span><span class="sxs-lookup"><span data-stu-id="1142c-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="1142c-146">attivare un rollback</span><span class="sxs-lookup"><span data-stu-id="1142c-146">trigger a rollback</span></span>
2. <span data-ttu-id="1142c-147">Procedere manualmente con il resto dell'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="1142c-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="1142c-148">Riprendere l'aggiornamento monitorato</span><span class="sxs-lookup"><span data-stu-id="1142c-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="1142c-149">È possibile usare il comando **Start-ServiceFabricApplicationRollback** in qualsiasi momento per avviare il rollback dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="1142c-150">Se il comando ha esito positivo, la richiesta di rollback viene registrata nel sistema e il rollback si avvia poco dopo.</span><span class="sxs-lookup"><span data-stu-id="1142c-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="1142c-151">È possibile usare il comando **Resume-ServiceFabricApplicationUpgrade** per procedere manualmente con il resto dell'aggiornamento, un dominio di aggiornamento per volta.</span><span class="sxs-lookup"><span data-stu-id="1142c-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="1142c-152">In questa modalità il sistema esegue solo i controlli di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1142c-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="1142c-153">Non viene eseguito alcun controllo di integrità.</span><span class="sxs-lookup"><span data-stu-id="1142c-153">No more health checks are performed.</span></span> <span data-ttu-id="1142c-154">Questo comando può essere usato soltanto se l'elemento *UpgradeState* è impostato su *RollingForwardPending*, a indicare che l'aggiornamento del dominio di aggiornamento corrente è terminato e non è ancora iniziato quello successivo (in sospeso).</span><span class="sxs-lookup"><span data-stu-id="1142c-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="1142c-155">Il comando **Update-ServiceFabricApplicationUpgrade** può essere usato per riprendere l'aggiornamento in modalità monitorata con l'esecuzione sia dei controlli di sicurezza sia dei controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="1142c-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="1142c-156">L'aggiornamento continua dal dominio di aggiornamento in corrispondenza del quale è stato sospeso e userà gli stessi parametri di aggiornamento e criteri di integrità usati precedentemente.</span><span class="sxs-lookup"><span data-stu-id="1142c-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="1142c-157">Se necessario, i parametri di aggiornamento e i criteri di integrità mostrati nell'output precedente possono essere modificati nello stesso comando alla ripresa dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1142c-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="1142c-158">In questo esempio l'aggiornamento è stato ripreso in modalità monitorata con i parametri e i criteri di integrità invariati.</span><span class="sxs-lookup"><span data-stu-id="1142c-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="1142c-159">Risoluzione di altri problemi</span><span class="sxs-lookup"><span data-stu-id="1142c-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="1142c-160">Service Fabric non segue i criteri di integrità specificati</span><span class="sxs-lookup"><span data-stu-id="1142c-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="1142c-161">Possibile causa 1:</span><span class="sxs-lookup"><span data-stu-id="1142c-161">Possible Cause 1:</span></span>

<span data-ttu-id="1142c-162">Service Fabric converte tutte le percentuali in numeri effettivi di entità (ad esempio repliche, partizioni e servizi) per la valutazione dell'integrità ed esegue sempre l'arrotondamento alle entità intere.</span><span class="sxs-lookup"><span data-stu-id="1142c-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="1142c-163">Se ad esempio il valore massimo di *MaxPercentUnhealthyReplicasPerPartition* è 21% e ci sono cinque repliche, Service Fabric accetta un massimo di due repliche non integre, ovvero `Math.Ceiling (5*0.21)`.</span><span class="sxs-lookup"><span data-stu-id="1142c-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="1142c-164">Perciò, i criteri di integrità devono essere impostati in modo da tenere conto di questo.</span><span class="sxs-lookup"><span data-stu-id="1142c-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="1142c-165">Possibile causa 2:</span><span class="sxs-lookup"><span data-stu-id="1142c-165">Possible Cause 2:</span></span>

<span data-ttu-id="1142c-166">I criteri di integrità sono specificati in termini di percentuali dei servizi totali e non di specifiche istanze di servizi.</span><span class="sxs-lookup"><span data-stu-id="1142c-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="1142c-167">Si consideri ad esempio uno scenario in cui, prima di un aggiornamento, un'applicazione dispone di quattro istanze di servizi, A, B, C e D, in cui il servizio D non è integro tuttavia non ha un impatto significativo sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="1142c-168">Si vuole ignorare il servizio D non integro durante l'aggiornamento e impostare il parametro *MaxPercentUnhealthyServices* su 25%, presupponendo che solo i servizi A, B e C debbano essere integri.</span><span class="sxs-lookup"><span data-stu-id="1142c-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="1142c-169">Durante l'aggiornamento però D diventa integro mentre C diventa non integro.</span><span class="sxs-lookup"><span data-stu-id="1142c-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="1142c-170">L'aggiornamento riesce comunque perché solo il 25% dei servizi non è integro.</span><span class="sxs-lookup"><span data-stu-id="1142c-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="1142c-171">Tuttavia c'è la possibilità di errori imprevisti causati dalla non integrità di C invece di D. In questa situazione D dovrebbe essere modellato come tipo di servizio diverso rispetto ad A, B e C. Poiché i criteri di integrità sono specificati per tipo di servizio, è possibile applicare soglie di percentuali di non integrità diverse a servizi diversi.</span><span class="sxs-lookup"><span data-stu-id="1142c-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="1142c-172">Non sono stati specificati criteri di integrità per l'aggiornamento dell'applicazione, ma l'aggiornamento non riesce a causa di alcuni timeout che però non sono mai stati specificati.</span><span class="sxs-lookup"><span data-stu-id="1142c-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="1142c-173">Se i criteri di integrità non vengono forniti alla richiesta di aggiornamento, vengono rilevati dal file *ApplicationManifest.xml* della versione dell'applicazione corrente.</span><span class="sxs-lookup"><span data-stu-id="1142c-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="1142c-174">Ad esempio, se si aggiorna l'applicazione X dalla versione 1.0 alla versione 2.0, vengono usati i criteri di integrità specificati per la versione 1.0.</span><span class="sxs-lookup"><span data-stu-id="1142c-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="1142c-175">Se devono essere usati criteri di integrità diversi per l'aggiornamento, specificarli nella chiamata API di aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="1142c-176">I criteri specificati nella chiamata API si applicano soltanto durante l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1142c-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="1142c-177">Una volta completato l'aggiornamento, vengono usati i criteri specificati nel file *ApplicationManifest.xml* .</span><span class="sxs-lookup"><span data-stu-id="1142c-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="1142c-178">Sono stati specificati timeout non corretti</span><span class="sxs-lookup"><span data-stu-id="1142c-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="1142c-179">Ci si potrebbe chiedere cosa succede quando i timeout sono impostati in modo incoerente.</span><span class="sxs-lookup"><span data-stu-id="1142c-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="1142c-180">Ad esempio, può essere impostato un valore *UpgradeTimeout* inferiore al valore *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="1142c-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="1142c-181">viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="1142c-181">The answer is that an error is returned.</span></span> <span data-ttu-id="1142c-182">Si verificano errori se il valore di *UpgradeDomainTimeout* è inferiore alla somma di *HealthCheckWaitDuration* e *HealthCheckRetryTimeout* o se il valore di *UpgradeDomainTimeout* è inferiore alla somma di *HealthCheckWaitDuration* e *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="1142c-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="1142c-183">Gli aggiornamenti richiedono troppo tempo</span><span class="sxs-lookup"><span data-stu-id="1142c-183">My upgrades are taking too long</span></span>
<span data-ttu-id="1142c-184">Il tempo per il completamento dell'aggiornamento dipende dai controlli di integrità e dai timeout specificati.</span><span class="sxs-lookup"><span data-stu-id="1142c-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="1142c-185">I controlli di integrità e i timeout dipendono dal tempo necessario per copiare, distribuire e stabilizzare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1142c-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="1142c-186">L'uso di timeout eccessivamente rigidi può comportare un numero elevato di aggiornamenti non riusciti. È quindi consigliabile iniziare prudenzialmente con valori di timeout più lunghi.</span><span class="sxs-lookup"><span data-stu-id="1142c-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="1142c-187">Segue un rapido ripasso sull'interazione dei timeout con i tempi di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="1142c-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="1142c-188">Gli aggiornamenti di un dominio di aggiornamento non possono completarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="1142c-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="1142c-189">Un errore di aggiornamento non può verificarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="1142c-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="1142c-190">Il tempo di aggiornamento di un dominio di aggiornamento è limitato da *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="1142c-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="1142c-191">Se i valori di *HealthCheckRetryTimeout* e *HealthCheckStableDuration* sono entrambi diversi da zero e l'integrità dell'applicazione continua a oscillare, si verifica il timeout dell'aggiornamento in *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="1142c-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="1142c-192">*UpgradeDomainTimeout* inizia il conto alla rovescia dopo l'avvio dell'aggiornamento del dominio di aggiornamento corrente.</span><span class="sxs-lookup"><span data-stu-id="1142c-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1142c-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1142c-193">Next steps</span></span>
<span data-ttu-id="1142c-194">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1142c-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="1142c-195">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1142c-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="1142c-196">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="1142c-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="1142c-197">Rendere compatibili gli aggiornamenti dell'applicazione imparando a usare [Serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="1142c-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="1142c-198">Per informazioni su come usare funzionalità avanzate durante l'aggiornamento dell'applicazione, vedere [Argomenti avanzati](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="1142c-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
