---
title: aaaDefragmentation di metriche in Azure Service Fabric | Documenti Microsoft
description: Informazioni generali sull'uso della deframmentazione o della compressione come strategia per le metriche in Service Fabric
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Deframmentazione delle metriche e del carico in Service Fabric
strategia predefinita Hello servizio infrastruttura Cluster di gestione risorse per la gestione delle metriche di caricamento nel cluster hello è carico hello toodistribute. Assicurare che i nodi vengono utilizzati in modo uniforme evita e calda aree che portano tooboth contesa e uno spreco di risorse. Distribuzione dei carichi di lavoro nel cluster hello è anche hello più sicuro in termini di sopravvivenza errori dal momento che assicura che un errore di non estrarre una percentuale elevata di un determinato carico di lavoro. 

Hello gestione delle risorse Cluster di Service Fabric supporta una strategia diversa per la gestione di carico, ovvero la deframmentazione. Deframmentazione significa che anziché tentare di utilizzo di hello toodistribute di una metrica cluster hello, verrà consolidata. Consolidamento è semplicemente un'inversione del valore predefinito di hello strategia: invece di riduzione Media deviazione hello del carico di metrica di bilanciamento del carico, tenta di gestione delle risorse Cluster hello tooincrease è.

## <a name="when-toouse-defragmentation"></a>Quando la deframmentazione toouse
Distribuzione del carico nel cluster hello utilizza alcune risorse hello in ogni nodo. Alcuni carichi di lavoro creano servizi di dimensioni eccezionalmente elevate e consumano la maggior parte o tutto un nodo. In questi casi, è possibile che quando sono presenti grandi carichi di lavoro recupero creati non è sufficiente una spaziatura su toorun qualsiasi nodo. I carichi di lavoro di grandi dimensioni non sono un problema nell'infrastruttura del servizio; In questi hello casi Gestione delle risorse Cluster determina che deve tooreorganize hello cluster toomake spazio a questo carico di lavoro di grandi dimensioni. Tuttavia, in hello frattempo tale carico di lavoro ha toobe toowait pianificata cluster hello.

Se sono presenti molti servizi e stato toomove intorno, potrebbero richiedere molto tempo per hello elevato carico di lavoro toobe inserito in cluster hello. Questo è più probabile se altri carichi di lavoro in cluster hello inoltre sono di grandi dimensioni e pertanto richiedere tooreorganize più lungo. il team di Service Fabric Hello misurata tempi di creazione delle simulazioni di questo scenario. È stato rilevato che la creazione di servizi di grandi dimensioni ha richiesto molto più tempo quando l'uso del cluster ha superato il valore tra il 30 e il 50%. toohandle questo scenario, è stata introdotta la deframmentazione come strategia di bilanciamento del carico. Si è scoperto che per carichi di lavoro di grandi dimensioni, soprattutto quelli in cui ora di creazione è importante, la deframmentazione ha consentito di questi nuovi carichi di lavoro Pianificazione cluster hello.

È possibile configurare la deframmentazione metriche toohave hello carico di gestione delle risorse Cluster tooproactively try toocondense hello dei servizi hello in un minor numero di nodi. Ciò garantisce che c'è quasi sempre spazio per i servizi di grandi dimensioni senza la riorganizzazione cluster hello. Non cluster hello tooreorganize consente di creare rapidamente grandi carichi di lavoro.

La maggior parte degli utenti non avrà bisogno della deframmentazione. I servizi sono in genere essere piccolo, pertanto non è una chat room toofind disco per tali cluster hello. Quando la riorganizzazione è possibile avviene rapidamente poiché la maggior parte dei servizi sono di dimensioni ridotte e possono essere spostati rapidamente e in parallelo. Tuttavia, se si dispone di servizi di grandi dimensioni e inutili creati rapidamente hello strategia deframmentazione in linea è per l'utente. Verranno discussi i compromessi hello dell'utilizzo di deframmentazione accanto. 

## <a name="defragmentation-tradeoffs"></a>Svantaggi della deframmentazione
La deframmentazione può aumentare l'impatto degli errori, poiché vengono eseguiti più servizi sui nodi che presentano errori. Deframmentazione in linea è possibile aumentare anche i costi, poiché le risorse cluster hello devono essere tenute di riserva in attesa per la creazione di hello di carichi di lavoro di grandi dimensioni.

Hello diagramma seguente offre una rappresentazione visiva di due cluster, che viene deframmentato e uno che non sia. 

<center>
![Confronto tra cluster bilanciati e deframmentati][Image1]
</center>

In caso di hello bilanciato, prendere in considerazione hello numero di spostamenti di tipo che sarebbe necessario tooplace uno degli oggetti servizio più grande hello. Cluster deframmentato hello, carichi di lavoro elevati hello potrebbe trovarsi in nodi quattro o cinque senza toowait per qualsiasi altro toomove di servizi.

## <a name="defragmentation-pros-and-cons"></a>Vantaggi e svantaggi della deframmentazione
Quali sono quindi questi altri compromessi concettuali? Qui è una tabella rapida di operazioni toothink su:

| Vantaggi della deframmentazione | Svantaggi della deframmentazione |
| --- | --- |
| Consente di creare servizi di grandi dimensioni più rapidamente |Concentra i carichi in meno nodi, aumentando il conflitto |
| Consente di ridurre lo spostamento dei dati durante la creazione |Eventuali errori possono impattare più servizi e causare una maggiore varianza |
| Consente una descrizione completa dei requisiti e il recupero di spazio |Configurazione di gestione delle risorse complessiva più complessa |

È possibile combinare deframmentato e metriche normale in hello dello stesso cluster. Hello gestione delle risorse Cluster tenta tooconsolidate hello deframmentazione metriche quanto possibile durante la distribuzione hello ad altri utenti. risultati Hello della combinazione di deframmentazione e bilanciamento del carico strategie dipende da diversi fattori, tra cui:
  - numero di Hello di bilanciamento del carico metriche rispetto al numero di hello di metriche di deframmentazione in linea
  - se un servizio usa entrambi i tipi di metriche 
  - pesi metrica Hello
  - i carichi correnti delle metriche
  
Sperimentazione è obbligatorio toodetermine hello esatta configurazione necessaria. Si consiglia di misurare accuratamente i carichi di lavoro prima di abilitare le metriche di deframmentazione nella produzione. Ciò vale soprattutto quando la combinazione di deframmentazione in linea e metrica bilanciata in hello stesso servizio. 

## <a name="configuring-defragmentation-metrics"></a>Configurazione delle metriche di deframmentazione
Configurazione di metriche di deframmentazione in linea è una decisione globale cluster hello e metriche singoli possono essere selezionate per la deframmentazione. Hello configurazione frammenti di codice seguente mostra come tooconfigure metrica per la deframmentazione. In questo caso, "Metric1" è configurato come una metrica di deframmentazione in linea, mentre "Metric2" continuerà toobe bilanciato normalmente. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Passaggi successivi
- opzioni di man per descrivere il cluster hello Hello gestione delle risorse Cluster. toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Le metriche sono la modalità di gestione di consumo e la capacità in cluster hello in hello gestore di risorse Cluster dell'infrastruttura del servizio. ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [in questo articolo](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
