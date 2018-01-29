---
title: "Eseguire i carichi di lavoro di Azure Batch su macchine virtuali convenienti con priorità bassa | Microsoft Docs"
description: "Informazioni su come eseguire il provisioning di macchine virtuali con priorità bassa per ridurre i costi dei carichi di lavoro di Azure Batch."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 09/28/2017
ms.author: markscu
ms.openlocfilehash: b9e5181baedba7cc4783553221521f5b08a7bc4d
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/11/2017
---
# <a name="use-low-priority-vms-with-batch"></a>Usare le macchine virtuali con priorità bassa in Batch

Azure Batch offre macchine virtuali con priorità bassa per ridurre i costi dei carichi di lavoro Batch. Le macchine virtuali con priorità bassa rendono possibili nuovi tipi di carichi di lavoro Batch, assicurando una grande quantità di potenza di calcolo risultando anche economica.

Le macchine virtuali con priorità bassa sfruttano la capacità in eccesso di Azure. Quando si specificano le macchine virtuali con priorità bassa nei pool, Azure Batch può usare automaticamente questo surplus quando disponibile.

Il compromesso per l'uso di macchine virtuali con priorità bassa è che queste macchine virtuali possono essere interrotte quando non c'è capacità in surplus in Azure. Per questo motivo, le macchine virtuali con priorità bassa sono più adatte per determinati tipi di carichi di lavoro. Usare le macchine virtuali con priorità bassa per carichi di lavoro di batch ed elaborazione asincrona in cui il tempo di completamento del processo è flessibile e il lavoro viene distribuito su più macchine virtuali.

Le macchine virtuali con priorità bassa sono caratterizzate da un prezzo notevolmente ridotto rispetto alle macchine virtuali dedicate. Per i dettagli sui prezzi vedere [Prezzi dei Batch](https://azure.microsoft.com/pricing/details/batch/).


> [!IMPORTANT]
> Le macchine virtuali con priorità bassa sono attualmente disponibili solo per i carichi di lavoro in esecuzione in Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Casi di uso per le macchine virtuali con priorità bassa

Considerando le caratteristiche delle macchine virtuali con priorità bassa, quali carichi di lavoro possono e non sono usarle? In generale, i carichi di elaborazione batch sono la soluzione ideale, quando i processi sono suddivisi in più attività in parallelo o viene eseguita la scalabilità orizzontale su più processi che vengono distribuiti tra più macchine virtuali.

-   Per ottimizzare l'uso della capacità in eccedenza in Azure, è possibile eseguire una scalabilità orizzontale su processi appropriati.

-   In alcuni casi le macchine virtuali potrebbero non essere disponibili o possono essere superate e ciò comporta una riduzione della capacità per i processi e può provocare un'interruzione e una riesecuzione delle attività. I processi devono pertanto essere flessibili nel periodo in cui potrebbero essere eseguiti.

-   I processi con attività più lunghe potrebbero subire maggiormente gli effetti se vengono interrotti. Se attività con tempi di esecuzione lunghi implementano il checkpoint per salvare l'avanzamento durante l'esecuzione, l'impatto dell'interruzione è minore. Le attività con tempi di esecuzione più brevi tendono a funzionare meglio con macchine virtuali con priorità bassa poiché l'impatto dell'interruzione è decisamente minore.

-   I processi MPI con tempi di esecuzione lunghi che usano più macchine virtuali non sono adatti all'uso di macchine virtuali con priorità bassa poiché una macchina virtuale superata può causare la necessità riesecuzione del processo.

Esempi di casi d'uso di elaborazione batch adatti all'uso di macchine virtuali con priorità bassa sono:

-   **Sviluppo e test**: in particolare, se sono in fase di sviluppo soluzioni su larga scala, è possibile realizzare risparmi significativi. Tutti i tipi di test possono trarre vantaggio, ma i test di carico su larga scala e i test di regressione ne traggono il miglio uso.

-   **Integrazione della capacità su richiesta**: le macchine virtuali con priorità bassa possono essere usate per integrare le normali macchine virtuali dedicate. Quando disponibili, i processi possono essere ridimensionati e pertanto possono essere completati più rapidamente a un costo inferiore. Quando non sono disponibili, rimangono disponibili le macchine virtuali dedicate di base.

-   **Tempi di esecuzione del processo flessibili**: se c'è flessibilità nei tempi di completamento dei processi, le possibili cadute di capacità vengono considerate tollerabili; i processi delle macchine virtuali con priorità bassa, per giunta, vengono spesso eseguiti più rapidamente e a costi inferiori.

È possibile configurare i pool di batch per usare macchine virtuali con priorità bassa in diversi modi, a seconda della flessibilità dei tempi di esecuzione del processo:

-   Le macchine virtuali con priorità bassa possono essere usate esclusivamente in un pool. In questo caso, il servizio Batch recupera qualsiasi capacità superata, se disponibile. Questa configurazione rappresenta il modo più conveniente per eseguire i processi poiché vengono usate solo le macchine virtuali con priorità bassa.

-   Le macchine virtuali con priorità bassa possono essere usate in combinazione con macchine virtuali dedicate predefinite di base. Il numero fisso di macchine virtuali dedicate garantisce che ci sia sempre una certa capacità per mantenere l'avanzamento del processo.

-   Può verificarsi una combinazione dinamica di macchine virtuali dedicate e con priorità bassa, in modo che le macchine virtuali con priorità bassa più economiche vengano usate esclusivamente quando disponibili, mentre le capacità delle macchine virtuali dedicate a prezzo pieno vengono aumentate quando necessario. Questa configurazione consente di mantenere una quantità minima di capacità disponibile al fine di far avanzare il processo.

## <a name="batch-support-for-low-priority-vms"></a>Supporto batch per le macchine virtuali con priorità bassa

Azure Batch offre diverse funzionalità che semplificano l'uso e i vantaggi dalle macchine virtuali con priorità bassa:

-   I pool di batch può contenere sia macchine virtuali dedicate che macchine virtuali con priorità bassa. Il numero di ciascun tipo di macchina virtuale può essere specificato al momento della creazione di un nuovo pool o della modifica di un pool esistente, tramite l'operazione di ridimensionamento esplicito o la scalabilità automatica. L'invio di attività e processi può rimanere invariato indipendentemente dai tipi di macchine virtuali nel pool. È anche possibile configurare un pool in modo che usi solo le macchine virtuali con priorità bassa per eseguire processi nel modo più economico possibile, ma che avvii macchine virtuali dedicate se la capacità scende al di sotto di una soglia minima, per mantenere i processi in esecuzione.

-   I pool del servizio Batch rilevano automaticamente il numero di macchine virtuali con priorità bassa. Se le macchine virtuali sono superate, il servizio Batch cerca di sostituire la capacità persa e di tornare all'obiettivo.

-   Quando le attività vengono interrotte, il servizio Batch rileva e reinserisce automaticamente nella coda le attività da eseguire di nuovo.

-   Le macchine virtuali con priorità bassa hanno una quota di CPU virtuali diversa rispetto a quella delle macchine virtuali dedicate. 
    La quota per le macchine virtuali con priorità bassa è superiore a quella delle macchine virtuali dedicate, perché le macchine virtuali con priorità bassa sono meno costose. Per altre informazioni, vedere [Quote e limiti del servizio Batch](batch-quota-limit.md#resource-quotas).    


## <a name="create-and-update-pools"></a>Crea e aggiornare i pool

Un pool Batch può contenere sia macchine virtuali dedicate sia VM con priorità bassa, definite anche nodi di calcolo. È possibile impostare il numero di nodi di calcolo sia per le macchine virtuali dedicate sia per le VM con priorità bassa. Il numero di nodi di destinazione specifica il numero di macchine virtuali che si desidera avere nel pool.

Ad esempio, per creare un pool con le macchine virtuali del servizio cloud di Azure con una destinazione di 5 VM dedicate e 20 macchine virtuali con priorità bassa:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

Per creare un pool con le macchine virtuali di Azure, in questo caso le macchine virtuali Linux, con una destinazione di 5 VM dedicate e 20 macchine virtuali con priorità bassa:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

È possibile ottenere il numero corrente di nodi sia per le macchine virtuali dedicate che per quelle con priorità bassa:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

I nodi pool dispongono di una proprietà che indica se il nodo è una macchina virtuale dedicata o con priorità bassa:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Quando uno o più nodi in un pool sono superati, un'operazione di elenco nodi nel pool restituisce comunque tali nodi. Il numero corrente di nodi con priorità bassa rimane invariato, ma lo stato di tali nodi viene impostato su **Superato**. Il servizio Batch tenterà di individuare le macchine virtuali di sostituzione e, se l'operazione ha esito positivo, i nodi avranno lo stato **Creazione in corso** e poi **Avvio in corso** prima di essere disponibili per l'esecuzione di attività, come avviene per i nuovi nodi.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Ridimensionare un pool che contiene macchine virtuali con priorità bassa

Così come avviene per i pool costituiti esclusivamente da macchine virtuali dedicate, è possibile ridimensionare un pool che contiene macchine virtuali con priorità bassa chiamando il metodo di ridimensionamento o mediante la scalabilità automatica.

L'operazione di ridimensionamento del pool richiede un secondo parametro facoltativo che aggiorna il valore di **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

La formula di scalabilità automatica del pool supporta le macchine virtuali con priorità bassa nel modo seguente:

-   È possibile ottenere o impostare il valore della variabile definita dal servizio **$TargetLowPriorityNodes**.

-   È possibile ottenere il valore della variabile definita dal servizio **$CurrentLowPriorityNodes**.

-   È possibile ottenere il valore della variabile definita dal servizio **$PreemptedNodeCount**. 
    Questa variabile restituisce il numero di nodi con lo stato Annullato e consente di aumentare o ridurre il numero di nodi dedicati, a seconda del numero di nodi di annullati che non sono disponibili.

## <a name="jobs-and-tasks"></a>Processi e attività

I processi e le attività richiedono una configurazione aggiuntiva minima per nodi con priorità bassa. L'unico supporto è il seguente:

-   La proprietà JobManagerTask di un processo ha una nuova proprietà, **AllowLowPriorityNode**. 
    Quando questa proprietà è true, è possibile programmare le attività di gestione dei processi su un nodo dedicato o su un nodo con priorità bassa. Se questa proprietà è false, l'attività di gestione dei processi viene programmata solo per un nodo dedicato.

-   Per un'applicazione di attività è disponibile una [variabile di ambiente](batch-compute-node-environment-variables.md), in modo da determinarne l'esecuzione su un nodo dedicato o con priorità bassa. La variabile di ambiente è AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Gestione delle priorità

Le macchine virtuali in alcuni casi possono essere superate. In questo caso, il servizio Batch effettua le operazioni seguenti:

-   Le macchine virtuali interrotte hanno lo stato aggiornato ad **Annullato**.
-   Se sulle macchine virtuali di un nodo annullato vi erano delle attività in esecuzione, queste vengono riaccodate e rieseguire.
-   La macchina virtuale viene eliminata in modo efficace e tutti i dati memorizzati in locale nella macchina virtuale andranno persi.
-   Il pool tenta continuamente raggiungere il numero stabilito di nodi con priorità bassa disponibili. Quando viene individuata una capacità di sostituzione, i nodi mantengono il proprio ID, ma vengono inizializzati di nuovo, attraversando gli stati **Creazione in corso** e **Avvio in corso** prima che siano disponibili per la pianificazione delle attività.
-   Il numero delle priorità è disponibile come metrica nel portale di Azure.

## <a name="metrics"></a>Metriche

Per i nodi con priorità bassa sono disponibili nuove metriche nel [portale di Azure](https://portal.azure.com). Le metriche sono:

- Numero di nodi a bassa priorità
- Numero di core a bassa priorità 
- Numero di nodi annullati

Per visualizzare le metriche nel portale di Azure:

1. Passare all'account Batch nel portale e visualizzare le impostazioni per l'account Batch.
2. Selezionare **Metrica** dalla sezione **Monitoraggio**.
3. Selezionare le metriche da usare dall'elenco **Metriche disponibili**.

![Metriche per i nodi a priorità bassa](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Passaggi successivi

* Vedere [Panoramica sulle funzionalità di Batch per sviluppatori](batch-api-basics.md)per informazioni essenziali per chiunque si prepari all'uso di Batch. L'articolo contiene informazioni più dettagliate sulle risorse del servizio Batch, ad esempio pool, nodi, processi e attività, e sulle numerose funzionalità delle API che è possibile usare durante la compilazione dell'applicazione Batch.
* Informazioni sulle [API e gli strumenti di Batch](batch-apis-tools.md) disponibili per la compilazione di soluzioni Batch.
