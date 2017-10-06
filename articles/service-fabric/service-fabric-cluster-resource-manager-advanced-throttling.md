---
title: in Gestione risorse del cluster di Service Fabric hello aaaThrottling | Documenti Microsoft
description: Informazioni su limitazioni hello tooconfigure fornite dal servizio di gestione delle risorse Cluster dell'infrastruttura di hello.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>La limitazione delle richieste di servizio di gestione delle risorse Cluster dell'infrastruttura di hello
Anche se hai configurato la gestione delle risorse Cluster hello correttamente, è possibile ottenere interrotte cluster hello. Ad esempio, potrebbe essere nodo e errore di dominio errori simultanei - che cosa accadrebbe se che si è verificato durante l'aggiornamento? Gestione delle risorse Cluster Hello tenta sempre toofix tutto, risorse del cluster hello tentativo tooreorganize e correzione di cluster hello. Le limitazioni forniscono una barriera in modo che il cluster hello può utilizzare risorse toostabilize - nodi hello passerà nuovamente, le partizioni di rete hello di correzione, vengono distribuiti i bit corretti.

toohelp con questi tipi di situazioni, hello gestione delle risorse Cluster dell'infrastruttura del servizio include numerose limitazioni. Queste limitazioni intervengono tutte in modo piuttosto pesante. In genere non devono essere modificate senza una pianificazione e un test accurati.

Se si modificano le limitazioni di gestione risorse del Cluster di hello, è consigliabile ottimizzarla li tooyour carico effettivo. È possibile determinare che toohave alcune limita sul posto, è necessario anche se questo comporta cluster hello accetta più toostabilize in alcune situazioni. Il test è obbligatorio toodetermine hello i valori corretti per le limitazioni. Le limitazioni necessario toobe tooallow sufficientemente elevato hello cluster toorespond toochanges in un intervallo di tempo ragionevole, e basso sufficiente tooactually impedire eccessivo consumo di risorse. 

La maggior parte del tempo di hello che clienti abbiamo visto utilizzare velocità che è stato in quanto sono già in un ambiente vincolato di risorse. Alcuni esempi possono essere di larghezza di banda di rete limitata per singoli nodi, o i dischi che non sono in grado di toobuild numero di repliche con stato in parallelo a causa di limitazioni toothroughput. Senza limitazioni, le operazioni Impossibile sovraccarico queste risorse, a causa di operazioni toofail o lenta. In questi casi i clienti utilizzato le limitazioni e informata che sono stati estendendo quantità hello di tempo impiegata hello cluster tooreach uno stato stabile. I clienti inoltre hanno compreso anche che il livello complessivo di affidabilità era inferiore in presenza di limitazioni.


## <a name="configuring-hello-throttles"></a>Configurare le limitazioni di hello

Service Fabric sono disponibili due meccanismi per la limitazione del numero di hello di spostamenti di tipo di replica. meccanismo predefinito di Hello che esistevano prima di Service Fabric 5.7 rappresenta la limitazione delle richieste come numero assoluto degli spostamenti è consentito. Non funziona per i cluster di tutte le dimensioni. In particolare, per impostazione predefinita di cluster di grandi dimensioni hello valore può essere troppo piccolo, rallentare notevolmente bilanciamento del carico anche quando è necessario, con un impatto non in cluster più piccoli. Questo meccanismo precedente è stato sostituito dalla limitazione basata sulla percentuale, che offre una maggiore scalabilità con i cluster dinamici in quale numero di hello di servizi e i nodi modificare regolarmente.

le limitazioni di Hello sono basate su una percentuale del numero di hello di repliche in cluster hello. Le limitazioni di base Percetage abilitare esprimere regola hello: "non si spostano più del 10% di repliche in un intervallo di 10 minuti", ad esempio.

impostazioni di configurazione Hello per la limitazione basata sulla percentuale sono:

  - GlobalMovementThrottleThresholdPercentage - numero massimo di spostamenti di tipo consentito nel cluster in qualsiasi momento, espresso come percentuale del numero massimo di repliche cluster hello. Impostarlo su 0 per non avere limiti. valore predefinito di Hello è 0. Se questa impostazione e GlobalMovementThrottleThreshold vengono specificati, quindi hello limite più attento viene utilizzato.
  - GlobalMovementThrottleThresholdPercentageForPlacement - numero massimo di spostamenti di tipo consentito nella fase hello posizione, espressa come percentuale del numero totale di repliche cluster hello. Impostarlo su 0 per non avere limiti. valore predefinito di Hello è 0. Se questa impostazione e GlobalMovementThrottleThresholdForPlacement vengono specificati, quindi hello limite più attento viene utilizzato.
  - GlobalMovementThrottleThresholdPercentageForBalancing - numero massimo di spostamenti di tipo durante la fase, espressa come percentuale del numero totale di repliche cluster hello di bilanciamento del carico hello è consentito. Impostarlo su 0 per non avere limiti. valore predefinito di Hello è 0. Se questa impostazione e GlobalMovementThrottleThresholdForBalancing vengono specificati, quindi hello limite più attento viene utilizzato.

Quando si specifica la percentuale di accelerazione hello, è necessario specificare % 5 come 0,05. intervallo di Hello in cui vengono gestite queste limitazioni è hello GlobalMovementThrottleCountingInterval, che è espresso in secondi.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Limitazioni basate sul conteggio predefinito
Queste informazioni vengono fornite nel caso in cui si disponga di cluster precedenti o si mantengano queste configurazioni in cluster che sono quindi stati aggiornati. In generale, è consigliabile che queste ultime vengono sostituite con hello basate su percentuale le limitazioni precedenti. Poiché la limitazione basata sulla percentuale è disabilitata per impostazione predefinita, queste limitazioni rimangono le limitazioni di hello predefinito per un cluster finché non vengono disabilitati e sostituiti con le limitazioni di hello basata sulla percentuale. 

  - GlobalMovementThrottleThreshold: questa impostazione controlla il numero totale di hello di spostamenti di tipo cluster hello su tempo. tempo totale di Hello è espresso in secondi come hello GlobalMovementThrottleCountingInterval. il valore predefinito Hello per hello GlobalMovementThrottleThreshold è 1000 e il valore predefinito hello per hello GlobalMovementThrottleCountingInterval è 600.
  - MovementPerPartitionThrottleThreshold: questa impostazione controlla il numero totale di hello di spostamenti di tipo per ogni partizione del servizio su tempo. tempo totale di Hello è espresso in secondi come hello MovementPerPartitionThrottleCountingInterval. il valore predefinito Hello per hello MovementPerPartitionThrottleThreshold è 50 e il valore predefinito hello per hello MovementPerPartitionThrottleCountingInterval è 600.

configurazione di Hello per queste limitazioni segue hello stesso schema come la limitazione basata sulla percentuale di hello.

## <a name="next-steps"></a>Passaggi successivi
- toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)
- Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello. toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
