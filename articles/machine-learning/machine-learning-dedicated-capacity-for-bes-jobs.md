---
title: "Capacità per i processi del servizio esecuzione Batch Machine Learning aaaDedicated | Documenti Microsoft"
description: Panoramica dei servizi di Azure Batch per i processi di Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Servizio Azure Batch per i processi di Machine Learning

L'elaborazione di Machine Learning Batch Pool fornisce scalabilità gestita dal cliente per hello servizio esecuzione Batch di Azure Machine Learning. Elaborazione per machine learning classico batch viene eseguito in un ambiente multi-tenant, il numero di hello limiti di processi simultanei, è possibile inviare e i processi viene messe in coda con cadenza first-in-first-out. Non è quindi possibile prevedere con precisione quando verrà eseguito il processo.

L'elaborazione di batch Pool consente toocreate pool in cui è possibile inviare i processi batch. È possibile controllare le dimensioni di hello del pool di hello e toowhich pool hello processo viene inviato. Il processo di BES viene eseguito in proprio fornire spazio di elaborazione delle prestazioni di elaborazione stimabile e hello possibilità toocreate i pool di risorse che corrispondono a carico di elaborazione toohello inviati.

## <a name="how-toouse-batch-pool-processing"></a>Come l'elaborazione Batch Pool toouse

Configurazione del Pool di elaborazione Batch non è attualmente disponibile tramite hello portale di Azure. toouse Pool Batch l'elaborazione, è necessario:

-   Chiamare CSS toocreate un Account del Pool di Batch e ottenere un URL del servizio del Pool e una chiave di autorizzazione
-   Creare un nuovo servizio Web e un nuovo piano di fatturazione basati su Resource Manager

toocreate il tuo account, chiamare il servizio clienti e supporto tecnico e fornire l'ID sottoscrizione. CSS funziona con si toodetermine hello capacità per il proprio scenario. CSS configura quindi l'account con numero massimo di hello di pool, è possibile creare e hello numero massimo di macchine virtuali (VM) che è possibile inserire in ciascun pool. Al termine della configurazione dell'account viene fornito l'URL del servizio pool e una chiave di autorizzazione.

Dopo aver creato l'account, utilizzare hello URL del servizio del Pool e l'autorizzazione tooperform chiave pool operazioni di gestione nel Pool di Batch.

![Architettura del servizio pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Creare pool chiamando l'operazione di creazione del Pool di hello all'URL di servizio del pool di hello che tooyou CSS fornito. Quando si crea un pool, specificare il numero di hello di macchine virtuali e l'URL di hello di hello swagger di un nuovo gestore di risorse basato su servizio web Machine Learning. Questo servizio web viene fornito l'associazione di fatturazione hello tooestablish. servizio del Pool di Batch di Hello utilizza hello swagger tooassociate hello pool con un piano di fatturazione. È possibile eseguire qualsiasi BES entrambi nuovo gestore di risorse basato su servizio web e classico, si sceglie nel pool di hello.

È possibile utilizzare qualsiasi servizio web basato su nuovo gestore di risorse, ma tenere presente che la fatturazione per i processi di hello hello vengano addebitati rispetto al piano di fatturazione hello associato al servizio. È progettato per l'esecuzione di processi Batch Pool toocreate un servizio web e fatturazione nuovo piano.

Per altre informazioni sulla creazione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Dopo aver creato un pool, si invia hello BES processo tramite hello Batch le richieste di URL per il servizio web hello. È possibile scegliere toosubmit è tooa tooclassic o del pool di elaborazione di batch. toosubmit un'elaborazione Pool tooBatch, aggiungere hello seguendo il corpo della richiesta parametro toohello processo invio:

"AzureBatchPoolId":"&lt;ID pool&gt;"

Se non si aggiunge il parametro hello, processo di hello viene eseguito nell'ambiente di elaborazione batch classico hello. Se il pool di hello ha risorse disponibili, il processo di hello avvia immediatamente l'esecuzione. Se il pool di hello non dispone di liberare le risorse, il processo viene accodato fino a quando non è disponibile una risorsa.

Se si ritiene che si raggiunge regolarmente i pool di capacità hello ed è necessario maggiore capacità, è possibile chiamare CSS e lavorare con un rappresentante tooincrease le quote.

Richiesta di esempio:

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Considerazioni sull'elaborazione di pool Batch

Pool di elaborazione batch è un servizio di fatturabile always-on e che richiede tooassociate è un gestore di risorse basato su piano di fatturazione. Verrà addebitato solo per il numero di ore di calcolo è in esecuzione il pool di hello; hello indipendentemente dal numero di hello dei processi eseguiti durante tale pool di tempo. Se si crea un pool, verrà addebitato per ore di calcolo hello di ogni macchina virtuale nel pool di hello fino a quando non viene eliminato il pool di hello, anche se nessun processo batch è in esecuzione nel pool di hello. La fatturazione per le macchine virtuali hello inizia quando hanno finito di provisioning e si arresta quando sono state eliminate. È possibile utilizzare uno dei piani di hello trovati in hello [dettagli prezzi di Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).

Esempio di fatturazione:

Se si crea un pool Batch con 2 macchine virtuali e lo si elimina dopo 24 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo, indipendentemente dal numero di processi eseguiti in questo periodo.

Se si crea un pool Batch con 4 macchine virtuali e lo si elimina dopo 12 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo.

È consigliabile eseguire il polling hello processo stato toodetermine quando completamento dei processi. Quando tutti i processi hanno terminato l'esecuzione, chiamata hello ridimensionamento Pool tooset hello numero delle operazioni delle macchine virtuali in hello pool toozero. Se sono brevi su risorse del pool ed è necessario toocreate un nuovo pool, ad esempio toobill rispetto a un piano di fatturazione diverso, è possibile eliminare pool hello invece al termine del tutti i processi in esecuzione.


| **Usare l'elaborazione di pool Batch quando**    | **Usare l'elaborazione di batch classica quando**  |
|---|---|
|È necessario un numero elevato di processi toorun<br>Or<br/>È necessario tooknow che i processi verranno eseguiti immediatamente<br/>Or<br/>È necessario garantire la velocità effettiva. Ad esempio necessario toorun un numero di processi in un determinato intervallo di tempo e desidera tooscale out del toomeet risorse di calcolo le proprie esigenze.    | Si sta eseguendo un numero limitato di processi<br/>e<br/> Non è necessario hello processi toorun immediatamente |
