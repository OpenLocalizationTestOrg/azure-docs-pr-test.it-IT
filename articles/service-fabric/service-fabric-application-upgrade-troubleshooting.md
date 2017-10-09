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
# <a name="troubleshoot-application-upgrades"></a>Risolvere i problemi relativi agli aggiornamenti delle applicazioni
In questo articolo vengono illustrati alcuni dei problemi comuni di hello intorno a un'applicazione Azure Service Fabric e come tooresolve li.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Risolvere i problemi relativi all'aggiornamento di un'applicazione non riuscito
Quando un aggiornamento non riesce, output di hello di hello **Get-ServiceFabricApplicationUpgrade** comando contiene informazioni aggiuntive per il debug di un errore di hello.  Hello elenco seguente specifica come utilizzare informazioni aggiuntive hello:

1. Identificare il tipo di errore hello.
2. Identificare motivo dell'errore hello.
3. Isolare uno o più componenti che hanno causato l'errore per altre indagini.

Queste informazioni sono disponibili quando Service Fabric rileva gli errori di hello indipendentemente se hello **FailureAction** è tooroll back o sospendere l'aggiornamento di hello.

### <a name="identify-hello-failure-type"></a>Identificare il tipo di errore hello
Nell'output di hello di **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifica hello timestamp (UTC) in corrispondenza del quale è stato rilevato un errore di aggiornamento da Service Fabric e  **FailureAction** è stata attivata. **Motivo dell'errore** identifica uno dei tre possibili cause di alto livello di errore hello:

1. UpgradeDomainTimeout - indica che un particolare dominio di aggiornamento ha impiegato troppo tempo toocomplete e **UpgradeDomainTimeout** scaduto.
2. OverallUpgradeTimeout - indica tale hello aggiornamento complessivo ha impiegato troppo tempo toocomplete e **UpgradeTimeout** scaduto.
3. Controllo integrità - indica che, dopo l'aggiornamento di un dominio di aggiornamento, un'applicazione hello rimasto integro in base toohello specificati criteri di integrità e **HealthCheckRetryTimeout** scaduto.

Queste voci solo visualizzati nell'output di hello quando l'aggiornamento di hello non riesce e viene avviato il rollback. Per ulteriori informazioni viene visualizzate in base al tipo di hello di hello errore.

### <a name="investigate-upgrade-timeouts"></a>Analizzare i timeout di aggiornamento
Gli errori di timeout di aggiornamento si verificano più comunemente a causa di problemi di disponibilità dei servizi. output di Hello dopo il paragrafo è tipico di aggiornamento se le repliche del servizio o le istanze non toostart nella nuova versione del codice hello. Hello **UpgradeDomainProgressAtFailure** campo acquisisce uno snapshot delle operazioni di aggiornamento in sospeso in fase di hello dell'errore.

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

In questo esempio, l'aggiornamento di hello non riuscita nel dominio di aggiornamento *MYUD1* e due partizioni (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* e *4b43f4d8-b26b-424e-9307-7a7a62e79750*) sono stati bloccati. le partizioni Hello sono state bloccate perché il runtime di hello è repliche primarie tooplace non è possibile (*WaitForPrimaryPlacement*) nei nodi di destinazione *Node1* e *Nodo4*.

Hello **Get ServiceFabricNode** comando può essere utilizzato tooverify presenti questi due nodi nel dominio di aggiornamento *MYUD1*. Hello *UpgradePhase* afferma *PostUpgradeSafetyCheck*, il che significa che questi controlli di protezione si verificano dopo avranno completato l'aggiornamento di tutti i nodi nel dominio di aggiornamento hello. Tutte queste informazioni punta tooa potenziale problema con una nuova versione di hello hello del codice dell'applicazione. problemi più comuni di Hello sono hello open o i percorsi del codice promozione tooprimary errori del servizio.

Un *UpgradePhase* di *PreUpgradeSafetyCheck* indica che si sono verificati problemi di preparazione aggiornamento del dominio hello prima è stata eseguita. in questo caso, i problemi più comuni di Hello sono errori del servizio in hello chiudere o abbassamento di livello da percorsi del codice principale.

Hello corrente **UpgradeState** è *RollingBackCompleted*, pertanto l'aggiornamento originale hello è stata eseguita con un rollback **FailureAction**, che automaticamente aggiornamento di hello in caso di errore il rollback. Se l'aggiornamento originale hello è stata eseguita con un manuale **FailureAction**, l'aggiornamento di hello sarà invece in una tooallow stato sospeso in tempo reale il debug di un'applicazione hello.

### <a name="investigate-health-check-failures"></a>Analizzare gli errori di controllo dell'integrità
Gli errori di controllo dell'integrità possono essere attivati da vari problemi che possono verificarsi dopo l'aggiornamento di tutti i nodi di un dominio di aggiornamento e dopo aver superato tutti i controlli di sicurezza. output di Hello dopo il paragrafo è tipica di un aggiornamento non riuscito a causa di controlli di integrità toofailed. Hello **UnhealthyEvaluations** campo acquisisce uno snapshot di controlli di integrità che non è in fase di aggiornamento hello in base toohello specificato di hello [criteri di integrità](service-fabric-health-introduction.md).

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

Ricercando la causa di errori di controllo di integrità prima richiede la comprensione del modello di integrità di Service Fabric hello. Ma anche in assenza di tali una conoscenza approfondita, si noterà che i due servizi sono integri: *fabric: / DemoApp/Svc3* e *fabric: / DemoApp/Svc2*, insieme ai rapporti di stato di errore hello ("InjectedFault "in questo caso). In questo esempio, due dei quattro servizi non sono integri, che è di sotto di destinazione predefinita hello pari a 0% Integro (*MaxPercentUnhealthyServices*).

Hello aggiornamento è stato sospeso dopo errori specificando un **FailureAction** When manuale avvio hello l'aggiornamento. Questa modalità consente tooinvestigate sistema in tempo reale di hello in stato non è stato possibile hello prima di eseguire ulteriori azioni.

### <a name="recover-from-a-suspended-upgrade"></a>Eseguire il ripristino da un aggiornamento sospeso
Con un'operazione di rollback **FailureAction**, non è recupero non è necessaria perché l'aggiornamento di hello automaticamente il rollback al failover. Con una proprietà **FailureAction**impostata per l'azione manuale invece sono disponibili diverse opzioni di ripristino:

1.  attivare un rollback
2. Procedere con il resto di hello dell'aggiornamento hello manualmente
3. Aggiornamento di monitoraggio hello Resume

Hello **inizio ServiceFabricApplicationRollback** comando può essere utilizzato in qualsiasi toostart ora eseguire il rollback di un'applicazione hello. Comando hello restituisce correttamente, richiesta di rollback hello è stato registrato nel sistema hello e avvia dopo poco tempo.

Hello **Resume-ServiceFabricApplicationUpgrade** comando può essere utilizzato tooproceed attraverso il resto di hello di hello manualmente, aggiornare un dominio di aggiornamento alla volta. In questa modalità, vengono eseguiti controlli di sicurezza solo dal sistema hello. Non viene eseguito alcun controllo di integrità. Questo comando può essere utilizzato solo quando hello *UpgradeState* Mostra *RollingForwardPending*, ovvero il dominio di aggiornamento corrente di hello ha completato l'aggiornamento ma hello successivamente uno non è stato avviato (in sospeso).

Hello **aggiornamento ServiceFabricApplicationUpgrade** comando può essere utilizzato tooresume hello monitorato aggiornamento con i controlli di sicurezza e di salute in corso.

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

aggiornamento di Hello continua dal dominio di aggiornamento hello in cui era stata sospesa e utilizzare hello stesso aggiornare i parametri e i criteri di integrità come prima. Se necessario, tutti i parametri di aggiornamento hello e criteri di integrità mostrati nella precedente l'output di hello può essere modificato in hello stesso comando quando viene riattivato l'aggiornamento di hello. In questo esempio, l'aggiornamento di hello è stata ripresa in modalità di monitoraggio, con i parametri di hello e criteri di integrità hello invariati.

## <a name="further-troubleshooting"></a>Risoluzione di altri problemi
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric non è seguito hello specificato criteri di integrità
Possibile causa 1:

Service Fabric converte tutte le percentuali nei valori effettivi delle entità (ad esempio, partizioni e repliche services) per la valutazione dell'integrità e arrotonda sempre toowhole entità. Ad esempio, se hello massimo *MaxPercentUnhealthyReplicasPerPartition* è % 21 e sono disponibili cinque repliche, quindi Service Fabric consente backup delle repliche di tipo non integro tootwo (vale a dire`Math.Ceiling (5*0.21)`). Perciò, i criteri di integrità devono essere impostati in modo da tenere conto di questo.

Possibile causa 2:

I criteri di integrità sono specificati in termini di percentuali dei servizi totali e non di specifiche istanze di servizi. Ad esempio, prima di un aggiornamento, se un'applicazione dispone di quattro istanze A, B, C e D, del servizio in cui servizio D non è integro, ma con applicazione toohello impatto. Vogliamo hello tooignore noto servizio integro D durante il parametro di aggiornamento e impostare hello *MaxPercentUnhealthyServices* toobe 25%, presupponendo che solo A, B e C necessario toobe integro.

Tuttavia, durante l'aggiornamento di hello, D possono diventare integra mentre C diventa non integro. l'aggiornamento di Hello comunque esito positivo perché solo il 25% dei servizi di hello non sono integri. Tuttavia, ma potrebbe causare errori imprevisti dovuti tooC viene inaspettatamente integri anziché D. In questo caso, D deve essere modellata come un tipo di servizio diverso da A, B e C. Poiché per ogni tipo di servizio vengono specificati i criteri di integrità, soglie di percentuale non integro diversi possono essere applicati toodifferent servizi. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Non ha specificato un criterio di integrità per l'aggiornamento dell'applicazione, ma l'aggiornamento di hello non riesce ancora alcuni valori di timeout non specificato
Quando i criteri di integrità non sono forniti toohello richiesta di aggiornamento, essi vengono prelevati hello *ApplicationManifest.xml* della versione corrente dell'applicazione hello. Ad esempio, se si esegue l'aggiornamento dell'applicazione X dalla versione 1.0 tooversion 2.0, vengono utilizzati criteri di integrità dell'applicazione specificati per nella versione 1.0. Se un criterio di integrità diverso deve essere utilizzato per l'aggiornamento di hello, i criteri di hello devono toobe specificato come parte della chiamata all'API aggiornamento applicazione hello. Hello specificati come parte della chiamata API hello criteri si applicano solo durante l'aggiornamento di hello. Una volta completato l'aggiornamento di hello, i criteri di hello specificati in hello *ApplicationManifest.xml* vengono utilizzati.

### <a name="incorrect-time-outs-are-specified"></a>Sono stati specificati timeout non corretti
Ci si potrebbe chiedere cosa succede quando i timeout sono impostati in modo incoerente. Ad esempio, si potrebbe avere un *UpgradeTimeout* è minore di hello *UpgradeDomainTimeout*. risposte Hello sono che viene restituito un errore. Gli errori vengono restituiti se hello *UpgradeDomainTimeout* è minore di somma hello *HealthCheckWaitDuration* e *HealthCheckRetryTimeout*, o se  *UpgradeDomainTimeout* è minore di somma hello *HealthCheckWaitDuration* e *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>Gli aggiornamenti richiedono troppo tempo
tempo Hello per un aggiornamento toocomplete dipende dai controlli di integrità hello e valori di timeout specificati. Controlli di integrità e i timeout dipendono da quanto tempo servirebbe toocopy, distribuire e stabilizzano applicazione hello. L'uso di timeout eccessivamente rigidi può comportare un numero elevato di aggiornamenti non riusciti. È quindi consigliabile iniziare prudenzialmente con valori di timeout più lunghi.

Ecco un rapido promemoria sulle modalità di interazione con i tempi di aggiornamento hello timeout hello:

Gli aggiornamenti di un dominio di aggiornamento non possono completarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckStableDuration*.

Un errore di aggiornamento non può verificarsi in tempi più rapidi della somma dei valori di *HealthCheckWaitDuration*  +  *HealthCheckRetryTimeout*.

Hello tempi di aggiornamento per un dominio di aggiornamento sono limitato dalla *UpgradeDomainTimeout*.  Se *HealthCheckRetryTimeout* e *HealthCheckStableDuration* sono entrambi diverso da zero e l'integrità hello di un'applicazione hello mantiene cambio avanti e indietro, quindi l'aggiornamento di hello alla fine scade in  *UpgradeDomainTimeout*. *UpgradeDomainTimeout* inizia una volta hello aggiornamento per il dominio di aggiornamento corrente di hello inizia.

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).
