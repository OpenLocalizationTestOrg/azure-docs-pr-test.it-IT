---
title: aaaBalance il cluster di Azure Service Fabric | Documenti Microsoft
description: Toobalancing un'introduzione del cluster con hello servizio di gestione delle risorse Cluster dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Bilanciamento del carico nel cluster di Service Fabric
Hello gestione delle risorse Cluster di Service Fabric supporta modifiche al caricamento dinamico, reazione tooadditions o la rimozione di nodi o servizi. Corregge automaticamente anche le violazioni dei vincoli ed eseguito in modo proattivo il ribilanciamento cluster hello. Ma con quale frequenza vengono eseguite queste azioni, e che cosa le attiva?

Sono disponibili tre diverse categorie di lavoro che hello esegue Gestione risorse di Cluster. Sono:

1. Posizionamento: questa fase riguarda l'inserimento di repliche con stato o istanze senza stato mancanti. Il posizionamento include sia i nuovi servizi sia la gestione di repliche con stato o istanze senza stato non riuscite. In questa fase viene gestita l'eliminazione di istanze e repliche.
2. Vincolo di verifica: questa fase controllate e corrette le violazioni dei vincoli di posizionamento diverse hello (regole) all'interno del sistema hello. Le regole servono, ad esempio, per controllare che i nodi non superino la capacità o che i vincoli di posizionamento di un servizio vengano rispettati.
3. Bilanciamento del carico: questa fase controlla toosee se ribilanciamento è necessario in base a hello configurato desiderato a livello di bilanciamento per metriche. In tal caso tenta toofind una disposizione in hello del cluster che è più bilanciato.

## <a name="configuring-cluster-resource-manager-timers"></a>Configurazione dei timer di Cluster Resource Manager
Hello primi dei controlli intorno a bilanciamento del carico sono un set di timer. Questi timer determinano la frequenza con cui hello gestione delle risorse Cluster esamina cluster hello e accetta le azioni correttive.

Ognuno di questi tipi diversi di hello correzioni consentono di gestione delle risorse Cluster è controllato da un diverso timer che determina la frequenza. Quando viene generato ogni timer, i hello è pianificata. Per impostazione predefinita hello Gestione risorse:

* Analizza lo stato e applica gli aggiornamenti, ad esempio la registrazione di un nodo inattivo, ogni decimo di secondo.
* Imposta flag di controllo di selezione host hello 
* Imposta flag di controllo di vincolo hello ogni secondo
* Imposta hello bilanciamento del carico flag ogni cinque secondi.

Di seguito sono riportati esempi di configurazione di hello che governano questi timer:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Oggi hello gestione delle risorse Cluster esegue solo una di queste azioni contemporaneamente, in modo sequenziale. È per questo motivo è vedere timer toothese come "intervalli minimi" e hello azioni eseguite quando il timer di hello si trovi in come "impostazione flag" ottengano. Hello occupa gestione delle risorse Cluster in sospeso, ad esempio, richiede i servizi di toocreate prima hello cluster di bilanciamento. Come si può notare da intervalli di tempo predefinito hello specificati, hello gestione delle risorse Cluster per qualsiasi elemento viene analizzato toodo esigenze di frequente. In genere, ciò significa che il set di hello delle modifiche apportate durante ogni passaggio è piccolo. Apportare piccole modifiche spesso consente hello toobe di gestione delle risorse Cluster risponde quando si verificano eventi in cluster hello. Hello timer predefiniti forniscono alcuni batch poiché molte delle hello stessi tipi di eventi tendono toooccur contemporaneamente. 

Ad esempio, quando i nodi presentano errori possono procedere con interi domini di errore alla volta. Tutti questi errori vengono acquisiti durante il successivo stato hello aggiornamento dopo hello *PLBRefreshGap*. correzioni di Hello vengono determinate durante hello dopo la selezione, controllo del vincolo e bilanciamento del carico viene eseguito. Per hello predefinito gestione delle risorse Cluster è non l'analisi di ore di modifiche in cluster hello e tentativo tooaddress tutte le modifiche in una sola volta. In questo modo potrebbe causare toobursts di varianza.

Gestione delle risorse Cluster Hello deve inoltre toodetermine alcune informazioni aggiuntive se hello cluster sbilanciata. Per gestire questi aspetti sono disponibili due controlli di configurazione: le *soglie di bilanciamento* e le *soglie di attività*.

## <a name="balancing-thresholds"></a>Soglie di bilanciamento del carico
Una soglia di bilanciamento del carico è controllo principale di hello per l'attivazione di ribilanciamento. Hello bilanciamento del carico di soglia per una metrica è un _rapporto_. Se il carico hello per una misurazione in hello caricato più nodo divisa per la quantità di hello di carico nel minor caricata hello nodo supera tale metrica *BalancingThreshold*, quindi cluster hello è bilanciato. Di conseguenza bilanciamento del carico è hello ora successiva hello trigger Controlla gestione delle risorse Cluster. Hello *MinLoadBalancingInterval* timer definisce con quale frequenza hello gestione delle risorse Cluster deve verificare se il ribilanciamento è necessario. Controllare non comporta che venga eseguita un'operazione. 

Soglie di bilanciamento del carico sono definite con cadenza per metriche come parte della definizione di cluster hello. Per altre informazioni sulle metriche, vedere [questo articolo](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![Esempio di soglia di bilanciamento][Image1]
</center>

In questo esempio ogni servizio usa una unità di una metrica. Nell'esempio hello superiore hello del carico massimo in un nodo è cinque e minimo hello è due. Si supponga che hello bilanciamento del carico di soglia per questa metrica è tre. Poiché il rapporto di hello cluster hello è 5/2 = 2.5 e che è inferiore a quello hello specificato soglia del cluster di tre, hello di bilanciamento del carico viene bilanciato. Nessun bilanciamento del carico viene attivata quando verifica la gestione delle risorse Cluster hello.

Nell'esempio hello basso carico massimo di hello in un nodo è 10, mentre hello minimo è due, risultante in un rapporto di cinque. Cinque è maggiore del valore soglia di bilanciamento del carico designato hello di tre per tale metrica. Di conseguenza, esecuzione di un ribilanciamento sarà pianificato hello ora successiva bilanciamento del carico generato timer. In una situazione simile al seguente parte del carico è in genere distribuite tooNode3. Perché hello servizio di gestione delle risorse Cluster dell'infrastruttura non utilizza un approccio greedy, potrebbe essere anche un carico tooNode2 distribuita. 

<center>
![Azioni sull'esempio di soglia di bilanciamento][Image2]
</center>

> [!NOTE]
> Il "Bilanciamento" gestisce due diverse strategie per gestire il carico nel cluster. strategia predefinita Hello hello Usa Gestione risorse di Cluster è toodistribute carico tra i nodi del cluster hello hello. Hello altri strategia è [deframmentazione](service-fabric-cluster-resource-manager-defragmentation-metrics.md). La deframmentazione viene eseguita durante hello stesso bilanciamento del carico di esecuzione. Hello strategie di bilanciamento del carico e deframmentazione in linea possono essere utilizzate per le metriche diversi all'interno di hello dello stesso cluster. Un servizio può disporre di metriche di bilanciamento e di deframmentazione. Per la metrica di deframmentazione in linea, rapporto hello di hello carica nei trigger cluster hello in questo caso il ribilanciamento _seguito_ hello soglia di bilanciamento del carico. 
>

Recupero seguito hello soglia di bilanciamento del carico non è un obiettivo esplicito. Le soglie di bilanciamento sono semplicemente un *trigger*. Quando Bilanciamento del carico viene eseguito, hello gestione delle risorse Cluster determina quali miglioramenti rendere, se presente. Il fatto che venga avviata una ricerca di bilanciamento non significa che vengano spostati degli elementi. A volte hello cluster è toocorrect sbilanciata ma troppo limitata. In alternativa, miglioramenti di hello richiedono i movimenti che sono troppo [costosi](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>soglie di attività
In alcuni casi, anche se i nodi sono relativamente sbilanciati, hello *totale* quantità di carico nel cluster hello è bassa. mancanza di Hello di carico può essere un dip temporaneo o perché cluster hello è nuovo e recupero appena avviato automaticamente. In entrambi i casi, è opportuno non ora toospend hello cluster di bilanciamento perché è poco toobe acquisita. Se il cluster hello sottoposti a bilanciamento del carico, si sarebbe spesa rete e risorse toomove diversi elementi di calcolo senza apportare qualsiasi grande *assoluto* differenza. Sposta tooavoid non necessari, è noto come soglie di attività di un altro controllo. Soglie di attività consente toospecify limite alcuni inferiore assoluto per l'attività. Se nessun nodo oltre questa soglia, bilanciamento del carico non viene attivato anche se hello bilanciamento del carico viene raggiunta la soglia.

Si supponga che abbiamo mantenuto la soglia di bilanciamento su tre per questa metrica. Si supponga anche che sia disponibile una Soglia di attività di 1536. Nel primo caso hello, mentre il cluster hello è bilanciato per hello bilanciamento del carico di soglia sono soddisfa alcun nodo tale soglia di attività è avviene quindi alcuna operazione. Nell'esempio hello inferiore Node1 è su hello soglia di attività. Poiché entrambi hello soglia di bilanciamento del carico e hello soglia di attività per la metrica hello vengono superate, bilanciamento del carico è pianificata. Ad esempio, si esaminerà hello seguente diagramma: 

<center>
![Esempio di soglia di attività][Image3]
</center>

Analogamente alle soglie di bilanciamento del carico, le soglie di attività sono definiti per ogni metrica tramite la definizione del cluster di hello:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

mediante ClusterConfig.json per le distribuzioni autonome o Template.json per i cluster ospitati in Azure:

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Soglie di bilanciamento carico di rete e attività sono entrambi legati tooa metrica specifica - bilanciamento del carico viene generato solo se entrambi hello soglia di bilanciamento del carico e viene superata la soglia di attività per hello stessa metrica.

## <a name="balancing-services-together"></a>Bilanciamento composto dei servizi
Se non è bilanciato cluster hello o non è una decisione a livello di cluster. È tuttavia modo hello passiamo su correggerlo lo spostamento repliche singolo servizio e le istanze. Questo approccio ha senso, giusto? Se aggiunti allo stack memoria in un nodo, più repliche o istanze potrebbero contribuire tooit. Correzione sbilanciamento hello potrebbe richiedere lo spostamento di una delle repliche con stato hello o istanze senza state che utilizzano metrica sbilanciata hello.

In alcuni casi però viene spostato un servizio che non era stesso sbilanciata (a questo proposito hello locale e globale pesi in precedenza). Per quale motivo si dovrebbe spostare un servizio quando tutte le metriche di quel servizio sono state bilanciate? Di seguito viene illustrato un esempio:

- Si supponga di avere quattro servizi: Service1, Service2, Service3 e Service4. 
- Service1 riporta le metriche Metric1 e Metric2. 
- Service2 riporta le metriche Metric2 e Metric3. 
- Service3 riporta le metriche Metric3 e Metric4.
- Service4 riporta la metrica Metric99. 

Sicuramente è già possibile intravedere una spiegazione: la catena. Non ci sono quattro servizi indipendenti, ma tre servizi correlati tra loro e uno autonomo.

<center>
![Bilanciamento composto dei servizi][Image4]
</center>

A causa di questa catena, è possibile che uno squilibrio nelle metriche 1-4 può causare le repliche o le istanze appartenenti tooservices 1-3 toomove intorno. Sappiamo anche che uno sbilanciamento delle metriche 1, 2 o 3 non può comportare movimenti in Service4. Non vi sarà alcun punto dopo lo spostamento le repliche hello o le istanze appartenenti tooService4 intorno può assolutamente nessun saldo hello tooimpact delle metriche 1-3.

Hello gestione delle risorse Cluster determina automaticamente i servizi correlati. Aggiunta, rimozione o modifica le metriche di hello per i servizi possono influire sulle relative relazioni. Ad esempio, tra due esecuzioni del bilanciamento del carico Service2 potrebbe essere stato aggiornato tooremove Metric2. Viene interrotta la catena di hello tra Service1 e Service2. Ora, invece di due gruppi di servizi correlati ce ne sono tre:

<center>
![Bilanciamento composto dei servizi][Image5]
</center>

## <a name="next-steps"></a>Passaggi successivi
* Le metriche sono la modalità di gestione di consumo e la capacità in cluster hello in hello gestore di risorse Cluster dell'infrastruttura del servizio. ulteriori informazioni sulle metriche toolearn come tooconfigure, archiviazione ed estrazione [in questo articolo](service-fabric-cluster-resource-manager-metrics.md)
* Il costo dello spostamento è un modo di segnalazione toohello gestione delle risorse Cluster che alcuni servizi siano toomove più costosi rispetto ad altri. Per ulteriori informazioni sul costo di spostamento, fare riferimento troppo[in questo articolo](service-fabric-cluster-resource-manager-movement-cost.md)
* Hello gestione delle risorse Cluster ha le limitazioni diversi che è possibile configurare tooslow verso il basso la varianza del cluster di hello. Queste limitazioni non sono in genere necessarie, ma sono eventualmente disponibili altre informazioni [qui](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
