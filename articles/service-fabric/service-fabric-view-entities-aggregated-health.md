---
title: "aaaHow tooview Azure Service Fabric entità aggregato di integrità | Documenti Microsoft"
description: "Viene descritto come tooquery, visualizzare e valutare l'integrità di entità Azure Service Fabric aggregato, tramite query sull'integrità e le query generali."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Come visualizzare i report sull'integrità di Service Fabric
Azure Service Fabric introduce un [modello di integrità](service-fabric-health-introduction.md) con entità di integrità per le quali i componenti di sistema e i watchdog possono creare report sulle condizioni locali sottoposte a monitoraggio. Hello [archivio integrità](service-fabric-health-introduction.md#health-store) aggrega tutti toodetermine di dati di integrità se le entità siano integri.

cluster Hello viene popolato automaticamente con i rapporti di stati inviati dai componenti di sistema hello. Leggere informazioni, vedere [tootroubleshoot report l'integrità di sistema utilizzare](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Infrastruttura del servizio sono disponibili più modi tooget hello aggregato integrità di entità hello:

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) o altri strumenti di visualizzazione
* Query di integrità (tramite PowerShell, API o REST)
* Generale query che restituiscono un elenco di entità che dispongono di integrità come una delle proprietà di hello (tramite PowerShell, API o REST)

toodemonstrate queste opzioni, consente l'utilizzo di un cluster locale con cinque nodi e hello [fabric: / applicazione WordCount](http://aka.ms/servicefabric-wordcountapp). Hello **fabric: / WordCount** applicazione contiene due servizi predefiniti, un servizio con stato di tipo `WordCountServiceType`e un servizio senza stato di tipo `WordCountWebServiceType`. In seguito alla modifica hello `ApplicationManifest.xml` toorequire sette repliche di destinazione per i servizi con stato hello e una partizione. Poiché sono presenti solo cinque nodi nel cluster hello, i componenti di sistema hello report un avviso sulla partizione di servizio hello perché è inferiore al conteggio di destinazione hello.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Integrità in Esplora Infrastruttura di servizi
Service Fabric Explorer fornisce una visualizzazione di cluster hello. Nell'immagine hello riportata di seguito, è possibile vedere che:

* applicazione Hello **fabric: / WordCount** è rosso (errore) perché dispone di un evento di errore segnalato da **MyWatchdog** per la proprietà hello **disponibilità**.
* Uno dei servizi di questa applicazione, **fabric:/WordCount/WordCountService** è di colore giallo (condizione di avviso). servizio Hello è configurato con le sette repliche e cluster hello include cinque nodi, in modo non è possibile inserire due repicas. Sebbene non illustrato di seguito, partizione del servizio hello è giallo a causa di un report di sistema da `System.FM` che informa che `Partition is below target replica or instance count`. i trigger di partizione giallo Hello hello servizio giallo.
* cluster Hello è rosso a causa di un'applicazione hello rosso.

valutazione Hello utilizza criteri predefiniti dal manifesto del cluster hello e manifesto dell'applicazione. Questi sono criteri rigorosi e non tollerano errori.

Visualizzazione del cluster di hello di Service Fabric Explorer:

![Visualizzazione del cluster di hello di Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Ulteriori informazioni su [Esplora Infrastruttura di servizi](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Query relative all’integrità
Service Fabric espone una query sull'integrità per ogni hello supportato [tipi di entità](service-fabric-health-introduction.md#health-entities-and-hierarchy). Sono accessibili mediante API, utilizzando i metodi di hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), i cmdlet di PowerShell e REST. Queste query restituiscono informazioni di stato completo sull'entità hello: hello aggregati lo stato di integrità, gli eventi di integrità di entità, gli stati di integrità figlio (se applicabile), non integro valutazioni (quando l'entità hello non integro) e le statistiche di integrità di elementi figlio (quando applicabile).

> [!NOTE]
> Un'entità di integrità viene restituita quando viene compilata completamente nell'archivio integrità hello. entità Hello deve essere attivo (non eliminata) e dispone di un report di sistema. Le entità padre nella catena della gerarchia hello devono inoltre disporre di report del sistema. Se una di queste condizioni non vengono soddisfatti, integrità hello query restituiscono un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) con [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` che mostra perché non vengono restituite entità hello.
>
>

Identificatore dell'entità hello, che dipende dal tipo di entità hello deve passare query sull'integrità Hello. le query Hello accettano parametri dei criteri di integrità facoltativi. Se non è stato specificato alcun criterio di integrità, hello [criteri di integrità](service-fabric-health-introduction.md#health-policies) dal manifesto del cluster o l'applicazione hello vengono utilizzati per la valutazione. Se i manifesti hello non contengono una definizione di criteri di integrità, criteri di integrità hello predefiniti vengono utilizzati per la valutazione. criteri di integrità Hello predefinito non essere in grado di tollerare eventuali errori. le query Hello accettano anche i filtri per la restituzione solo elementi figlio parziali o eventi: hello quelli che rispettano hello i filtri specificati. Un altro filtro consente di escludere le statistiche di hello elementi figlio.

> [!NOTE]
> i filtri di output di Hello vengono applicati sul lato server hello, pertanto le dimensioni di risposta messaggio hello sono ridotto. Si consiglia di utilizzare i filtri di output di hello toolimit hello dati restituito, anziché applicano filtri sul lato client hello.
>
>

L'integrità di un'entità contiene quanto segue:

* Hello lo stato di integrità aggregato dell'entità hello. Calcolato dall'archivio integrità hello basato su rapporti di integrità di entità, gli stati di integrità figlio (se applicabile) e criteri di integrità. Per altre informazioni, vedere [valutazione dell'integrità dell'entità](service-fabric-health-introduction.md#health-evaluation).  
* eventi di integrità Hello nell'entità hello.
* raccolta di Hello degli stati di integrità di tutti gli elementi figlio per le entità hello possono avere elementi figlio. gli stati di integrità Hello contengono gli identificatori di entità e hello stato di integrità aggregato. tooget stato completo per un elemento figlio, chiamare integrità query hello per tipo di entità figlio hello e passare identificatore figlio hello.
* le valutazioni di tipo non integro Hello toohello tale punto del report che attivata stato hello dell'entità di hello, se l'entità hello non è integro. valutazioni Hello sono ricorsivi, contenente valutazioni dell'integrità hello figli che ha attivato lo stato di integrità. Un watchdog ha segnalato ad esempio un errore in una replica. integrità applicazione Hello viene illustrata una versione di valutazione non integro scadenza tooan servizio di tipo non integro. servizio di Hello è danneggiato a causa di partizione tooa in errore. partizione di Hello è danneggiato a causa di replica tooa in errore. non è integro scadenza rapporto di stato di errore watchdog toohello replica Hello.
* statistiche di integrità Hello per tutti i tipi di elementi figlio di entità hello che hanno elementi figlio. Ad esempio, l'integrità del cluster Mostra hello il numero totale di applicazioni, servizi, partizioni, le repliche e distribuiti entità cluster hello. Stato servizio Mostra numero totale di hello di partizioni e repliche in hello servizio specificato.

## <a name="get-cluster-health"></a>Get cluster health
Restituisce l'integrità di entità cluster hello hello e contiene hello gli stati di integrità delle applicazioni e i nodi (elementi figlio del cluster hello). Input:

* Criteri di integrità del cluster [facoltativo] hello utilizzato nodi hello tooevaluate e gli eventi cluster hello.
* Mappa criteri di integrità dell'applicazione di hello [facoltativo], con i criteri di integrità hello utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per eventi, i nodi e le applicazioni che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi, i nodi e le applicazioni sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.
* [Facoltativo] Filtrare le statistiche di integrità tooexclude.
* [Facoltativo] Filtrare tooinclude fabric: / statistiche di integrità del sistema in hello delle statistiche di integrità. Questo campo è applicabile solo quando non sono escluse le statistiche di integrità hello. Per impostazione predefinita, le statistiche di integrità hello includono solo le statistiche per le applicazioni utente e non un'applicazione hello del sistema.

### <a name="api"></a>API
tooget integrità del cluster, creare un `FabricClient` chiamata hello e [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) metodo relativo **HealthManager**.

Hello chiamata seguente ottiene l'integrità del cluster hello:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Hello codice seguente ottiene l'integrità del cluster hello utilizzando un criterio di integrità del cluster personalizzato e i filtri per i nodi e applicazioni. Specifica che le statistiche di integrità hello includono infrastruttura hello: / statistiche di sistema. Crea [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), che contiene informazioni di input hello.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integrità del cluster hello tooget cmdlet Hello è [Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello stato del cluster hello è cinque nodi, l'applicazione di sistema hello e fabric: / WordCount configurato come descritto.

Hello cmdlet seguente ottiene l'integrità del cluster tramite criteri di integrità predefinito. Hello stato di integrità aggregato è avviso, in quanto hello fabric: / applicazione WordCount è in avviso. Si noti come valutazioni integro hello forniscono dettagli sulle condizioni di hello che ha attivato integrità hello aggregato.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Hello cmdlet di PowerShell seguente ottiene hello integrità del cluster hello utilizzando un criterio di applicazione personalizzata. Filtra i risultati tooget solo le applicazioni e i nodi in errore o avviso. Di conseguenza, non vengono restituiti nodi, perché sono tutti integri. Solo hello fabric: / applicazione WordCount rispetta filtro applicazioni hello. Poiché i criteri personalizzati di hello specificano tooconsider avvisi come errori per l'infrastruttura di hello: / applicazione WordCount, un'applicazione hello viene valutata come in errore e pertanto è hello cluster.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità del cluster con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-node-health"></a>Get node health
Restituisce hello integrità di un'entità del nodo e contiene gli eventi di integrità hello segnalati nel nodo hello. Input:

* Nome del nodo hello [obbligatorio] che identifica il nodo hello.
* Impostazioni dei criteri di integrità del cluster [facoltativo] hello utilizzato tooevaluate integrità.
* [Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.

### <a name="api"></a>API
integrità del nodo tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) metodo relativo HealthManager.

Hello codice seguente ottiene integrità del nodo per il nome di nodo specificato hello hello:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Hello codice seguente ottiene integrità del nodo hello per hello specificato nome di nodo e passa nel filtro di eventi e criteri personalizzati tramite [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integrità del nodo hello tooget cmdlet Hello è [Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.
Hello seguente cmdlet Ottiene l'integrità del nodo hello tramite criteri di integrità predefinito:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello cmdlet seguente ottiene hello integrità di tutti i nodi nel cluster hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità del nodo con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-application-health"></a>Ottieni lo stato dell'integrità dell'applicazione
Restituisce hello integrità di un'entità di applicazione. Contiene gli stati di integrità hello di un'applicazione hello distribuito e gli elementi figlio del servizio. Input:

* Hello [obbligatorio] nome dell'applicazione (URI) che identifica un'applicazione hello.
* Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi, servizi e applicazioni distribuite che specificano le voci che sono di interesse e devono essere restituiti nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi, servizi e applicazioni distribuite sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.
* [Facoltativo] Filtrare le statistiche di integrità hello tooexclude. Se non specificato, le statistiche di integrità hello includono hello ok, avviso e il numero di errore per tutti gli elementi figlio dell'applicazione: servizi, partizioni e repliche, le applicazioni distribuite e distribuiti i pacchetti del servizio.

### <a name="api"></a>API
integrità applicazione tooget, creare un `FabricClient` chiamata hello e [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) metodo relativo HealthManager.

Hello codice seguente ottiene lo stato di applicazioni hello per nome dell'applicazione specificato hello (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Hello codice seguente ottiene integrità applicazione hello per nome dell'applicazione specificato hello (URI), con i filtri e i criteri personalizzati specificati tramite [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
l'integrità dell'applicazione Hello cmdlet tooget hello è [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

il cmdlet seguente Hello restituisce integrità hello di hello **fabric: / WordCount** applicazione:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Hello seguendo i passaggi di cmdlet di PowerShell nei criteri personalizzati. Filtra anche gli elementi figlio e gli eventi.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità dell'applicazione con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-service-health"></a>Get service health
Restituisce hello integrità di un'entità servizio. Contiene gli stati di integrità di hello partizione. Input:

* Hello [obbligatorio] nome del servizio (URI) che identifica il servizio di hello.
* Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi e le partizioni che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi e le partizioni sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.
* [Facoltativo] Filtrare le statistiche di integrità tooexclude. Se non specificato, hello hello Mostra le statistiche di integrità ok, avviso e errore numero per tutte le partizioni e repliche del servizio hello.

### <a name="api"></a>API
integrità del servizio tooget attraverso hello API, creare un `FabricClient` chiamata hello e [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) metodo relativo HealthManager.

Hello seguente esempio ottiene hello integrità di un servizio con il nome di servizio specifico (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

il codice seguente Hello Ottiene hello dell'integrità del servizio per nome del servizio specificato hello (URI), specificando i filtri e i criteri personalizzati tramite [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hello cmdlet tooget hello servizio integrità è [Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello seguente cmdlet Ottiene integrità servizio hello tramite criteri di integrità predefiniti:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità del servizio con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-partition-health"></a>Get partition health
Restituisce hello integrità di un'entità di partizione. Contiene gli stati di integrità replica hello. Input:

* Partizione hello [obbligatorio] ID (GUID) che identifica la partizione hello.
* Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi e le repliche che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi e le repliche sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.
* [Facoltativo] Filtrare le statistiche di integrità tooexclude. Se non specificato, le statistiche di integrità hello mostrano il numero di repliche ok, avviso ed errore stati.

### <a name="api"></a>API
integrità della partizione tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) metodo relativo HealthManager. parametri facoltativi toospecify, creare [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
integrità della partizione hello tooget cmdlet Hello è [Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello seguente ottiene integrità hello per tutte le partizioni di hello **fabric: / WordCount/WordCountService** servizio ed esclude quelli gli stati di integrità di replica:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità della partizione con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-replica-health"></a>Get replica health
Restituisce l'integrità di hello di una replica del servizio con stato o un'istanza del servizio senza stato. Input:

* Hello [obbligatorio] ID (GUID) e replica ID partizione che identifica hello replica.
* Parametri dei criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.

### <a name="api"></a>API
integrità della replica hello tooget tramite hello API, creare un `FabricClient` chiamata hello e [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) metodo relativo HealthManager. Utilizzare parametri avanzati toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
integrità della replica hello tooget cmdlet Hello è [Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello cmdlet seguente ottiene hello integrità della replica primaria di hello per tutte le partizioni del servizio hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità della replica con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-deployed-application-health"></a>Ottieni lo stato dell'integrità delle applicazioni distribuite.
Restituisce hello integrità di un'applicazione distribuita in un'entità del nodo. Contiene gli stati di integrità pacchetto servizio hello distribuito. Input:

* Nome dell'applicazione hello [obbligatorio] (URI) e il nome di nodo (stringa) che identificano hello applicazione distribuita.
* Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi e i pacchetti del servizio distribuiti che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi e i pacchetti del servizio distribuito sono lo stato dell'entità aggregati hello tooevaluate utilizzato, indipendentemente dal filtro hello.
* [Facoltativo] Filtrare le statistiche di integrità tooexclude. Se non specificato, le statistiche di integrità hello mostrano il numero di hello di pacchetti del servizio distribuiti negli Stati di integrità ok, avviso e di errore.

### <a name="api"></a>API
integrità hello tooget di un'applicazione distribuita in un nodo tramite hello API, creare un `FabricClient` chiamata hello e [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) metodo relativo HealthManager. Utilizzare parametri facoltativi toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
è Hello integrità dell'applicazione hello distribuito cmdlet tooget [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toofind out in cui viene distribuita un'applicazione, eseguire [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ed esaminerà hello distribuiti gli elementi figlio dell'applicazione.

il cmdlet seguente Hello Ottiene integrità hello di hello **fabric: / WordCount** applicazione distribuita in **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità dell'applicazione distribuita con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="get-deployed-service-package-health"></a>Get deployed service package health
Restituisce hello integrità di un'entità di pacchetto del servizio distribuito. Input:

* Nome dell'applicazione hello [obbligatorio] (URI), il nome di nodo (stringa) e nome del manifesto del servizio (string) che identificano hello distribuiti pacchetto del servizio.
* Criteri di integrità dell'applicazione hello [facoltativo] utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per gli eventi che specificano le voci di interesse e devono essere restituite nel risultato hello (ad esempio, solo gli errori o avvisi e gli errori). Tutti gli eventi sono di integrità aggregato dell'entità di hello tooevaluate utilizzato, indipendentemente dal filtro hello.

### <a name="api"></a>API
integrità hello tooget di un pacchetto del servizio distribuito tramite hello API, creare un `FabricClient` chiamata hello e [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) metodo relativo HealthManager. Utilizzare parametri facoltativi toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
è Hello integrità del pacchetto del servizio distribuito hello tooget cmdlet [Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toosee in cui viene distribuita un'applicazione, eseguire [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ed esaminare le applicazioni distribuita hello. toosee i pacchetti del servizio in un'applicazione, cercare nella hello distribuito gli elementi figlio del pacchetto di servizio in hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.

il cmdlet seguente Hello Ottiene integrità hello di hello **WordCountServicePkg** pacchetto del servizio di hello **fabric: / WordCount** applicazione distribuita in **_Node_2**. entità Hello è **System.Hosting** report per l'attivazione del pacchetto di servizio e del punto di ingresso e tipo di servizio di registrazione corretta.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
È possibile ottenere l'integrità del pacchetto del servizio distribuito con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) che include criteri di integrità descritti nel corpo di hello.

## <a name="health-chunk-queries"></a>Query sul blocco di integrità
query di blocchi sull'integrità Hello può restituire gli elementi figlio di un cluster a più livelli (ricorsivo), per i filtri di input. Supporta i filtri avanzati che consentono una notevole flessibilità nella scelta di elementi figlio di hello toobe restituito. i filtri di Hello possono specificare gli elementi figlio da un identificatore univoco hello o altri identificatori di gruppo e/o gli stati di integrità. Per impostazione predefinita, non è incluso, come i comandi toohealth anziché sempre includono gli elementi figlio di primo livello elementi figlio.

Hello [query sull'integrità](service-fabric-view-entities-aggregated-health.md#health-queries) restituiti elementi figlio di primo livello solo di hello specificato entità per i filtri necessari. tooget hello figli dei figli di hello, è necessario chiamare integrità altre API per ogni entità di interesse. Analogamente, dello stato di hello tooget di entità specifico, è necessario chiamare uno stato API per ogni entità desiderata. Hello blocco query filtro avanzato consente toorequest più elementi di interesse in un'unica query, riducendo al minimo la dimensione dei messaggi hello e numero di hello di messaggi.

il valore di Hello di query di blocco hello è che è possibile ottenere lo stato di integrità per più cluster le entità (potenzialmente tutti i cluster entità a partire dalla radice obbligatorio) in un'unica chiamata. È possibile esprimere query sull'integrità complesse, ad esempio:

* Restituzione solo delle applicazioni con errore e inclusione di tutti i servizi con avviso o errore per queste applicazioni. Per i servizi restituiti, inclusione di tutte le partizioni.
* Restituire solo hello dello stato di quattro applicazioni, specificato con i relativi nomi.
* Restituire solo hello dello stato di applicazioni di un tipo di applicazione desiderata.
* Restituzione di tutte le entità distribuite su un nodo. Restituisce tutte le applicazioni, tutte le applicazioni distribuite nel nodo specificato hello e tutti i pacchetti hello distribuito servizio su tale nodo.
* Restituzione di tutte le repliche con errore. Vengono restituiti tutti i servizi, le applicazioni e le partizioni e le sole repliche con errore.
* Restituzione di tutte le applicazioni. Per un servizio specificato, inclusione di tutte le partizioni.

Attualmente, query di blocco integrità hello viene esposta solo per entità di cluster hello. Restituisce un blocco di integrità del cluster che contiene:

* stato di integrità aggregato cluster Hello.
* Hello integrità stato blocco elenco di nodi che rispettano i filtri di input.
* Hello integrità stato blocco elenco di applicazioni che rispettano i filtri di input. Ogni blocco di stato di integrità dell'applicazione contiene un elenco di blocco con tutti i servizi che rispettano i filtri di input e un elenco di blocco con tutte le applicazioni distribuite che rispettano i filtri di hello. Uguale per gli elementi figlio hello dei servizi e applicazioni distribuite. In questo modo, tutte le entità nel cluster hello possono essere potenzialmente restituite se richiesto, in modo gerarchico.

### <a name="cluster-health-chunk-query"></a>Query sul blocco di integrità del cluster
Restituisce l'integrità di entità cluster hello hello e contiene blocchi di stato di integrità gerarchica hello di figli obbligatori. Input:

* Criteri di integrità del cluster [facoltativo] hello utilizzato nodi hello tooevaluate e gli eventi cluster hello.
* Mappa criteri di integrità dell'applicazione di hello [facoltativo], con i criteri di integrità hello utilizzato Criteri di manifesto dell'applicazione hello toooverride.
* [Facoltativo] Filtri per i nodi e le applicazioni che specificano le voci di interesse e devono essere restituite nel risultato hello. i filtri di Hello sono entità tooan specifico/gruppo di entità o entità tooall applicabile a tale livello. elenco di Hello dei filtri può contenere un filtro generale e/o i filtri per le entità con granularità fine toofine identificatori specifici restituiti dalla query hello. Se vuoto, gli elementi figlio hello non vengono restituiti per impostazione predefinita.
  Ulteriori informazioni sui filtri hello [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). in modo ricorsivo di Hello applicazione filtri possono specificare i filtri avanzati per gli elementi figlio.

il risultato di blocco Hello include elementi figlio di hello che rispettano i filtri di hello.

Attualmente, hello blocco restituiti valutazioni non integro o eventi di entità. Informazioni aggiuntive possono essere ottenuti utilizzando query di integrità del cluster esistente hello.

### <a name="api"></a>API
integrità del cluster tooget blocco, creare un `FabricClient` chiamata hello e [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) metodo relativo **HealthManager**. È possibile passare [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe criteri di integrità e filtri avanzati.

Hello codice seguente ottiene il blocco di integrità del cluster con i filtri avanzati.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
integrità del cluster hello tooget cmdlet Hello è [Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). In primo luogo, connettere il cluster di toohello utilizzando hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hello codice seguente ottiene i nodi solo se sono in errore, ad eccezione di un nodo specifico, deve sempre essere restituito.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Hello seguente cmdlet Ottiene il blocco di cluster con i filtri di applicazione.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Hello cmdlet seguente restituisce entità tutti distribuite in un nodo.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
È possibile ottenere il blocco di integrità del cluster con un [richiesta GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) o [richiesta POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) che include criteri di integrità e i filtri avanzati descritti nel corpo di hello.

## <a name="general-queries"></a>Query generali
Le query generali restituiscono l'elenco delle entità di Service Fabric di un tipo specificato. Gli oggetti vengono esposti tramite API hello (tramite metodi hello sulla **FabricClient.QueryManager**), i cmdlet di PowerShell e REST. Queste query aggregano sottoquery da più componenti. Uno di essi è hello [archivio integrità](service-fabric-health-introduction.md#health-store), che popola hello aggregato dello stato di integrità per ogni risultato della query.  

> [!NOTE]
> Le query generale restituiscono hello aggregato di stato di integrità di entità hello e non contengono dati di integrità avanzati. Se un'entità non è integra, è possibile giungere a integrità query tooget tutte le informazioni di integrità, inclusi gli eventi, gli stati di integrità figlio e valutazioni non integro.
>
>

Se le query generale restituiscono uno stato sconosciuto per un'entità, è possibile che tale archivio integrità hello non dispone di dati completo sull'entità hello. È inoltre possibile che un archivio di integrità toohello sottoquery non è riuscito (ad esempio, si è verificato un errore di comunicazione o dell'archivio integrità hello è stata limitata). Follow-up con una query di integrità per entità hello. Se la sottoquery hello ha rilevato errori temporanei, ad esempio problemi di rete, questa query follow-up può essere completata. Può anche fornire ulteriori dettagli dall'archivio integrità hello sui motivi per cui non è esposta entità hello.

le query che contengono Hello **HealthState** per le entità sono:

* Elenco di nodi: restituisce i nodi di elenco hello in cluster hello (paginato).
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode
* Elenco di applicazioni: elenco di hello restituisce delle applicazioni in cluster hello (paginata).
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication
* Elenco di servizio: elenco di hello restituisce dei servizi in un'applicazione (paginata).
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService
* Elenco partizioni: elenco di hello restituisce delle partizioni in un servizio (paginata).
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition
* Elenco di replica: elenco di hello restituisce delle repliche in una partizione (paginata).
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica
* Elenco di applicazioni distribuite: elenco di hello restituisce delle applicazioni distribuite in un nodo.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication
* Elenco dei pacchetti del servizio distribuito: elenco di hello restituisce dei pacchetti del servizio in un'applicazione distribuita.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Alcune delle query hello restituiscono risultati di paging. Hello delle query viene restituito un elenco derivato da [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Se i risultati di hello un messaggio non corrispondono, viene restituita solo una pagina e un ContinuationToken che tiene traccia di punto di interruzione di enumerazione. Continuare toocall hello stessa query e passare il token di continuazione hello dal hello precedente query tooget successivo dei risultati.
>
>

### <a name="examples"></a>esempi
Hello codice seguente ottiene applicazioni non integre hello cluster hello:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

il cmdlet seguente Hello Ottiene i dettagli dell'applicazione hello per l'infrastruttura di hello: / applicazione WordCount. Lo stato di integrità è di tipo avviso.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Hello seguente ottiene servizi hello con uno stato di errore:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Aggiornamenti del cluster e dell'applicazione
Durante un aggiornamento monitorato del cluster hello e dell'applicazione, Service Fabric Controlla integrità tooensure che tutto ciò che resta integro. Se un'entità non è integra valutato usando i criteri di integrità configurato, l'aggiornamento di hello Applica azione successiva hello toodetermine di criteri specifici per l'aggiornamento. aggiornamento Hello sia interazione dell'utente tooallow sospesa (come correggere le condizioni di errore o la modifica dei criteri) oppure potrebbe automaticamente il rollback toohello precedente versione funzionante.

Durante un *cluster* esegue l'aggiornamento, è possibile ottenere lo stato di aggiornamento cluster hello. stato di aggiornamento Hello include le valutazioni non integro, non è integro cluster hello toowhat quale punto. Se l'aggiornamento di hello viene eseguito il rollback a causa di problemi di toohealth, lo stato dell'aggiornamento hello memorizza motivi non integro ultimo hello. Queste informazioni consente agli amministratori di analizzare la causa dell'errore dopo l'aggiornamento di hello rollback o l'arresto.

Analogamente, durante un *applicazione* esegue l'aggiornamento, tutte le valutazioni integro sono contenute in stato di aggiornamento dell'applicazione hello.

Hello seguito è riportato lo stato di aggiornamento dell'applicazione hello per un'infrastruttura modificata: / applicazione WordCount. Un watchdog ha segnalato un errore in una delle repliche. è in corso l'aggiornamento di Hello in quanto i controlli di integrità hello non viene rispettati.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Altre informazioni su hello [aggiornamento dell'applicazione di Service Fabric](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Utilizzare tootroubleshoot valutazioni di integrità
Ogni volta che si verifica un problema con il cluster hello o un'applicazione, esaminare toopinpoint di integrità del cluster o l'applicazione hello qual è il problema. valutazioni integro Hello forniscono dettagli sulle quali stato non integro corrente hello attivate. Se necessario, è possibile scorrere verso il basso causa radice di elementi figlio non integri entità tooidentify hello.

Si consideri, ad esempio, un'applicazione non integra a causa di un errore segnalato in una delle relative repliche. Hello cmdlet di Powershell seguente mostra le valutazioni di tipo non integro hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

È possibile esaminare hello replica tooget ulteriori informazioni:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hello valutazioni problematico mostra hello autorità entità hello è valutata toocurrent lo stato di integrità. Potrebbero essere presenti più altri eventi che attivano questo stato, ma non risulteranno in valutazioni hello. tooget ulteriori informazioni, drill-down hello integrità entità toofigure out tutti i report non integro hello cluster hello.
>
>

## <a name="next-steps"></a>Passaggi successivi
[Utilizzare tootroubleshoot rapporti di integrità sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Aggiungere report sull'integrità di Service Fabric personalizzati](service-fabric-report-health.md)

[Come tooreport e controllo del servizio integrità](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorare e diagnosticare servizi in locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)
