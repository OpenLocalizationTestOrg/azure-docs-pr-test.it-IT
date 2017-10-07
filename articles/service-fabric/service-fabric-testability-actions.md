---
title: errori aaaSimulate in Azure microservizi | Documenti Microsoft
description: "In questo articolo comunica sulle azioni di testabilità hello disponibili in Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Azioni di Testabilità
In ordine toosimulate un'infrastruttura affidabile, Azure Service Fabric fornisce sviluppatore hello e con toosimulate modi diversi del mondo reale errori e le transizioni di stato. esposti come azioni di testabilità. azioni Hello sono hello API di basso livello che causano un attacco intrusivo nel codice di errore specifico, la transizione dello stato o la convalida. La combinazione di queste azioni consente di scrivere scenari di test completi per i servizi.

Service Fabric fornisce alcuni scenari di test comuni costituiti da queste azioni. Si consiglia di utilizzare questi scenari predefiniti, che vengono scelti attentamente le transizioni di stato comuni tootest e casi di errore. Tuttavia, azioni possono essere scenari di test personalizzata toocreate utilizzato quando si desidera tooadd copertura per gli scenari che non rientrano scenari incorporato hello ancora o che sono personalizzati specifici per l'applicazione.

In c# le implementazioni di azioni di hello si trovano in hello System.Fabric.dll assembly. modulo di PowerShell dell'infrastruttura di sistema Hello viene trovato nell'assembly Microsoft.ServiceFabric.Powershell.dll hello. Come parte dell'installazione di runtime, hello modulo ServiceFabric di PowerShell è installato tooallow per facilità d'uso.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Azioni di errore normali e anomale
Le azioni di Testabilità sono classificate in due bucket principali:

* Errori anomali: questi errori simulano errori come il riavvio del computer e gli arresti anomali dei processi. In questi casi di errori, il contesto di esecuzione hello del processo di interruzione. Ciò significa che alcuna pulizia dello stato di hello può essere eseguito prima dell'applicazione hello è stato riavviato.
* Errori normali: questi errori simulano azioni normali come gli spostamenti delle repliche e le eliminazioni attivate dal bilanciamento del carico. In questi casi, il servizio di hello Ottiene una notifica di hello Chiudi e possibile pulire lo stato di hello prima della chiusura.

Per la convalida di qualità migliore, eseguire il servizio di hello e carico di lavoro di business durante la generazione di diversi errori normale e anomali. Errori anomali esercitare scenari in cui il processo di servizio hello termina improvvisamente centro hello di un flusso di lavoro. Ciò consente di verificare il percorso di recupero hello una volta ripristinato replica del servizio hello dall'infrastruttura del servizio. Ciò consentirà di verificare la coerenza dei dati e se lo stato del servizio hello viene mantenuto correttamente dopo gli errori. Hello altri set di errori (hello normale) verificare che il servizio hello reagisce correttamente tooreplicas viene spostata dal Service Fabric. Ciò consente di verificare la gestione dell'annullamento nel metodo RunAsync hello. servizio Hello deve toocheck hello annullamento token elaborate per impostare correttamente il salvataggio dello stato ed esce dal metodo RunAsync hello.

## <a name="testability-actions-list"></a>Elenco delle azioni di Testabilità
| Azione | Descrizione | API gestita | Cmdlet di PowerShell | Errori normali/anomali |
| --- | --- | --- | --- | --- |
| CleanTestState |Rimuove tutti gli stati di test hello dal cluster hello in caso di chiusura non valido di driver di test hello. |CleanTestStateAsync |Remove-ServiceFabricTestState |Non applicabile |
| InvokeDataLoss |Provoca la perdita di dati in una partizione del servizio. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Normale |
| InvokeQuorumLoss |Inserisce una partizione del servizio con stato in una perdita di quorum. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |Normale |
| Move Primary |Sposta hello specificato replica primaria di un nodo di servizio con stato toohello cluster specificato. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |Normale |
| Move Secondary |Sposta una replica secondaria hello corrente di un nodo di cluster diverso tooa servizio con stato. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |Normale |
| RemoveReplica |Simula un errore di replica tramite la rimozione di una replica da un cluster. Questo comporta la chiusura replica hello e passerà il toorole 'None', il relativo stato rimozione dal cluster hello. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Normale |
| RestartDeployedCodePackage |Simula un errore di processo del pacchetto di codice mediante il riavvio di un pacchetto di codice distribuito in un nodo in un cluster. Questo processo pacchetto codice hello, che verrà riavviato tutti hello utente servizio le repliche ospitate in tale processo si interrompe. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |Anomalo |
| RestartNode |Simula un errore del nodo cluster Infrastruttura di servizi tramite il riavvio di un nodo. |RestartNodeAsync |Restart-ServiceFabricNode |Anomalo |
| RestartPartition |Simula uno scenario di blackout del data center o del cluster mediante il riavvio di alcune o di tutte le repliche di una partizione. |RestartPartitionAsync |Restart-ServiceFabricPartition |Normale |
| RestartReplica |Simula un errore di replica tramite il riavvio di una replica persistente in un cluster, la chiusura replica hello e riaprirlo. |RestartReplicaAsync |Restart-ServiceFabricReplica |Normale |
| StartNode |Avvia un nodo in un cluster già arrestato. |StartNodeAsync |Start-ServiceFabricNode |Non applicabile |
| StopNode |Simula l’errore in un nodo mediante l’arresto di un nodo in un cluster. nodo Hello resterà verso il basso fino a quando viene chiamato StartNode. |StopNodeAsync |Stop-ServiceFabricNode |Anomalo |
| ValidateApplication |Convalida integrità di tutti i servizi di Service Fabric all'interno di un'applicazione, in genere dopo la generazione di un errore nel sistema hello e disponibilità hello. |ValidateApplicationAsync |Test-ServiceFabricApplication |Non applicabile |
| ValidateService |Convalida la disponibilità di hello e l'integrità di un servizio di Service Fabric, in genere dopo la generazione di un errore nel sistema hello. |ValidateServiceAsync |Test-ServiceFabricService |Non applicabile |

## <a name="running-a-testability-action-using-powershell"></a>Esecuzione di un'azione di testabilità con PowerShell
In questa esercitazione illustra come toorun un'azione di testabilità tramite PowerShell. Si apprenderà come toorun un'azione di testabilità rispetto a un cluster (uno-box) locale o un cluster di Azure. Microsoft.Fabric.Powershell.dll - hello modulo PowerShell di Service Fabric - viene installato automaticamente quando si installa Microsoft Service Fabric MSI hello. modulo Hello viene caricato automaticamente quando si apre un prompt dei comandi di PowerShell.

Sezioni dell'esercitazione:

* [Eseguire un'azione su un cluster di una casella](#run-an-action-against-a-one-box-cluster)
* [Eseguire un'azione su un cluster di Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Eseguire un'azione su un cluster di una casella
toorun un'azione di testabilità su un cluster locale, connettersi innanzitutto toohello cluster e il prompt PowerShell hello aperto in modalità amministratore. Esaminiamo hello **riavvio ServiceFabricNode** azione.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Qui hello azione **riavvio ServiceFabricNode** è in esecuzione in un nodo denominato "Node1". modalità di terminazione Hello specifica non deve verificare se azione di riavvio del nodo hello è effettivamente riuscito. Modalità di completamento hello specificando come "Verifica" determinerà tooverify se l'azione di riavvio hello è effettivamente riuscito. Anziché specificare direttamente il nodo hello in base al nome, è possibile specificare tramite un tipo di chiave e hello partizione della replica, come indicato di seguito:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Riavvio ServiceFabricNode** deve essere un nodo di Service Fabric in un cluster toorestart utilizzato. Processo di Fabric.exe hello, che verrà riavviato tutte hello sistema utente e servizio servizio repliche ospitate su tale nodo verrà interrotta. Utilizzando questo tootest API del servizio consente di rilevare i bug ai percorsi di recupero di failover hello. Consente di simulare errori di nodo nel cluster hello.

Hello schermata riportata di seguito viene illustrato hello **riavvio ServiceFabricNode** comando testabilità azione.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Hello di output di hello innanzitutto **Get ServiceFabricNode** (un cmdlet dal modulo di PowerShell di Service Fabric hello) viene illustrato il cluster locale hello include cinque nodi: Node.1 tooNode.5. Dopo l'azione di testabilità hello (cmdlet) **riavvio ServiceFabricNode** viene eseguita nel nodo hello, denominato Node.4, vediamo tempi di attività del nodo hello è stata reimpostata.

### <a name="run-an-action-against-an-azure-cluster"></a>Eseguire un'azione su un cluster di Azure
Esecuzione di un'azione di testabilità (tramite PowerShell) su un cluster di Azure è l'azione hello toorunning simile su un cluster locale. Hello solo differenza è che, prima di eseguire l'azione di hello, anziché connessione cluster locale toohello, è necessario tooconnect toohello Azure prima del cluster.

## <a name="running-a-testability-action-using-c35"></a>Esecuzione di un'azione di testabilità con C&#35;
toorun un'azione di testabilità mediante c#, è necessario innanzitutto tooconnect toohello cluster utilizzando FabricClient. Ottenere quindi hello parametri necessari toorun hello azione. È possibile utilizzare diversi parametri toorun hello stessa azione.
Ricerca di hello RestartServiceFabricNode action toorun unidirezionale è utilizzando le informazioni sul nodo hello (nome del nodo e ID istanza del nodo) in cluster hello.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Spiegazione di alcuni parametri:

* **CompleteMode** specifica che la modalità hello non deve verificare se azione di riavvio hello è effettivamente riuscito. Modalità di completamento hello specificando come "Verifica" determinerà tooverify se l'azione di riavvio hello è effettivamente riuscito.  
* **OperationTimeout** set hello di hello operazione toofinish intervallo di tempo prima che venga generata un'eccezione TimeoutException.
* **CancellationToken** consente un toobe in sospeso chiamata annullata.

Anziché specificare direttamente il nodo hello in base al nome, è possibile specificare tramite un tipo di chiave e hello partizione della replica.

Per altre informazioni vedere [PartitionSelector e ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector e ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector è un helper esposto in testabilità ed è tooselect usato un oggetto specifico di partizione in cui tooperform hello testabilità azioni. Può essere utilizzato tooselect una partizione specifica se l'ID di partizione hello è noto in anticipo. In alternativa, è possibile fornire la chiave di partizione hello e operazione hello risolverà l'ID di partizione hello internamente. È anche possibile hello selezionare una partizione casuale.

toouse questo supporto, creare l'oggetto PartitionSelector hello e selezionare la partizione hello utilizzando uno dei metodi di hello Select *. Passare quindi hello PartitionSelector oggetto toohello API che lo richiede. Se viene selezionata alcuna opzione, per impostazione predefinita la partizione casuale tooa.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector è un helper esposto in testabilità e viene utilizzato toohelp selezionare una replica su quali tooperform hello testabilità azioni. Può essere utilizzato tooselect una replica specifica se l'ID replica hello è noto in anticipo. Inoltre, è possibile hello la selezione di una replica primaria o secondaria casuale. ReplicaSelector deriva da PartitionSelector, pertanto è necessario tooselect entrambi hello replica e hello partizione in cui si desidera operazione testabilità di hello tooperform.

toouse questo supporto, creare un oggetto ReplicaSelector e set di partizioni di replica e hello hello tooselect hello desiderato. È quindi possibile passare in hello API che lo richiede. Se viene selezionata alcuna opzione, per impostazione predefinita replica casuale tooa e partizione casuale.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Passaggi successivi
* [Scenari di testabilità](service-fabric-testability-scenarios.md)
* Come tootest il servizio
  * [Simulare gli errori durante i carichi di lavoro del servizio](service-fabric-testability-workload-tests.md)
  * [Errori di comunicazione da servizio a servizio](service-fabric-testability-scenarios-service-communication.md)

