---
title: gli aggiornamenti dell'applicazione aaaTroubleshooting | Documenti Microsoft
description: In questo articolo vengono descritti alcuni problemi comuni intorno a un'applicazione di Service Fabric e come tooresolve li.
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
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="63270-103">Risolvere i problemi relativi agli aggiornamenti delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="63270-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="63270-104">In questo articolo vengono illustrati alcuni dei problemi comuni di hello intorno a un'applicazione Azure Service Fabric e come tooresolve li.</span><span class="sxs-lookup"><span data-stu-id="63270-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="63270-105">Risolvere i problemi relativi all'aggiornamento di un'applicazione non riuscito</span><span class="sxs-lookup"><span data-stu-id="63270-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="63270-106">Quando un aggiornamento non riesce, output di hello di hello **Get-ServiceFabricApplicationUpgrade** comando contiene informazioni aggiuntive per il debug di un errore di hello.</span><span class="sxs-lookup"><span data-stu-id="63270-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="63270-107">Hello elenco seguente specifica come utilizzare informazioni aggiuntive hello:</span><span class="sxs-lookup"><span data-stu-id="63270-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="63270-108">Identificare il tipo di errore hello.</span><span class="sxs-lookup"><span data-stu-id="63270-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="63270-109">Identificare motivo dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="63270-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="63270-110">Isolare uno o più componenti che hanno causato l'errore per altre indagini.</span><span class="sxs-lookup"><span data-stu-id="63270-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="63270-111">Queste informazioni sono disponibili quando Service Fabric rileva gli errori di hello indipendentemente se hello **FailureAction** è tooroll back o sospendere l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="63270-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="63270-112">Identificare il tipo di errore hello</span><span class="sxs-lookup"><span data-stu-id="63270-112">Identify hello failure type</span></span>
<span data-ttu-id="63270-113">Nell'output di hello di **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica hello timestamp (UTC) in corrispondenza del quale è stato rilevato un errore di aggiornamento da Service Fabric e  **FailureAction** è stata attivata.</span><span class="sxs-lookup"><span data-stu-id="63270-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="63270-114">**Motivo dell'errore** identifica uno dei tre possibili cause di alto livello di errore hello:</span><span class="sxs-lookup"><span data-stu-id="63270-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="63270-115">UpgradeDomainTimeout - indica che un particolare dominio di aggiornamento ha impiegato troppo tempo toocomplete e **UpgradeDomainTimeout** scaduto.</span><span class="sxs-lookup"><span data-stu-id="63270-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="63270-116">OverallUpgradeTimeout - indica tale hello aggiornamento complessivo ha impiegato troppo tempo toocomplete e **UpgradeTimeout** scaduto.</span><span class="sxs-lookup"><span data-stu-id="63270-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="63270-117">Controllo integrità - indica che, dopo l'aggiornamento di un dominio di aggiornamento, un'applicazione hello rimasto integro in base toohello specificati criteri di integrità e **HealthCheckRetryTimeout** scaduto.</span><span class="sxs-lookup"><span data-stu-id="63270-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="63270-118">Queste voci solo visualizzati nell'output di hello quando l'aggiornamento di hello non riesce e viene avviato il rollback.</span><span class="sxs-lookup"><span data-stu-id="63270-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="63270-119">Per ulteriori informazioni viene visualizzate in base al tipo di hello di hello errore.</span><span class="sxs-lookup"><span data-stu-id="63270-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="63270-120">Analizzare i timeout di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="63270-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="63270-121">Gli errori di timeout di aggiornamento si verificano più comunemente a causa di problemi di disponibilità dei servizi.</span><span class="sxs-lookup"><span data-stu-id="63270-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="63270-122">output di Hello dopo il paragrafo è tipico di aggiornamento se le repliche del servizio o le istanze non toostart nella nuova versione del codice hello.</span><span class="sxs-lookup"><span data-stu-id="63270-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="63270-123">Hello **UpgradeDomainProgressAtFailure** campo acquisisce uno snapshot delle operazioni di aggiornamento in sospeso in fase di hello dell'errore.</span><span class="sxs-lookup"><span data-stu-id="63270-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

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

<span data-ttu-id="63270-124">In questo esempio, l'aggiornamento di hello non riuscita nel dominio di aggiornamento *MYUD1* e due partizioni (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) sono stati bloccati.</span><span class="sxs-lookup"><span data-stu-id="63270-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="63270-125">le partizioni Hello sono state bloccate perché il runtime di hello è repliche primarie tooplace non è possibile (*WaitForPrimaryPlacement*) nei nodi di destinazione *Node1* e *Nodo4*.</span><span class="sxs-lookup"><span data-stu-id="63270-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="63270-126">Hello **Get ServiceFabricNode** comando può essere utilizzato tooverify presenti questi due nodi nel dominio di aggiornamento *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="63270-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="63270-127">Hello *UpgradePhase* afferma *PostUpgradeSafetyCheck*, il che significa che questi controlli di protezione si verificano dopo avranno completato l'aggiornamento di tutti i nodi nel dominio di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="63270-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="63270-128">Tutte queste informazioni punta tooa potenziale problema con una nuova versione di hello hello del codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="63270-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="63270-129">problemi più comuni di Hello sono hello open o i percorsi del codice promozione tooprimary errori del servizio.</span><span class="sxs-lookup"><span data-stu-id="63270-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="63270-130">Un *UpgradePhase* di *PreUpgradeSafetyCheck* indica che si sono verificati problemi di preparazione aggiornamento del dominio hello prima è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="63270-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="63270-131">in questo caso, i problemi più comuni di Hello sono errori del servizio in hello chiudere o abbassamento di livello da percorsi del codice principale.</span><span class="sxs-lookup"><span data-stu-id="63270-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="63270-132">Hello corrente **UpgradeState** è *RollingBackCompleted*, pertanto l'aggiornamento originale hello è stata eseguita con un rollback **FailureAction**, che automaticamente aggiornamento di hello in caso di errore il rollback.</span><span class="sxs-lookup"><span data-stu-id="63270-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="63270-133">Se l'aggiornamento originale hello è stata eseguita con un manuale **FailureAction**, l'aggiornamento di hello sarà invece in una tooallow stato sospeso in tempo reale il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63270-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="63270-134">Analizzare gli errori di controllo dell'integrità</span><span class="sxs-lookup"><span data-stu-id="63270-134">Investigate health check failures</span></span>
<span data-ttu-id="63270-135">Gli errori di controllo dell'integrità possono essere attivati da vari problemi che possono verificarsi dopo l'aggiornamento di tutti i nodi di un dominio di aggiornamento e dopo aver superato tutti i controlli di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="63270-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="63270-136">output di Hello dopo il paragrafo è tipica di un aggiornamento non riuscito a causa di controlli di integrità toofailed.</span><span class="sxs-lookup"><span data-stu-id="63270-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="63270-137">Hello **UnhealthyEvaluations** campo acquisisce uno snapshot di controlli di integrità che non è in fase di aggiornamento hello in base toohello specificato di hello [criteri di integrità](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="63270-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="63270-138">Ricercando la causa di errori di controllo di integrità prima richiede la comprensione del modello di integrità di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="63270-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="63270-139">Ma anche in assenza di tali una conoscenza approfondita, si noterà che i due servizi sono integri: *fabric: / DemoApp/Svc3* e *fabric: / DemoApp/Svc2*, insieme ai rapporti di stato di errore hello ("InjectedFault "in questo caso).</span><span class="sxs-lookup"><span data-stu-id="63270-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="63270-140">In questo esempio, due dei quattro servizi non sono integri, che è di sotto di destinazione predefinita hello pari a 0% Integro (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="63270-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="63270-141">Hello aggiornamento è stato sospeso dopo errori specificando un **FailureAction** When manuale avvio hello l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="63270-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="63270-142">Questa modalità consente tooinvestigate sistema in tempo reale di hello in stato non è stato possibile hello prima di eseguire ulteriori azioni.</span><span class="sxs-lookup"><span data-stu-id="63270-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="63270-143">Eseguire il ripristino da un aggiornamento sospeso</span><span class="sxs-lookup"><span data-stu-id="63270-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="63270-144">Con un'operazione di rollback **FailureAction**, non è recupero non è necessaria perché l'aggiornamento di hello automaticamente il rollback al failover.</span><span class="sxs-lookup"><span data-stu-id="63270-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="63270-145">Con una proprietà **FailureAction**impostata per l'azione manuale invece sono disponibili diverse opzioni di ripristino:</span><span class="sxs-lookup"><span data-stu-id="63270-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="63270-146">attivare un rollback</span><span class="sxs-lookup"><span data-stu-id="63270-146">trigger a rollback</span></span>
2. <span data-ttu-id="63270-147">Procedere con il resto di hello dell'aggiornamento hello manualmente</span><span class="sxs-lookup"><span data-stu-id="63270-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="63270-148">Aggiornamento di monitoraggio hello Resume</span><span class="sxs-lookup"><span data-stu-id="63270-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="63270-149">Hello **inizio ServiceFabricApplicationRollback** comando può essere utilizzato in qualsiasi toostart ora eseguire il rollback di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63270-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="63270-150">Comando hello restituisce correttamente, richiesta di rollback hello è stato registrato nel sistema hello e avvia dopo poco tempo.</span><span class="sxs-lookup"><span data-stu-id="63270-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="63270-151">Hello **Resume-ServiceFabricApplicationUpgrade** comando può essere utilizzato tooproceed attraverso il resto di hello di hello manualmente, aggiornare un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="63270-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="63270-152">In questa modalità, vengono eseguiti controlli di sicurezza solo dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="63270-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="63270-153">Non viene eseguito alcun controllo di integrità.</span><span class="sxs-lookup"><span data-stu-id="63270-153">No more health checks are performed.</span></span> <span data-ttu-id="63270-154">Questo comando può essere utilizzato solo quando hello *UpgradeState* Mostra *RollingForwardPending*, ovvero il dominio di aggiornamento corrente di hello ha completato l'aggiornamento ma hello successivamente uno non è stato avviato (in sospeso).</span><span class="sxs-lookup"><span data-stu-id="63270-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="63270-155">Hello **aggiornamento ServiceFabricApplicationUpgrade** comando può essere utilizzato tooresume hello monitorato aggiornamento con i controlli di sicurezza e di salute in corso.</span><span class="sxs-lookup"><span data-stu-id="63270-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="63270-156">aggiornamento di Hello continua dal dominio di aggiornamento hello in cui era stata sospesa e utilizzare hello stesso aggiornare i parametri e i criteri di integrità come prima.</span><span class="sxs-lookup"><span data-stu-id="63270-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="63270-157">Se necessario, tutti i parametri di aggiornamento hello e criteri di integrità mostrati nella precedente l'output di hello può essere modificato in hello stesso comando quando viene riattivato l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="63270-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="63270-158">In questo esempio, l'aggiornamento di hello è stata ripresa in modalità di monitoraggio, con i parametri di hello e criteri di integrità hello invariati.</span><span class="sxs-lookup"><span data-stu-id="63270-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="63270-159">Risoluzione di altri problemi</span><span class="sxs-lookup"><span data-stu-id="63270-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="63270-160">Service Fabric non è seguito hello specificato criteri di integrità</span><span class="sxs-lookup"><span data-stu-id="63270-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="63270-161">Possibile causa 1:</span><span class="sxs-lookup"><span data-stu-id="63270-161">Possible Cause 1:</span></span>

<span data-ttu-id="63270-162">Service Fabric converte tutte le percentuali nei valori effettivi delle entità (ad esempio, partizioni e repliche services) per la valutazione dell'integrità e arrotonda sempre toowhole entità.</span><span class="sxs-lookup"><span data-stu-id="63270-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="63270-163">Ad esempio, se hello massimo *MaxPercentUnhealthyReplicasPerPartition* è % 21 e sono disponibili cinque repliche, quindi Service Fabric consente backup delle repliche di tipo non integro tootwo (vale a dire`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="63270-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="63270-164">Perciò, i criteri di integrità devono essere impostati in modo da tenere conto di questo.</span><span class="sxs-lookup"><span data-stu-id="63270-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="63270-165">Possibile causa 2:</span><span class="sxs-lookup"><span data-stu-id="63270-165">Possible Cause 2:</span></span>

<span data-ttu-id="63270-166">I criteri di integrità sono specificati in termini di percentuali dei servizi totali e non di specifiche istanze di servizi.</span><span class="sxs-lookup"><span data-stu-id="63270-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="63270-167">Ad esempio, prima di un aggiornamento, se un'applicazione dispone di quattro istanze A, B, C e D, del servizio in cui servizio D non è integro, ma con applicazione toohello impatto.</span><span class="sxs-lookup"><span data-stu-id="63270-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="63270-168">Vogliamo hello tooignore noto servizio integro D durante il parametro di aggiornamento e impostare hello *MaxPercentUnhealthyServices* toobe 25%, presupponendo che solo A, B e C necessario toobe integro.</span><span class="sxs-lookup"><span data-stu-id="63270-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="63270-169">Tuttavia, durante l'aggiornamento di hello, D possono diventare integra mentre C diventa non integro.</span><span class="sxs-lookup"><span data-stu-id="63270-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="63270-170">l'aggiornamento di Hello comunque esito positivo perché solo il 25% dei servizi di hello non sono integri.</span><span class="sxs-lookup"><span data-stu-id="63270-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="63270-171">Tuttavia, ma potrebbe causare errori imprevisti dovuti tooC viene inaspettatamente integri anziché D. In questo caso, D deve essere modellata come un tipo di servizio diverso da A, B e C. Poiché per ogni tipo di servizio vengono specificati i criteri di integrità, soglie di percentuale non integro diversi possono essere applicati toodifferent servizi.</span><span class="sxs-lookup"><span data-stu-id="63270-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="63270-172">Non ha specificato un criterio di integrità per l'aggiornamento dell'applicazione, ma l'aggiornamento di hello non riesce ancora alcuni valori di timeout non specificato</span><span class="sxs-lookup"><span data-stu-id="63270-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="63270-173">Quando i criteri di integrità non sono forniti toohello richiesta di aggiornamento, essi vengono prelevati hello *ApplicationManifest.xml* della versione corrente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63270-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="63270-174">Ad esempio, se si esegue l'aggiornamento dell'applicazione X dalla versione 1.0 tooversion 2.0, vengono utilizzati criteri di integrità dell'applicazione specificati per nella versione 1.0.</span><span class="sxs-lookup"><span data-stu-id="63270-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="63270-175">Se un criterio di integrità diverso deve essere utilizzato per l'aggiornamento di hello, i criteri di hello devono toobe specificato come parte della chiamata all'API aggiornamento applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63270-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="63270-176">Hello specificati come parte della chiamata API hello criteri si applicano solo durante l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="63270-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="63270-177">Una volta completato l'aggiornamento di hello, i criteri di hello specificati in hello *ApplicationManifest.xml* vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="63270-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="63270-178">Sono stati specificati timeout non corretti</span><span class="sxs-lookup"><span data-stu-id="63270-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="63270-179">Ci si potrebbe chiedere cosa succede quando i timeout sono impostati in modo incoerente.</span><span class="sxs-lookup"><span data-stu-id="63270-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="63270-180">Ad esempio, si potrebbe avere un *UpgradeTimeout* è minore di hello *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="63270-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="63270-181">risposte Hello sono che viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="63270-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="63270-182">Gli errori vengono restituiti se hello *UpgradeDomainTimeout* è minore di somma hello *HealthCheckWaitDuration* e *HealthCheckRetryTimeout*, o se  *UpgradeDomainTimeout* è minore di somma hello *HealthCheckWaitDuration* e *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="63270-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="63270-183">Gli aggiornamenti richiedono troppo tempo</span><span class="sxs-lookup"><span data-stu-id="63270-183">My upgrades are taking too long</span></span>
<span data-ttu-id="63270-184">tempo Hello per un aggiornamento toocomplete dipende dai controlli di integrità hello e valori di timeout specificati.</span><span class="sxs-lookup"><span data-stu-id="63270-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="63270-185">Controlli di integrità e i timeout dipendono da quanto tempo servirebbe toocopy, distribuire e stabilizzano applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="63270-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="63270-186">L'uso di timeout eccessivamente rigidi può comportare un numero elevato di aggiornamenti non riusciti. È quindi consigliabile iniziare prudenzialmente con valori di timeout più lunghi.</span><span class="sxs-lookup"><span data-stu-id="63270-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="63270-187">Ecco un rapido promemoria sulle modalità di interazione con i tempi di aggiornamento hello timeout hello:</span><span class="sxs-lookup"><span data-stu-id="63270-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="63270-188">Gli aggiornamenti di un dominio di aggiornamento non possono completarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="63270-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="63270-189">Un errore di aggiornamento non può verificarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="63270-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="63270-190">Hello tempi di aggiornamento per un dominio di aggiornamento sono limitato dalla *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="63270-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="63270-191">Se *HealthCheckRetryTimeout* e *HealthCheckStableDuration* sono entrambi diverso da zero e l'integrità hello di un'applicazione hello mantiene cambio avanti e indietro, quindi l'aggiornamento di hello alla fine scade in  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="63270-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="63270-192">*UpgradeDomainTimeout* inizia una volta hello aggiornamento per il dominio di aggiornamento corrente di hello inizia.</span><span class="sxs-lookup"><span data-stu-id="63270-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63270-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63270-193">Next steps</span></span>
<span data-ttu-id="63270-194">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63270-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="63270-195">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63270-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="63270-196">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="63270-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="63270-197">Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="63270-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="63270-198">Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="63270-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
