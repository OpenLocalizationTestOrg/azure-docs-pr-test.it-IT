---
title: aaaService gestione delle risorse dell'infrastruttura Cluster - gruppi di applicazioni | Documenti Microsoft
description: "Panoramica delle funzionalità gruppo di applicazioni nel servizio di gestione delle risorse Cluster dell'infrastruttura di hello hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Introduzione tooApplication gruppi
Gestione delle risorse dell'infrastruttura servizio Cluster gestisce in genere le risorse cluster distribuendo il carico hello (rappresentato tramite [metriche](service-fabric-cluster-resource-manager-metrics.md)) in modo uniforme in tutto il cluster hello. Service Fabric gestisce la capacità di hello dei nodi hello hello e hello cluster nel suo complesso tramite [capacità](service-fabric-cluster-resource-manager-cluster-description.md). Metriche e capacità rappresentano un'ottima soluzione per molti tipi di carichi di lavoro, ma i modelli che fanno largo uso di diverse istanze di applicazione di Service Fabric comportano a volte requisiti aggiuntivi. Ad esempio, si può desiderare di:

- Alcune capacità in nodi hello hello cluster per i servizi all'interno di un'istanza di applicazione denominata hello di riserva
- Limitare hello il numero totale di nodi che hello all'interno di un'istanza dell'applicazione denominata vengono eseguiti i servizi (anziché distribuirli tramite l'intero cluster hello)
- Definire le capacità nell'istanza di applicazione denominata hello stesso numero di hello toolimit servizi o totale del consumo della risorsa dei servizi di hello all'interno

toomeet questi requisiti, hello gestione delle risorse Cluster di Service Fabric supporta una funzionalità denominata gruppi di applicazioni.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Limitando hello il numero massimo di nodi
Hello più semplice per la capacità dell'applicazione viene usata quando un'istanza di applicazione deve toobe limitato tooa determinato numero massimo di nodi. Consolida tutti i servizi all'interno di tale istanza dell'applicazione su un numero di set di macchine. Consolidamento è utile quando si sta tentando di toopredict o limitare l'utilizzo delle risorse fisiche da servizi di hello all'interno di tale istanza dell'applicazione denominata. 

Hello immagine seguente mostra un'istanza dell'applicazione con e senza un numero massimo di nodi definiti:

<center>
![Istanza di applicazione che definisce il numero massimo di nodi][Image1]
</center>

Nell'esempio di sinistra hello, un'applicazione hello non dispone di un numero massimo di nodi definiti e dispone di tre servizi. Gestione delle risorse Cluster Hello è diffondere tutte le repliche tra sei nodi disponibili tooachieve hello equilibrio migliore in cluster hello (comportamento predefinito di hello). Nell'esempio di destra hello, vediamo hello stessa applicazione limitata toothree nodi.

il parametro Hello che controlla questo comportamento viene chiamato numero massimo di nodi. Questo parametro può essere impostato durante la creazione dell'applicazione oppure può essere aggiornato per un'istanza di applicazione già in esecuzione.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

In set di nodi hello hello gestione delle risorse Cluster non garantisce gli oggetti per cui ottengano posizionati o ottengano utilizzati i nodi.

## <a name="application-metrics-load-and-capacity"></a>Metriche, carico e capacità dell'applicazione
Gruppi di applicazioni consentono anche metriche toodefine associate a un'istanza dell'applicazione denominata specificato e la capacità del tale istanza applicazione per tali metriche. Le metriche dell'applicazione consentono di tootrack riserva e limitare il consumo di risorse hello dei servizi di hello all'interno di tale istanza dell'applicazione.

Per ogni metrica di applicazione, è possibile impostare due valori:

- **Applicazione capacità totale** : questa impostazione rappresenta la capacità totale hello dell'applicazione hello per una determinata metrica. Hello gestione delle risorse Cluster non consente la creazione di hello di eventuali nuovi servizi all'interno di questa istanza di applicazione che fa sì che il carico totale tooexceed questo valore. Si supponga, ad esempio, ha una capacità pari a 10 di istanza dell'applicazione hello e dispone già di carico di cinque. creazione di Hello di un servizio con un carico totale predefinito di 10 sarebbe non consentita.
- **Capacità massima del nodo** : questa impostazione specifica carico totale massimo di hello per un'applicazione hello in un singolo nodo. Se il carico passa in questa capacità, hello gestione delle risorse Cluster consente di spostare i nodi tooother repliche hello carico diminuisce.


Powershell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Riserva della capacità
Un altro utilizzo comune per gruppi di applicazioni è che le risorse all'interno di hello cluster tooensure sono riservati per un'istanza dell'applicazione specificato. Quando viene creata l'istanza dell'applicazione hello, è sempre riservato Hello uno spazio.

Riserva spazio nel cluster hello per un'applicazione hello avviene immediatamente, anche se:
- istanza dell'applicazione Hello viene creato ma non dispone ancora di tutti i servizi all'interno di essa
- numero di Hello dei servizi all'interno di istanza dell'applicazione hello cambia ogni volta 
- servizi di Hello esistano ma non utilizzano risorse di hello 

Per prenotare le risorse per un'istanza dell'applicazione è necessario definire due parametri aggiuntivi: *MinimumNodes* e *NodeReservationCapacity*

- **Numero minimo di nodi** -definisce il numero minimo di hello di nodi che hello applicazione istanza deve essere eseguita.  
- **NodeReservationCapacity** -questa impostazione è per ogni metrica per un'applicazione hello. il valore di Hello è quantità hello di tale metrica riservato per un'applicazione hello su qualsiasi nodo in cui che hello servizi in esecuzione tale applicazione.

La combinazione di **nodi** e **NodeReservationCapacity** garantisce una prenotazione di un carico minimo per un'applicazione hello all'interno di cluster hello. Se si verifica meno rimanenti del cluster di prenotazione di hello totale necessaria capacità di hello, si verifica un errore di creazione di un'applicazione hello. 

Di seguito viene illustrato un esempio di come viene riservata la capacità:

<center>
![Istanze di applicazione che definiscono la capacità riservata][Image2]
</center>

Nell'esempio di sinistra hello, le applicazioni non dispone capacità qualsiasi applicazione definito. Gestione delle risorse Cluster Hello saldi tutti gli elementi in base a regole toonormal.

Nell'esempio hello hello destra, si supponga che Application1 sia stato creato con hello seguenti impostazioni:

- Numero minimo di nodi set tootwo
- Una metrica dell'applicazione definita con le impostazioni seguenti:
  - NodeReservationCapacity pari a 20

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric riserva capacità in due nodi per /Application1 e non consentono di servizi da Application2 tooconsume tale capacità anche se sono presenti che senza alcun carico non viene consumato da servizi di hello all'interno di Application1 in fase di hello. Questa capacità riservata applicazione è considerata utilizzata e concorre hello residua in tale nodo e all'interno di cluster hello.  prenotazione Hello viene sottratto dal hello residua di cluster immediatamente, ma hello riservato consumo viene sottratto dalla capacità di hello di un nodo specifico solo quando almeno un servizio oggetto viene posizionato su di esso. Questa prenotazione successiva consente un utilizzo ottimale delle risorse e flessibilità, dal momento che le risorse sono riservate nei nodi solo quando necessario.

## <a name="obtaining-hello-application-load-information"></a>Ottenere informazioni sul caricamento di applicazione hello
Per ogni applicazione che ha una capacità di applicazioni definito per una o più metriche è possibile ottenere informazioni di hello sul carico di aggregazione hello segnalato da repliche dei relativi servizi.

Powershell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

query ApplicationLoad Hello restituisce informazioni di base sulla capacità di applicazione che è stato specificato per un'applicazione hello hello. Queste informazioni includono le informazioni di nodi di minimo e massimo hello e numero hello che un'applicazione hello è attualmente occupata. Sono inoltre incluse informazioni su ogni metrica di carico dell'applicazione, tra cui:

* Il nome della metrica: Nome della metrica hello.
* Capacità di prenotazione: La capacità Cluster nel cluster hello viene riservata per l'applicazione.
* Carico dell'applicazione: carico totale delle repliche figlio dell'applicazione.
* Capacità dell'applicazione: valore massimo consentito di carico dell'applicazione.

## <a name="removing-application-capacity"></a>Rimozione della capacità dell'applicazione
Dopo aver impostati i parametri di capacità dell'applicazione hello per un'applicazione, può essere rimosso utilizzando le API di aggiornamento dell'applicazione o i cmdlet PowerShell. ad esempio:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Questo comando rimuove tutti i parametri di gestione della capacità dell'applicazione dall'istanza di applicazione hello. Sono inclusi nodi, numero massimo di nodi e le metriche dell'applicazione hello, se presente. effetto di Hello del comando hello è immediato. Dopo il completamento del comando, hello gestione delle risorse Cluster utilizza il comportamento predefinito di hello per la gestione delle applicazioni. I parametri di capacità dell'applicazione possono essere specificati nuovamente tramite `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Restrizioni relative alla capacità dell'applicazione
Esistono diverse restrizioni da rispettare per i parametri di capacità dell'applicazione. Se sono presenti errori di convalida non viene apportata alcuna modifica.

- Tutti i parametri di tipo integer devono essere numeri non negativi.
- MinimumNodes non deve essere mai maggiore di MaximumNodes.
- Se definite, le capacità per una metrica di carico devono rispettare queste regole:
  - La capacità di prenotazione del nodo non deve essere maggiore della capacità massima del nodo. Ad esempio, non è possibile limitare la capacità di hello per la metrica di hello "CPU" in unità di hello nodo tootwo si cerca tooreserve tre unità su ogni nodo.
  - Se il numero massimo di nodi viene specificato, il prodotto di hello del numero massimo di nodi e capacità massima del nodo non deve essere maggiore rispetto alla capacità totale di applicazione. Si supponga, ad esempio, hello capacità massima di nodo per la metrica di caricamento "CPU" è impostata tooeight. Si supponga inoltre che impostare hello too10 numero massimo di nodi. In questo caso, la capacità totale dell'applicazione deve essere superiore a 80 per la metrica di carico.

Hello restrizioni vengono applicate sia durante la creazione di applicazioni e aggiornamenti.

## <a name="how-not-toouse-application-capacity"></a>La modalità non toouse capacità di applicazione
- Non tentare toouse hello gruppo di applicazioni funzionalità tooconstrain hello applicazione tooa _specifico_ subset di nodi. In altre parole, è possibile specificare che un'applicazione hello viene eseguito su al massimo cinque nodi, ma non le cinque nodi specifici cluster hello. Vincolare un toospecific applicazione nodi possono essere ottenuti utilizzando vincoli di posizionamento per i servizi.
- Non tentare toouse hello applicazione capacità tooensure che due servizi dalla stessa applicazione si trovano in hello hello stessi nodi. Usare invece [affinità](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) o [vincoli di posizionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulla configurazione dei servizi, [Informazioni sulla configurazione dei servizi](service-fabric-cluster-resource-manager-configure-services.md)
- toofind out sulla modalità di gestione delle risorse Cluster hello gestisce e bilancia il carico nel cluster hello, controllare l'articolo hello [bilanciamento del carico](service-fabric-cluster-resource-manager-balancing.md)
- Iniziare dall'inizio hello e [ottenere un servizio di gestione delle risorse Cluster dell'infrastruttura di toohello introduzione](service-fabric-cluster-resource-manager-introduction.md)
- Per altre informazioni sul funzionamento generale delle metriche, vedere l'articolo sulle [metriche di carico di Service Fabric](service-fabric-cluster-resource-manager-metrics.md)
- Hello gestione delle risorse Cluster dispone di numerose opzioni per la descrizione del cluster di hello. toofind ulteriori informazioni, consultare questo articolo in [che descrive un cluster di Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
