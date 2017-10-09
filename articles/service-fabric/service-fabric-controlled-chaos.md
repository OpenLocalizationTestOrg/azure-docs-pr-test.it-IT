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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="793a9-103">Eseguire Chaos in ambiente controllato nei cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="793a9-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="793a9-104">I sistemi distribuiti di grandi dimensioni come le infrastrutture cloud sono intrinsecamente inaffidabili.</span><span class="sxs-lookup"><span data-stu-id="793a9-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="793a9-105">Azure Service Fabric consente agli sviluppatori toowrite affidabili servizi distribuiti su un'infrastruttura affidabile.</span><span class="sxs-lookup"><span data-stu-id="793a9-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="793a9-106">toowrite affidabili servizi distribuiti su un'infrastruttura affidabile, gli sviluppatori devono stabilità di hello in grado di tootest toobe dei servizi mentre hello inaffidabile infrastruttura sottostante viene eseguita tramite le transizioni di stato complicato toofaults scadenza.</span><span class="sxs-lookup"><span data-stu-id="793a9-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="793a9-107">Hello [attacco intrusivo nel codice di errore e il servizio Cluster Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (noto anche come hello errore Analysis Services) consente agli sviluppatori hello tooinduce errori tootest i propri servizi.</span><span class="sxs-lookup"><span data-stu-id="793a9-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="793a9-108">Questi destinazione simulato gli errori, ad esempio [il riavvio di una partizione](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), consentono di esercitare transizioni più comuni di hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="793a9-109">Gli errori simulati mirati sono tuttavia parziali per definizione e quindi possono non coprire i bug che si verificano solo in sequenze di transizioni di stato difficili da prevedere, lunghe e complesse.</span><span class="sxs-lookup"><span data-stu-id="793a9-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="793a9-110">Per un test imparziale, è possibile usare Chaos.</span><span class="sxs-lookup"><span data-stu-id="793a9-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="793a9-111">CHAOS simula errori periodici interleaved (normale e anomali) in cluster hello per periodi prolungati di tempo.</span><span class="sxs-lookup"><span data-stu-id="793a9-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="793a9-112">Dopo aver configurato caos con frequenza hello e tipo hello degli errori, è possibile avviare Chaos tramite c# o Powershell API toostart generazione di errori nel cluster hello e nei servizi.</span><span class="sxs-lookup"><span data-stu-id="793a9-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="793a9-113">È possibile configurare Chaos toorun per un periodo di tempo specificato (ad esempio, per un'ora), dopo il quale viene interrotto automaticamente, Chaos oppure è possibile chiamare toostop StopChaos API (in c# o Powershell) in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="793a9-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="793a9-114">Nella sua forma corrente, Chaos provoca errori solo sicuri, che implica che in assenza di hello errori esterni di una perdita del quorum o perdita di dati si verifica mai.</span><span class="sxs-lookup"><span data-stu-id="793a9-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="793a9-115">Durante l'esecuzione Chaos, genera eventi diversi che consentono di acquisire lo stato di hello di eseguire un determinato momento hello hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="793a9-116">Ad esempio, un ExecutingFaultsEvent contiene tutti gli errori di hello Chaos ha deciso di tooexecute in quell'iterazione.</span><span class="sxs-lookup"><span data-stu-id="793a9-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="793a9-117">Un ValidationFailedEvent contiene i dettagli di hello di un errore di convalida (problemi di integrità o stabilità) che è stato trovato durante la convalida di hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="793a9-118">È possibile richiamare hello GetChaosReport API (in c# o Powershell) tooget hello report viene eseguito Chaos.</span><span class="sxs-lookup"><span data-stu-id="793a9-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="793a9-119">Gli eventi vengono conservati in un oggetto [Reliable ​Dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), che ha un criterio di troncamento influenzato da due configurazioni: **MaxStoredChaosEventCount** (valore predefinito 25000) e **StoredActionCleanupIntervalInSeconds** (valore predefinito 3600).</span><span class="sxs-lookup"><span data-stu-id="793a9-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="793a9-120">Ogni *StoredActionCleanupIntervalInSeconds* controlli Chaos e tutti i ma hello più recente *MaxStoredChaosEventCount* eventi, vengono eliminati dal dizionario di hello affidabile.</span><span class="sxs-lookup"><span data-stu-id="793a9-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="793a9-121">Errori indotti da Chaos</span><span class="sxs-lookup"><span data-stu-id="793a9-121">Faults induced in Chaos</span></span>
<span data-ttu-id="793a9-122">CHAOS genera errori nel cluster di Service Fabric intera hello e comprime gli errori che sono visibili in mesi o anni in poche ore.</span><span class="sxs-lookup"><span data-stu-id="793a9-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="793a9-123">combinazione di Hello di interfoliazione errori con frequenza elevata errore hello consente di trovare casi estremi che in caso contrario potrebbero essere perso.</span><span class="sxs-lookup"><span data-stu-id="793a9-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="793a9-124">Questo esercizio di Chaos lead tooa significativo miglioramento nella qualità del codice del servizio hello hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="793a9-125">CHAOS provoca errori da hello seguenti categorie:</span><span class="sxs-lookup"><span data-stu-id="793a9-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="793a9-126">Riavvio di un nodo</span><span class="sxs-lookup"><span data-stu-id="793a9-126">Restart a node</span></span>
* <span data-ttu-id="793a9-127">Riavvio di un pacchetto di codice distribuito</span><span class="sxs-lookup"><span data-stu-id="793a9-127">Restart a deployed code package</span></span>
* <span data-ttu-id="793a9-128">Rimozione di una replica</span><span class="sxs-lookup"><span data-stu-id="793a9-128">Remove a replica</span></span>
* <span data-ttu-id="793a9-129">Riavvio di una replica</span><span class="sxs-lookup"><span data-stu-id="793a9-129">Restart a replica</span></span>
* <span data-ttu-id="793a9-130">Spostamento di una replica primaria (configurabile)</span><span class="sxs-lookup"><span data-stu-id="793a9-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="793a9-131">Spostamento di una replica secondaria (configurabile)</span><span class="sxs-lookup"><span data-stu-id="793a9-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="793a9-132">Chaos esegue più iterazioni.</span><span class="sxs-lookup"><span data-stu-id="793a9-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="793a9-133">Ogni iterazione è costituito da errori e convalida del cluster per hello periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="793a9-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="793a9-134">È possibile configurare tempo hello per hello cluster toostabilize e toosucceed di convalida.</span><span class="sxs-lookup"><span data-stu-id="793a9-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="793a9-135">Se trova un errore nella convalida del cluster, Chaos viene generata e salvata una ValidationFailedEvent con timestamp UTC hello e informazioni dettagliate sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="793a9-136">Si consideri ad esempio un'istanza di Chaos impostato toorun per un'ora con un massimo di tre errori simultanei.</span><span class="sxs-lookup"><span data-stu-id="793a9-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="793a9-137">CHAOS provoca tre errori e quindi convalidare l'integrità del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="793a9-138">Scorre hello precedente passa passaggio finché viene esplicitamente interrotto tramite hello StopChaosAsync API o un'ora.</span><span class="sxs-lookup"><span data-stu-id="793a9-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="793a9-139">Se il cluster hello diventa non integro in qualsiasi iterazione (vale a dire non stabilizzazione all'interno di hello passato in MaxClusterStabilizationTimeout), Chaos genera un ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="793a9-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="793a9-140">Questo evento indica che si è verificato un errore e potrebbe richiedersi un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="793a9-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="793a9-141">tooget cui Chaos indotta si verifica un errore, è possibile utilizzare API GetChaosReport (powershell o c#).</span><span class="sxs-lookup"><span data-stu-id="793a9-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="793a9-142">Hello API Ottiene successivo segmento di hello di hello Chaos report basato su token di continuazione passato hello o hello passato-intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="793a9-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="793a9-143">È possibile specificare hello ContinuationToken tooget hello successivo segmento di report Chaos hello o è possibile specificare l'intervallo di tempo hello tramite StartTimeUtc ed EndTimeUtc, ma non è possibile specificare sia hello ContinuationToken e intervallo di tempo hello in hello stessa chiamata.</span><span class="sxs-lookup"><span data-stu-id="793a9-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="793a9-144">Quando sono presenti più di 100 eventi Chaos, hello report Chaos viene restituito in segmenti in cui un segmento contiene eventi Chaos non più di 100.</span><span class="sxs-lookup"><span data-stu-id="793a9-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="793a9-145">Opzioni di configurazione importanti</span><span class="sxs-lookup"><span data-stu-id="793a9-145">Important configuration options</span></span>
* <span data-ttu-id="793a9-146">**TimeToRun**: tempo totale di esecuzione di Chaos prima del completamento con esito positivo.</span><span class="sxs-lookup"><span data-stu-id="793a9-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="793a9-147">È possibile arrestare Chaos prima che ha eseguito per il periodo di TimeToRun hello tramite hello StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="793a9-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="793a9-148">**MaxClusterStabilizationTimeout**: quantità di tempo toowait per hello cluster toobecome integro prima di produrre un ValidationFailedEvent massima hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="793a9-149">Questo tipo di attesa è tooreduce hello carico nel cluster hello durante ripristino.</span><span class="sxs-lookup"><span data-stu-id="793a9-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="793a9-150">controlli di Hello eseguiti sono:</span><span class="sxs-lookup"><span data-stu-id="793a9-150">hello checks performed are:</span></span>
  * <span data-ttu-id="793a9-151">Se l'integrità del cluster hello è OK</span><span class="sxs-lookup"><span data-stu-id="793a9-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="793a9-152">Se l'integrità del servizio hello è OK</span><span class="sxs-lookup"><span data-stu-id="793a9-152">If hello service health is OK</span></span>
  * <span data-ttu-id="793a9-153">Se le dimensioni del set di repliche di destinazione hello avviene per la partizione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="793a9-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="793a9-154">Che non esistano repliche InBuild</span><span class="sxs-lookup"><span data-stu-id="793a9-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="793a9-155">**MaxConcurrentFaults**: hello numero massimo di errori simultanei indotte in ogni iterazione.</span><span class="sxs-lookup"><span data-stu-id="793a9-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="793a9-156">più alto numero di hello Hello, hello più aggressiva è Chaos e hello failover e hello transizione combinazioni di stati che hello cluster passa attraverso sono anche più complessa.</span><span class="sxs-lookup"><span data-stu-id="793a9-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="793a9-157">Indipendentemente dal fatto che un valore alto come *MaxConcurrentFaults* ha, Chaos garantisce - in assenza di hello sugli errori esterni - nessuna perdita del quorum o perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="793a9-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="793a9-158">**EnableMoveReplicaFaults**: Abilita o disabilita gli errori di hello che causano hello repliche primario o secondario toomove.</span><span class="sxs-lookup"><span data-stu-id="793a9-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="793a9-159">Questi errori sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="793a9-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="793a9-160">**WaitTimeBetweenIterations**: quantità di hello di toowait di tempo tra le iterazioni.</span><span class="sxs-lookup"><span data-stu-id="793a9-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="793a9-161">Salve, quantità di tempo che CHAOS verrà sospesa dopo l'esecuzione di un ciclo di errori e avere terminato la convalida di corrispondente hello sanitario hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="793a9-162">Hello valore hello superiore, inferiore hello è frequenza attacco intrusivo nel codice di errore medio hello.</span><span class="sxs-lookup"><span data-stu-id="793a9-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="793a9-163">**WaitTimeBetweenFaults**: quantità di hello di toowait di tempo tra due errori consecutivi in una singola iterazione.</span><span class="sxs-lookup"><span data-stu-id="793a9-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="793a9-164">Hello valore più alto di hello, hello concorrenza hello minore di (o hello sovrapposizione tra) gli errori.</span><span class="sxs-lookup"><span data-stu-id="793a9-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="793a9-165">**ClusterHealthPolicy**: criteri di integrità del Cluster viene utilizzato toovalidate hello dell'integrità del cluster di hello tra iterazioni Chaos.</span><span class="sxs-lookup"><span data-stu-id="793a9-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="793a9-166">Se l'integrità del cluster hello è in errore o se si verifica un'eccezione imprevista durante l'esecuzione di errore, Chaos attende per 30 minuti prima di hello successivo controllo integrità - cluster hello tooprovide con alcuni toorecuperate ora.</span><span class="sxs-lookup"><span data-stu-id="793a9-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="793a9-167">**Context**: raccolta di coppie chiave-valore di tipo (string, string).</span><span class="sxs-lookup"><span data-stu-id="793a9-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="793a9-168">mappa di Hello può essere utilizzato toorecord informazioni hello Chaos eseguire.</span><span class="sxs-lookup"><span data-stu-id="793a9-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="793a9-169">Non possono esserci più di 100 coppie di questo tipo e ogni stringa (chiave o valore) può essere costituita da un massimo di 4095 caratteri.</span><span class="sxs-lookup"><span data-stu-id="793a9-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="793a9-170">Questa mappa è l'impostazione starter hello del contesto hello Chaos eseguire toooptionally archivio hello sull'esecuzione hello specifico.</span><span class="sxs-lookup"><span data-stu-id="793a9-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="793a9-171">Come toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="793a9-171">How toorun Chaos</span></span>

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
