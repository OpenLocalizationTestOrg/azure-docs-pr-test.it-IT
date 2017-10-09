---
title: aaaInduce Chaos nell'infrastruttura del servizio cluster | Documenti Microsoft
description: Utilizzo di attacco intrusivo nel codice di errore e l'API dei servizi Cluster Analysis toomanage Chaos cluster hello.
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Eseguire Chaos in ambiente controllato nei cluster di Service Fabric
I sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili. Azure Service Fabric consente agli sviluppatori toowrite affidabili servizi distribuiti su un'infrastruttura affidabile. toowrite affidabili servizi distribuiti su un'infrastruttura affidabile, gli sviluppatori devono stabilità di hello in grado di tootest toobe dei servizi mentre hello inaffidabile infrastruttura sottostante viene eseguita tramite le transizioni di stato complicato toofaults scadenza.

Hello [attacco intrusivo nel codice di errore e il servizio Cluster Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (noto anche come hello errore Analysis Services) consente agli sviluppatori hello tooinduce errori tootest i propri servizi. Questi destinazione simulato gli errori, ad esempio [il riavvio di una partizione](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), consentono di esercitare transizioni più comuni di hello. Gli errori simulati mirati sono tuttavia parziali per definizione e quindi possono non coprire i bug che si verificano solo in sequenze di transizioni di stato difficili da prevedere, lunghe e complesse. Per un test imparziale, è possibile usare Chaos.

CHAOS simula errori periodici interleaved (normale e anomali) in cluster hello per periodi prolungati di tempo. Dopo aver configurato caos con frequenza hello e tipo hello degli errori, è possibile avviare Chaos tramite c# o Powershell API toostart generazione di errori nel cluster hello e nei servizi. È possibile configurare Chaos toorun per un periodo di tempo specificato (ad esempio, per un'ora), dopo il quale viene interrotto automaticamente, Chaos oppure è possibile chiamare toostop StopChaos API (in c# o Powershell) in qualsiasi momento.

> [!NOTE]
> Nella sua forma corrente, Chaos provoca errori solo sicuri, che implica che in assenza di hello errori esterni di una perdita del quorum o perdita di dati si verifica mai.
>

Durante l'esecuzione Chaos, genera eventi diversi che consentono di acquisire lo stato di hello di eseguire un determinato momento hello hello. Ad esempio, un ExecutingFaultsEvent contiene tutti gli errori di hello Chaos ha deciso di tooexecute in quell'iterazione. Un ValidationFailedEvent contiene i dettagli di hello di un errore di convalida (problemi di integrità o stabilità) che è stato trovato durante la convalida di hello del cluster di hello. È possibile richiamare hello GetChaosReport API (in c# o Powershell) tooget hello report viene eseguito Chaos. Gli eventi vengono conservati in un oggetto [Reliable ​Dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), che ha un criterio di troncamento influenzato da due configurazioni: **MaxStoredChaosEventCount** (valore predefinito 25000) e **StoredActionCleanupIntervalInSeconds** (valore predefinito 3600). Ogni *StoredActionCleanupIntervalInSeconds* controlli Chaos e tutti i ma hello più recente *MaxStoredChaosEventCount* eventi, vengono eliminati dal dizionario di hello affidabile.

## <a name="faults-induced-in-chaos"></a>Errori indotti da Chaos
CHAOS genera errori nel cluster di Service Fabric intera hello e comprime gli errori che sono visibili in mesi o anni in poche ore. combinazione di Hello di interfoliazione errori con frequenza elevata errore hello consente di trovare casi estremi che in caso contrario potrebbero essere perso. Questo esercizio di Chaos lead tooa significativo miglioramento nella qualità del codice del servizio hello hello.

CHAOS provoca errori da hello seguenti categorie:

* Riavvio di un nodo
* Riavvio di un pacchetto di codice distribuito
* Rimozione di una replica
* Riavvio di una replica
* Spostamento di una replica primaria (configurabile)
* Spostamento di una replica secondaria (configurabile)

Chaos esegue più iterazioni. Ogni iterazione è costituito da errori e convalida del cluster per hello periodo specificato. È possibile configurare tempo hello per hello cluster toostabilize e toosucceed di convalida. Se trova un errore nella convalida del cluster, Chaos viene generata e salvata una ValidationFailedEvent con timestamp UTC hello e informazioni dettagliate sull'errore hello. Si consideri ad esempio un'istanza di Chaos impostato toorun per un'ora con un massimo di tre errori simultanei. CHAOS provoca tre errori e quindi convalidare l'integrità del cluster hello. Scorre hello precedente passa passaggio finché viene esplicitamente interrotto tramite hello StopChaosAsync API o un'ora. Se il cluster hello diventa non integro in qualsiasi iterazione (vale a dire non stabilizzazione all'interno di hello passato in MaxClusterStabilizationTimeout), Chaos genera un ValidationFailedEvent. Questo evento indica che si è verificato un errore e potrebbe richiedersi un'ulteriore analisi.

tooget cui Chaos indotta si verifica un errore, è possibile utilizzare API GetChaosReport (powershell o c#). Hello API Ottiene successivo segmento di hello di hello Chaos report basato su token di continuazione passato hello o hello passato-intervallo di tempo. È possibile specificare hello ContinuationToken tooget hello successivo segmento di report Chaos hello o è possibile specificare l'intervallo di tempo hello tramite StartTimeUtc ed EndTimeUtc, ma non è possibile specificare sia hello ContinuationToken e intervallo di tempo hello in hello stessa chiamata. Quando sono presenti più di 100 eventi Chaos, hello report Chaos viene restituito in segmenti in cui un segmento contiene eventi Chaos non più di 100.

## <a name="important-configuration-options"></a>Opzioni di configurazione importanti
* **TimeToRun**: tempo totale di esecuzione di Chaos prima del completamento con esito positivo. È possibile arrestare Chaos prima che ha eseguito per il periodo di TimeToRun hello tramite hello StopChaos API.

* **MaxClusterStabilizationTimeout**: quantità di tempo toowait per hello cluster toobecome integro prima di produrre un ValidationFailedEvent massima hello. Questo tipo di attesa è tooreduce hello carico nel cluster hello durante ripristino. controlli di Hello eseguiti sono:
  * Se l'integrità del cluster hello è OK
  * Se l'integrità del servizio hello è OK
  * Se le dimensioni del set di repliche di destinazione hello avviene per la partizione del servizio hello
  * Che non esistano repliche InBuild
* **MaxConcurrentFaults**: hello numero massimo di errori simultanei indotte in ogni iterazione. più alto numero di hello Hello, hello più aggressiva è Chaos e hello failover e hello transizione combinazioni di stati che hello cluster passa attraverso sono anche più complessa. 

> [!NOTE]
> Indipendentemente dal fatto che un valore alto come *MaxConcurrentFaults* ha, Chaos garantisce - in assenza di hello sugli errori esterni - nessuna perdita del quorum o perdita di dati.
>

* **EnableMoveReplicaFaults**: Abilita o disabilita gli errori di hello che causano hello repliche primario o secondario toomove. Questi errori sono disabilitati per impostazione predefinita.
* **WaitTimeBetweenIterations**: quantità di hello di toowait di tempo tra le iterazioni. Salve, quantità di tempo che CHAOS verrà sospesa dopo l'esecuzione di un ciclo di errori e avere terminato la convalida di corrispondente hello sanitario hello del cluster di hello. Hello valore hello superiore, inferiore hello è frequenza attacco intrusivo nel codice di errore medio hello.
* **WaitTimeBetweenFaults**: quantità di hello di toowait di tempo tra due errori consecutivi in una singola iterazione. Hello valore più alto di hello, hello concorrenza hello minore di (o hello sovrapposizione tra) gli errori.
* **ClusterHealthPolicy**: criteri di integrità del Cluster viene utilizzato toovalidate hello dell'integrità del cluster di hello tra iterazioni Chaos. Se l'integrità del cluster hello è in errore o se si verifica un'eccezione imprevista durante l'esecuzione di errore, Chaos attende per 30 minuti prima di hello successivo controllo integrità - cluster hello tooprovide con alcuni toorecuperate ora.
* **Context**: raccolta di coppie chiave-valore di tipo (string, string). mappa di Hello può essere utilizzato toorecord informazioni hello Chaos eseguire. Non possono esserci più di 100 coppie di questo tipo e ogni stringa (chiave o valore) può essere costituita da un massimo di 4095 caratteri. Questa mappa è l'impostazione starter hello del contesto hello Chaos eseguire toooptionally archivio hello sull'esecuzione hello specifico.

## <a name="how-toorun-chaos"></a>Come toorun Chaos

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
