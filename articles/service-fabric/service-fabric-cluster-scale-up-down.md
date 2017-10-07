---
title: aaaScale un'infrastruttura del servizio cluster in o out | Documenti Microsoft
description: "Ridimensionare un cluster di Service Fabric in o out toomatch richiesta impostando le regole di scalabilità automatica per ogni set di scalabilità macchina/virtuale di tipo di nodo. Aggiungere o rimuovere nodi tooa dell'infrastruttura del servizio cluster"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Aumentare o ridurre le istanze del cluster di Service Fabric con le regole di scalabilità automatica
Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure che è possibile utilizzare toodeploy e gestire una raccolta di macchine virtuali come un set. Ogni tipo di nodo definito in un cluster di Service Fabric viene configurato come set di scalabilità di macchine virtuali distinto. Ogni tipo di nodo può quindi essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse. Ulteriori informazioni in hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) documento. Poiché hello Service Fabric tipi di nodi del cluster sono costituiti da set di scalabilità di macchine virtuali nel back-end hello, è necessario tooset le regole di scalabilità automatica per ogni set di scalabilità macchina/virtuale di tipo di nodo.

> [!NOTE]
> La sottoscrizione deve avere sufficiente tooadd core hello nuove macchine virtuali che costituiscono il cluster. Non è attualmente alcuna convalida del modello in modo da ottenere un errore in fase di distribuzione, se uno qualsiasi dei limiti di quota hello raggiunti.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Scegliere tipo nodo hello/virtuale scalabilità della macchina impostare tooscale
Attualmente, non le regole di scalabilità automatica hello in grado di toospecify per set di scalabilità di macchine virtuali tramite il portale di hello, pertanto consentire di utilizzare i tipi di nodo di Azure PowerShell (1.0 +) toolist hello e quindi aggiungere toothem regole di scalabilità automatica.

elenco di hello tooget della macchina virtuale, set di scalabilità che costituiscono il cluster, eseguire hello seguente cmdlet:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Impostare le regole di ridimensionamento automatico per set di scalabilità macchina virtuale di tipo/nodo hello
Se il cluster con più tipi di nodo, quindi ripetere l'operazione per ogni tipi di nodo/virtuale scalabilità della macchina imposta che si desidera tooscale (in o out). Prendere in numero di account hello di nodi che è necessario disporre prima di configurare la scalabilità automatica. numero minimo di Hello di nodi che è necessario che per il tipo di nodo primario hello viene gestita dal livello di affidabilità hello scelto. Per altre informazioni, vedere la sezione relativa ai [livelli di affidabilità](service-fabric-cluster-capacity.md).

> [!NOTE]
> Riduzione tooless tipo di nodo primario hello del numero minimo di hello rendere cluster hello instabile o attivare la modalità verso il basso. Ciò potrebbe causare la perdita di dati per le applicazioni e servizi di sistema hello.
> 
> 

Funzionalità di scalabilità automatica hello attualmente non dipende da carichi hello che le applicazioni possono essere reporting tooService dell'infrastruttura. Pertanto in hello questo tempo è ottenere scalabilità automatica viene gestita esclusivamente dai contatori delle prestazioni generati da ciascuna delle istanze set di scalabilità di macchine virtuali hello hello.  

Seguire queste istruzioni [tooset di scalabilità automatica per ogni set di scalabilità della macchina virtuale](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> In una scala scenario verso il basso, a meno che il tipo di nodo dispone di un livello di durabilità di oro o argento è necessario hello toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) con il nome di nodo appropriato hello.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Aggiungere manualmente le macchine virtuali tooa nodo tipo/virtuale set di scalabilità della macchina
Seguire l'esempio hello le istruzioni in hello [raccolta di modelli di avvio rapido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) numero hello toochange delle macchine virtuali in ogni tipo di nodo. 

> [!NOTE]
> Aggiunta di macchine virtuali richiede tempo, in modo non si prevede hello aggiunte toobe istantaneo. Quindi pianificare la capacità di tooadd anche in fase di tooallow più di 10 minuti prima che sia disponibile per le repliche hello hello capacità di macchine Virtuali / inserito tooget di istanze del servizio.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Rimuovere manualmente le macchine virtuali dal set di scalabilità macchina virtuale di tipo/hello nodo primario
> [!NOTE]
> servizi di sistema di infrastruttura servizio Hello eseguire nel tipo di nodo primario hello del cluster. Minore rispetto a quale livello di affidabilità hello garantisce pertanto mai arrestare o ridurre il numero di hello di istanze di tipi di nodo. Fare riferimento troppo[hello dettagli sui livelli di affidabilità qui](service-fabric-cluster-capacity.md). 
> 
> 

È necessario tooexecute hello seguenti passaggi viene un'istanza di macchina virtuale alla volta. In questo modo i servizi di sistema hello (e i servizi con stati) toobe arrestare normalmente nell'istanza VM hello si intende rimuovere e nuove repliche create in altri nodi.

1. Eseguire [Disable ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) con finalità del nodo 'RemoveNode' hello toodisable eseguirai tooremove (istanza di quel tipo di nodo più alto per hello).
2. Eseguire [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake che tale nodo hello effettivamente ha eseguito la transizione toodisabled. In caso contrario, attendere che il nodo hello è disabilitato. Non è possibile accelerare questo passaggio.
3. Seguire l'esempio hello le istruzioni in hello [raccolta di modelli di avvio rapido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello numero di macchine virtuali in tale tipo di nodo. istanza di Hello rimosso è istanza VM massimo hello. 
4. Ripetere i passaggi da 1 a 3 in base alle necessità, ma mai scalare verso il basso il numero di hello di istanze in hello principali tipi di nodo minore garantisce il livello di affidabilità hello. Fare riferimento troppo[hello dettagli sui livelli di affidabilità qui](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Rimuovere manualmente le macchine virtuali dal tipo di nodo non primario hello/virtuale set di scalabilità della macchina
> [!NOTE]
> Per un servizio con stato, è necessario un certo numero di nodi toobe sempre backup dello stato di disponibilità e mantenere toomaintain del servizio. In hello requisito minimo, è necessario hello numero di nodi uguale toohello destinazione replica set numero di partizione o hello del servizio. 
> 
> 

È necessario hello hello segue un'istanza VM passaggi in una fase di esecuzione. In questo modo i servizi di sistema hello (e i servizi con stati) toobe arrestare normalmente in hello istanza della macchina virtuale che si intende rimuovere e nuove repliche creato where else.

1. Eseguire [Disable ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) con finalità del nodo 'RemoveNode' hello toodisable eseguirai tooremove (istanza di quel tipo di nodo più alto per hello).
2. Eseguire [Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake che tale nodo hello effettivamente ha eseguito la transizione toodisabled. Se non attendere hello del nodo è disabilitato. Non è possibile accelerare questo passaggio.
3. Seguire l'esempio hello le istruzioni in hello [raccolta di modelli di avvio rapido](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello numero di macchine virtuali in tale tipo di nodo. Istanza della macchina virtuale più alto hello rimuoverà. 
4. Ripetere i passaggi da 1 a 3 in base alle necessità, ma mai scalare verso il basso il numero di hello di istanze in hello principali tipi di nodo minore garantisce il livello di affidabilità hello. Fare riferimento troppo[hello dettagli sui livelli di affidabilità qui](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Comportamenti che è possibile osservare in Service Fabric Explorer
Quando è la scalabilità verticale hello un cluster Service Fabric Explorer riflette il numero di hello di nodi (istanze di set di scalabilità della macchina virtuale) che fanno parte del cluster di hello.  Tuttavia, quando scala in un cluster è verrà visualizzato istanza nodo/VM hello rimosso visualizzato in uno stato non integro, a meno che non si chiama [cmd Remove ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx) con il nome di nodo appropriato hello.   

Di seguito viene fornita la spiegazione hello per questo comportamento.

nodi elencati in Service Fabric Explorer Hello sono un riflesso di quali servizi di sistema di Service Fabric hello (FM specificamente) numero hello di nodi del cluster di hello avuto è a conoscenza. Quando si ridimensiona hello scalabilità della macchina virtuale impostata verso il basso, hello macchina virtuale è stata eliminata, ma il servizio di sistema FM consente comunque di tale nodo hello (che è stato mappato toohello macchina virtuale che è stato eliminato), verrà ripristinato. Pertanto, Service Fabric Explorer continua toodisplay quel nodo (se lo stato di integrità hello errore o sconosciuto).

In ordine toomake assicurarsi che un nodo viene rimosso quando viene rimossa una macchina virtuale, sono disponibili due opzioni:

1) Scegliere un livello di durabilità di oro o Silver (disponibile non appena) hello tipi di nodo del cluster, che consente di integrazione di un'infrastruttura di hello. Che verranno quindi automaticamente rimossi hello nodi dallo stato di servizi (FM) sistema durante il ridimensionamento verso il basso.
Fare riferimento troppo[hello dettagli sui livelli di durabilità qui](service-fabric-cluster-capacity.md)

2) Una volta ridimensionata istanza hello della macchina virtuale, è necessario hello toocall [cmdlet Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Servizio cluster di infrastruttura richiedono un certo numero di nodi toobe backup in tutto il tempo hello in toomaintain disponibilità e mantenere lo stato dell'ordine - tooas cui "gestione quorum". In tal caso, è in genere unsafe tooshut verso il basso tutte le macchine hello cluster hello a meno che non è stata innanzitutto eseguita una [backup completo dello stato del](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Hello lettura seguente tooalso informazioni sulla pianificazione della capacità del cluster, l'aggiornamento di un cluster e partizionamento servizi:

* [Considerazioni sulla pianificazione della capacità del cluster di Service Fabric](service-fabric-cluster-capacity.md)
* [Aggiornare un cluster di Service Fabric](service-fabric-cluster-upgrade.md)
* [Partizionare Reliable Services di Service Fabric](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
