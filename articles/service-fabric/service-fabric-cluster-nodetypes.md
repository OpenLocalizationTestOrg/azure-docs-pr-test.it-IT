---
title: "Infrastruttura aaaService tipi di nodo e il set di scalabilità di macchine Virtuali | Documenti Microsoft"
description: "Descrive come tipi di nodo di Service Fabric correlare tooVM set di scalabilità e la modalità di connessione tooremote tooa istanza del Set di scalabilità della macchina virtuale o un nodo del cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>relazione Hello tra set di scalabilità di macchine virtuali e i tipi di nodo di Service Fabric
Set di scalabilità di macchine virtuali sono una risorsa di calcolo di Azure è possibile utilizzare toodeploy e gestire una raccolta di macchine virtuali come un set. Ogni tipo di nodo definito in un cluster di Service Fabric è configurato come un set di scalabilità di macchine virtuali separato. Ogni tipo di nodo può quindi essere aumentato o ridotto in modo indipendente, avere diversi set di porte aperte e avere metriche per la capacità diverse.

Hello cattura di schermata seguente viene illustrato un cluster con due tipi di nodo: front-end e back-end.  Ogni tipo di nodo ha cinque nodi.

![Screenshot di un cluster con due tipi di nodo][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>Mapping di Set di scalabilità della macchina virtuale toonodes istanze
Come si può notare in precedenza, le istanze di Set di scalabilità della macchina virtuale hello avviare dall'istanza 0 e quindi aumenta. numerazione Hello viene riflessa nei nomi di hello. Ad esempio, BackEnd_0 è istanza 0 del Set di scalabilità della macchina virtuale back-end hello. Questo particolare set di scalabilità di macchine virtuali ha cinque istanze, denominate BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 e BackEnd_4.

Quando si aumenta un set di scalabilità di macchine virtuali, viene creata una nuova istanza. Hello nuovo Set di scalabilità della macchina virtuale Nome istanza corrisponderà in genere il nome di Set di scalabilità della macchina virtuale hello + numero istanza successivo hello. Nell'esempio sarà BackEnd_5.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Mapping VM bilanciamento tooeach nodo tipo/VM Set di scalabilità di caricare set di scalabilità
Se è stato distribuito il cluster dal portale hello o modello di gestione risorse di esempio hello è forniti, quindi quando si ottiene un elenco di tutte le risorse in un gruppo di risorse non è utilizzato verrà visualizzato servizi di bilanciamento del carico hello per ogni tipo di Set di scalabilità della macchina virtuale o di nodo.

Hello nome sarebbe simile al seguente: **LB -&lt;nome NodeType&gt;**. ad esempio, LB-sfcluster4doc-0, come in questo screenshot:

![Risorse][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Istanza di tooa Set di scalabilità della macchina virtuale o un nodo del cluster della connessione remota
Ogni tipo di nodo definito in un cluster viene configurato come set di scalabilità di macchine virtuali separato.  È possibile scalare che indica hello tipi di nodo alto o verso il basso in modo indipendente e può essere costituita da diverse SKU di macchina virtuale. A differenza delle macchine virtuali a singola istanza, le istanze di hello Set di scalabilità della macchina virtuale non si ottengono un indirizzo IP virtuale di propri. Pertanto può essere un po' difficile quando si cercano un indirizzo IP indirizzo e la porta che è possibile utilizzare tooremote connettersi tooa specifica istanza.

Di seguito sono hello è possibile attenersi alla procedura toodiscover li.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>Passaggio 1: Trovare l'indirizzo IP virtuale hello per il tipo di nodo hello e quindi le regole NAT in ingresso per RDP
Nel tooget ordine, è necessario tooget hello NAT in ingresso, le regole i valori che sono stati definiti come parte della definizione di risorsa hello per **Microsoft.Network/loadBalancers**.

Nel portale di hello passare pannello del servizio di bilanciamento carico di toohello e quindi **impostazioni**.

![Pannello servizio di bilanciamento del carico][LBBlade]

In **Impostazioni** fare clic su **Regole NAT in ingresso**. A questo punto si hello indirizzo IP e porta che è possibile utilizzare tooremote consente di connettono toohello prima istanza del Set di scalabilità della macchina virtuale. Nella seguente schermata hello è **104.42.106.156** e **3389**

![Regole NAT][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>Passaggio 2: Individuare porta hello che è possibile utilizzare tooremote connettersi toohello specifico Set di scalabilità della macchina virtuale/nodo dell'istanza
In questo documento, è parlato mapping toohello nodi di istanze di Set di scalabilità della macchina virtuale hello. Si utilizzerà tale toofigure out hello esatta per la porta.

porte Hello vengono allocate in ordine crescente dell'istanza di hello Set di scalabilità della macchina virtuale. Pertanto, in questo esempio per il tipo di nodo front-end hello, porte hello per ognuno dei cinque istanze di hello sono seguente hello. è ora necessario toodo hello stesso mapping per l'istanza del Set di scalabilità della macchina virtuale.

| **Istanza del set di scalabilità di macchine virtuali** | **Porta** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>Passaggio 3: Toohello specifica istanza di macchina virtuale del Set di scalabilità della connessione remota
Utilizzare connessione Desktop remoto tooconnect toohello FrontEnd_1 in hello schermata riportata di seguito:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Come valori di intervallo hello toochange porta RDP
### <a name="before-cluster-deployment"></a>Prima della distribuzione cluster
Quando si configura il cluster hello utilizzando un modello di gestione delle risorse, è possibile specificare l'intervallo hello in hello **inboundNatPools**.

Vai a definizione di risorsa toohello **Microsoft.Network/loadBalancers**. In cui si trova descrizione hello per **inboundNatPools**.  Sostituire hello *valore finale* e *frontendPortRangeEnd* valori.

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Dopo la distribuzione cluster
Questo è un po' più complicata e può comportare nelle macchine virtuali hello recupero riciclate. È ora tooset i nuovi valori utilizzando Azure PowerShell. Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva. Se non è stata eseguita questa operazione prima di, fortemente consigliabile seguire passaggi descritti nella procedura hello [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)

Accedi tooyour account Azure. Se per qualche motivo questo comando PowerShell genera un errore, verificare che Azure PowerShell sia installato correttamente.

```
Login-AzureRmAccount
```

Eseguire i seguenti dettagli tooget nel servizio di bilanciamento del carico hello e vengono visualizzati valori hello per descrizione hello per **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Impostare ora *frontendPortRangeEnd* e *valore finale* toohello valori desiderati.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Passaggi successivi
* [Panoramica sulla funzionalità di "In un punto qualsiasi distribuzione" hello e un confronto con i cluster gestito di Azure](service-fabric-deploy-anywhere.md)
* [Sicurezza del cluster](service-fabric-cluster-security.md)
* [ Service Fabric SDK e introduzione](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
