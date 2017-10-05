---
title: "Risoluzione dei problemi con i report sull'integrità del sistema | Documentazione Microsoft"
description: "Descrive i report di integrità inviati dai componenti dell’Infrastruttura dei servizi di Azure e il relativo utilizzo per la risoluzione dei problemi del cluster o dei problemi delle applicazioni."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="73f7a-103">Usare i report sull'integrità del sistema per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="73f7a-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="73f7a-104">I componenti di Azure Service Fabric forniscono report predefiniti su tutte le entità del cluster.</span><span class="sxs-lookup"><span data-stu-id="73f7a-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="73f7a-105">L' [archivio integrità](service-fabric-health-introduction.md#health-store) crea ed elimina le entità in base ai report di sistema.</span><span class="sxs-lookup"><span data-stu-id="73f7a-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="73f7a-106">Le organizza anche in una gerarchia che acquisisce le interazioni delle entità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="73f7a-107">Per comprendere i concetti correlati all'integrità, vedere altre informazioni sul [modello di integrità di Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73f7a-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="73f7a-108">I report sull'integrità del sistema forniscono la visibilità delle funzionalità del cluster e dell'applicazione e contrassegnano i problemi riscontrati tramite a livello di integrità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="73f7a-109">Per le applicazioni e i servizi i report sull'integrità del sistema verificano che le entità siano implementate e si comportino correttamente dal punto di vista di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="73f7a-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="73f7a-110">I report non forniscono il monitoraggio dell'integrità della logica di business del servizio o il rilevamento dei processi bloccati.</span><span class="sxs-lookup"><span data-stu-id="73f7a-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="73f7a-111">I servizi utente possono arricchire i dati di integrità con informazioni specifiche per la logica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="73f7a-112">I report sull'integrità dei watchdog sono visibili solo *dopo* che i componenti di sistemala hanno creato un'entità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="73f7a-113">Quando si elimina un'entità, l'archivio integrità elimina automaticamente tutti i report sull'integrità ad essa associati.</span><span class="sxs-lookup"><span data-stu-id="73f7a-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="73f7a-114">Lo stesso vale quando si crea una nuova istanza dell'entità, ad esempio viene creata una nuova istanza di replica del servizio persistente con stato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="73f7a-115">Tutti i report associati all'istanza precedente vengono eliminati e rimossi dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="73f7a-116">I report sui componenti di sistema vengono identificati dall'origine, che inizia con il prefisso "**System.**"</span><span class="sxs-lookup"><span data-stu-id="73f7a-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="73f7a-117">.</span><span class="sxs-lookup"><span data-stu-id="73f7a-117">prefix.</span></span> <span data-ttu-id="73f7a-118">I watchdog non possono usare lo stesso prefisso per le proprie origini, perché i report con parametri non validi vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="73f7a-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="73f7a-119">Si osserveranno alcuni report di sistema per capire da quali eventi vengono attivati e come risolvere gli eventuali problemi che rappresentano.</span><span class="sxs-lookup"><span data-stu-id="73f7a-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="73f7a-120">Service Fabric continua ad aggiungere report sulle condizioni di interesse che possono migliorare la visibilità degli eventi che si verificano nel cluster o nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73f7a-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="73f7a-121">È anche possibile migliorare i report esistenti con maggiori dettagli, per consentire di risolvere i problemi più velocemente.</span><span class="sxs-lookup"><span data-stu-id="73f7a-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="73f7a-122">Report sull'integrità del sistema cluster</span><span class="sxs-lookup"><span data-stu-id="73f7a-122">Cluster system health reports</span></span>
<span data-ttu-id="73f7a-123">L'entità di integrità del cluster viene creata automaticamente nell'archivio integrità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="73f7a-124">Se tutto funziona correttamente, non è disponibile un report di sistema.</span><span class="sxs-lookup"><span data-stu-id="73f7a-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="73f7a-125">Perdita di nodi vicini</span><span class="sxs-lookup"><span data-stu-id="73f7a-125">Neighborhood loss</span></span>
<span data-ttu-id="73f7a-126">**System.Federation** segnala un errore quando rileva una perdita di nodi vicini.</span><span class="sxs-lookup"><span data-stu-id="73f7a-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="73f7a-127">Il report è relativo a singoli nodi e l'ID del nodo è incluso nel nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="73f7a-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="73f7a-128">Se si verifica la perdita di un nodo vicino nell'intero anello di Service Fabric, in genere è possibile prevedere due eventi (entrambi i lati del gap effettuano la segnalazione).</span><span class="sxs-lookup"><span data-stu-id="73f7a-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="73f7a-129">In caso di perdita di più nodi vicini, si verificano più eventi.</span><span class="sxs-lookup"><span data-stu-id="73f7a-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="73f7a-130">Il report specifica il timeout di lease globale come durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="73f7a-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="73f7a-131">Il report viene inviato di nuovo ogni metà della durata TTL finché la condizione rimane attiva.</span><span class="sxs-lookup"><span data-stu-id="73f7a-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="73f7a-132">Quando scade, l'evento viene rimosso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="73f7a-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="73f7a-133">Il comportamento di rimozione alla scadenza garantisce la corretta eliminazione del report dall'archivio integrità anche quando il nodo da cui è stato creato è inattivo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="73f7a-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="73f7a-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="73f7a-135">**Proprietà**: inizia con **Neighborhood** e include informazioni sul nodo</span><span class="sxs-lookup"><span data-stu-id="73f7a-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="73f7a-136">**Passaggi successivi**: analizzare il motivo della perdita del nodo vicino, ad esempio controllare la comunicazione tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="73f7a-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="73f7a-137">Report sull'integrità del sistema di nodi</span><span class="sxs-lookup"><span data-stu-id="73f7a-137">Node system health reports</span></span>
<span data-ttu-id="73f7a-138">**System.FM**, che rappresenta il servizio Gestione failover, è l'autorità che gestisce le informazioni sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="73f7a-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="73f7a-139">Ogni nodo deve avere un report generato da System.FM che mostra il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="73f7a-140">Le entità nodo vengono rimosse quando viene rimosso lo stato del nodo (vedere [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="73f7a-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="73f7a-141">Nodo attivo/inattivo</span><span class="sxs-lookup"><span data-stu-id="73f7a-141">Node up/down</span></span>
<span data-ttu-id="73f7a-142">System.FM restituisce OK quando il nodo viene aggiunto all'anello, ovvero è operativo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="73f7a-143">Segnala un errore quando il nodo non fa più parte dell'anello, ovvero è inattivo perché è in corso un aggiornamento o semplicemente perché si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="73f7a-144">La gerarchia di integrità creata dall'archivio integrità agisce sulle entità distribuite in correlazione con i report sui nodi di System.FM.</span><span class="sxs-lookup"><span data-stu-id="73f7a-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="73f7a-145">Considera il nodo un elemento padre virtuale di tutte le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="73f7a-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="73f7a-146">Le entità distribuite in tale nodo vengono esposte tramite query se il nodo è segnalato come attivo da System.FM, con la stessa istanza associata alle entità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="73f7a-147">Quando System.FM segnala che il nodo è inattivo o riavviato (nuova istanza), l'archivio integrità elimina automaticamente le entità distribuite eventualmente esistenti solo nel nodo inattivo o nell'istanza precedente del nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="73f7a-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="73f7a-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="73f7a-149">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="73f7a-149">**Property**: State</span></span>
* <span data-ttu-id="73f7a-150">**Passaggi successivi**: se il nodo è inattivo per un aggiornamento, deve tornare attivo dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="73f7a-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="73f7a-151">In questo caso, lo stato di integrità deve tornare a essere OK.</span><span class="sxs-lookup"><span data-stu-id="73f7a-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="73f7a-152">Se il nodo non ritorna attivo o in caso di errore, è necessario proseguire nell'analisi del problema.</span><span class="sxs-lookup"><span data-stu-id="73f7a-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="73f7a-153">L'esempio seguente illustra l'evento System.FM con stato di integrità OK per il nodo attivo:</span><span class="sxs-lookup"><span data-stu-id="73f7a-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="73f7a-154">Scadenza dei certificati</span><span class="sxs-lookup"><span data-stu-id="73f7a-154">Certificate expiration</span></span>
<span data-ttu-id="73f7a-155">**System.FabricNode** segnala una condizione di avviso quando si avvicina la scadenza dei certificati usati dal nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="73f7a-156">Ogni nodo ha tre certificati: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="73f7a-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="73f7a-157">Quando mancano almeno due settimane alla scadenza, lo stato di integrità del report è OK.</span><span class="sxs-lookup"><span data-stu-id="73f7a-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="73f7a-158">Quando la scadenza è entro due settimane, il tipo di report è un avviso.</span><span class="sxs-lookup"><span data-stu-id="73f7a-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="73f7a-159">Il valore TTL di questi eventi è infinito e vengono rimossi quando un nodo esce dal cluster.</span><span class="sxs-lookup"><span data-stu-id="73f7a-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="73f7a-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="73f7a-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="73f7a-161">**Proprietà**: inizia con **Certificate** e contiene altre informazioni sul tipo di certificato</span><span class="sxs-lookup"><span data-stu-id="73f7a-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="73f7a-162">**Passaggi successivi**: aggiornare i certificati se sono prossimi alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="73f7a-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="73f7a-163">Violazione della capacità di carico</span><span class="sxs-lookup"><span data-stu-id="73f7a-163">Load capacity violation</span></span>
<span data-ttu-id="73f7a-164">Il servizio di bilanciamento del carico di Service Fabric segnala un avviso se rileva una violazione della capacità del nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="73f7a-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="73f7a-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="73f7a-166">**Proprietà**: inizia con **Capacity**</span><span class="sxs-lookup"><span data-stu-id="73f7a-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="73f7a-167">**Passaggi successivi**: controllare la metrica fornita e visualizzare la capacità corrente nel nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="73f7a-168">Report sull'integrità del sistema di applicazioni</span><span class="sxs-lookup"><span data-stu-id="73f7a-168">Application system health reports</span></span>
<span data-ttu-id="73f7a-169">**System.CM**, che rappresenta il servizio Cluster Manager, è l'autorità che gestisce le informazioni sull'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73f7a-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="73f7a-170">Stato</span><span class="sxs-lookup"><span data-stu-id="73f7a-170">State</span></span>
<span data-ttu-id="73f7a-171">System.CM restituisce OK quando l'applicazione viene creata o aggiornata.</span><span class="sxs-lookup"><span data-stu-id="73f7a-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="73f7a-172">Informa l'archivio integrità quando l'applicazione viene eliminata, in modo che possa essere rimossa dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="73f7a-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="73f7a-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="73f7a-174">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="73f7a-174">**Property**: State</span></span>
* <span data-ttu-id="73f7a-175">**Passaggi successivi**: se l'applicazione è stata creata o aggiornata, deve includere il report sull'integrità dello strumento di gestione cluster.</span><span class="sxs-lookup"><span data-stu-id="73f7a-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="73f7a-176">In caso contrario, controllare lo stato dell'applicazione eseguendo una query, ad esempio con il cmdlet di PowerShell **Get-ServiceFabricApplication -ApplicationName *applicationName***.</span><span class="sxs-lookup"><span data-stu-id="73f7a-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="73f7a-177">L'esempio seguente illustra l'evento State nell'applicazione **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="73f7a-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="73f7a-178">Report sull'integrità del sistema di servizi</span><span class="sxs-lookup"><span data-stu-id="73f7a-178">Service system health reports</span></span>
<span data-ttu-id="73f7a-179">**System.FM**, che rappresenta il servizio Gestione failover, è l'autorità che gestisce le informazioni sui servizi.</span><span class="sxs-lookup"><span data-stu-id="73f7a-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="73f7a-180">Stato</span><span class="sxs-lookup"><span data-stu-id="73f7a-180">State</span></span>
<span data-ttu-id="73f7a-181">System.FM restituisce OK quando il servizio viene creato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="73f7a-182">Elimina l'entità dall'archivio integrità quando il servizio viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="73f7a-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="73f7a-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="73f7a-184">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="73f7a-184">**Property**: State</span></span>

<span data-ttu-id="73f7a-185">L'esempio seguente illustra l'evento State nel servizio **fabric:/WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="73f7a-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="73f7a-186">Errore di correlazione del servizio</span><span class="sxs-lookup"><span data-stu-id="73f7a-186">Service correlation error</span></span>
<span data-ttu-id="73f7a-187">**System.PLB** segnala un errore quando rileva che l'aggiornamento di un servizio da correlare con un altro servizio crea una catena di affinità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="73f7a-188">Il report viene cancellato quando l'aggiornamento viene completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="73f7a-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="73f7a-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="73f7a-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="73f7a-190">**Proprietà**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="73f7a-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="73f7a-191">**Passaggi successivi**: controllare le descrizioni dei servizi correlati.</span><span class="sxs-lookup"><span data-stu-id="73f7a-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="73f7a-192">Report sull'integrità del sistema di partizioni</span><span class="sxs-lookup"><span data-stu-id="73f7a-192">Partition system health reports</span></span>
<span data-ttu-id="73f7a-193">**System.FM**, che rappresenta il servizio Gestione failover, è l'autorità che gestisce le informazioni sulle partizioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="73f7a-194">Stato</span><span class="sxs-lookup"><span data-stu-id="73f7a-194">State</span></span>
<span data-ttu-id="73f7a-195">System.FM restituisce OK quando la partizione viene creata ed è integra.</span><span class="sxs-lookup"><span data-stu-id="73f7a-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="73f7a-196">Elimina l'entità dall'archivio integrità quando la partizione viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="73f7a-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="73f7a-197">Se il numero di repliche della partizione è inferiore al minimo, viene segnalata una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="73f7a-198">Se il numero di repliche della partizione non è inferiore al minimo, ma è al di sotto del numero di repliche di destinazione, viene segnalata una condizione di avviso.</span><span class="sxs-lookup"><span data-stu-id="73f7a-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="73f7a-199">Se la partizione è in una condizione di perdita del quorum, System.FM segnala un errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="73f7a-200">Altri eventi importanti includono un avviso quando le operazioni di riconfigurazione e di compilazione richiedono più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="73f7a-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="73f7a-201">I tempi previsti per la compilazione e la riconfigurazione sono configurabili in base agli scenari del servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="73f7a-202">Ad esempio, se un servizio ha uno stato di un terabyte, come ad esempio un database SQL, la compilazione richiederà più tempo rispetto a un servizio con una quantità di stato ridotta.</span><span class="sxs-lookup"><span data-stu-id="73f7a-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="73f7a-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="73f7a-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="73f7a-204">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="73f7a-204">**Property**: State</span></span>
* <span data-ttu-id="73f7a-205">**Passaggi successivi**: se lo stato di integrità non è OK, è possibile che alcune repliche non vengano create, aperte o alzate di livello, primario o secondario, nel modo corretto.</span><span class="sxs-lookup"><span data-stu-id="73f7a-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="73f7a-206">In molti casi, la causa radice è un bug del servizio nell'implementazione del ruolo di apertura o modifica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="73f7a-207">L'esempio seguente illustra una partizione integra:</span><span class="sxs-lookup"><span data-stu-id="73f7a-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="73f7a-208">L'esempio seguente illustra l'integrità di una partizione che è al di sotto del numero di repliche di destinazione.</span><span class="sxs-lookup"><span data-stu-id="73f7a-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="73f7a-209">Il passaggio successivo consiste nell'ottenere la descrizione della partizione, che mostra come è configurata: **MinReplicaSetSize** corrisponde a tre e **TargetReplicaSetSize** a sette.</span><span class="sxs-lookup"><span data-stu-id="73f7a-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="73f7a-210">Ottenere quindi il numero di nodi nel cluster: cinque.</span><span class="sxs-lookup"><span data-stu-id="73f7a-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="73f7a-211">Pertanto, in questo caso, non è possibile collocare due repliche in quanto il numero di repliche di destinazione è superiore al numero di nodi disponibili.</span><span class="sxs-lookup"><span data-stu-id="73f7a-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="73f7a-212">Violazione del vincolo di replica</span><span class="sxs-lookup"><span data-stu-id="73f7a-212">Replica constraint violation</span></span>
<span data-ttu-id="73f7a-213">**System.PLB** segnala un avviso se rileva una violazione del vincolo di replica e non può posizionare tutte le repliche della partizione.</span><span class="sxs-lookup"><span data-stu-id="73f7a-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="73f7a-214">Il report indica in modo dettagliato i vincoli e le proprietà che impediscono il posizionamento della replica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="73f7a-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="73f7a-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="73f7a-216">**Proprietà**: inizia con **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="73f7a-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="73f7a-217">Report sull'integrità del sistema di repliche</span><span class="sxs-lookup"><span data-stu-id="73f7a-217">Replica system health reports</span></span>
<span data-ttu-id="73f7a-218">**System.RA**, che rappresenta il componente agente di riconfigurazione, è l'autorità per lo stato della replica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="73f7a-219">Stato</span><span class="sxs-lookup"><span data-stu-id="73f7a-219">State</span></span>
<span data-ttu-id="73f7a-220">**System.RA** restituisce OK quando viene creata la replica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="73f7a-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="73f7a-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="73f7a-222">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="73f7a-222">**Property**: State</span></span>

<span data-ttu-id="73f7a-223">L'esempio seguente illustra una replica integra:</span><span class="sxs-lookup"><span data-stu-id="73f7a-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="73f7a-224">Stato aperto della replica</span><span class="sxs-lookup"><span data-stu-id="73f7a-224">Replica open status</span></span>
<span data-ttu-id="73f7a-225">La descrizione di questo report sull'integrità include l'ora (UTC) in cui è iniziata l'esecuzione della chiamata API.</span><span class="sxs-lookup"><span data-stu-id="73f7a-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="73f7a-226">**System.RA** segnala una condizione di avviso se l'apertura della replica richiede più tempo del periodo configurato (impostazione predefinita: 30 minuti).</span><span class="sxs-lookup"><span data-stu-id="73f7a-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="73f7a-227">Se l'API influisce sulla disponibilità del servizio, il report viene eseguito molto più rapidamente. L'intervallo di tempo è configurabile, con valore predefinito di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="73f7a-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="73f7a-228">Il tempo misurato include il tempo impiegato per l'apertura del replicatore e del servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="73f7a-229">Se l'apertura viene completata, la proprietà restituisce OK.</span><span class="sxs-lookup"><span data-stu-id="73f7a-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="73f7a-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="73f7a-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="73f7a-231">**Proprietà**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="73f7a-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="73f7a-232">**Passaggi successivi**: se lo stato di integrità non è OK, verificare per quale motivo l'apertura della replica richiede più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="73f7a-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="73f7a-233">Chiamata API del servizio lenta</span><span class="sxs-lookup"><span data-stu-id="73f7a-233">Slow service API call</span></span>
<span data-ttu-id="73f7a-234">**System.RAP** e **System.Replicator** segnalano una condizione di avviso se una chiamata al codice del servizio utente richiede più tempo di quello configurato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="73f7a-235">L'avviso viene cancellato al completamento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="73f7a-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="73f7a-236">**SourceId**: System.RAP o System.Replicator</span><span class="sxs-lookup"><span data-stu-id="73f7a-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="73f7a-237">**Proprietà**: nome dell'API lenta.</span><span class="sxs-lookup"><span data-stu-id="73f7a-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="73f7a-238">La descrizione fornisce altri dettagli sull'ora in cui l'API è rimasta in sospeso.</span><span class="sxs-lookup"><span data-stu-id="73f7a-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="73f7a-239">**Passaggi successivi**: esaminare il motivo per cui la chiamata richiede più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="73f7a-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="73f7a-240">L'esempio seguente illustra una partizione in uno stato di perdita del quorum e i passaggi di analisi eseguiti per capire il motivo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="73f7a-241">Una delle repliche presenta uno stato di integrità di avviso, che ne indica l'integrità.</span><span class="sxs-lookup"><span data-stu-id="73f7a-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="73f7a-242">Mostra che l'operazione di servizio richiede più tempo del previsto, un evento segnalato da System.RAP.</span><span class="sxs-lookup"><span data-stu-id="73f7a-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="73f7a-243">Dopo aver ottenuto queste informazioni, il passaggio successivo consiste nell'esaminare il codice del servizio e procedere con l'analisi.</span><span class="sxs-lookup"><span data-stu-id="73f7a-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="73f7a-244">In questo caso, l'implementazione di **RunAsync** del servizio con stato genera un'eccezione non gestita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="73f7a-245">Viene eseguito il riciclo delle repliche, quindi è possibile che non vengano visualizzate repliche con stato di avviso.</span><span class="sxs-lookup"><span data-stu-id="73f7a-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="73f7a-246">È possibile provare di nuovo a ottenere lo stato di integrità e cercare eventuali differenze nell'ID replica.</span><span class="sxs-lookup"><span data-stu-id="73f7a-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="73f7a-247">In alcuni casi, i nuovi tentativi possono offrire indicazioni utili.</span><span class="sxs-lookup"><span data-stu-id="73f7a-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="73f7a-248">Quando si avvia l'applicazione che presenta errori nel debugger, le finestre degli eventi di diagnostica mostrano l'eccezione generata da RunAsync:</span><span class="sxs-lookup"><span data-stu-id="73f7a-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Eventi di diagnostica di Visual Studio 2015: errore RunAsync in fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="73f7a-250">Eventi di diagnostica di Visual Studio 2015: errore RunAsync in **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="73f7a-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="73f7a-251">Coda di replica piena</span><span class="sxs-lookup"><span data-stu-id="73f7a-251">Replication queue full</span></span>
<span data-ttu-id="73f7a-252">**System.Replicator** segnala un avviso se la coda di replica è piena.</span><span class="sxs-lookup"><span data-stu-id="73f7a-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="73f7a-253">Nel server primario la coda di replica in genere si riempie perché una o più repliche secondarie sono lente nel riconoscere le operazioni.</span><span class="sxs-lookup"><span data-stu-id="73f7a-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="73f7a-254">Nel server secondario ciò si verifica di solito quando il servizio è lento nell'applicare le operazioni.</span><span class="sxs-lookup"><span data-stu-id="73f7a-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="73f7a-255">La condizione di avviso viene cancellata quando la coda non è più piena.</span><span class="sxs-lookup"><span data-stu-id="73f7a-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="73f7a-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="73f7a-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="73f7a-257">**Proprietà**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, a seconda del ruolo della replica</span><span class="sxs-lookup"><span data-stu-id="73f7a-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="73f7a-258">Operazioni di Naming lente</span><span class="sxs-lookup"><span data-stu-id="73f7a-258">Slow Naming operations</span></span>
<span data-ttu-id="73f7a-259">**System.NamingService** segnala lo stato di integrità per la replica primaria quando un'operazione di Naming richiede più tempo di quanto sia accettabile.</span><span class="sxs-lookup"><span data-stu-id="73f7a-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="73f7a-260">Esempi di operazioni di Naming sono [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) e [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="73f7a-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="73f7a-261">Altri metodi sono disponibili in FabricClient, ad esempio nell'ambito dei [metodi di gestione dei servizi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o dei [metodi di gestione delle proprietà](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="73f7a-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="73f7a-262">Il servizio Naming risolve i nomi del servizio in una posizione nel cluster e consente agli utenti di gestire i nomi e le proprietà del servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="73f7a-263">È un servizio permanente partizionato di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="73f7a-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="73f7a-264">Una partizione rappresenta l'authority owner, contenente i metadati relativi a tutti i nomi e i servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="73f7a-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="73f7a-265">I nomi di Service Fabric sono mappati a partizioni diverse, denominate name owner, e il servizio è quindi estendibile.</span><span class="sxs-lookup"><span data-stu-id="73f7a-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="73f7a-266">Per altre informazioni, vedere [Architettura di Service Fabric](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="73f7a-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="73f7a-267">Quando un'operazione di Naming richiede più tempo del previsto, viene contrassegnata con un report di tipo avviso nella *replica primaria della partizione del servizio Naming che gestisce l'operazione*.</span><span class="sxs-lookup"><span data-stu-id="73f7a-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="73f7a-268">Se l'operazione viene completata, l'avviso viene cancellato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="73f7a-269">Se l'operazione viene completata con un errore, il report sull'integrità include i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="73f7a-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="73f7a-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="73f7a-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="73f7a-271">**Proprietà**: inizia con il prefisso **Duration_** e identifica l'operazione lenta e il nome di Service Fabric su cui viene applicata.</span><span class="sxs-lookup"><span data-stu-id="73f7a-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="73f7a-272">Se l'operazione di creazione servizio per il nome fabric:/MyApp/MyService richiede troppo tempo, ad esempio, la proprietà è Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="73f7a-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="73f7a-273">AO punta al ruolo della partizione di Naming per il nome e l'operazione.</span><span class="sxs-lookup"><span data-stu-id="73f7a-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="73f7a-274">**Passaggi successivi**: controllare i motivi per cui l'operazione di Naming non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="73f7a-275">A ogni operazione può corrispondere una causa radice diversa.</span><span class="sxs-lookup"><span data-stu-id="73f7a-275">Each operation can have different root causes.</span></span> <span data-ttu-id="73f7a-276">L'eliminazione di un servizio, ad esempio, può bloccarsi in un nodo perché l'host applicazione continua ad arrestarsi in modo anomalo nel nodo a causa di un bug utente nel codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="73f7a-277">L'esempio seguente illustra un'operazione di creazione servizio.</span><span class="sxs-lookup"><span data-stu-id="73f7a-277">The following example shows a create service operation.</span></span> <span data-ttu-id="73f7a-278">L'operazione ha richiesto un tempo superiore alla durata configurata.</span><span class="sxs-lookup"><span data-stu-id="73f7a-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="73f7a-279">AO riprova e invia l'attività a NO.</span><span class="sxs-lookup"><span data-stu-id="73f7a-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="73f7a-280">NO completa l'ultima operazione con Timeout.</span><span class="sxs-lookup"><span data-stu-id="73f7a-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="73f7a-281">In questo caso, la stessa replica è primaria per entrambi i ruoli AO e NO.</span><span class="sxs-lookup"><span data-stu-id="73f7a-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="73f7a-282">Report sull'integrità del sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="73f7a-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="73f7a-283">**System.Hosting** è l'autorità per le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="73f7a-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="73f7a-284">Activation</span><span class="sxs-lookup"><span data-stu-id="73f7a-284">Activation</span></span>
<span data-ttu-id="73f7a-285">System.Hosting restituisce OK quando un'applicazione viene attivata correttamente nel nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="73f7a-286">In caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="73f7a-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-288">**Proprietà**: Activation, inclusa la versione di implementazione</span><span class="sxs-lookup"><span data-stu-id="73f7a-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="73f7a-289">**Passaggi successivi**: se l'applicazione non è integra, provare ad analizzare i motivi per cui l'attivazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="73f7a-290">L'esempio seguente illustra l'attivazione riuscita:</span><span class="sxs-lookup"><span data-stu-id="73f7a-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="73f7a-291">Scaricare</span><span class="sxs-lookup"><span data-stu-id="73f7a-291">Download</span></span>
<span data-ttu-id="73f7a-292">**System.Hosting** segnala un errore se il download del pacchetto dell'applicazione non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="73f7a-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="73f7a-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-294">**Proprietà**: **Download:*VersioneRollout***</span><span class="sxs-lookup"><span data-stu-id="73f7a-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="73f7a-295">**Passaggi successivi**: ricercare la causa del download non riuscito nel nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="73f7a-296">Report sull'integrità del sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="73f7a-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="73f7a-297">**System.Hosting** è l'autorità per le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="73f7a-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="73f7a-298">Attivazione del pacchetto di servizi</span><span class="sxs-lookup"><span data-stu-id="73f7a-298">Service package activation</span></span>
<span data-ttu-id="73f7a-299">System.Hosting restituisce OK se l'attivazione del pacchetto di servizi nel nodo è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="73f7a-300">In caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="73f7a-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-302">**Proprietà**: Activation</span><span class="sxs-lookup"><span data-stu-id="73f7a-302">**Property**: Activation</span></span>
* <span data-ttu-id="73f7a-303">**Passaggi successivi**: analizzare i motivi per cui l'attivazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="73f7a-304">Attivazione del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="73f7a-304">Code package activation</span></span>
<span data-ttu-id="73f7a-305">**System.Hosting** restituisce OK per ogni pacchetto di codice se l'attivazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73f7a-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="73f7a-306">In caso contrario, restituisce l'avviso configurato.</span><span class="sxs-lookup"><span data-stu-id="73f7a-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="73f7a-307">Se l'attivazione di **CodePackage** non riesce o termina con un errore superiore alla soglia configurata per **CodePackageHealthErrorThreshold**, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="73f7a-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="73f7a-308">Se un pacchetto servizio contiene più pacchetti di codice, viene generato un report sull'attivazione per ognuno.</span><span class="sxs-lookup"><span data-stu-id="73f7a-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="73f7a-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-310">**Proprietà**: usa il prefisso **CodePackageActivation** e contiene il nome del pacchetto di codice e il punto di ingresso come **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** ad esempio **CodePackageActivation:Code:SetupEntryPoint**</span><span class="sxs-lookup"><span data-stu-id="73f7a-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="73f7a-311">Registrazione del tipo di servizio</span><span class="sxs-lookup"><span data-stu-id="73f7a-311">Service type registration</span></span>
<span data-ttu-id="73f7a-312">**System.Hosting** restituisce OK se il tipo di servizio è stato registrato correttamente.</span><span class="sxs-lookup"><span data-stu-id="73f7a-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="73f7a-313">Viene restituito un errore se la registrazione non è stata eseguita in tempo, secondo quanto configurato con **ServiceTypeRegistrationTimeout**.</span><span class="sxs-lookup"><span data-stu-id="73f7a-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="73f7a-314">In caso di chiusura del runtime, viene annullata la registrazione del tipo di servizio nel nodo e viene segnalato un avviso.</span><span class="sxs-lookup"><span data-stu-id="73f7a-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="73f7a-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-316">**Proprietà**: usa il prefisso **ServiceTypeRegistration** e contiene il nome del tipo di servizio, ad esempio **ServiceTypeRegistration:FileStoreServiceType**</span><span class="sxs-lookup"><span data-stu-id="73f7a-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="73f7a-317">L'esempio seguente illustra un pacchetto servizio distribuito integro:</span><span class="sxs-lookup"><span data-stu-id="73f7a-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="73f7a-318">Scaricare</span><span class="sxs-lookup"><span data-stu-id="73f7a-318">Download</span></span>
<span data-ttu-id="73f7a-319">**System.Hosting** segnala un errore se il download del pacchetto del servizio non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="73f7a-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="73f7a-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-321">**Proprietà**: **Download:*VersioneRollout***</span><span class="sxs-lookup"><span data-stu-id="73f7a-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="73f7a-322">**Passaggi successivi**: ricercare la causa del download non riuscito nel nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="73f7a-323">Convalida dell’aggiornamento</span><span class="sxs-lookup"><span data-stu-id="73f7a-323">Upgrade validation</span></span>
<span data-ttu-id="73f7a-324">**System.Hosting** segnala un errore se la convalida durante l'aggiornamento non è riuscita oppure se non è riuscito l'aggiornamento nel nodo.</span><span class="sxs-lookup"><span data-stu-id="73f7a-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="73f7a-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="73f7a-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="73f7a-326">**Proprietà**: usa il prefisso **FabricUpgradeValidation** e contiene la versione dell'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="73f7a-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="73f7a-327">**Descrizione**: punta all'errore che si è verificato</span><span class="sxs-lookup"><span data-stu-id="73f7a-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="73f7a-328">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73f7a-328">Next steps</span></span>
[<span data-ttu-id="73f7a-329">Come visualizzare i report sull'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="73f7a-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="73f7a-330">Creare report e verificare l'integrità dei servizi</span><span class="sxs-lookup"><span data-stu-id="73f7a-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="73f7a-331">Monitorare e diagnosticare servizi in locale</span><span class="sxs-lookup"><span data-stu-id="73f7a-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="73f7a-332">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="73f7a-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

