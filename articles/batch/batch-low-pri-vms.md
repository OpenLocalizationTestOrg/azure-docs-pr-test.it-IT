---
title: "carichi di lavoro di Azure Batch aaaRun in economiche macchine virtuali con priorità bassa (anteprima) | Documenti Microsoft"
description: "Informazioni su come hello di tooreduce macchine virtuali con priorità bassa tooprovision costo dei carichi di lavoro di Azure Batch."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Usare le VM con priorità bassa in Batch (anteprima)

Azure Batch offre un costo hello tooreduce limitati al virtuali (VM) dei carichi di lavoro di Batch. Le macchine virtuali con priorità bassa rendono possibili nuovi tipi di carichi di lavoro Batch, assicurando una grande quantità di potenza di calcolo risultando anche economica.

Le macchine virtuali con priorità bassa sfruttano la capacità in eccesso di Azure. Quando si specificano le macchine virtuali con priorità bassa nei pool, Azure Batch può usare automaticamente questo surplus quando disponibile.

compromesso di Hello per l'utilizzo di macchine virtuali con priorità bassa è che tali macchine virtuali possono essere interrotta quando nessun surplus della capacità è disponibile in Azure. Per questo motivo, le macchine virtuali con priorità bassa sono più adatte per determinati tipi di carichi di lavoro. Utilizzare le macchine virtuali con priorità bassa per l'elaborazione asincrona di carichi di lavoro in cui tempo di completamento del processo di hello è flessibile e lavoro hello viene distribuito tra più macchine virtuali e batch.

Le macchine virtuali con priorità bassa sono decisamente meno dispendiose delle macchine virtuali dedicate. Per i dettagli sui prezzi vedere [Prezzi dei Batch](https://azure.microsoft.com/pricing/details/batch/).

Per un approfondimento delle macchine virtuali con priorità bassa, vedere l'annuncio del post di blog hello: [Batch calcolo a una frazione del prezzo di hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Le macchine virtuali con priorità bassa sono attualmente in anteprima e sono disponibili solo per i carichi di lavoro in esecuzione in Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Casi di uso per le macchine virtuali con priorità bassa

Considerando caratteristiche hello di macchine virtuali con priorità bassa, quali carichi di lavoro può e non è possibile utilizzarli? In generale, i carichi di elaborazione batch sono la soluzione ideale, quando i processi sono suddivisi in più attività in parallelo o viene eseguita la scalabilità orizzontale su più processi che vengono distribuiti tra più macchine virtuali.

-   utilizzo di toomaximize di surplus della capacità nei processi di Azure, adatti possibile scalare orizzontalmente.

-   In alcuni casi le macchine virtuali potrebbero non essere disponibili o per essere interrotta, comporterà la riduzione della capacità per i processi che possono causare repliche e l'interruzione tootask. I processi devono pertanto essere flessibili nel tempo hello che possono assumere toorun.

-   I processi con attività più lunghe potrebbero subire maggiormente gli effetti se vengono interrotti. Se l'attività di implementano lo stato di avanzamento di checkpoint toosave mentre vengono eseguite con esecuzione prolungata, quindi l'impatto dell'interruzione sarebbe decisamente minore. Attività con tempi di esecuzione inferiore tendono toowork meglio con le macchine virtuali con priorità bassa come impatto hello di interruzione è molto inferiore.

-   I processi MPI che utilizzano più macchine virtuali non sono adatti toouse con esecuzione prolungata macchine virtuali con priorità bassa come una macchina virtuale superata verranno probabilmente lead toohello intero processo eseguiva toobe nuovamente.

Alcuni esempi di elaborazione batch usano toouse adatto a casi sono macchine virtuali con priorità bassa:

-   **Sviluppo e test**: in particolare, se sono in fase di sviluppo soluzioni su larga scala, è possibile realizzare risparmi significativi. Tutti i tipi di test possono trarre vantaggio, ma i test di carico su larga scala e i test di regressione ne traggono il miglio uso.

-   **Integrazione di capacità su richiesta**: le macchine virtuali con priorità bassa possono essere utilizzate per integrare le macchine virtuali regular dedicate - scalare e pertanto completare più rapidamente a un costo inferiore quando è disponibile, i processi; quando non è disponibile, hello della linea di base di dedicato le macchine virtuali sono disponibili.

-   **Tempo di esecuzione processo flessibile**: se è disponibile una flessibilità in processi timer hello è toocomplete, quindi cadute potenziale di capacità è possibile tollerare; tuttavia hello aggiunta dei processi di macchine virtuali con priorità bassa frequenza eseguirà più velocemente e con un costo inferiore.

Pool di batch può essere configurato toouse macchine virtuali con priorità bassa in diversi modi, a seconda flessibilità hello in fase di esecuzione del processo:

-   Le macchine virtuali con priorità bassa possono essere usate esclusivamente in un pool e Batch dovrà soltanto recuperare le capacità interrotte se disponibile. Si tratta di processi di tooexecute modo più economici hello come vengono utilizzate le macchine virtuali solo con priorità bassa.

-   Le macchine virtuali con priorità bassa possono essere usate in combinazione con macchine virtuali dedicate predefinite di base. Hello numero fisso di macchine virtuali dedicate garantisce che vi siano sempre alcune tookeep capacità un avanzamento del processo.

-   Può essere dinamica combinazione di macchine virtuali con priorità bassa e dedicate, in modo che più economiche macchine virtuali con priorità bassa vengono utilizzate esclusivamente quando è disponibile, ma le macchine virtuali hello con un prezzo full dedicato vengono ridimensionate quando richiesto, tookeep una quantità minima di processi di capacità disponibile tookeep hello avanzamento.

## <a name="batch-support-for-low-priority-vms"></a>Supporto batch per le macchine virtuali con priorità bassa

Azure Batch offre diverse funzionalità che rendono facilmente tooconsume e trarre vantaggio dalle macchine virtuali con priorità bassa:

-   I pool di batch può contenere sia macchine virtuali dedicate che macchine virtuali con priorità bassa. Quando un pool viene creato o modificato in qualsiasi momento per un pool esistente, tramite l'operazione di ridimensionamento esplicita hello o scalabilità automatica, è possibile specificare il numero di Hello di ogni tipo di macchina virtuale. Invio di processi e delle attività può rimanere invariato e non è necessario preoccuparsi di tipi di macchine Virtuali hello nel pool di hello. È inoltre possibile toohave un pool completamente utilizzare processi toorun di macchine virtuali con priorità bassa come economici possibile, ma di spin up dedicate macchine virtuali se la capacità di hello scende di sotto di una soglia minima, per mantenere i processi in esecuzione.

-   Pool di batch di posizionamento automaticamente toohello numero di macchine virtuali con priorità bassa. Se le macchine virtuali vengono sostituite, Batch tenterà hello tooreplace perdita capacità e la destinazione toohello restituito.

-   Nel caso di hello di attività viene interrotta, Batch rileverà e automaticamente riaccodare toobe attività eseguire di nuovo.

-   Le macchine virtuali con priorità bassa hanno una quota di code diversa rispetto a quella delle VM dedicate. 
    Hello offerta per le macchine virtuali con priorità bassa è superiore a quello delle macchine virtuali dedicate, perché le macchine virtuali con priorità bassa costano inferiori. Per altre informazioni, vedere [Quote e limiti del servizio Batch](batch-quota-limit.md#resource-quotas).    

> [!NOTE]
> Macchine virtuali con priorità bassa non sono attualmente supportate per gli account Batch in modalità di allocazione del pool di hello è impostata troppo[sottoscrizione utente](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Crea e aggiornare i pool

Un pool di Batch può contenere le macchine virtuali sia dedicate e con priorità bassa (anche noto tooas nodi di calcolo). È possibile impostare il numero di destinazione hello di nodi di calcolo per le macchine virtuali sia dedicate e con priorità bassa. numero di nodi di destinazione Hello specifica hello numero di macchine virtuali desiderate toohave nel pool di hello.

Ad esempio, toocreate un pool usando il servizio cloud di Azure le macchine virtuali con una destinazione di 5 dedicato macchine virtuali e 20 macchine virtuali con priorità bassa:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

toocreate un pool con macchine virtuali di Azure (in questo caso, le macchine virtuali Linux) con una destinazione di 5 dedicato macchine virtuali e 20 macchine virtuali con priorità bassa:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

È possibile ottenere il numero corrente di hello dei nodi per le macchine virtuali sia dedicate e con priorità bassa:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

I nodi del pool sono tooindicate una proprietà se il nodo di hello è una macchina virtuale dedicata o con priorità bassa:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Quando vengono interrotti uno o più nodi in un pool, un'operazione di elenco nodi del pool continuerà a restituire i nodi, hello numero corrente di nodi con priorità bassa rimane invariata, ma tali nodi avrà il relativo stato è impostato toothe **annullato**stato. Batch tenterà toofind sostituzione, le macchine virtuali e, se ha esito positivo, i nodi di hello verranno esaminate **creazione** e quindi **iniziale** stati prima di essere rese disponibili per l'esecuzione di attività, come i nuovi nodi.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Ridimensionare un pool che contiene macchine virtuali con priorità bassa

Come con pool esclusivamente costituito da macchine virtuali dedicate, è possibili tooscale una pool che contiene con priorità bassa VM chiamando il metodo di ridimensionamento hello o con scalabilità automatica.

operazione di ridimensionamento pool Hello accetta un parametro di secondo parametro facoltativo che aggiorna il valore di **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

formula di scalabilità automatica pool Hello supporta le macchine virtuali con priorità bassa, come segue:

-   È possibile ottenere o impostare il valore di hello della variabile definito dal servizio hello **$TargetLowPriorityNodes**.

-   È possibile ottenere il valore di hello della variabile definito dal servizio hello **$CurrentLowPriorityNodes**.

-   È possibile ottenere il valore di hello della variabile definito dal servizio hello **$PreemptedNodeCount**. 
    Questa variabile restituisce il numero di hello di nodi in hello stato interrotto e consente di aumentare o diminuire il numero di hello dei nodi dedicati, in base al numero di hello di nodi di annullamento che non sono disponibili.

## <a name="jobs-and-tasks"></a>Processi e attività

Processi e attività richiedono il supporto minimo per i nodi con priorità bassa. è supportata solo Hello è indicato di seguito:

-   Hello JobManagerTask proprietà di un processo ha una nuova proprietà, **AllowLowPriorityNode**. 
    Quando questa proprietà è true, è possibile programmare attività del gestore processi hello in un nodo dedicato o con priorità bassa. Se questa proprietà è false, attività del gestore processi hello sarà tooa pianificato solo nodo dedicato.

-   Un [variabile di ambiente](batch-compute-node-environment-variables.md) è disponibile tooa applicazione attività in modo che possa determinare se è in esecuzione in un nodo con priorità bassa o dedicato. variabile di ambiente Hello è AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Gestione delle priorità

Macchine virtuali in alcuni casi possono essere interrotta; In questo caso, hello Batch seguenti:

-   le macchine virtuali interrotto Hello avere lo stato di aggiornamento troppo**annullato**.
-   Se l'attività in esecuzione in hello superata macchine virtuali del nodo, queste attività vengono reinserito nella coda e quindi eseguire di nuovo.
-   Hello macchina virtuale viene eliminata in modo efficace, iniziali tooany dati archiviati localmente nelle hello VM andrà perduta.
-   pool di Hello tenterà continuamente tooreach hello destinazione numerosi nodi con priorità bassa disponibili. Quando viene individuata una capacità di sostituzione, i nodi mantengono il proprio ID, ma vengono inizializzati di nuovo, attraversando gli stati **Creazione in corso** e **Avvio in corso** prima che siano disponibili per la pianificazione delle attività.
-   Conteggi di priorità sono disponibili come metrica in hello portale di Azure.

## <a name="metrics"></a>Metrica

Nuova metrica è disponibile in hello [portale di Azure](https://portal.azure.com) per i nodi con priorità bassa. Le metriche sono:

- Numero di nodi a bassa priorità
- Numero di core a bassa priorità 
- Numero di nodi annullati

metriche tooview in hello portale di Azure:

1. Passare tooyour account Batch nel portale di hello e visualizzare le impostazioni di hello per l'account Batch.
2. Selezionare **metriche** da hello **monitoraggio** sezione.
3. Selezionare le metriche di hello desiderate hello **le metriche disponibili** elenco.

![Metriche per i nodi a priorità bassa](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Passaggi successivi

* Hello lettura [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md), informazioni essenziale per chiunque preparazione toouse Batch. articolo Hello contiene informazioni più dettagliate sulle risorse del servizio Batch come pool di nodi, processi e attività e hello molte funzionalità dell'API che è possibile utilizzare durante la compilazione dell'applicazione di Batch.
* Informazioni su hello [Batch API e strumenti](batch-apis-tools.md) disponibili per la creazione di soluzioni di Batch.
