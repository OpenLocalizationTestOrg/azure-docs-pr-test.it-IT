---
title: "aaaTroubleshoot con i report di integrità di sistema | Documenti Microsoft"
description: "Vengono descritti i report di integrità hello inviati dai componenti di Azure Service Fabric e il relativo utilizzo per la risoluzione dei problemi del cluster o i problemi dell'applicazione."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="85e96-103">Utilizzare tootroubleshoot rapporti di integrità sistema</span><span class="sxs-lookup"><span data-stu-id="85e96-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="85e96-104">Azure Service Fabric componenti report predefinito hello in tutte le entità nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="85e96-105">Hello [archivio integrità](service-fabric-health-introduction.md#health-store) crea ed Elimina le entità in base ai report di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="85e96-106">Le organizza anche in una gerarchia che acquisisce le interazioni delle entità.</span><span class="sxs-lookup"><span data-stu-id="85e96-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="85e96-107">concetti relativi a integrità toounderstand, leggere informazioni, vedere [il modello di integrità di Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85e96-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="85e96-108">I report sull'integrità del sistema forniscono la visibilità delle funzionalità del cluster e dell'applicazione e contrassegnano i problemi riscontrati tramite a livello di integrità.</span><span class="sxs-lookup"><span data-stu-id="85e96-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="85e96-109">Per servizi e applicazioni, rapporti di integrità di sistema verificare che le entità vengono implementate e corretto dalla prospettiva di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="85e96-110">report di Hello non forniscono alcun monitoraggio dello stato di rilevamento dei processi bloccati o logica di business hello del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="85e96-111">Servizi utente possono migliorare i dati di integrità hello con logica tootheir specifici di informazioni.</span><span class="sxs-lookup"><span data-stu-id="85e96-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="85e96-112">Report sull'integrità watchdog sono visibili solo *dopo* componenti del sistema hello creano un'entità.</span><span class="sxs-lookup"><span data-stu-id="85e96-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="85e96-113">Quando viene eliminata un'entità, dell'archivio integrità hello Elimina automaticamente tutti i report di integrità è associati.</span><span class="sxs-lookup"><span data-stu-id="85e96-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="85e96-114">Hello stesso vale quando viene creata una nuova istanza dell'entità hello (ad esempio, viene creata una nuova istanza di replica con stato servizio persistente).</span><span class="sxs-lookup"><span data-stu-id="85e96-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="85e96-115">Tutti i report associati con l'istanza precedente di hello vengono eliminati e rimossi dal negozio hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="85e96-116">Hello sistema componente report sono identificati dall'origine hello, che inizia con hello "**System.**"</span><span class="sxs-lookup"><span data-stu-id="85e96-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="85e96-117">.</span><span class="sxs-lookup"><span data-stu-id="85e96-117">prefix.</span></span> <span data-ttu-id="85e96-118">Watchdog non è possibile utilizzare hello stesso prefisso, per le rispettive origini, come i report con parametri non validi vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="85e96-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="85e96-119">Si esamina alcuni sistema segnala toounderstand che cosa attiva li e come toocorrect hello possibili problemi che rappresentano.</span><span class="sxs-lookup"><span data-stu-id="85e96-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="85e96-120">Service Fabric continua tooadd report alle condizioni di interesse che consentono di migliorare la visibilità in ciò che avviene nell'applicazione e cluster hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="85e96-121">I report esistenti possono anche essere migliorati con maggiori dettagli toohelp problemi hello più velocemente.</span><span class="sxs-lookup"><span data-stu-id="85e96-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="85e96-122">Report sull'integrità del sistema cluster</span><span class="sxs-lookup"><span data-stu-id="85e96-122">Cluster system health reports</span></span>
<span data-ttu-id="85e96-123">entità di integrità del cluster Hello viene creata automaticamente nell'archivio integrità hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="85e96-124">Se tutto funziona correttamente, non è disponibile un report di sistema.</span><span class="sxs-lookup"><span data-stu-id="85e96-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="85e96-125">Perdita di nodi vicini</span><span class="sxs-lookup"><span data-stu-id="85e96-125">Neighborhood loss</span></span>
<span data-ttu-id="85e96-126">**System.Federation** segnala un errore quando rileva una perdita di nodi vicini.</span><span class="sxs-lookup"><span data-stu-id="85e96-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="85e96-127">ID del nodo hello è incluso nel nome della proprietà hello report Hello è dai singoli nodi.</span><span class="sxs-lookup"><span data-stu-id="85e96-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="85e96-128">Se uno di risorse verrà persi nel anello Service Fabric intera hello, è possibile che in genere due eventi (entrambi i lati della relazione di distanza hello).</span><span class="sxs-lookup"><span data-stu-id="85e96-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="85e96-129">In caso di perdita di più nodi vicini, si verificano più eventi.</span><span class="sxs-lookup"><span data-stu-id="85e96-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="85e96-130">report Hello specifica il timeout di lease globale hello come ora di hello toolive.</span><span class="sxs-lookup"><span data-stu-id="85e96-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="85e96-131">report Hello viene nuovamente inviato a ogni parte della durata TTL hello finché la condizione hello rimane attivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="85e96-132">evento Hello viene rimosso automaticamente dopo la scadenza.</span><span class="sxs-lookup"><span data-stu-id="85e96-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="85e96-133">Rimuovere quando scaduto comportamento assicura che i report di hello è rimossi dall'archivio integrità hello correttamente, anche se il nodo di creazione rapporti hello è attivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="85e96-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="85e96-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="85e96-135">**Proprietà**: inizia con **Neighborhood** e include informazioni sul nodo</span><span class="sxs-lookup"><span data-stu-id="85e96-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="85e96-136">**Passaggi successivi**: analizzare perché le risorse di hello vanno persa (ad esempio, controllo hello comunicazione tra i nodi del cluster).</span><span class="sxs-lookup"><span data-stu-id="85e96-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="85e96-137">Report sull'integrità del sistema di nodi</span><span class="sxs-lookup"><span data-stu-id="85e96-137">Node system health reports</span></span>
<span data-ttu-id="85e96-138">**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="85e96-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="85e96-139">Ogni nodo deve avere un report generato da System.FM che mostra il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="85e96-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="85e96-140">le entità di nodo Hello vengono rimosse quando viene rimosso lo stato del nodo hello (vedere [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="85e96-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="85e96-141">Nodo attivo/inattivo</span><span class="sxs-lookup"><span data-stu-id="85e96-141">Node up/down</span></span>
<span data-ttu-id="85e96-142">Viene segnalato System.FM OK quando viene aggiunto a nodo hello anello hello (è attivo e in esecuzione).</span><span class="sxs-lookup"><span data-stu-id="85e96-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="85e96-143">Viene segnalato un errore quando il nodo hello si allontana anello hello (è attivo, uno per l'aggiornamento o semplicemente perché non è riuscito).</span><span class="sxs-lookup"><span data-stu-id="85e96-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="85e96-144">gerarchia di integrità Hello generato dall'archivio integrità hello interviene su entità distribuita in correlazione con i report del nodo System.FM.</span><span class="sxs-lookup"><span data-stu-id="85e96-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="85e96-145">Nodo hello considera un elemento virtuale padre di tutte le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="85e96-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="85e96-146">Se il nodo hello viene segnalato come backup per System.FM, con hello stessa istanza come istanza hello associato hello entità, entità Hello distribuito in tale nodo sono esposte tramite le query.</span><span class="sxs-lookup"><span data-stu-id="85e96-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="85e96-147">Quando System.FM segnala tale nodo hello è inattivo o riavviato (una nuova istanza), archivio integrità hello pulizia automatica delle entità hello distribuito che possono essere presenti solo in hello verso il basso nodo o sull'istanza precedente di hello del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="85e96-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="85e96-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="85e96-149">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="85e96-149">**Property**: State</span></span>
* <span data-ttu-id="85e96-150">**Passaggi successivi**: se il nodo hello è inattivo per un aggiornamento, deve disporre di eseguire il dopo che è stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="85e96-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="85e96-151">In questo caso, lo stato di integrità hello deve passare tooOK indietro.</span><span class="sxs-lookup"><span data-stu-id="85e96-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="85e96-152">Se non viene eseguito il ritorno nodo hello o ha esito negativo, il problema di hello deve ulteriori indagini.</span><span class="sxs-lookup"><span data-stu-id="85e96-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="85e96-153">Hello riportato di seguito evento System.FM hello con uno stato di integrità di OK per nodo:</span><span class="sxs-lookup"><span data-stu-id="85e96-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="85e96-154">Scadenza dei certificati</span><span class="sxs-lookup"><span data-stu-id="85e96-154">Certificate expiration</span></span>
<span data-ttu-id="85e96-155">**System.FabricNode** segnala un avviso quando i certificati utilizzati da nodo hello si avvicinano alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="85e96-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="85e96-156">Ogni nodo ha tre certificati: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="85e96-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="85e96-157">Una volta scadenza hello almeno due settimane, lo stato di integrità report hello è OK.</span><span class="sxs-lookup"><span data-stu-id="85e96-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="85e96-158">Una volta scadenza hello entro due settimane, il tipo di report hello è un avviso.</span><span class="sxs-lookup"><span data-stu-id="85e96-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="85e96-159">Durata (TTL) di questi eventi è infinito, e vengono rimossi quando un nodo abbandona cluster hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="85e96-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="85e96-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="85e96-161">**Proprietà**: inizia con **certificato** e contiene ulteriori informazioni sul tipo di certificato hello</span><span class="sxs-lookup"><span data-stu-id="85e96-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="85e96-162">**Passaggi successivi**: aggiornamento dei certificati di hello in tal caso prossimo alla scadenza.</span><span class="sxs-lookup"><span data-stu-id="85e96-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="85e96-163">Violazione della capacità di carico</span><span class="sxs-lookup"><span data-stu-id="85e96-163">Load capacity violation</span></span>
<span data-ttu-id="85e96-164">Hello bilanciamento del carico dell'infrastruttura di servizio restituisce un avviso quando rileva una violazione della capacità nodo.</span><span class="sxs-lookup"><span data-stu-id="85e96-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="85e96-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="85e96-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="85e96-166">**Proprietà**: inizia con **Capacity**</span><span class="sxs-lookup"><span data-stu-id="85e96-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="85e96-167">**Passaggi successivi**: controllo fornito capacità corrente hello metriche e visualizzare nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="85e96-168">Report sull'integrità del sistema di applicazioni</span><span class="sxs-lookup"><span data-stu-id="85e96-168">Application system health reports</span></span>
<span data-ttu-id="85e96-169">**System.CM**, che rappresenta il servizio di gestione Cluster hello, hello autorità che gestisce le informazioni relative a un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="85e96-170">Stato</span><span class="sxs-lookup"><span data-stu-id="85e96-170">State</span></span>
<span data-ttu-id="85e96-171">System.CM segnala come OK quando un'applicazione hello è stata creata o aggiornata.</span><span class="sxs-lookup"><span data-stu-id="85e96-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="85e96-172">Comunica archivio integrità hello quando un'applicazione hello è stata eliminata, in modo che può essere rimosso dall'archivio.</span><span class="sxs-lookup"><span data-stu-id="85e96-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="85e96-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="85e96-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="85e96-174">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="85e96-174">**Property**: State</span></span>
* <span data-ttu-id="85e96-175">**Passaggi successivi**: se un'applicazione hello è stata creata o aggiornata, deve includere il rapporto di stato gestione Cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="85e96-176">In caso contrario, controllare lo stato di hello di un'applicazione hello eseguendo una query (ad esempio, hello cmdlet PowerShell **ServiceFabricApplication di Get - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="85e96-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="85e96-177">Hello riportato di seguito evento dello stato di hello in hello **fabric: / WordCount** applicazione:</span><span class="sxs-lookup"><span data-stu-id="85e96-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="85e96-178">Report sull'integrità del sistema di servizi</span><span class="sxs-lookup"><span data-stu-id="85e96-178">Service system health reports</span></span>
<span data-ttu-id="85e96-179">**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sui servizi.</span><span class="sxs-lookup"><span data-stu-id="85e96-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="85e96-180">Stato</span><span class="sxs-lookup"><span data-stu-id="85e96-180">State</span></span>
<span data-ttu-id="85e96-181">System.FM segnala come OK quando il servizio di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="85e96-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="85e96-182">Elimina entità di hello dall'archivio integrità hello quando hello servizio è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="85e96-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="85e96-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="85e96-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="85e96-184">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="85e96-184">**Property**: State</span></span>

<span data-ttu-id="85e96-185">Hello riportato di seguito evento dello stato di hello sul servizio hello **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="85e96-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="85e96-186">Errore di correlazione del servizio</span><span class="sxs-lookup"><span data-stu-id="85e96-186">Service correlation error</span></span>
<span data-ttu-id="85e96-187">**System.PLB** segnala un errore quando rileva che un toobe servizio correlato a un altro servizio di aggiornamento crea una catena di affinità.</span><span class="sxs-lookup"><span data-stu-id="85e96-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="85e96-188">report Hello viene cancellato quando si verifica l'aggiornamento ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="85e96-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="85e96-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="85e96-190">**Proprietà**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="85e96-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="85e96-191">**Passaggi successivi**: hello controllo correlato alle descrizioni di servizi.</span><span class="sxs-lookup"><span data-stu-id="85e96-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="85e96-192">Report sull'integrità del sistema di partizioni</span><span class="sxs-lookup"><span data-stu-id="85e96-192">Partition system health reports</span></span>
<span data-ttu-id="85e96-193">**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sulle partizioni di servizio.</span><span class="sxs-lookup"><span data-stu-id="85e96-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="85e96-194">Stato</span><span class="sxs-lookup"><span data-stu-id="85e96-194">State</span></span>
<span data-ttu-id="85e96-195">System.FM segnala come OK quando partizione hello è stata creata ed è integro.</span><span class="sxs-lookup"><span data-stu-id="85e96-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="85e96-196">Elimina entità di hello dall'archivio integrità hello quando hello partizione viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="85e96-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="85e96-197">Se la partizione hello è inferiore al conteggio di replica minimo hello, viene segnalato un errore.</span><span class="sxs-lookup"><span data-stu-id="85e96-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="85e96-198">Se la partizione hello non è inferiore al conteggio di replica minimo hello, ma è inferiore al conteggio di replica di destinazione hello, viene segnalato un avviso.</span><span class="sxs-lookup"><span data-stu-id="85e96-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="85e96-199">Se la partizione hello è perso il quorum, System.FM segnala un errore.</span><span class="sxs-lookup"><span data-stu-id="85e96-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="85e96-200">Altri eventi importanti includono un avviso quando la riconfigurazione di hello richiede più tempo del previsto e quando la compilazione hello richiede più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="85e96-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="85e96-201">tempi di Hello previsto per la compilazione hello e riconfigurazione sono configurabili in base agli scenari di servizio.</span><span class="sxs-lookup"><span data-stu-id="85e96-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="85e96-202">Ad esempio, se un servizio è un terabyte di stato, ad esempio Database SQL, compilazione hello richiede più tempo per un servizio con una piccola quantità di stato.</span><span class="sxs-lookup"><span data-stu-id="85e96-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="85e96-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="85e96-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="85e96-204">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="85e96-204">**Property**: State</span></span>
* <span data-ttu-id="85e96-205">**Passaggi successivi**: se lo stato di integrità hello è OK, è possibile che alcune repliche non sono stato creato, aperto o innalzata di livello tooprimary o secondario correttamente.</span><span class="sxs-lookup"><span data-stu-id="85e96-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="85e96-206">In molti casi, causa radice di hello è un bug del servizio aprire hello e l'implementazione di modifica ruolo.</span><span class="sxs-lookup"><span data-stu-id="85e96-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="85e96-207">Hello di esempio seguente viene illustrata una partizione integro:</span><span class="sxs-lookup"><span data-stu-id="85e96-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="85e96-208">Hello riportato di seguito integrità hello di una partizione che si trova sotto il numero di repliche di destinazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="85e96-209">passaggio successivo Hello è tooget descrizione della partizione hello, che mostra come viene configurato: **MinReplicaSetSize** è tre e **TargetReplicaSetSize** sette.</span><span class="sxs-lookup"><span data-stu-id="85e96-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="85e96-210">Quindi ottenere il numero di hello di nodi nel cluster hello: cinque.</span><span class="sxs-lookup"><span data-stu-id="85e96-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="85e96-211">Pertanto, in questo caso, due repliche non possono trovarsi perché il numero di destinazione hello delle repliche è superiore hello numero di nodi disponibili.</span><span class="sxs-lookup"><span data-stu-id="85e96-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="replica-constraint-violation"></a><span data-ttu-id="85e96-212">Violazione del vincolo di replica</span><span class="sxs-lookup"><span data-stu-id="85e96-212">Replica constraint violation</span></span>
<span data-ttu-id="85e96-213">**System.PLB** segnala un avviso se rileva una violazione del vincolo di replica e non può posizionare tutte le repliche della partizione.</span><span class="sxs-lookup"><span data-stu-id="85e96-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="85e96-214">i vincoli di visualizzare i dettagli del rapporto Hello e proprietà impediscono l'inserimento di replica hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="85e96-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="85e96-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="85e96-216">**Proprietà**: inizia con **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="85e96-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="85e96-217">Report sull'integrità del sistema di repliche</span><span class="sxs-lookup"><span data-stu-id="85e96-217">Replica system health reports</span></span>
<span data-ttu-id="85e96-218">**System.RA**, che rappresenta una componente Agente di riconfigurazione hello, rappresenta l'autorità di hello per lo stato della replica hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="85e96-219">Stato</span><span class="sxs-lookup"><span data-stu-id="85e96-219">State</span></span>
<span data-ttu-id="85e96-220">**System.RA** segnala OK quando hello replica è stata creata.</span><span class="sxs-lookup"><span data-stu-id="85e96-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="85e96-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="85e96-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="85e96-222">**Proprietà**: State</span><span class="sxs-lookup"><span data-stu-id="85e96-222">**Property**: State</span></span>

<span data-ttu-id="85e96-223">Hello di esempio seguente viene illustrata una replica integro:</span><span class="sxs-lookup"><span data-stu-id="85e96-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="85e96-224">Stato aperto della replica</span><span class="sxs-lookup"><span data-stu-id="85e96-224">Replica open status</span></span>
<span data-ttu-id="85e96-225">descrizione di Hello di questo rapporto di stato contiene l'ora di inizio hello (Coordinated Universal Time) quando è stata richiamata hello API chiamata.</span><span class="sxs-lookup"><span data-stu-id="85e96-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="85e96-226">**System.RA** segnala un avviso se replica hello open richiede più tempo periodo hello configurata (impostazione predefinita: 30 minuti).</span><span class="sxs-lookup"><span data-stu-id="85e96-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="85e96-227">Se hello API influisce sulla disponibilità del servizio, report hello è emesso molto più veloce (un intervallo configurabile, con valore predefinito è 30 secondi).</span><span class="sxs-lookup"><span data-stu-id="85e96-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="85e96-228">tempo Hello misurato include tempo hello per replicator hello aperto e il servizio di hello aperto.</span><span class="sxs-lookup"><span data-stu-id="85e96-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="85e96-229">Hello proprietà modifiche tooOK se apre hello completa.</span><span class="sxs-lookup"><span data-stu-id="85e96-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="85e96-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="85e96-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="85e96-231">**Proprietà**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="85e96-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="85e96-232">**Passaggi successivi**: se lo stato di integrità hello non è corretta, esaminare perché replica hello open richiede più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="85e96-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="85e96-233">Chiamata API del servizio lenta</span><span class="sxs-lookup"><span data-stu-id="85e96-233">Slow service API call</span></span>
<span data-ttu-id="85e96-234">**System.RAP** e **System.Replicator** segnala un avviso se un codice del servizio chiamata toohello utente impiegato più tempo di hello configurato di.</span><span class="sxs-lookup"><span data-stu-id="85e96-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="85e96-235">avviso di Hello viene cancellata al completamento della chiamata di hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="85e96-236">**SourceId**: System.RAP o System.Replicator</span><span class="sxs-lookup"><span data-stu-id="85e96-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="85e96-237">**Proprietà**: nome hello dell'API lenta hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="85e96-238">descrizione di Hello fornisce ulteriori dettagli su hello ora hello API è stato in sospeso.</span><span class="sxs-lookup"><span data-stu-id="85e96-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="85e96-239">**Passaggi successivi**: analizzare perché chiamata hello richiede più tempo del previsto.</span><span class="sxs-lookup"><span data-stu-id="85e96-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="85e96-240">Hello di esempio seguente mostra una partizione in perdita del quorum e hello analisi eseguiti passaggi toofigure motivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="85e96-241">Una delle repliche hello ha uno stato di integrità di avviso, per ottenere l'integrità.</span><span class="sxs-lookup"><span data-stu-id="85e96-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="85e96-242">Viene illustrato che l'operazione del servizio hello impiega più tempo del previsto, un evento segnalato dal System.RAP.</span><span class="sxs-lookup"><span data-stu-id="85e96-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="85e96-243">Dopo la ricezione di queste informazioni, passaggio successivo hello è toolook al codice del servizio hello e analizzare non esiste.</span><span class="sxs-lookup"><span data-stu-id="85e96-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="85e96-244">In questo caso, hello **RunAsync** implementazione del servizio con stato hello genera un'eccezione non gestita.</span><span class="sxs-lookup"><span data-stu-id="85e96-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="85e96-245">repliche Hello sono riciclo, in modo non sarà possibile visualizzare tutte le repliche in uno stato di avviso hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="85e96-246">È possibile ripetere il recupero dello stato di integrità hello e cercare eventuali differenze nell'ID di replica hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="85e96-247">In alcuni casi, i tentativi di hello possono fornire indicazioni.</span><span class="sxs-lookup"><span data-stu-id="85e96-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="85e96-248">Quando si avvia un'applicazione hello non corretto nel debugger hello, finestre di eventi di diagnostica hello mostrano eccezione hello generata da RunAsync:</span><span class="sxs-lookup"><span data-stu-id="85e96-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Eventi di diagnostica di Visual Studio 2015: errore RunAsync in fabric:/HelloWorldStatefulApplication.][1]

<span data-ttu-id="85e96-250">Eventi di diagnostica di Visual Studio 2015: errore RunAsync in **fabric:/HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="85e96-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="85e96-251">Coda di replica piena</span><span class="sxs-lookup"><span data-stu-id="85e96-251">Replication queue full</span></span>
<span data-ttu-id="85e96-252">**System.Replicator** genera un avviso quando la coda di replica hello è piena.</span><span class="sxs-lookup"><span data-stu-id="85e96-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="85e96-253">Hello primario, la coda di replica in genere diventa completa perché una o più repliche secondarie sono operazioni tooacknowledge lento.</span><span class="sxs-lookup"><span data-stu-id="85e96-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="85e96-254">In hello secondario, questo in genere si verifica quando il servizio di hello è lenta tooapply hello operazioni.</span><span class="sxs-lookup"><span data-stu-id="85e96-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="85e96-255">avviso di Hello viene cancellato quando la coda hello non è più completa.</span><span class="sxs-lookup"><span data-stu-id="85e96-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="85e96-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="85e96-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="85e96-257">**Proprietà**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, a seconda del ruolo della replica hello</span><span class="sxs-lookup"><span data-stu-id="85e96-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="85e96-258">Operazioni di Naming lente</span><span class="sxs-lookup"><span data-stu-id="85e96-258">Slow Naming operations</span></span>
<span data-ttu-id="85e96-259">**System.NamingService** segnala lo stato di integrità per la replica primaria quando un'operazione di Naming richiede più tempo di quanto sia accettabile.</span><span class="sxs-lookup"><span data-stu-id="85e96-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="85e96-260">Esempi di operazioni di Naming sono [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) e [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="85e96-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="85e96-261">Altri metodi sono disponibili in FabricClient, ad esempio nell'ambito dei [metodi di gestione dei servizi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o dei [metodi di gestione delle proprietà](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="85e96-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="85e96-262">Hello Naming service risolve percorso tooa i nomi del servizio cluster hello e consente di proprietà e i nomi di servizio toomanage utenti.</span><span class="sxs-lookup"><span data-stu-id="85e96-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="85e96-263">È un servizio permanente partizionato di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85e96-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="85e96-264">Una delle partizioni hello rappresenta hello Authority Owner, che contiene i metadati relativi a tutti i servizi e i nomi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="85e96-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="85e96-265">i nomi di Service Fabric Hello sono mappate toodifferent partizioni, chiamate partizioni nome proprietario, pertanto il servizio di hello è estensibile.</span><span class="sxs-lookup"><span data-stu-id="85e96-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="85e96-266">Per altre informazioni, vedere [Architettura di Service Fabric](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="85e96-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="85e96-267">Quando un'operazione di denominazione richiede più tempo del previsto, operazione hello è contrassegnata con un report di avviso su hello *replica primaria di hello partizione del servizio di denominazione che serve operazione hello*.</span><span class="sxs-lookup"><span data-stu-id="85e96-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="85e96-268">Se il completamento dell'operazione di hello, hello avviso è deselezionato.</span><span class="sxs-lookup"><span data-stu-id="85e96-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="85e96-269">Se hello concludere con un errore, il rapporto di stato hello include dettagli sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="85e96-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="85e96-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="85e96-271">**Proprietà**: inizia con prefisso **Duration_** e identifica operazione lenta hello e il nome di Service Fabric hello in cui hello viene applicata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="85e96-272">Ad esempio, se creare infrastruttura nome servizio: / MyApp/MyService impiega troppo tempo, la proprietà hello Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="85e96-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="85e96-273">Ruolo di toohello AO punti di hello partizione di denominazione per il nome e l'operazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="85e96-274">**Passaggi successivi**: controllo perché hello denominazione operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="85e96-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="85e96-275">A ogni operazione può corrispondere una causa radice diversa.</span><span class="sxs-lookup"><span data-stu-id="85e96-275">Each operation can have different root causes.</span></span> <span data-ttu-id="85e96-276">Ad esempio, l'eliminazione di servizio potrebbe trovarsi in un nodo perché mantiene un arresto anomalo host applicazione hello in un nodo a causa di bug utente tooa nel codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="85e96-277">Hello di esempio seguente viene illustrata un'operazione di servizio di creazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="85e96-278">operazione Hello ha richiesto più tempo rispetto a durata hello configurato.</span><span class="sxs-lookup"><span data-stu-id="85e96-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="85e96-279">AO Ritenta e invia tooNO di lavoro.</span><span class="sxs-lookup"><span data-stu-id="85e96-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="85e96-280">Nessuna operazione ultimo hello completato con Timeout.</span><span class="sxs-lookup"><span data-stu-id="85e96-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="85e96-281">In questo caso, hello stessa replica è primaria per hello AO sia alcun ruolo.</span><span class="sxs-lookup"><span data-stu-id="85e96-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="85e96-282">Report sull'integrità del sistema DeployedApplication</span><span class="sxs-lookup"><span data-stu-id="85e96-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="85e96-283">**System.Hosting** autorità hello per le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="85e96-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="85e96-284">Activation</span><span class="sxs-lookup"><span data-stu-id="85e96-284">Activation</span></span>
<span data-ttu-id="85e96-285">System.Hosting segnala come OK quando un'applicazione è stata attivata nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="85e96-286">In caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="85e96-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="85e96-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-288">**Proprietà**: attivazione, compresa hello implementazione versione</span><span class="sxs-lookup"><span data-stu-id="85e96-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="85e96-289">**Passaggi successivi**: se un'applicazione hello è integra, provare a causa dell'errore attivazione hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="85e96-290">Hello seguente illustra l'attivazione:</span><span class="sxs-lookup"><span data-stu-id="85e96-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="85e96-291">Scaricare</span><span class="sxs-lookup"><span data-stu-id="85e96-291">Download</span></span>
<span data-ttu-id="85e96-292">**System.Hosting** segnala un errore se si verifica un errore di download del pacchetto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="85e96-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-294">**Proprietà**: **Download:*VersioneRollout***</span><span class="sxs-lookup"><span data-stu-id="85e96-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="85e96-295">**Passaggi successivi**: analizzare perché download hello non è riuscito nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="85e96-296">Report sull'integrità del sistema DeployedServicePackage</span><span class="sxs-lookup"><span data-stu-id="85e96-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="85e96-297">**System.Hosting** autorità hello per le entità distribuite.</span><span class="sxs-lookup"><span data-stu-id="85e96-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="85e96-298">Attivazione del pacchetto di servizi</span><span class="sxs-lookup"><span data-stu-id="85e96-298">Service package activation</span></span>
<span data-ttu-id="85e96-299">System.Hosting segnala come OK se l'attivazione del pacchetto di servizio nel nodo hello hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="85e96-300">In caso contrario, restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="85e96-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="85e96-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-302">**Proprietà**: Activation</span><span class="sxs-lookup"><span data-stu-id="85e96-302">**Property**: Activation</span></span>
* <span data-ttu-id="85e96-303">**Passaggi successivi**: provare a causa dell'errore attivazione hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="85e96-304">Attivazione del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="85e96-304">Code package activation</span></span>
<span data-ttu-id="85e96-305">**System.Hosting** segnala come OK per ogni pacchetto di codice se hello attivazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="85e96-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="85e96-306">Se l'attivazione di hello ha esito negativo, genera un avviso in base alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="85e96-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="85e96-307">Se **CodePackage** ha esito negativo tooactivate o termina con un errore maggiore hello configurato **CodePackageHealthErrorThreshold**, hosting segnala un errore.</span><span class="sxs-lookup"><span data-stu-id="85e96-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="85e96-308">Se un pacchetto servizio contiene più pacchetti di codice, viene generato un report sull'attivazione per ognuno.</span><span class="sxs-lookup"><span data-stu-id="85e96-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="85e96-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-310">**Proprietà**: prefisso hello utilizza **CodePackageActivation** e contiene il nome di hello del pacchetto di codice hello e il punto di ingresso hello come  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint** * (ad esempio, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="85e96-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="85e96-311">Registrazione del tipo di servizio</span><span class="sxs-lookup"><span data-stu-id="85e96-311">Service type registration</span></span>
<span data-ttu-id="85e96-312">**System.Hosting** segnala come OK se il tipo di servizio hello è stato registrato correttamente.</span><span class="sxs-lookup"><span data-stu-id="85e96-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="85e96-313">Viene segnalato un errore se non è stata effettuata la registrazione di hello nel tempo (in base alla configurazione utilizzando **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="85e96-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="85e96-314">Se il runtime hello è chiuso, il tipo di servizio hello è stato annullato dal nodo hello e Hosting segnala un avviso.</span><span class="sxs-lookup"><span data-stu-id="85e96-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="85e96-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-316">**Proprietà**: prefisso hello utilizza **ServiceTypeRegistration** e contiene il nome di tipo servizio hello (ad esempio, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="85e96-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="85e96-317">Hello di esempio seguente viene illustrato un pacchetto del servizio distribuito integro:</span><span class="sxs-lookup"><span data-stu-id="85e96-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="85e96-318">Scaricare</span><span class="sxs-lookup"><span data-stu-id="85e96-318">Download</span></span>
<span data-ttu-id="85e96-319">**System.Hosting** segnala un errore se si verifica un errore di download del pacchetto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="85e96-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-321">**Proprietà**: **Download:*VersioneRollout***</span><span class="sxs-lookup"><span data-stu-id="85e96-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="85e96-322">**Passaggi successivi**: analizzare perché download hello non è riuscito nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="85e96-323">Convalida dell’aggiornamento</span><span class="sxs-lookup"><span data-stu-id="85e96-323">Upgrade validation</span></span>
<span data-ttu-id="85e96-324">**System.Hosting** segnala un errore se la convalida durante l'aggiornamento di hello non riesce o se hello aggiornamento ha esito negativo nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="85e96-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="85e96-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="85e96-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="85e96-326">**Proprietà**: prefisso hello utilizza **FabricUpgradeValidation** e contiene la versione di hello aggiornamento</span><span class="sxs-lookup"><span data-stu-id="85e96-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="85e96-327">**Descrizione**: punti di errore toohello</span><span class="sxs-lookup"><span data-stu-id="85e96-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="85e96-328">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85e96-328">Next steps</span></span>
[<span data-ttu-id="85e96-329">Come visualizzare i report sull'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="85e96-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="85e96-330">Come tooreport e controllo del servizio integrità</span><span class="sxs-lookup"><span data-stu-id="85e96-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="85e96-331">Monitorare e diagnosticare servizi in locale</span><span class="sxs-lookup"><span data-stu-id="85e96-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="85e96-332">Aggiornamento di un'applicazione di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="85e96-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

