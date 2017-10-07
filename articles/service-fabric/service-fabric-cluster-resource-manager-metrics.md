---
title: il carico di Azure microservizio aaaManage utilizzando metriche | Documenti Microsoft
description: Informazioni su come l'uso di risorse del servizio metriche tooconfigure e l'utilizzo in Service Fabric toomanage.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Gestione dell'utilizzo delle risorse e del carico in Service Fabric con le metriche
*Metriche* sono risorse hello che pone i servizi e che vengono forniti per i nodi nel cluster hello hello. Una metrica è un valore che si desidera toomanage delle prestazioni di hello tooimprove o il monitoraggio di ordine dei servizi. Ad esempio si potrebbe controllare tooknow consumo di memoria se il servizio è in overload. Un altro utilizzo consiste toofigure out se è stato possibile spostare il servizio hello in un' posizione in cui memoria è che minore di vincolata un miglioramento delle prestazioni tooget ordine.

Sono metriche, ad esempio, l'utilizzo della CPU, della memoria e dei dischi. Queste metriche sono metriche fisiche, le risorse che corrispondono toophysical risorse nel nodo hello necessarie toobe gestiti. Le metriche possono anche essere logiche e in genere sono di questo tipo. Sono metriche logiche, ad esempio, "MyWorkQueueDepth", "MessagesToProcess" e "TotalRecords". Metriche logiche sono definiti dall'applicazione e indirettamente corrispondono toosome il consumo di risorse fisiche. Metriche logiche sono comuni in quanto può essere toomeasure disco rigido e consumo delle risorse fisiche in base al servizio di report. la complessità di Hello di misurazione e report proprie metriche fisico è anche perché Service Fabric fornisce alcune metriche predefinito.

## <a name="default-metrics"></a>Metriche predefinite
Si supponga di voler tooget avviata la scrittura e la distribuzione del servizio. Ancora non si conoscono le risorse fisiche o logiche che il servizio consuma. Questo approccio non presenta problemi. Hello servizio di gestione delle risorse Cluster dell'infrastruttura Usa alcune metriche predefinite quando non vengono specificate altre metriche. Sono:

  - PrimaryCount - numero di repliche primarie su nodi hello 
  - ReplicaCount - numero di repliche totali di informazioni sullo stato nel nodo hello
  - Conteggio: conteggio di tutti gli oggetti servizio (e senza stato) nel nodo hello

| Metrica | Carico di istanza senza stato | Carico secondario con stato | Carico primario con stato |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Numero |1 |1 |1 |

Per carichi di lavoro di base, metriche predefinito hello forniscono una distribuzione di lavoro in cluster hello ragionevole. Nell'esempio seguente di hello, vediamo cosa accade quando si creano due servizi e si basano sulle metriche di hello predefinito per il bilanciamento del. primo servizio Hello è un servizio con stato con tre partizioni e una replica di destinazione Imposta dimensioni di tre. Hello secondo è un servizio senza stato con una partizione e un conteggio delle istanze di tre.

Il risultato è il seguente:

<center>
![Layout dei cluster con metriche predefinite][Image1]
</center>

Toonote alcune operazioni:
  - Le repliche primarie per il servizio con stato hello vengono distribuite tra più nodi
  - Repliche per la stessa partizione si trovano in nodi diversi di hello
  - numero totale di Hello di colori primari e secondari è distribuito in cluster hello
  - numero totale di Hello degli oggetti servizio viene allocata in modo uniforme in ogni nodo

Ottimo.

criteri predefiniti Hello soluzione ideale come punto di partenza. Tuttavia, le metriche predefinito hello solo trasporterà è finora. Ad esempio: che cos'è probabilità hello che hello partizionamento dello schema è selezionato risultati utilizzo perfettamente anche da tutte le partizioni? Che cos'è il possibilità hello che hello carico per un servizio specifico è costante nel tempo o semplicemente hello uguali tra più partizioni ora?

È possibile eseguire con solo le metriche di predefinito hello. tuttavia, in genere ciò significa che il consumo del cluster è inferiore e non uniforme come desiderato. In questo modo le metriche di hello predefinito non sono adattivo e presuppongono che tutto ciò che è equivalente. Ad esempio, una replica primaria è occupata e uno che non sia contribuiscono metrica di PrimaryCount toohello "1". Nel caso peggiore hello, utilizzando solo la metrica di hello predefinito può inoltre comportare nodi overscheduled causando problemi di prestazioni. Se è interessati a ottenere la maggior parte all'esterno del cluster hello ed evitare problemi di prestazioni, è necessario toouse di metriche personalizzate e creazione di report di carico dinamico.

## <a name="custom-metrics"></a>Metriche personalizzate
Le metriche sono configurate in base al-servizio-istanza denominata quando si crea il servizio di hello.

Qualsiasi metrica è descritta da alcune proprietà: nome, carico predefinito e peso.

* Il nome della metrica: hello Nome metrica hello. il nome della metrica Hello è un identificatore univoco per la metrica hello all'interno di cluster hello dal punto di vista di gestione risorse di hello.
* Peso: Peso metrico definisce il livello di importanza questa metrica è toohello relativo altre metriche per questo servizio.
* Carico predefinito: carico predefinito hello è rappresentato in modo diverso a seconda che il servizio hello sia con stato o senza stato.
  * Per i servizi senza stato, ogni metrica ha un'unica proprietà denominata DefaultLoad
  * Per i servizi con stato si definiscono le proprietà seguenti.
    * PrimaryDefaultLoad: quantità hello predefinita di questa metrica che questo servizio utilizza quando è un database primario
    * SecondaryDefaultLoad: quantità hello predefinita di questa metrica che questo servizio utilizza quando è un database secondario

> [!NOTE]
> Se si definiscono metriche personalizzate e si desidera too_also_ Usa il formato predefinito hello, è necessario too_explicitly_ aggiungere metriche predefinito hello eseguire il backup e definiscono i pesi e i valori per tali. Questo avviene perché è necessario definire una relazione di hello tra le metriche di hello predefinito e le metriche personalizzate. Ad esempio, si può essere più interessati a una metrico di tipo ConnectionCount o WorkQueueDepth che alla distribuzione della metrica primaria. Peso hello predefinito di hello PrimaryCount metrica è elevata, pertanto si tooreduce è tooMedium quando si aggiunta le altre metriche tooensure hanno la precedenza.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Definizione delle metriche per il servizio: esempio
Si supponga che si desideri hello seguente configurazione:

  - Il servizio segnala una metrica denominata "ConnectionCount".
  - È anche opportuno criteri predefiniti di hello toouse 
  - Sono state eseguite alcune misurazioni rilevando che normalmente per una replica primaria del servizio sono necessarie 20 unità di "ConnectionCount",
  - mentre per quelle secondarie ne sono necessarie cinque.
  - Si sa che "ConnectionCount" metrica più importante di hello in termini di gestione delle prestazioni di hello del servizio specifico
  - ma si vuole comunque che le repliche primarie siano bilanciate. Il bilanciamento delle repliche primarie è comunque un approccio consigliabile. Ciò consente di evitare conseguenze per la maggior parte delle repliche primarie con il perdita hello di alcuni domini di errore o di nodo. 
  - In caso contrario, le metriche predefinito hello sono supportate

Ecco il codice hello che si scriverebbe toocreate un servizio con metrica configurazione:

Codice:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Hello esempi sopra riportati e hello resto di questo documento descrivono la gestione delle metriche in base al nome-servizio. È inoltre possibile toodefine metriche per i servizi nel servizio hello _tipo_ livello. A tal fine, specificarle nei manifesti del servizio. La definizione delle metriche a livello di tipo non è consigliata per diversi motivi. Hello primo motivo è che i nomi di metrica sono spesso specifici dell'ambiente. A meno che non è disponibile un contratto di società, non è possibile assicurarsi che metrica hello "Core" in un ambiente non è "MiliCores" o "Core" in altri. Se le metriche sono definite nel manifesto, è necessario toocreate nuovi manifesti per ogni ambiente. Ciò provoca in genere tooa proliferazione dei manifesti diversi con solo piccole differenze, che possono causare difficoltà toomanagement.  
>
> I carichi delle metriche vengono in genere assegnati in base a determinate istanze del servizio. Ad esempio, supponiamo che si crea un'istanza di hello del servizio per ClienteA che prevede toouse scarsamente. Si supponga quindi di crearne un'altra per ClienteB, che ha un carico di lavoro maggiore. In questo caso, può essere utile predefinito hello tootweak carica per tali servizi. Se si dispone di metriche e carica definiti tramite i manifesti e si desidera toosupport questo scenario, è necessario altra applicazione e tipi di servizio per ogni cliente. i valori Hello definiti al momento della creazione del servizio eseguire l'override di quelli definiti nel manifesto di hello, pertanto è possibile utilizzare impostazioni predefinite specifiche che hello tooset. Tuttavia, l'operazione che causa dichiarati in corrispondenza di toonot manifesti hello che tali servizio hello viene effettivamente eseguito con i valori hello. Questo può causare tooconfusion. 
>

Come promemoria: per impostare le metriche di toouse hello predefinito, non la raccolta di metriche hello tootouch affatto o se operazioni particolari durante la creazione del servizio. criteri predefiniti Hello get utilizzati automaticamente quando altri utenti non sono definiti. 

A questo punto, verrà ora analizzato da ciascuna di queste impostazioni in modo più dettagliato e informazioni sul comportamento di hello che influisce sul.

## <a name="load"></a>Caricamento
Hello intero punto della definizione di metriche è toorepresent parte del carico. Il *carico* è la quantità di una determinata metrica che viene consumata da una replica o un'istanza del servizio in un nodo specifico. Il carico può essere configurato in qualsiasi momento, ad esempio:

  - Può essere definito quando viene creato un servizio. Si tratta in questo caso del _carico predefinito_.
  - caricamento delle informazioni di metrica Hello, tra cui impostazione predefinita, per un servizio può aggiornare dopo la creazione servizio hello. Si tratta in questo caso di _aggiornamento di un servizio_. 
  - Carica Hello per una determinata partizione può essere reimpostazione toohello predefinite per il servizio. Viene definita _reimpostazione del carico della partizione_.
  - Il carico può essere restituito per ogni oggetto servizio in modo dinamico in fase di esecuzione. Si ha in questo caso la _creazione di report di carico_. 
  
Tutte queste strategie può essere usate in hello per tutta la durata del servizio stesso. 

## <a name="default-load"></a>Carico predefinito
*Carico predefinito* è la quantità di metrica hello utilizza ogni oggetto di servizio (istanza senza informazioni sullo stato o una replica con stato) di questo servizio. Gestione delle risorse Cluster Hello utilizzato questo numero per il carico di hello dell'oggetto servizio hello finché riceve altre informazioni, ad esempio un report del carico dinamico. Per i servizi più semplici, hello del carico predefinito è una definizione statica. carico predefinito Hello non viene mai aggiornato e viene utilizzata per la durata di hello del servizio hello. Predefinito carica funziona bene per scenari in cui determinati quantità di risorse sono carichi di lavoro toodifferent dedicato e non cambiano di pianificazione della capacità di semplice.

> [!NOTE]
> Per ulteriori informazioni sulla gestione della capacità e la definizione di capacità per i nodi di hello del cluster, vedere [questo articolo](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Hello gestione delle risorse Cluster consente toospecify servizi con stato di un carico predefinito diverso per i relativi componenti primari e secondari. I servizi senza stati è possono specificare solo un valore che applica le istanze di tooall. Per i servizi con stati, il carico predefinito hello per le repliche di database primario e secondario sono solitamente diversi poiché le repliche di eseguire diversi tipi di lavoro in ogni ruolo. Ad esempio, primari in genere servono le operazioni di lettura e scrittura e gestiscono la maggior parte delle attività di calcolo hello, mentre le repliche secondarie non. In genere un carico predefinito hello per una replica primaria è superiore al carico predefinito hello per le repliche secondarie. numeri reali Hello dovrebbero dipendere dalle proprie misurazioni.

## <a name="dynamic-load"></a>Carico dinamico
Si supponga di aver eseguito un servizio per un determinato periodo di tempo e di aver rilevato, con alcune attività di monitoraggio, quanto segue:

1. Alcune partizioni o istanze di un determinato servizio utilizzano più risorse di altre.
2. Il carico di alcuni servizi varia nel tempo.

Fluttuazioni del carico di questo tipo possono avere diverse cause. Ad esempio, servizi o partizioni diversi sono associati a clienti diversi con esigenze differenti. Carico potrebbe anche cambiare poiché quantità hello del servizio hello lavoro varia nel corso di hello del giorno hello. Indipendentemente dal motivo hello, non è in genere alcun singolo numero che è possibile utilizzare per impostazione predefinita. Ciò vale soprattutto se si desidera hello tooget la maggior parte delle utilizzo all'esterno di cluster hello. Qualsiasi valore che scelto per il carico predefinito non è corretto alcuni ora hello. Predefinito non corretto carica il risultato in hello Gestione risorse di Cluster di failover o sotto l'allocazione delle risorse. Di conseguenza, si dispone di nodi sopra o sotto utilizzati anche se ritiene di hello gestione delle risorse Cluster viene bilanciato cluster hello. I carichi predefiniti sono comunque validi perché forniscono alcune informazioni, ma non rappresentano interamente i carichi di lavoro reali. acquisizione tooaccurately variazioni dei requisiti di risorse, gestione delle risorse Cluster hello consente il proprio carico ogni tooupdate oggetto servizio in fase di esecuzione. con la creazione di report di carico dinamici.

I report di carico dinamico consentono tooadjust repliche o istanze il loro carico allocazione/segnalata delle metriche nel relativo ciclo di vita. Una replica o un'istanza del servizio che è inattiva e non esegue alcuna operazione segnalerà in genere un uso ridotto di una determinata metrica, mentre una replica o un'istanza occupata segnalerà un uso superiore.

Reporting di carico per ogni replica o istanza consente hello tooreorganize di gestione delle risorse Cluster hello singoli oggetti assistenza hello cluster. La riorganizzazione di servizi di hello contribuisce a garantire che venga applicato alle risorse di hello che necessarie. Servizi occupati ottenere in modo efficace troppo "recuperare" risorse da altre repliche di istanze o che sono attualmente freddo o meno operazioni.

All'interno di servizi affidabili, carico tooreport di codice hello in modo dinamico è simile al seguente:

Codice:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Un servizio può segnalare in una delle metriche hello definite al momento della creazione. Se un carico di report del servizio per una misurazione che non è configurato toouse, Service Fabric ignora tale report. Se esistono altre metriche viene segnalato a hello stessa ora in cui sono validi, tali relazioni sono accettati. Codice del servizio è possibile misurare e segnalare tutti hello metriche sa come, e gli operatori possono specificare hello configurazione metrica toouse senza la necessità di codice del servizio toochange hello. 

### <a name="updating-a-services-metric-configuration"></a>Aggiornamento della configurazione delle metriche di un servizio
elenco Hello delle metriche associato servizio hello e può essere aggiornata in modo dinamico proprietà hello di queste metriche mentre è attivo il servizio di hello. Questo approccio consente di sperimentare con flessibilità. Di seguito alcuni esempi che mostrano l'utilità di questo tipo di aggiornamento:

  - disabilitazione di una metrica con un report anomalo per un determinato servizio;
  - riconfigurazione di pesi hello di metriche in base alle modalità di funzionamento
  - l'abilitazione di una nuova metrica solo dopo il codice hello già distribuito e convalidato tramite altri meccanismi di
  - la modifica di un carico hello predefinito per un servizio basato sul consumo e comportamento osservato

Hello principale API per la modifica della configurazione di metrica sono `FabricClient.ServiceManagementClient.UpdateServiceAsync` in c# e `Update-ServiceFabricService` in PowerShell. Tutte le informazioni specificate con queste API sostituiscono informazioni metrica hello esistenti per il servizio hello immediatamente. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Combinazione di valori di carico predefiniti e report sul carico dinamico
Carico predefinito e carichi dinamici possono essere utilizzati per hello stesso servizio. Quando un servizio usa sia il carico predefinito sia i report di carico dinamici, il carico predefinito funge da stima finché non sono disponibili i report dinamici. È infatti possibile hello gestione delle risorse Cluster qualcosa toowork con, è buona carico predefinito. carico predefinito Hello consente hello tooplace di gestione delle risorse Cluster oggetti servizio hello in posizioni ottimale quando vengono creati. Se non vengono specificate informazione sul carico predefinito, i servizi vengono posizionati in modo casuale. Quando i report di carico ricevuti in un secondo momento hello gestione delle risorse Cluster è toomove servizi posizionamento casuale iniziale hello spesso non è corretto.

Partendo dall'esempio precedente, è possibile verificare le conseguenze dell'aggiunta di alcune metriche personalizzate e dei report di carico dinamici. In questo esempio verrà usata la metrica "MemoryInMb".

> [!NOTE]
> La memoria è una delle metriche di sistema hello che può essere Service Fabric [risorse regolano](service-fabric-resource-governance.md), e report è in genere difficile. Non è effettivamente previsto è tooreport sul consumo di memoria; La memoria viene utilizzata come un toolearning aiuto sulle funzionalità di hello di hello gestione delle risorse Cluster.
>

Si presume che servizio con stato hello è creato inizialmente con hello comando seguente:

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Si ricordi che la sintassi è ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

Un layout di cluster può avere un aspetto analogo al seguente:

<center>
![Cluster bilanciato con metriche sia predefinite che personalizzate][Image2]
</center>

Occorre notare alcuni aspetti:

* Le repliche secondarie in una partizione possono avere un carico specifico.
* Complessiva metriche hello Cerca bilanciate. Per la memoria, hello rapporto tra hello massimo e minimo del carico è 1,75 (nodo hello con hello la maggior parte del carico è N3, hello almeno N2 e 28/16 = 1,75).

Esistono alcuni aspetti che è comunque necessario tooexplain:

* In che modo è stato stabilito se un rapporto di 1,75 è ragionevole? Come gestore delle risorse Cluster hello sapere se è sufficiente o se è presente più lavoro toodo?
* Quando viene applicato il bilanciamento?
* Cosa significa che il peso di Memory è "High"?

## <a name="metric-weights"></a>Pesi metrici
Rilevamento hello stesso metriche tra diversi servizi sono importante. Visualizzazione globale è consente hello consumo tootrack gestione delle risorse Cluster nel cluster hello bilanciare consumo tra nodi e verificare che i nodi non sfruttano la capacità. Tuttavia, i servizi possono presentare diverse visualizzazioni come toohello importanza di hello stessa metrica. In un cluster con molte metriche e numerosi servizi, inoltre, potrebbero non esistere soluzioni perfettamente bilanciate per tutte le metriche. Come hello gestione delle risorse Cluster deve gestire queste situazioni?

Metrica pesi consentono hello toodecide di gestione delle risorse Cluster come hello toobalance cluster quando non viene data risposta ideale. Metrica pesi consentono inoltre a hello toobalance di gestione delle risorse Cluster servizi specifici in modo diverso. Le metriche possono avere quattro livelli di peso diversi: Zero, Low, Medium e High. Una metrica con peso zero non ha impatto quando si valuta se gli elementi sono bilanciati o meno, Tuttavia, il relativo carico ancora contribuiscono toocapacity gestione. Le metriche con peso zero sono comunque utili e vengono spesso usate come componenti del comportamento del servizio e del monitoraggio delle prestazioni. [In questo articolo](service-fabric-diagnostics-event-generation-infra.md) vengono fornite ulteriori informazioni sull'uso di hello delle metriche per il monitoraggio e diagnostica dei servizi. 

un impatto reale Hello di pesi metrica diversi cluster hello è che il gestore delle risorse Cluster hello genera diverse soluzioni. Metrica pesi indicano hello gestione delle risorse Cluster che alcune metriche sono più importanti rispetto ad altri. Quando è presente alcun hello soluzione perfetta gestione delle risorse Cluster può preferire soluzioni che bilanciare hello superiore ponderata metriche migliori. Se una particolare metrica non è importante per un servizio, potrebbe sbilanciarne l'uso In questo modo un altro servizio tooget una distribuzione uniforme di alcune metriche che è importante tooit.

Esaminiamo un esempio di alcuni report di carico e la metrica per ponderare i risultati in diverse allocazioni cluster hello. In questo esempio viene illustrato che scambiare peso relativo di hello delle metriche hello provoca hello toocreate di gestione delle risorse Cluster differenti versioni dei servizi.

<center>
![Esempio di peso delle metriche e del relativo impatto sulle soluzioni di bilanciamento][Image3]
</center>

In questo esempio sono presenti quattro diversi servizi, tutti con valori diversi nei report di due diverse metriche, MetricA e MetricB. In un caso, tutti i servizi di hello definiscono MetricA è più importante di hello (peso = alto) e MetricB come non importanti (peso = basso). Di conseguenza, viene illustrato che il gestore delle risorse Cluster hello posiziona servizi hello in modo che MetricA risulta più bilanciato di MetricB. "Bilanciamento migliore" significa che MetricA presenta una deviazione standard inferiore rispetto a MetricB. Nel secondo caso hello è inverso pesi metrica hello. Di conseguenza, hello gestione delle risorse Cluster consente di scambiare servizi A e B toocome backup con un'allocazione in cui MetricB risulta più bilanciato di MetricA.

> [!NOTE]
> Metrica pesi determinano come deve bilanciare i hello gestione delle risorse Cluster, ma non quando bilanciamento del carico deve verificarsi. Per altre informazioni sul bilanciamento, vedere [questo articolo](service-fabric-cluster-resource-manager-balancing.md).
>

### <a name="global-metric-weights"></a>Pesi metrici globali
Si supponga Service definisce MetricA come peso elevata e ServiceB imposta il peso di hello per MetricA tooLow o Zero. Che cos'è il peso reale hello che finisce per essere utilizzata?

Per ogni metrica esistono più pesi di cui tenere traccia. peso prima Hello è hello definito per la metrica hello quando viene creato il servizio di hello. Hello altri peso è uno spessore globale, che viene calcolato automaticamente. Hello gestione delle risorse Cluster utilizza entrambi questi pesi quando le soluzioni di punteggio. Considerare entrambi i pesi è importante. In questo modo hello toobalance di gestione delle risorse Cluster ogni servizio tooits secondo proprietari priorità e assicurarsi anche tale cluster hello come intero è allocato correttamente.

Che cosa accadrebbe se hello gestione delle risorse Cluster non si preoccupa dell'equilibrio globale e locali? È anche facile tooconstruct soluzioni a livello globale, che sono bilanciati, ma il risultato che il saldo di risorse insufficienti per i singoli servizi. Nel seguente esempio di hello, si esamina un servizio configurato con solo i criteri predefiniti hello e vedere cosa accade quando viene considerato solo globale saldo:

<center>
![Hello impatto di una soluzione solo globale][Image4]
</center>

Nell'esempio di hello superiore basato solo su globale saldo, l'intero cluster hello effettivamente viene bilanciato. Tutti i nodi dispongono hello stesso numero di colori primari e hello stesso numero di repliche totali. Tuttavia, se si esamina l'impatto di effettivo hello di questa allocazione non è pertanto valida: hello perdita di un nodo ha conseguenze negative un determinato carico di lavoro estremamente, poiché accetta tutte relativo primari. Ad esempio, se primo nodo hello non riesce a tre colori primari hello per hello tre diverse partizioni di hello servizio cerchio tutti sarebbe persi. Al contrario, hello triangolo e servizi esagono hanno le relative partizioni perdere una replica. In questo modo alcuna interruzione del servizio, diverso da con hello toorecover verso il basso di replica.

Nell'esempio hello inferiore hello gestione delle risorse Cluster è distribuiti repliche hello in base a entrambi equilibrio hello, globali e di servizio. Quando si calcola il punteggio di hello della soluzione hello offre la maggior parte di una soluzione globale di hello peso toohello e i servizi di tooindividual una porzione (configurabile). Stato globale per una misurazione è calcolato in base Media hello dei pesi di metrica hello da ogni servizio. Ogni servizio viene bilanciato secondo tooits personalizzate definite pesi metrica. In questo modo si garantisce che i servizi di hello sono bilanciati fra loro in base a tootheir alle proprie esigenze. Di conseguenza, se hello stesso nodo del primo errore hello viene distribuito tra tutte le partizioni di tutti i servizi. tooeach impatto Hello è hello stesso.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulla configurazione dei servizi vedere [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- La definizione di metriche di deframmentazione in linea è tooconsolidate unidirezionale carico sui nodi anziché distribuirlo. toolearn come tooconfigure deframmentazione, fare riferimento troppo[in questo articolo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)
- Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)
- Il costo dello spostamento è un modo di segnalazione toohello gestione delle risorse Cluster che alcuni servizi siano toomove più costosi rispetto ad altri. toolearn ulteriori informazioni su costo di spostamento, fare riferimento troppo[in questo articolo](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
