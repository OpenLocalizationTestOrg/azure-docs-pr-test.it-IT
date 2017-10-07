---
title: "Scalabilità a livello di codice dell'infrastruttura di servizio aaaAzure | Documenti Microsoft"
description: "Scalabilità di un cluster di Azure Service Fabric in o out in base a livello di programmazione di trigger toocustom"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Aumentare o ridurre le istanze di un cluster di Service Fabric a livello di codice 

Le nozioni di base sulla scalabilità di un cluster Service Fabric in Azure sono trattate nella documentazione sulla [scalabilità del cluster](./service-fabric-cluster-scale-up-down.md). Questo articolo descrive come i cluster Service Fabric sono costruiti su set di scalabilità di macchine virtuali ed è possibile ottenere la scalabilità manualmente o usando regole di scalabilità automatica. Vengono esaminati i metodi a livello di codice per il coordinamento delle operazioni di scalabilità in Azure per scenari più avanzati. 

## <a name="reasons-for-programmatic-scaling"></a>Motivi per eseguire la scalabilità a livello di codice
In molti scenari, la scalabilità manuale o mediante regole di scalabilità automatica sono soluzioni valide. In altri scenari, tuttavia, possono non essere hello adatta a destra. Approcci di potenziali svantaggi toothese includono:

- Ridimensionamento manuale richiede toolog in e, in modo esplicito, le operazioni di ridimensionamento richiesta. Questo approccio potrebbe non essere una soluzione valida se le operazioni di scalabilità vengono richieste di frequente oppure in momenti imprevisti.
- Quando le regole di scalabilità automatica consente di rimuovere un'istanza di un set di scalabilità della macchina virtuale, essi non vengono rimossi automaticamente conoscenza di tale nodo dal cluster di Service Fabric hello associato, a meno che il tipo di nodo hello ha un livello di durabilità di Silver o oro. Poiché le regole di scalabilità automatica funzionano su larga scala hello impostare il livello (anziché a livello di Service Fabric hello), le regole di scalabilità automatica è possono rimuovere i nodi di Service Fabric senza arresto li. Questo tipo di rimozione dei nodi lascerà il nodo Service Fabric nello stato "ghost" dopo le operazioni di riduzione delle istanze. Una persona (o un servizio) sarebbe necessario tooperiodically pulire lo stato del nodo rimosso in cluster di Service Fabric hello.
  - Si noti che un tipo di nodo con un livello di durabilità Gold o Silver eseguirà automaticamente la pulizia dei nodi rimossi.  
- Anche se le regole di scalabilità automatica supportano [molte metriche](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), si tratta comunque di un set limitato. Se lo scenario richiede la scalabilità basata su alcune metriche non incluse in questo set, le regole di scalabilità automatica potrebbero non essere una soluzione valida.

In base a queste limitazioni, è preferibile tooimplement più automatico scalabilità modelli personalizzati. 

## <a name="scaling-apis"></a>Scalabilità delle API
Le API di Azure esistono in questo modo il lavoro tooprogrammatically applicazioni con set di scalabilità di macchine virtuali e i cluster di Service Fabric. Se le opzioni di scalabilità automatica esistenti non funzionano per lo scenario, queste API rendono possibili tooimplement logica di ridimensionamento personalizzata. 

Un approccio tooimplementing questo 'home-reso' scalabilità automatica funzionalità è tooadd un nuovo servizio senza stato toohello Service Fabric applicazione toomanage operazioni di ridimensionamento. All'interno del servizio hello `RunAsync` metodo, un set di trigger consente di determinare se la scalabilità è necessario (inclusi i parametri come la dimensione massima di un cluster di controllo e scalabilità cooldowns).   

Hello API utilizzata per le interazioni di set di scalabilità macchina virtuale (numero corrente di hello entrambi toocheck di istanze di macchine virtuali e toomodify è) è hello [libreria di gestione di Azure calcolo fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). libreria di calcolo di Microsoft Office fluent Hello fornisce un'API da utilizzare per l'interazione con il set di scalabilità di macchine virtuali.

Utilizzare toointeract con i cluster di Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Naturalmente, hello scalabilità codice non deve necessariamente toorun come servizio in toobe cluster hello in scala. Entrambi `IAzure` e `FabricClient` possibile connettersi in modalità remota, le risorse di Azure tootheir associata in modo hello scalabilità servizio potrebbe essere facilmente un'applicazione console o il servizio Windows in esecuzione da un'applicazione hello di fuori dell'infrastruttura di servizio. 

## <a name="credential-management"></a>Gestione delle credenziali
Una sfida di scrittura di un servizio di toohandle ridimensionamento è che il servizio di hello deve essere in grado di tooaccess risorse set scala della macchina virtuale senza un account di accesso interattivo. L'accesso a Service Fabric hello cluster è facile se hello scalabilità servizio sta modificando l'applicazione di Service Fabric, ma le credenziali sono necessarie tooaccess hello set di scalabilità. toolog in, è possibile utilizzare un [dell'entità servizio](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) creato con hello [CLI di Azure 2.0](https://github.com/azure/azure-cli).

È possibile creare un'entità servizio con hello alla procedura seguente:

1. Accedi toohello CLI di Azure (`az login`) come utente con scalabilità di macchine virtuali toohello di accesso set
2. Creare l'entità con il servizio hello`az ad sp create-for-rbac`
    1. Prendere nota del appId hello (chiamato altrove 'ID client'), nome, password e tenant per un uso successivo.
    2. Sarà inoltre necessario l'ID sottoscrizione, che può essere visualizzato con `az account list`

Hello calcolo fluent libreria può effettuare l'accesso utilizzando queste credenziali come indicato di seguito (si noti che i tipi Azure intuitiva di base come `IAzure` in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

Una volta eseguito l'accesso, è possibile eseguire una query del numero di istanze di set di scalabilità tramite `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Aumento del numero di istanze
Utilizzando Microsoft Office fluent hello calcolo di Azure SDK, è possono aggiungere istanze di scalabilità della macchina virtuale toohello impostata con pochi chiamate-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

In alternativa, le dimensioni del set di scalabilità di macchine virtuali possono essere gestite anche con i cmdlet di PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)recuperare l'oggetto set di scalabilità della macchina virtuale hello. la capacità corrente Hello verrà archiviata in hello `.sku.capacity` proprietà. Dopo la modifica di hello capacità toohello valore desiderato, scalabilità della macchina virtuale hello impostato in Azure possono essere aggiornati con hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.

Come quando si aggiunge manualmente un nodo, l'aggiunta di una scala di imposta l'istanza deve essere tutti toostart necessari che include un nuovo nodo di Service Fabric poiché il modello di set di scalabilità di hello estensioni tooautomatically aggiungere nuovo cluster di Service Fabric toohello istanze. 

## <a name="scaling-in"></a>Riduzione

La scalabilità è simile tooscaling out. set di scalabilità della macchina virtuale effettivo Hello le modifiche sono praticamente hello stesso. Tuttavia, come illustrato in precedenza, Service Fabric pulisce automaticamente solo i nodi rimossi con la durabilità Gold o Silver. Pertanto, in caso di hello bronzo durabilità, scala aggiuntivo è necessario toointeract con hello Service Fabric cluster tooshut toobe nodo hello rimosso verso il basso e quindi tooremove il relativo stato.

Preparazione nodo hello per arresto riguarda la ricerca hello nodo toobe rimosso (nodo aggiunto più di recente hello) e disattivarlo. Per i nodi non di inizializzazione, è possibile trovare i nodi più recenti confrontando il valore `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Tenere presente che *valore di inizializzazione* nodi non sembrano tooalways seguono la convenzione di hello che gli ID istanza maggiore verranno rimosse per prime.

Una volta trovata hello nodo toobe rimosso, può essere disattivata e rimosso utilizzando hello stesso `FabricClient` istanza e hello `IAzure` istanza precedenti.

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

Anche in questo caso, come per l'aumento del numero di istanze, è possibile usare i cmdlet di PowerShell per modificare la capacità del set di scalabilità di macchine virtuali, se si preferisce un approccio basato sugli script. Una volta che viene rimossa l'istanza di macchina virtuale di hello, è possibile rimuovere lo stato del nodo Service Fabric.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Potenziali svantaggi

Come illustrato nel hello frammenti di codice precedente, la creazione di un proprio servizio scalabilità fornisce elevato hello di controllo e personalizzazione tramite l'applicazione della scala. Questa condizione può essere utile negli scenari che richiedono un controllo preciso su quando e come aumentare o ridurre il numero di istanze dell'applicazione. Tuttavia, questo controllo implica un compromesso a livello di complessità del codice. Questo approccio, è pertanto necessario tooown scalabilità codice, non è semplice.

L'approccio da scegliere per la scalabilità di Service Fabric dipende dallo scenario specifico. Se il ridimensionamento è insolito, hello possibilità tooadd o rimuovere i nodi è manualmente sia sufficiente. Per scenari più complessi, le regole di scalabilità automatica e SDK esposizione a livello di codice hello possibilità tooscale offrono potenti alternative.

## <a name="next-steps"></a>Passaggi successivi

tooget iniziato a implementare la logica di ridimensionamento automatico, acquisire familiarità con hello seguenti concetti e le API utili:

- [Scalabilità manuale o con regole di scalabilità automatica](./service-fabric-cluster-scale-up-down.md)
- [Fluent Azure Management Libraries per .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utili per l'interazione con i set di scalabilità di macchine virtuali sottostanti del cluster Service Fabric)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile per l'interazione con un cluster Service Fabric e i relativi nodi)
