---
title: 'Aggiornamento di un''applicazione: parametri di aggiornamento | Documentazione Microsoft'
description: Descrive i parametri correlati tooupgrading un'applicazione di Service Fabric, incluso stato controlli tooperform e criteri tooautomatically annullamento hello aggiornamento.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Parametri di aggiornamento di un'applicazione
Questo articolo descrive i vari parametri che si applicano hello durante l'aggiornamento di un'applicazione Azure Service Fabric hello. parametri di Hello includono hello nome e la versione dell'applicazione hello. Sono manopole che controllano i timeout hello e controlli di integrità che vengono applicati durante l'aggiornamento di hello e specificano i criteri di hello che devono essere applicati quando un aggiornamento non riesce.

<br>

| . | Descrizione |
| --- | --- |
| ApplicationName |Nome dell'applicazione hello che viene aggiornata. Esempi: fabric:/VisualObjects, fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |versione di Hello del tipo di applicazione hello hello destinazioni di aggiornamento. |
| FailureAction |azione di Hello eseguita da Service Fabric quando hello aggiornamento ha esito negativo. un'applicazione Hello può essere eseguito il rollback versione pre-aggiornamento toohello (ripristino) o l'aggiornamento di hello potrebbe essere stato arrestato nel dominio di aggiornamento corrente hello. In quest'ultimo caso hello, la modalità di aggiornamento hello è tooManual modificato. I valori consentiti sono Rollback e Manual. |
| HealthCheckWaitDurationSec |prima di Service Fabric valuta l'integrità di hello di un'applicazione hello, Hello toowait di tempo (in secondi) dopo l'aggiornamento di hello è stata completata nel dominio di aggiornamento hello. Questa durata può anche essere considerata come tempo hello che un'applicazione deve essere in esecuzione prima che può essere considerato integro. Se viene superato il controllo di integrità hello, hello aggiornamento procede toohello dominio di aggiornamento successivo.  Se il controllo di integrità hello non riesce, Service Fabric attende per un intervallo (Buongiorno UpgradeHealthCheckInterval) prima di eseguire nuovamente il controllo di integrità hello finché viene raggiunto HealthCheckRetryTimeout hello. valore predefinito di Hello e un valore consigliato è 0 secondi. |
| HealthCheckRetryTimeoutSec |durata di Hello (in secondi) di Service Fabric continua tooperform valutazione dell'integrità prima di dichiarare l'aggiornamento di hello come non riuscita. valore predefinito di Hello è 600 secondi. Il calcolo del tempo inizia dopo che viene raggiunto il valore definito da HealthCheckWaitDuration. All'interno di questo HealthCheckRetryTimeout, Service Fabric potrebbe eseguire più controlli di integrità dell'integrità delle applicazioni hello. valore predefinito di Hello è 10 minuti e deve essere personalizzato in modo appropriato per l'applicazione. |
| HealthCheckStableDurationSec |Hello tooverify di durata (in secondi) che un'applicazione hello è stabile prima mobile dominio di aggiornamento successivo toohello o completamento hello l'aggiornamento. Questo periodo di attesa è utilizzato tooprevent non viene rilevata modifiche di integrità destra dopo l'esecuzione della verifica integrità hello. valore predefinito di Hello è 120 secondi e deve essere personalizzato in modo appropriato per l'applicazione. |
| UpgradeDomainTimeoutSec |Tempo massimo (in secondi) per l'aggiornamento di un singolo dominio di aggiornamento. Se viene raggiunto questo timeout, l'aggiornamento di hello viene arrestata e continua in base alle impostazioni di hello per UpgradeFailureAction. valore predefinito di Hello non è mai (infinito) e deve essere personalizzato in modo appropriato per l'applicazione. |
| UpgradeTimeout |Timeout (in secondi) che viene applicata per l'aggiornamento dell'intero hello. Se viene raggiunto questo timeout, hello aggiornamento si interrompe e viene attivato UpgradeFailureAction. valore predefinito di Hello non è mai (infinito) e deve essere personalizzato in modo appropriato per l'applicazione. |
| UpgradeHealthCheckInterval |frequenza di Hello che viene controllato lo stato di integrità di hello. Questo parametro viene specificato nella sezione ClusterManager di hello hello *cluster* *manifesto*e non è specificato come parte del cmdlet di aggiornamento hello. valore predefinito di Hello è 60 secondi. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Valutazione dell'integrità di un servizio durante l'aggiornamento dell'applicazione
<br>
criteri di valutazione salute Hello sono facoltativi. Se i criteri di valutazione salute hello non vengono specificati quando si avvia un aggiornamento, Service Fabric utilizza criteri di integrità dell'applicazione hello specificati in ApplicationManifest.xml dell'istanza dell'applicazione hello hello.

<br>

| . | Descrizione |
| --- | --- |
| ConsiderWarningAsError |Il valore predefinito è False. Considera gli eventi di integrità di avviso hello per un'applicazione hello come errori durante la valutazione salute hello di un'applicazione hello durante l'aggiornamento. Per impostazione predefinita, Service Fabric non valuta (errori), gli errori toobe eventi dello stato di avviso hello aggiornamento può continuare anche se sono presenti eventi di avviso. |
| MaxPercentUnhealthyDeployedApplications |Il valore predefinito e consigliato è 0. Specificare il numero massimo di hello delle applicazioni distribuite (vedere hello [sezione integrità](service-fabric-health-introduction.md)) che può essere integro prima di un'applicazione hello viene considerata non integra e l'aggiornamento di hello ha esito negativo. Questo parametro definisce l'integrità dell'applicazione hello nel nodo hello e consente di rilevare problemi durante l'aggiornamento. In genere, le repliche di hello di un'applicazione hello ottenere toohello con bilanciamento del carico altro nodo, che consente di tooappear applicazione hello integro, consentendo in tal modo tooproceed aggiornamento hello. Specificando un integrità MaxPercentUnhealthyDeployedApplications strict, Service Fabric è possibile individuare rapidamente un problema con il pacchetto di applicazione hello e aiutare a produrre un errore di aggiornamento rapido. |
| MaxPercentUnhealthyServices |Il valore predefinito e consigliato è 0. Specificare il numero massimo di hello dei servizi nell'istanza di applicazione hello che può essere integro prima di un'applicazione hello viene considerata non integra e si verifica un errore di aggiornamento hello. |
| MaxPercentUnhealthyPartitionsPerService |Il valore predefinito e consigliato è 0. Specificare il numero massimo di hello di partizioni in un servizio che può essere problematico prima che il servizio hello viene considerato non integro. |
| MaxPercentUnhealthyReplicasPerPartition |Il valore predefinito e consigliato è 0. Specificare il numero massimo di hello delle repliche nella partizione che può essere problematico prima partizione hello viene considerato non integro. |
| UpgradeReplicaSetCheckTimeout |**Servizio senza stato**-all'interno di un singolo dominio di aggiornamento, Service Fabric tenta tooensure che sono disponibili istanze aggiuntive di servizio hello. Se più di un numero di istanze di destinazione hello è Service Fabric attende più toobe di istanza disponibile, il valore di timeout massimo tooa. Questo timeout viene specificato tramite la proprietà UpgradeReplicaSetCheckTimeout hello. Se hello timeout scade, Service Fabric prosegue con l'aggiornamento di hello, indipendentemente dal numero di hello istanze del servizio. Se il numero di istanze di destinazione hello è uno, Service Fabric non attendere e procede immediatamente con l'aggiornamento di hello. **Servizio con stato**-all'interno di un singolo dominio di aggiornamento, Service Fabric tenta tooensure che hello replica set dispone di un quorum. Service Fabric in attesa di un quorum toobe disponibile, il valore di timeout massimo tooa (specificato dalla proprietà UpgradeReplicaSetCheckTimeout hello). Se hello timeout scade, Service Fabric prosegue con l'aggiornamento di hello, indipendentemente dal fatto di quorum. Questa impostazione è "mai" (infinito) per il roll forward e 900 secondi per il rollback. |
| ForceRestart |Se si aggiorna una configurazione o un pacchetto di dati senza aggiornare il codice di servizio hello, hello servizio riavviato solo se la proprietà ForceRestart hello è impostato tootrue. Al termine aggiornamento hello, Service Fabric notifica al servizio di hello che sia disponibile un nuovo pacchetto di configurazione o di un pacchetto di dati. servizio Hello è responsabile per l'applicazione delle modifiche hello. Se necessario, possibile riavviare il servizio hello stesso. |

<br>
<br>
Hello MaxPercentUnhealthyServices MaxPercentUnhealthyPartitionsPerService e MaxPercentUnhealthyReplicasPerPartition possono essere specificati per ogni tipo di servizio per un'istanza dell'applicazione. L'impostazione di questi parametri per ogni servizio consente tipi con i criteri di valutazione diversi per servizi diversi di toocontain un'applicazione. Ad esempio, un tipo di servizio gateway senza stato può avere un parametro MaxPercentUnhealthyPartitionsPerService diverso da un tipo di servizio motore con stato per una specifica istanza dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

[Aggiornamento dell'applicazione](service-fabric-application-lifecycle-sfctl.md#upgrade-application) descrive la procedura di aggiornamento di un'applicazione con l'interfaccia della riga di comando di Service Fabric.

[Aggiornamento dell'applicazione con il plug-in Eclipse per Service Fabric](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).
